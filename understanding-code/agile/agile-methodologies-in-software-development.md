# Agile Methodologies in Software Development

>
>
> We are uncovering better ways of developing software by doing it and helping others do it.
> Through this work we have come to value:
>
> - **Individuals and interactions** over processes and tools
> - **Working software** over comprehensive documentation
> - **Customer collaboration** over contract negotiation
> - **Responding to change** over following a plan
>
> That is, while there is value in the items on
> the right, we value the items on the left more.
>
> Reference - [Agile Manifesto](https://agilemanifesto.org/)
>

## Agile Manifesto

The Agile Manifesto, created in 2001 by a group of software developers, outlines the core values and principles of agile software development. It emphasizes collaboration, flexibility, and delivering working software frequently. The **4 core values** are:

- **Individuals and Interactions over Processes and Tools**: Emphasizes the importance of collaboration and communication among team members.
- **Working Software over Comprehensive Documentation**: Focuses on delivering functional software that meets user needs.
- **Customer Collaboration over Contract Negotiation**: Encourages continuous customer involvement and feedback throughout the development process.
- **Responding to Change over Following a Plan**: Prioritizes adaptability and responsiveness to changing requirements.

Agile methodologies are guided by **12 key principles**, which include:

- **Customer Satisfaction**: Delivering valuable software early and continuously.
- **Welcome Changing Requirements**: Agile processes harness change for the customer's competitive advantage.
- **Frequent Delivery**: Deliver working software frequently, with a preference for shorter timescales.
- **Collaboration**: Business people and developers must work together daily throughout the project.
- **Motivated Individuals**: Build projects around motivated individuals and trust them to get the job done.
- **Face-to-Face Conversation**: The most efficient and effective method of conveying information is face-to-face conversation.
- **Working Software**: The primary measure of progress is working software.
- **Sustainable Development**: Agile processes promote sustainable development, maintaining a constant pace.
- **Technical Excellence**: Continuous attention to technical excellence and good design enhances agility.
- **Simplicity**: Maximizing the amount of work not done is essential.
- **Self-Organizing Teams**: The best architectures, requirements, and designs emerge from self-organizing teams.
- **Reflect and Adjust**: Regularly reflect on how to become more effective and adjust accordingly.

>
> We follow these principles:
>
> 1. Our highest priority is to satisfy the customer through early and continuous delivery of valuable software.
> 2. Welcome changing requirements, even late in development. Agile processes harness change for the customer's competitive advantage.
> 3. Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
> 4. Business people and developers must work together daily throughout the project.
> 5. Build projects around motivated individuals. Give them the environment and support they need, and trust them to get the job done.
> 6. The most efficient and effective method of conveying information to and within a development team is face-to-face conversation.
> 7. Working software is the primary measure of progress.
> 8. Agile processes promote sustainable development. The sponsors, developers, and users should be able to maintain a constant pace indefinitely.
> 9. Continuous attention to technical excellence and good design enhances agility.
> 10. Simplicity--the art of maximizing the amount of work not done--is essential.
> 11. The best architectures, requirements, and designs emerge from self-organizing teams.
> 12. At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behavior accordingly.
>
> Reference - [Agile Manifesto - Principles](https://agilemanifesto.org/principles.html)
>

## Agile Methodologies

### Scrum

Scrum is an iterative and incremental framework for managing complex projects. It includes roles such as the Product Owner, Scrum Master, and Development Team. Key events include Sprint Planning, Daily Stand-ups, Sprint Reviews, and Sprint Retrospectives. Artifacts include the Product Backlog, Sprint Backlog, and Increment.

**Sample Sprint Cycle**:
- **Sprint Duration**: 2 weeks
- **Sprint Planning**: 4 hours at the beginning of the sprint
- **Daily Stand-up**: 15 minutes each day
- **Sprint Review**: 2 hours at the end of the sprint
- **Sprint Retrospective**: 1.5 hours at the end of the sprint

Wiki: [Scrum Methodology in Software Development](./agile-methodologies-scrum-in-software-development.md)

### Kanban

Kanban focuses on visualizing work, limiting work in progress (WIP), and managing flow. It uses a Kanban board divided into columns representing stages of the process. Work items move across the board, and WIP limits ensure a steady flow.

**Sample WIP Limits**:
- **Backlog**: Unlimited
- **In Progress**: Maximum of 5 tasks
- **Code Review**: Maximum of 3 tasks
- **Testing**: Maximum of 2 tasks

Wiki: [Kanban Methodology in Software Development](./agile-methodologies-kanban-in-software-development.md)

## Continuous Improvement (Kaizen)

Kaizen, meaning "change for the better" in Japanese, is a philosophy that encourages continuous, incremental improvements. In agile, Kaizen involves regularly reflecting on processes, identifying areas for improvement, and implementing changes. This practice is integral to retrospectives in Scrum and regular reviews in Kanban.

## Roles in Agile

- **Product Owner**: Manages the product backlog, prioritizes work, and ensures the team is working on the most valuable items.
- **Scrum Master/Kanban Facilitator**: Facilitates the process, ensures adherence to agile practices, and removes impediments.
- **Development Team**: Cross-functional group responsible for delivering the product increment.

## Tools for Agile in Azure DevOps

Azure DevOps provides several tools to support agile practices:

- **Boards**: For managing work items, creating Kanban boards, and tracking progress.
- **Repos**: For source control, supporting Git repositories.
- **Pipelines**: For continuous integration and continuous deployment (CI/CD).
- **Test Plans**: For managing test cases, test plans, and running automated tests.
- **Artifacts**: For package management and sharing code dependencies.

## Sample Implementation in Azure DevOps

1. **Setting Up a Project**: Create a new project in Azure DevOps, selecting the appropriate process template (Scrum or Agile).
2. **Managing the Product Backlog**: Use Azure Boards to add and prioritize work items, including detailed descriptions, acceptance criteria, and attachments.
3. **Sprint Planning**: Select backlog items and move them to the sprint backlog using the sprint planning tools in Azure DevOps.
4. **Daily Stand-ups**: Update the status of work items on the Kanban board, facilitating effective daily stand-ups.
5. **Sprint Review and Retrospective**: Use Azure DevOps dashboards and analytics for insights into team progress and performance. Document feedback and improvement actions using integrated tools like Confluence or third-party retrospective tools.

## References for Further Reading

- [Agile Manifesto](https://agilemanifesto.org/)
- [Scrum Guide](https://scrumguides.org/scrum-guide.html)
- [Kanban Guide](https://kanban.university/)
- [Azure DevOps Agile Tools](https://docs.microsoft.com/en-us/azure/devops/boards/get-started/what-is-azure-boards?view=azure-devops)

---
