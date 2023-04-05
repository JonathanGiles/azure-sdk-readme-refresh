# Java Documentation Refresh

## tl;dr

The text below proposes changes to the structure of the Java documentation. Most notably, it intends to simplify and de-dupe content in the 'readme.md' files found throughout our GitHub repo for each library. To see how these changes could be implemented, refer to the links below:

* [Existing readme](existing/README.md)
* [Variation #1](demo-1/README.md): Extremely minimal

## Further Details

There are multiple sources of Java documentation available to developers who use the Azure SDK for Java. We have the following:

* [Conceptual documentation](https://learn.microsoft.com/azure/developer/java/sdk/).
* Reference documentation - hosted in two different locations:
  * [learn.microsoft.com](https://learn.microsoft.com/java/api/overview/azure/?view=azure-java-stable) - rendered using Microsoft formatting.
  * [azure.github.io](https://azure.github.io/azure-sdk-for-java/index.html) - rendered using standard JavaDoc formatting.
* Readme files for each library, for example [App Configuration](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/appconfiguration/azure-data-appconfiguration).

The goal of this refresh is to ensure each of these locations has clear distinctions about what they are responsible for covering, and for what they should defer to other locations (via external links).

## Conceptual Documentation

Perhaps the easiest documentation source to classify is the conceptual documentation pages. These pages contain information about getting started with Azure SDK and using build tools such as Maven, Gradle, and GraalVM. It covers conceptual topics about logging, identity and auth, HTTP pipelines, etc. Finally, it talks about general troubleshooting for common problems encountered when using libraries.

## Reference Documentation

Reference documentation (also known as API documentation) is written in code as JavaDoc against classes and their members. It also includes package-level documentation written in `package-info.java` files.

Reference documentation is intended to explain to users what an API does, without telling the user how the API is implemented. It includes clarification about all questions the user may have as they go about their day-to-day development activities, including links out to relevant conceptual documentation, as well as code samples.

Reference documentation should **not** cover aspects such as troubleshooting the library, getting started with build tools, and dependencies. These topics belong elsewhere (in the readme.md file).

The major change I would propose for reference documentation is to remove the duplication of our reference documentation. As noted above, it currently exists in two places, with links throughout our documentation using these interchangeably. I would propose that we no longer generate the [github.io](https://azure.github.io/azure-sdk-for-java/index.html) JavaDoc, and instead only uses the [learn.microsoft.com](https://learn.microsoft.com/java/api/overview/azure/?view=azure-java-stable) JavaDoc.

## Readme Files

Readme files exist for each library, where they cover a number of aspects:

* Service introduction paragraph.
* Links to source code, Maven package, API docs, production docs, and samples.
* 'Getting Started' section
  * BOM (Maven)
  * Direct dependency (Maven, with and without BOM)
  * Code samples
    * Creating resources with `az`
    * Creating clients with builders
  * 'Key Concepts' section
  * 'Examples'
  * 'Troubleshooting'
  * 'Next Steps'
  * 'Contributing'

This can result in very long readme files. What follows is some suggestions on how we could improve our readme files:

1. **Remove the BOM and Maven dependency section**: Rather than have similar text in all readme files, perhaps we should include a short blurb that says something like the following:

> **Using this dependency**
>
> Azure SDK for Java libraries ship all libraries to Maven Central. This library is named `azure-data-appconfiguration`, and is included in the `azure-sdk-bom` for your convenience. If you use Maven, refer to the [Azure SDK for Java Maven](https://learn.microsoft.com/azure/developer/java/sdk/get-started-maven?view=azure-java-stable) docs, and if you use Gradle, refer to the [Azure SDK for Java Gradle](https://learn.microsoft.com/azure/developer/java/sdk/get-started-gradle?view=azure-java-stable) docs.

2. **Improve the 'Package (Maven)' links**: Currently these links point to, e.g. [https://search.maven.org/artifact/com.azure/azure-data-appconfiguration](https://search.maven.org/artifact/com.azure/azure-data-appconfiguration), but these links no longer resolve. We will need to update these links to instead point [here](https://central.sonatype.com/artifact/com.azure/azure-data-appconfiguration/1.4.3).

3. **Improve the 'API reference documentation' links**: Currently these links go to azure.github.io/azure-sdk-for-java, but these should instead point to [learn.microsoft.com](https://learn.microsoft.com/java/api/overview/azure/?view=azure-java-stable).

4. **Move 'Key Concepts' and 'Examples' out of readme**: Rather than have the 'key concepts' and 'examples' sections be part of the readme, lets instead put some, or all, of them in the reference documentation or a separate `samples/readme.md` file. We should instead simply have a 'Key Concepts and Examples' section that says something along the following lines shown below. Two variations to this would be to leave some core samples in the readme, or to link out explicitly to individual samples files in the 'samples/' directory.

> **Key Concepts and Examples**
>
> Key concepts, code examples, and usage instructions for this library are discussed in great detail in our reference documentation. **Click here** to see the reference documentation for this library. Additionally, there are more comprehensive code samples in the **samples/** directory of this library.

5. **Move 'Troubleshooting' section, where necessary, to external file**: Currently the troubleshooting section, at least in some readmes, contains general purpose troubleshooting information, along with occasional library-specific troubleshooting text. We should instead have text such as the following:

> **Troubleshooting**
>
> See our **troubleshooting guide** for details on how to diagnose various failure scenarios related specifically to this library. Additionally, refer to the **Azure SDK for Java troubleshooting** page to learn more about how to get started with troubleshooting issues when using the Azure SDK for Java client libraries.

6. Add 'Troubleshooting' link to top navigation section.

7. Remove 'Contributing' from each individual readme, instead rely on the root readme file to outline this process.

8. **Introduce a new 'Authentication' section'**: A list of all types of authentication a client library supports, with links to the JavaDoc describing each one in detail. It's hard to find this information unless you look at the builder. For example:

> **Authentication**
>
> This client library supports the following authentication methods:
>
> * Azure Active Directory
> * Access keys
> * Connection strings
> * SAS tokens

## Summary

The end result of these changes is that the readme files become drastically shorter, with the intention that we do not overload users with too much information up front. It means that we reduce the amount of information duplication, with the resulting outcome that we are less likely to have outdated guidance in any one place, and users have more trust in the accuracy of all documentation.