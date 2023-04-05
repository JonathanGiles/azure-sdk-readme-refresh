# HTTP Client Configuration and Troubleshooting Options

> **Note** At present, this page is missing from learn.microsoft.com, but I am proposing that it will be added into the 'troubleshooting section' alongside the existing 'network issues' and 'dependency conflicts' pages. The content here is not refined - it is simply content taken from the app config library documentation, that I do not believe should be included at the library level. Rather, I believe it is best if we centralize this content into one place.

## General

When you interact with App Configuration using this Java client library, errors returned by the service correspond to the same HTTP status codes returned for [REST API][rest_api] requests. For example, if you try to retrieve a configuration setting that doesn't exist in your configuration store, a `404` error is returned, indicating `Not Found`.

App Configuration provides a way to define customized headers through `Context` object in the public API. 

```java readme-sample-customHeaders
// Add your headers
HttpHeaders headers = new HttpHeaders();
headers.set("my-header1", "my-header1-value");
headers.set("my-header2", "my-header2-value");
headers.set("my-header3", "my-header3-value");
// Call API by passing headers in Context.
configurationClient.addConfigurationSettingWithResponse(
    new ConfigurationSetting().setKey("key").setValue("value"),
    new Context(AddHeadersFromContextPolicy.AZURE_REQUEST_HTTP_HEADERS_KEY, headers));
// Above three HttpHeader will be added in outgoing HttpRequest.
```

For more detail information, check out the [AddHeadersFromContextPolicy][add_headers_from_context_policy]

### Default HTTP Client
All client libraries by default use the Netty HTTP client. Adding the above dependency will automatically configure the client library to use the Netty HTTP client. Configuring or changing the HTTP client is detailed in the [HTTP clients wiki](https://github.com/Azure/azure-sdk-for-java/wiki/HTTP-clients).

### Default SSL library
All client libraries, by default, use the Tomcat-native Boring SSL library to enable native-level performance for SSL 
operations. The Boring SSL library is an uber jar containing native libraries for Linux / macOS / Windows, and provides 
better performance compared to the default SSL implementation within the JDK. For more information, including how to 
reduce the dependency size, refer to the [performance tuning][performance_tuning] section of the wiki.

### Enable client logging

To troubleshoot issues with Azure App Configuration library, it is important to first enable logging to monitor the
behavior of the application. The errors and warnings in the logs generally provide useful insights into what went wrong 
and sometimes include corrective actions to fix issues. The Azure client libraries for Java have two logging options:

* A built-in logging framework.
* Support for logging using the [SLF4J](https://www.slf4j.org/) interface.

Refer to the instructions in this reference document on how to [configure logging in Azure SDK for Java][logging_overview].

### Enable HTTP request/response logging

Reviewing the HTTP request sent or response received over the wire to/from the Azure App Configuration service can be 
useful in troubleshooting issues. To enable logging the HTTP request and response payload, the [ConfigurationClient][configuration_client] 
can be configured as shown below:

```java readme-sample-enablehttplogging
ConfigurationClient configurationClient = new ConfigurationClientBuilder()
        .connectionString(connectionString)
        .httpLogOptions(new HttpLogOptions().setLogLevel(HttpLogDetailLevel.BODY_AND_HEADERS))
        .buildClient();
// or
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
ConfigurationClient configurationClientAad = new ConfigurationClientBuilder()
        .credential(credential)
        .endpoint(endpoint)
        .httpLogOptions(new HttpLogOptions().setLogLevel(HttpLogDetailLevel.BODY_AND_HEADERS))
        .buildClient();
```

Alternatively, you can configure logging HTTP requests and responses for your entire application by setting the
following environment variable. Note that this change will enable logging for every Azure client that supports logging
HTTP request/response.

Environment variable name: `AZURE_HTTP_LOG_DETAIL_LEVEL`

| Value            | Logging level                                                        |
|------------------|----------------------------------------------------------------------|
| none             | HTTP request/response logging is disabled                            |
| basic            | Logs only URLs, HTTP methods, and time to finish the request.        |
| headers          | Logs everything in BASIC, plus all the request and response headers. |
| body             | Logs everything in BASIC, plus all the request and response body.    |
| body_and_headers | Logs everything in HEADERS and BODY.                                 |

**NOTE**: When logging the body of request and response, please ensure that they do not contain confidential
information. When logging headers, the client library has a default set of headers that are considered safe to log
but this set can be updated by updating the log options in the builder as shown below:

```java
clientBuilder.httpLogOptions(new HttpLogOptions().addAllowedHeaderName("safe-to-log-header-name"))
```

### Troubleshooting exceptions
Azure App Configuration service methods throw a [HttpResponseException][http_response_exception] or its subclass on failure.
The `HttpResponseException` thrown by the App Configuration client library includes detailed response error object
that provides specific useful insights into what went wrong and includes corrective actions to fix common issues.
This error information can be found inside the message property of the `HttpResponseException` object.

Here's the example of how to catch it with synchronous client

```java readme-sample-troubleshootingExceptions
try {
    ConfigurationSetting setting = new ConfigurationSetting().setKey("myKey").setValue("myValue");
    client.getConfigurationSetting(setting);
} catch (HttpResponseException e) {
    System.out.println(e.getMessage());
    // Do something with the exception
}
```

With async clients, you can catch and handle exceptions in the error callbacks:

```java readme-sample-troubleshootingExceptions-async
ConfigurationSetting setting = new ConfigurationSetting().setKey("myKey").setValue("myValue");
asyncClient.getConfigurationSetting(setting)
    .doOnSuccess(ignored -> System.out.println("Success!"))
    .doOnError(
        error -> error instanceof ResourceNotFoundException,
        error -> System.out.println("Exception: 'getConfigurationSetting' could not be performed."));
```

A scenario of receiving HTTP status code 429 response can be found at 
[FAQ: My application receives HTTP code 429 responses. Why?][faq_429_response].

### Authentication errors

Azure App Configuration supports Azure Active Directory authentication. [ConfigurationClientBuilder][configuration_client_builder]
has method to set the `credential`. To provide a valid credential, you can use `azure-identity` dependency. For more 
details on getting started, refer to the [README][how_to_create_appconfig_client]of Azure App Configuration library. 
You can also refer to the [Azure Identity documentation][identity_doc] for more details on the various types of 
credential supported in `azure-identity`.

<!-- Links -->
[best_practice_samples]: https://learn.microsoft.com/azure/azure-app-configuration/howto-best-practices
[configuration_client]: https://learn.microsoft.com/java/api/com.azure.data.appconfiguration.configurationclient?view=azure-java-stable
[configuration_client_builder]: https://learn.microsoft.com/java/api/com.azure.data.appconfiguration.configurationclientbuilder?view=azure-java-stable
[how_to_create_appconfig_client]: https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/appconfiguration/azure-data-appconfiguration#create-a-configuration-client
[faq]: https://learn.microsoft.com/azure/azure-app-configuration/faq
[faq_429_response]: https://learn.microsoft.com/azure/azure-app-configuration/faq#my-application-receives-http-status-code-429-responses--why
[http_response_exception]: https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/core/azure-core/src/main/java/com/azure/core/exception/HttpResponseException.java
[identity_doc]: https://docs.microsoft.com/azure/developer/java/sdk/identity
[logging_overview]: https://docs.microsoft.com/azure/developer/java/sdk/logging-overview
[support]: https://github.com/Azure/azure-sdk-for-java/blob/main/SUPPORT.md
[troubleshooting_network_issues]: https://learn.microsoft.com/azure/developer/java/sdk/troubleshooting-network
[troubleshooting_dependency_conflict]: https://docs.microsoft.com/azure/developer/java/sdk/troubleshooting-dependency-version-conflict
[troubleshooting_mitigate_version_mismatch]: https://docs.microsoft.com/azure/developer/java/sdk/troubleshooting-dependency-version-conflict#mitigate-version-mismatch-issues