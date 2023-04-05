# Azure App Configuration client library for Java

**Links:** [Source][source_code] | [Maven][maven_package] | [Ref Docs][api_documentation] | [Product Docs][product_docs] | [Samples][samples] | [Troubleshooting](TROUBLESHOOTING.md)

[Azure App Configuration][product_docs] is a managed service that helps developers centralize their application configurations simply and securely.

Modern programs, especially programs running in a cloud, generally have many components that are distributed in nature. Spreading configuration settings across these components can lead to hard-to-troubleshoot errors during an application deployment. Use App Configuration to store all the settings for your application and secure their accesses in one place.

Use this client library to create and manage application configuration settings.

## Getting started

Azure SDK for Java libraries are all available from [Maven Central][maven_package]. This library is named `azure-data-appconfiguration`, and is included in the `azure-sdk-bom` for your convenience. It is *highly* recommended to use the Azure SDK BOM to manage your dependencies. To use the Azure SDK BOM, follow our [Maven][bom_maven] and [Gradle][bom_gradle] docs. With the Azure SDK for Java BOM, you would add the following to your Maven *pom.xml* file:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.azure</groupId>
            <artifactId>azure-sdk-bom</artifactId>
            <version>{bom_version_to_target}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>com.azure</groupId>
    <artifactId>azure-data-appconfiguration</artifactId>
  </dependency>
</dependencies>
```

> **TODO** I want to auto-refresh the *{bom_version_to_target}* text with the latest BOM version, rather than have it be a placeholder and an exercise left to the reader.

Additionally, for projects using Maven as their build tool, it is *highly* recommended to use the [Maven Build Tool plugin][maven_build_tool], as this will ensure all Azure SDK best practices are being followed.

## Authentication

This client library supports the authentication methods listed below:

* Azure Active Directory
* Connection strings

Authentication is a complex topic, but fortunately there are [conceptual docs][azure_identity_concepts] and detailed [reference docs][azure_identity_ref_docs]. You can also [read through the samples for this library][samples], as these show precisely how how to authenticate clients in this library.

## Key Concepts and Examples

Key concepts, code examples, and usage instructions for this library are discussed in great detail in the [App Configuration ref docs][api_documentation]. Additionally, there are more comprehensive code samples in the [samples][samples] directory of this library.

## Creating a Client

With all of the links provided above, you should have ample guidance on most aspects of using this library. To make this concrete, the code snippets below show the critical code required to create a new client, including authentication.

### Using a Connection String

```java
ConfigurationClient configurationClient = new ConfigurationClientBuilder()
    .connectionString(connectionString)
    .buildClient();
```

> **Note** Connection strings are a great way to get started quickly on a new project, but are not recommended when your application is deployed to production. Consider using another authentication method at that stage.

### Using an Azure Active Directory (AAD) Token

Here we demonstrate using [DefaultAzureCredential][azure_identity_DAC] to authenticate as a service principal. However, the configuration client accepts any [azure-identity credential][azure_identity_concepts].

```java
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
ConfigurationClient configurationClient = new ConfigurationClientBuilder()
    .credential(credential)
    .endpoint(endpoint)
    .buildClient();
```

## Troubleshooting

See our [App Configuration troubleshooting guide](TROUBLESHOOTING.md) for details on how to diagnose various failure scenarios related specifically to this library. Additionally, refer to the [Azure SDK for Java troubleshooting][troubleshooting-guide] page to learn more about how to get started with troubleshooting issues when using the Azure SDK for Java client libraries.

## Next steps

* Comprehensive code samples are available [here][samples].
* Detailed reference docs and usage examples for the API in this library are provided [here][api_documentation].
* [Quickstart: Create a Java Spring app with App Configuration][spring_quickstart]

<!-- LINKS -->
[api_documentation]: https://learn.microsoft.com/java/api/com.azure.data.appconfiguration
[azure_identity]: https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/identity/azure-identity
[azure_identity_concepts]: https://learn.microsoft.com/azure/developer/java/sdk/identity
[azure_identity_DAC]: https://learn.microsoft.com/java/api/com.azure.identity.defaultazurecredential
[azure_identity_ref_docs]: https://learn.microsoft.com/java/api/com.azure.identity
[bom_maven]: https://learn.microsoft.com/azure/developer/java/sdk/get-started-maven#add-azure-sdk-for-java-to-an-existing-project
[bom_gradle]: https://learn.microsoft.com/azure/developer/java/sdk/get-started-gradle
[maven_build_tool]: https://learn.microsoft.com/azure/developer/java/sdk/get-started-maven#use-the-azure-sdk-for-java-build-tool
[maven_package]: https://central.sonatype.com/artifact/com.azure/azure-data-appconfiguration/1.4.3
[product_docs]: https://docs.microsoft.com/azure/azure-app-configuration
[samples]: https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/appconfiguration/azure-data-appconfiguration/src/samples
[source_code]: https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/appconfiguration/azure-data-appconfiguration/src
[spring_quickstart]: https://docs.microsoft.com/azure/azure-app-configuration/quickstart-java-spring-app
[troubleshooting-guide]: ../other/TROUBLESHOOTING.md
![Impressions](https://azure-sdk-impressions.azurewebsites.net/api/impressions/azure-sdk-for-java%2Fsdk%2Fappconfiguration%2Fazure-data-appconfiguration%2FREADME.png)
