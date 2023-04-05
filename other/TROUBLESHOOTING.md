# Troubleshooting

> **Note** At present, the learn.microsoft.com website has two 'troubleshooting' pages:
>
> * [Network Issues](https://learn.microsoft.com/azure/developer/java/sdk/troubleshooting-network)
> * [Dependency Conflicts](https://learn.microsoft.com/azure/developer/java/sdk/troubleshooting-dependency-version-conflict)
>
> What it currently lacks is a general-purpose overview page, that then fans out to these specific pages as appropriate for the reader. This document intends to represent what that overview page may be.

The Azure SDK for Java consists of many client libraries, for the various Azure services that are supported. Despite this breadth, the client libraries are built to a consistent standard, and therefore options related to configuration and troubleshooting are common across all libraries. This document introduces a number of options available to you, and links to other pages with further details.

## Overview

Because troubleshooting and advanced configuration spans such a wide topic area, there are a number of pages you may consider reviewing:

* [HTTP Options and Configuration](HTTP-OPTIONS-CONFIG.md) covers topics related to configuring the HTTP clients that are available in the Azure SDK for Java, including exception handling, passing custom headers in requests, logging request information, and so on.
* [Network Issues](https://learn.microsoft.com/azure/developer/java/sdk/troubleshooting-network) covers topics related to HTTP debugging *outside* of the client library, using tools like Fiddler and Wireshark.
* [Dependency Conflicts](https://learn.microsoft.com/azure/developer/java/sdk/troubleshooting-dependency-version-conflict) covers topics related to diagnosing, mitigating, and minimizing dependency conflicts, when using the Azure SDK for Java client libraries in systems that are built with tools such as Maven and Gradle.

## Next Steps

If the troubleshooting guidance above does not help to resolve issues when using the Azure SDK for Java client libraries, it is recommended that you reach out to the development team by [filing an issue on the projects GitHub page][azsdkjava_github_repo].

<!-- LINKS -->
[azsdkjava_github_repo]: https://github.com/Azure/azure-sdk-for-java