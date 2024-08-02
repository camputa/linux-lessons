# Hands-On Practical Manual for New Developers: Git and Azure DevOps

## Introduction

Welcome to the team! This practical manual is designed to help you get started with Git and Azure DevOps. By following this guide, you will learn how to checkout code, clone repositories, add a remote origin, perform `git diff` between feature branches, commit changes using conventional commit messages, and more. This tutorial will take you through a simple text file-based exercise to practice these essential Git commands and workflows.

## Prerequisites

Before you begin, ensure you have the following:

- Git installed on your local machine.
- Access to the Azure DevOps organization and project.
- A basic understanding of Git and version control concepts.

## Step-by-Step Guide

### Step 1: Clone the Repository

1. **Navigate to Azure DevOps**:
   - Open your web browser and go to your Azure DevOps organization.
   - Select the project you will be working on.
   - Go to "Repos" and find the repository you need to clone.

2. **Clone the Repository**:
   - Copy the HTTPS or SSH URL of the repository.
   - Open your terminal or command prompt and run the following command to clone the repository:

     ```sh
     git clone <repository-url>
     ```

   - Replace `<repository-url>` with the URL you copied from Azure DevOps.

### Step 2: Add a Remote Origin (if not already added)

1. **Check Current Remote**:
   - Navigate to the cloned repository folder:

     ```sh
     cd <repository-folder>
     ```

   - Run the following command to check the current remote URL:

     ```sh
     git remote -v
     ```

2. **Add Remote Origin**:
   - If the remote origin is not set or needs to be updated, run the following command:

     ```sh
     git remote add origin <repository-url>
     ```

   - Replace `<repository-url>` with the URL of your repository.

### Step 3: Checkout Code and Create a Feature Branch

1. **Create a Feature Branch**:
   - Run the following command to create a new feature branch:

     ```sh
     git checkout -b feature/add-name
     ```

   - This command creates a new branch named `feature/add-name` and switches to it.

### Step 4: Make Changes and Commit with Conventional Commit Messages

1. **Create or Edit a Text File**:
   - Open or create a text file named `team.txt` in your repository folder.
   - Add your name to the file, save, and close it.

2. **Stage Changes**:
   - Run the following command to stage your changes:

     ```sh
     git add team.txt
     ```

3. **Commit Changes**:
   - Commit your changes using a conventional commit message format:

     ```sh
     git commit -m "feat: add name to team.txt"
     ```

   - The `feat:` prefix indicates a new feature as per conventional commit guidelines.

### Step 5: Push Changes to Remote Repository

1. **Push Changes**:
   - Run the following command to push your feature branch to the remote repository:

     ```sh
     git push origin feature/add-name
     ```

### Step 6: Perform a `git diff` Between Branches

1. **Create Another Branch and Make Changes**:
   - Create a new branch and add a different name to the `team.txt` file:

     ```sh
     git checkout -b feature/add-another-name
     echo "Another Name" >> team.txt
     git add team.txt
     git commit -m "feat: add another name to team.txt"
     ```

2. **Compare Branches**:
   - Run the following command to see the differences between the two branches:

     ```sh
     git diff feature/add-name feature/add-another-name
     ```

### Step 7: Revert Changes

1. **Revert the Last Commit**:
   - Run the following command to revert your last commit:

     ```sh
     git revert HEAD
     ```

   - This will create a new commit that undoes the changes introduced by the previous commit.

### Step 8: Merge Feature Branch into Main Branch

1. **Switch to Main Branch**:
   - Run the following command to switch to the main branch:

     ```sh
     git checkout main
     ```

2. **Merge Feature Branch**:
   - Run the following command to merge the feature branch into the main branch:

     ```sh
     git merge feature/add-name
     ```

3. **Push Changes to Remote**:
   - Run the following command to push the merged changes to the remote repository:

     ```sh
     git push origin main
     ```

## Conclusion

By following this hands-on practical manual, you have learned how to clone a repository, add a remote origin, create and switch branches, make and commit changes using conventional commit messages, compare branches, revert changes, and merge branches using Git and Azure DevOps. These skills are essential for effective version control and collaboration within your development team. Keep practicing these commands to build confidence and proficiency in using Git and Azure DevOps.