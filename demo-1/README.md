# Azure App Configuration client library for Java

**Links:** [Source][source_code] | [Maven][package] | [Ref Docs][api_documentation] | [Product Docs][azconfig_docs] | [Samples][samples] | [Troubleshooting](TROUBLESHOOTING.md)

Azure App Configuration is a managed service that helps developers centralize their application configurations simply and securely.

Modern programs, especially programs running in a cloud, generally have many components that are distributed in nature. Spreading configuration settings across these components can lead to hard-to-troubleshoot errors during an application deployment. Use App Configuration to store all the settings for your application and secure their accesses in one place.

Use the client library for App Configuration to create and manage application configuration settings.

## Getting started

Azure SDK for Java libraries are all available from Maven Central. This library is named `azure-data-appconfiguration`, and is included in the `azure-sdk-bom` for your convenience. If you use Maven, refer to the [Azure SDK for Java Maven](https://learn.microsoft.com/azure/developer/java/sdk/get-started-maven?view=azure-java-stable) docs, and if you use Gradle, refer to the [Azure SDK for Java Gradle](https://learn.microsoft.com/azure/developer/java/sdk/get-started-gradle?view=azure-java-stable) docs.

## Authentication

This client library supports [authentication methods][azure_identity_concepts] listed below:

* Azure Active Directory
* Connection strings

Authentication uses the [azure-identity][azFor samples on how to connect using these authentication methods, refer to the [samples document][samples]

## Key Concepts and Examples

Key concepts, code examples, and usage instructions for this library are discussed in great detail in our reference documentation. [Click here][api_documentation] to see the reference documentation for this library. Additionally, there are more comprehensive code samples in the [samples][samples] directory of this library.

## Troubleshooting

See our [App Configuration troubleshooting guide](TROUBLESHOOTING.md) for details on how to diagnose various failure scenarios related specifically to this library. Additionally, refer to the [Azure SDK for Java troubleshooting][troubleshooting-guide] page to learn more about how to get started with troubleshooting issues when using the Azure SDK for Java client libraries.

## Next steps

* Samples are explained in detail [here][samples].
* Conceptual details are explained in detail [here][api_documentation].
* [Quickstart: Create a Java Spring app with App Configuration][spring_quickstart]

<!-- LINKS -->
[api_documentation]: https://learn.microsoft.com/java/api/com.azure.data.appconfiguration
[azure_identity]: https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/identity/azure-identity
[azure_identity_concepts]: https://learn.microsoft.com/azure/developer/java/sdk/identity
[azure_identity_ref_docs]: https://learn.microsoft.com/java/api/com.azure.identity
[package]: https://central.sonatype.com/artifact/com.azure/azure-data-appconfiguration/1.4.3
[samples]: https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/appconfiguration/azure-data-appconfiguration/src/samples
[source_code]: https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/appconfiguration/azure-data-appconfiguration/src
[spring_quickstart]: https://docs.microsoft.com/azure/azure-app-configuration/quickstart-java-spring-app
[troubleshooting-guide]: ../other/TROUBLESHOOTING.md
![Impressions](https://azure-sdk-impressions.azurewebsites.net/api/impressions/azure-sdk-for-java%2Fsdk%2Fappconfiguration%2Fazure-data-appconfiguration%2FREADME.png)
