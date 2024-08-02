# Git and Version Control Basics

## Introduction

Git is a powerful and widely used version control system that helps teams manage and track changes to their codebase efficiently. Understanding the basics of Git and version control concepts is essential for collaborative software development. This guide provides an overview of key Git concepts and commands, helping your team become proficient in using Git for version control.

## What is Version Control?

### 1. Definition

Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. It allows multiple developers to work on a project simultaneously without overwriting each other's changes.

### 2. Benefits

- **Collaboration**: Enables multiple developers to work on the same project.
- **History**: Keeps a detailed history of changes.
- **Backup**: Serves as a backup system for your code.
- **Branching and Merging**: Allows developers to work on new features without affecting the main codebase.

## Git Basics

### 1. Git Repositories

A Git repository is a collection of files and directories that Git tracks. Repositories can be local (on your computer) or remote (on a server).

### 2. Common Git Commands

- **git init**: Initializes a new Git repository.
- **git clone [url]**: Clones a remote repository to your local machine.
- **git status**: Shows the current status of your working directory.
- **git add [file]**: Stages changes for the next commit.
- **git commit -m "message"**: Commits staged changes with a descriptive message.
- **git push**: Pushes commits to a remote repository.
- **git pull**: Fetches and merges changes from a remote repository.

### 3. Git Workflow

A typical Git workflow involves the following steps:

1. **Cloning a Repository**: 

   ```sh
   git clone https://github.com/username/repository.git
   ```

2. **Making Changes**: Edit files in your working directory.

3. **Staging Changes**:

   ```sh
   git add filename
   ```

4. **Committing Changes**:

   ```sh
   git commit -m "Your commit message"
   ```

5. **Pushing Changes**:

   ```sh
   git push
   ```

### 4. Branching and Merging

Branches allow you to work on different parts of a project independently. The **main** branch is the default branch where all changes are eventually merged.

- **Creating a Branch**:

  ```sh
  git checkout -b new-feature
  ```

- **Switching Branches**:

  ```sh
  git checkout main
  ```

- **Merging Branches**:

  ```sh
  git merge new-feature
  ```

### 5. Resolving Conflicts

Conflicts occur when changes in different branches overlap. Git highlights conflicts in the affected files, and you must manually resolve them.

### 6. Remote Repositories

Remote repositories, such as those on GitHub or GitLab, facilitate collaboration. Commands like `git push` and `git pull` synchronize changes between your local repository and the remote repository.

## Hands-On Practice

### Practice Manual

1. **Clone a Repository**:

   ```sh
   git clone https://github.com/username/repository.git
   ```

2. **Create a Branch**:

   ```sh
   git checkout -b new-feature
   ```

3. **Make Changes**:
   - Edit or create a file in the repository.
   - For example, create a file named `example.txt` and add some text.

4. **Stage and Commit Changes**:

   ```sh
   git add example.txt
   git commit -m "feat: add example file with initial content"
   ```

5. **Push Changes**:

   ```sh
   git push origin new-feature
   ```

6. **Create a Pull Request** (if using GitHub):
   - Navigate to your repository on GitHub.
   - Click the "Pull Requests" tab.
   - Click "New Pull Request" and follow the prompts.

7. **Merge Branches**:

   ```sh
   git checkout main
   git merge new-feature
   ```

### Use Case: Government Project

1. **User Story**: As a developer, I want to create a new branch to add a feature for managing government audit reports.

2. **Step-by-Step**:
   - **Clone the repository**:

     ```sh
     git clone https://github.com/gov-project/audit-management.git
     ```

   - **Create a new branch**:

     ```sh
     git checkout -b feat/manage-audit-reports
     ```

   - **Edit or create a file**:
     - Create a file named `audit_reports.txt` and add initial content.

   - **Stage and commit the changes**:

     ```sh
     git add audit_reports.txt
     git commit -m "feat: add initial audit reports management feature"
     ```

   - **Push the branch to the remote repository**:

     ```sh
     git push origin feat/manage-audit-reports
     ```

   - **Create a pull request** on the remote repository platform.

   - **Merge the feature branch**:

     ```sh
     git checkout main
     git merge feat/manage-audit-reports
     ```
