### Wiki 1: Azure Boards

#### History and Evolution

Azure Boards is a critical component of the Azure DevOps suite, designed to facilitate agile project management. Initially, it was a feature of Visual Studio Team Services (VSTS), where it incorporated work item tracking and project management functionalities. Over time, as VSTS transitioned to Azure DevOps, Azure Boards was significantly enhanced to support modern agile methodologies such as Scrum and Kanban. Its evolution includes improved integration with other Azure DevOps services and third-party tools, making it a comprehensive tool for managing the entire development lifecycle.

#### 1. Key Features

Azure Boards offers an extensive set of features designed to streamline agile project management. These features include work item tracking, backlogs, Kanban boards, sprint planning, and querying capabilities.

##### 1.1 Work Items

Azure Boards provides a robust system for tracking and managing various types of work items, including user stories, tasks, bugs, and issues. Work items can be customized to fit specific project needs, allowing teams to tailor the tool to their processes.

![Work Items](placeholder1)
*Figure 1.1: Work Items Interface*

##### 1.2 Backlogs

Backlogs in Azure Boards help teams organize and prioritize work items. Product backlogs encompass high-level requirements, while iteration backlogs focus on tasks for a specific sprint or iteration. This structured approach ensures all work items are accounted for and progress is easily trackable.

![Backlogs](placeholder2)
*Figure 1.2: Backlogs View*

##### 1.3 Kanban Boards

Kanban boards offer a visual way to manage work in progress. Teams can customize columns to reflect their workflow, use swimlanes to differentiate types of work, and adjust card styles for better visibility. This visualization helps teams identify bottlenecks and optimize processes.

![Kanban Boards](placeholder3)
*Figure 1.3: Kanban Boards*

##### 1.4 Sprint Planning

Sprint planning in Azure Boards includes tools for managing iterations, tracking capacity, and viewing sprint burndown charts. These features help teams plan their work for each sprint, ensuring they do not overcommit and can deliver high-quality work within the iteration timeframe.

![Sprints](placeholder4)
*Figure 1.4: Sprint Planning*

##### 1.5 Queries

Azure Boards offers powerful querying capabilities. Teams can create custom queries to filter and find specific work items based on various criteria. Saved queries can be shared with team members, promoting transparency and collaboration.

![Queries](placeholder5)
*Figure 1.5: Work Item Queries*

#### 1.6 Getting Started

To begin using Azure Boards, navigate to the Azure DevOps portal and select the Boards option. From here, you can start creating and managing work items, organizing your backlogs, and setting up your Kanban boards and sprints. Customize your workflow and queries to fit your team’s needs and streamline your project management processes.

For more detailed information on using Azure Boards, refer to the [Azure Boards Documentation](https://docs.microsoft.com/en-us/azure/devops/boards/).

#### 1.7 References

- [Azure DevOps Blog](https://devblogs.microsoft.com/devops/)
- "Agile Project Management with Azure DevOps" by Joachim Rossberg

#### 1.8 Related Wiki

- [Next: Wiki 2: Azure Repos](#)

This wiki provides a comprehensive overview of Azure Boards, highlighting its history, key features, and practical usage. Use this guide to effectively manage your agile projects and enhance your team's productivity.

---

### Wiki 2: Azure Repos

#### History and Evolution

Azure Repos is a source code management system within the Azure DevOps suite, supporting both Git and Team Foundation Version Control (TFVC). It has its roots in Team Foundation Server (TFS) and later Visual Studio Team Services (VSTS). Over time, Azure Repos has evolved into a robust version control system that supports modern development practices, including branching strategies, pull requests, and CI/CD integrations.

#### 2. Key Features

Azure Repos allows teams to create and manage Git repositories, providing a central location for storing and versioning source code. With Git repositories, teams can leverage branching and merging to manage changes to the codebase effectively. This facilitates parallel development, feature isolation, and experimentation without affecting the main codebase.

##### 2.1 Pull Requests

Pull requests in Azure Repos enable code review and collaboration. Developers can submit pull requests to propose changes, which team members can review, comment on, and approve. This process ensures that code is reviewed for quality and consistency before being merged into the main branch. Additionally, policies can be set to require certain conditions, such as passing builds or specific reviewers, before a pull request can be merged.

![Pull Requests](placeholder1)
*Figure 2.1: Pull Requests Interface*

##### 2.2 Branch Policies

Branch policies in Azure Repos help enforce standards and practices within the codebase. These policies can include requirements for code review, build validation, and status checks. By enforcing these policies, teams can maintain high code quality and prevent issues from being introduced into the main branch.

![Branch Policies](placeholder2)
*Figure 2.2: Branch Policies*

##### 2.3 Code Search

Azure Repos offers a powerful code search feature that allows teams to search across repositories to find specific code, references, and definitions. Advanced search syntax helps refine search results, making it easier to locate the necessary code quickly.

![Code Search](placeholder3)
*Figure 2.3: Code Search*

##### 2.4 Commit History

The commit history feature in Azure Repos provides a detailed view of changes made to the codebase. Teams can track commits, view diffs, and read comments associated with each change. This historical context helps teams understand the evolution of the code and the rationale behind specific changes.

![Commit History](placeholder4)
*Figure 2.4: Commit History*

#### 2.5 Getting Started

To begin using Azure Repos, navigate to the Azure DevOps portal and select the Repos option. From here, you can create repositories, set up branching strategies, and start managing your source code. Integrate pull requests and branch policies to ensure code quality and streamline your development workflow.

For more detailed information on using Azure Repos, refer to the [Azure Repos Documentation](https://docs.microsoft.com/en-us/azure/devops/repos/).

#### 2.6 References

- "Professional Team Foundation Server 2013" by Steven St. Jean, Ed Blankenship, Martin Woodward, and Grant Holliday
- [Pro Git Book](https://git-scm.com/book/en/v2)

#### 2.7 Related Wiki

- [Next: Wiki 3: Azure Pipelines](#)

This wiki provides a comprehensive overview of Azure Repos, highlighting its history, key features, and practical usage. Use this guide to effectively manage your source code and enhance your team's productivity.

---

### Wiki 3: Azure Pipelines

#### History and Evolution

Azure Pipelines is a continuous integration and continuous delivery (CI/CD) service within Azure DevOps. Originally part of Visual Studio Team Services (VSTS), Azure Pipelines has evolved to support a wide range of languages and platforms, integrating seamlessly with GitHub, Bitbucket, and other repository services. Over time, it has become a versatile tool for automating the build, test, and deployment processes, supporting both Windows and Linux environments.

#### 3. Key Features

Azure Pipelines offers robust features to automate the CI/CD process, enabling teams to deliver high-quality software faster and with greater reliability. These features include YAML pipelines, classic release pipelines, and integration with various third-party services.

##### 3.1 YAML Pipelines

YAML pipelines provide a code-centric approach to defining CI/CD workflows. Teams can create and version their pipeline definitions using YAML files, which are stored in the repository alongside the source code. This approach promotes transparency and collaboration, as pipeline configurations are versioned and can be reviewed just like code changes.

![YAML Pipelines](placeholder1)
*Figure 3.1: YAML Pipelines Configuration*

##### 3.2 Classic Release Pipelines

Classic release pipelines offer a visual editor for defining CI/CD workflows. Teams can create pipelines by dragging and dropping tasks and configuring stages in a graphical interface. This approach is ideal for those who prefer a more visual representation of their CI/CD process.

![Classic Release Pipelines](placeholder2)
*Figure 3.2: Classic Release Pipelines*

##### 3.3 Integration with Third-Party Services

Azure Pipelines integrates with numerous third-party services, such as Docker, Kubernetes, and various testing tools. This integration allows teams to build, test, and deploy applications using the tools and services they are already familiar with, enhancing their existing workflows.

![Third-Party Integration](placeholder3)
*Figure 3.3: Integration with Third-Party Services*

#### 3.4 Getting Started

To begin using Azure Pipelines, navigate to the Azure DevOps portal and select the Pipelines option. From here, you can create new pipelines using either the YAML or classic editor. Connect your repository, configure your build and release stages, and start automating your CI/CD processes.

For more detailed information on using Azure Pipelines, refer to the [Azure Pipelines Documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/).

#### 3.5 References

- "The Phoenix Project" by Gene Kim, Kevin Behr, and George Spafford
- [Azure DevOps Blog](https://devblogs.microsoft.com/devops/)

#### 3.6 Related Wiki

- [Next: Wiki 4: Azure Test Plans](#)

This wiki provides a comprehensive overview of Azure Pipelines, highlighting its history, key features, and practical usage. Use this guide to automate your build, test, and deployment processes and enhance

 your team's productivity.

---

### Wiki 4: Azure Test Plans

#### History and Evolution

Azure Test Plans is a comprehensive test management solution within the Azure DevOps suite. Initially part of Visual Studio Team Services (VSTS), it evolved from basic test case management to a full-featured platform supporting manual, exploratory, and automated testing. This evolution includes enhanced integration with other Azure DevOps services, offering a seamless testing experience within the CI/CD pipeline.

#### 4. Key Features

Azure Test Plans provides a wide range of features to support the testing process, including test case management, exploratory testing, and integration with automated testing frameworks.

##### 4.1 Test Case Management

Azure Test Plans allows teams to create, manage, and execute test cases. Test cases can be organized into test suites and plans, enabling structured testing and comprehensive coverage of application functionality. Teams can also link test cases to work items, ensuring traceability between requirements and testing efforts.

![Test Case Management](placeholder1)
*Figure 4.1: Test Case Management Interface*

##### 4.2 Exploratory Testing

Exploratory testing in Azure Test Plans supports ad-hoc testing sessions where testers can explore the application and document findings without predefined test cases. This approach is useful for discovering unexpected issues and gaining insights into application behavior.

![Exploratory Testing](placeholder2)
*Figure 4.2: Exploratory Testing*

##### 4.3 Integration with Automated Testing

Azure Test Plans integrates with various automated testing frameworks, such as Selenium and Appium. This integration allows teams to execute automated tests within their CI/CD pipelines, ensuring that code changes are thoroughly tested before deployment.

![Automated Testing Integration](placeholder3)
*Figure 4.3: Integration with Automated Testing*

#### 4.4 Getting Started

To begin using Azure Test Plans, navigate to the Azure DevOps portal and select the Test Plans option. From here, you can create test plans and suites, define test cases, and start executing tests. Integrate your automated tests to enhance your testing strategy and improve application quality.

For more detailed information on using Azure Test Plans, refer to the [Azure Test Plans Documentation](https://docs.microsoft.com/en-us/azure/devops/test-plans/).

#### 4.5 References

- "Exploratory Software Testing" by James A. Whittaker
- [Test Management in Azure DevOps](https://devblogs.microsoft.com/devops/)

#### 4.6 Related Wiki

- [Next: Wiki 5: Azure Artifacts](#)

This wiki provides a comprehensive overview of Azure Test Plans, highlighting its history, key features, and practical usage. Use this guide to manage your testing processes effectively and ensure high-quality software releases.

---

### Wiki 5: Azure Artifacts

#### History and Evolution

Azure Artifacts is a package management solution within the Azure DevOps suite, designed to help teams manage and share code dependencies. Originally part of Visual Studio Team Services (VSTS), Azure Artifacts has evolved to support multiple package types, including NuGet, npm, Maven, and Python packages. This evolution includes enhanced security features and integration with CI/CD pipelines, making it a versatile tool for managing project dependencies.

#### 5. Key Features

Azure Artifacts provides robust features for managing and sharing packages, including feeds, upstream sources, and retention policies.

##### 5.1 Feeds

Feeds in Azure Artifacts allow teams to create and manage collections of packages. Teams can publish packages to feeds and control access to these packages, ensuring that only authorized users can consume them. Feeds can be scoped to a project or organization, providing flexibility in how packages are shared and managed.

![Feeds](placeholder1)
*Figure 5.1: Feeds Interface*

##### 5.2 Upstream Sources

Upstream sources enable teams to consume packages from external sources, such as public registries or other Azure Artifacts feeds. This feature simplifies dependency management by allowing teams to access all required packages from a single feed, reducing the need to configure multiple package sources.

![Upstream Sources](placeholder2)
*Figure 5.2: Upstream Sources*

##### 5.3 Retention Policies

Retention policies in Azure Artifacts help manage the lifecycle of packages by automatically cleaning up older versions based on predefined criteria. This feature ensures that feeds do not become cluttered with obsolete packages, maintaining a clean and efficient package repository.

![Retention Policies](placeholder3)
*Figure 5.3: Retention Policies*

#### 5.4 Getting Started

To begin using Azure Artifacts, navigate to the Azure DevOps portal and select the Artifacts option. From here, you can create feeds, publish packages, and configure upstream sources. Implement retention policies to manage your package lifecycle and ensure efficient use of storage.

For more detailed information on using Azure Artifacts, refer to the [Azure Artifacts Documentation](https://docs.microsoft.com/en-us/azure/devops/artifacts/).

#### 5.5 References

- "Managing Dependencies in Microsoft .NET Projects" by Jesse Liberty
- [Azure DevOps Blog](https://devblogs.microsoft.com/devops/)

#### 5.6 Related Wiki

- [Next: Wiki 6: Azure DevOps Extensions](#)

This wiki provides a comprehensive overview of Azure Artifacts, highlighting its history, key features, and practical usage. Use this guide to manage your project dependencies effectively and streamline your development workflow.