# Wiki 2: Azure Repos

Azure Repos is a source code management system within the Azure DevOps suite, supporting both Git and Team Foundation Version Control (TFVC). It has its roots in Team Foundation Server (TFS) and later Visual Studio Team Services (VSTS). Over time, Azure Repos has evolved into a robust version control system that supports modern development practices, including branching strategies, pull requests, and CI/CD integrations.

## Key Features

Azure Repos allows teams to create and manage Git repositories, providing a central location for storing and versioning source code. With Git repositories, teams can leverage branching and merging to manage changes to the codebase effectively. This facilitates parallel development, feature isolation, and experimentation without affecting the main codebase.

### Pull Requests

Pull requests in Azure Repos enable code review and collaboration. Developers can submit pull requests to propose changes, which team members can review, comment on, and approve. This process ensures that code is reviewed for quality and consistency before being merged into the main branch. Additionally, policies can be set to require certain conditions, such as passing builds or specific reviewers, before a pull request can be merged.

### Branch Policies

Branch policies in Azure Repos help enforce standards and practices within the codebase. These policies can include requirements for code review, build validation, and status checks. By enforcing these policies, teams can maintain high code quality and prevent issues from being introduced into the main branch.

### Code Search

Azure Repos offers a powerful code search feature that allows teams to search across repositories to find specific code, references, and definitions. Advanced search syntax helps refine search results, making it easier to locate the necessary code quickly.

### Commit History

The commit history feature in Azure Repos provides a detailed view of changes made to the codebase. Teams can track commits, view diffs, and read comments associated with each change. This historical context helps teams understand the evolution of the code and the rationale behind specific changes.

### Getting Started

To begin using Azure Repos, navigate to the Azure DevOps portal and select the Repos option. From here, you can create repositories, set up branching strategies, and start managing your source code. Integrate pull requests and branch policies to ensure code quality and streamline your development workflow.

For more detailed information on using Azure Repos, refer to the [Azure Repos Documentation](https://docs.microsoft.com/en-us/azure/devops/repos/).

### References

- "Professional Team Foundation Server 2013" by Steven St. Jean, Ed Blankenship, Martin Woodward, and Grant Holliday
- [Pro Git Book](https://git-scm.com/book/en/v2)

### Related Wiki

- [Next: Wiki 3: Azure Pipelines](3-wiki-azure-pipelines.md)

This wiki provides a comprehensive overview of Azure Repos, highlighting its history, key features, and practical usage. Use this guide to effectively manage your source code and enhance your team's productivity.