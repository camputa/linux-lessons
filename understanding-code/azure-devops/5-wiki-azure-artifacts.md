# Wiki 5: Azure Artifacts

Azure Artifacts is a package management solution within the Azure DevOps suite, designed to help teams manage and share code dependencies. Originally part of Visual Studio Team Services (VSTS), Azure Artifacts has evolved to support multiple package types, including NuGet, npm, Maven, and Python packages. This evolution includes enhanced security features and integration with CI/CD pipelines, making it a versatile tool for managing project dependencies.

## Key Features

Azure Artifacts provides robust features for managing and sharing packages, including feeds, upstream sources, and retention policies.

### Feeds

Feeds in Azure Artifacts allow teams to create and manage collections of packages. Teams can publish packages to feeds and control access to these packages, ensuring that only authorized users can consume them. Feeds can be scoped to a project or organization, providing flexibility in how packages are shared and managed.

### Upstream Sources

Upstream sources enable teams to consume packages from external sources, such as public registries or other Azure Artifacts feeds. This feature simplifies dependency management by allowing teams to access all required packages from a single feed, reducing the need to configure multiple package sources.

### Retention Policies

Retention policies in Azure Artifacts help manage the lifecycle of packages by automatically cleaning up older versions based on predefined criteria. This feature ensures that feeds do not become cluttered with obsolete packages, maintaining a clean and efficient package repository.

## Getting Started

To begin using Azure Artifacts, navigate to the Azure DevOps portal and select the Artifacts option. From here, you can create feeds, publish packages, and configure upstream sources. Implement retention policies to manage your package lifecycle and ensure efficient use of storage.

For more detailed information on using Azure Artifacts, refer to the [Azure Artifacts Documentation](https://docs.microsoft.com/en-us/azure/devops/artifacts/).

## References

- "Managing Dependencies in Microsoft .NET Projects" by Jesse Liberty
- [Azure DevOps Blog](https://devblogs.microsoft.com/devops/)

## Related Wiki

- [Next: Sample Azure DevOps Work Items - Government Portal](./hand-on-sample-user-stories-tasks-template-azure-devops-practice.md)

This wiki provides a comprehensive overview of Azure Artifacts, highlighting its history, key features, and practical usage. Use this guide to manage your project dependencies effectively and streamline your development workflow.