# Conventional Commit Content Guide

## Introduction to Conventional Commits

Conventional commits are a specification for adding human and machine-readable meaning to commit messages. This practice helps streamline the release process, create automated changelogs, and improve collaboration within your team. Conventional commits follow a specific format, allowing tools to parse the messages and generate meaningful documentation from your commit history.

## Conventional Commit Message Format

A conventional commit message consists of the following structure:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Components

1. **Type**: Indicates the nature of the change. Common types include:
   - **feat**: A new feature
   - **fix**: A bug fix
   - **docs**: Documentation changes
   - **style**: Code style changes (formatting, missing semi-colons, etc.)
   - **refactor**: Code changes that neither fix a bug nor add a feature
   - **perf**: Performance improvements
   - **test**: Adding or updating tests
   - **chore**: Maintenance tasks (build process, auxiliary tools, etc.)

2. **Scope** (optional): Specifies the area of the codebase affected by the commit. Common scopes include:
   - **api**: Changes to the API layer
   - **ui**: Changes to the user interface
   - **backend**: Backend system changes
   - **database**: Changes to the database schema or queries
   - **auth**: Authentication-related changes
   - **ci**: Changes to the continuous integration configuration
   - **deps**: Changes to dependencies

3. **Description**: A brief summary of the change.

4. **Body** (optional): Provides additional details about the change. This section can be several lines long and should explain the "why" and "how" of the change.

5. **Footer(s)** (optional): Includes any relevant metadata. Common footers include:
   - **BREAKING CHANGE**: Describes a breaking API change.
   - **Closes**: References the issue that the commit addresses.

### Using Conventional Commits for Changelogs

By adhering to conventional commit messages, you can automate the generation of changelogs. Here’s how to get started:

1. **Install Commitlint**:
   - Commitlint helps enforce conventional commit messages.
   - Install Commitlint and the conventional config:
     ```sh
     npm install --save-dev @commitlint/{cli,config-conventional}
     ```

   - Create a `commitlint.config.js` file:
     ```js
     module.exports = { extends: ['@commitlint/config-conventional'] };
     ```

2. **Generate Changelogs**:
   - Use tools like `standard-version` or `conventional-changelog` to generate changelogs.
   - Install `standard-version`:
     ```sh
     npm install --save-dev standard-version
     ```

   - Add a script in `package.json`:
     ```json
     "scripts": {
       "release": "standard-version"
     }
     ```

   - Generate a changelog:
     ```sh
     npm run release
     ```

   - This command will update your `CHANGELOG.md` based on the conventional commit messages in your repository.

## Hands-On Practice

### Practice Manual

1. **Clone the Repository**:
   ```sh
   git clone <repository-url>
   cd <repository-folder>
   ```

2. **Create a Feature Branch**:
   ```sh
   git checkout -b feat/add-greeting
   ```

3. **Edit a File**:
   - Open or create `greeting.txt`.
   - Add a greeting message (e.g., "Hello, team!").

4. **Stage and Commit the Change**:
   ```sh
   git add greeting.txt
   git commit -m "feat: add greeting message to greeting.txt"
   ```

5. **Push the Feature Branch**:
   ```sh
   git push origin feat/add-greeting
   ```

### Practical Examples for All Commit Types

1. **Feature Addition**:
```sh
   git checkout -b feat/add-welcome-message
   echo "Welcome to the team!" > welcome.txt
   git add welcome.txt
   git commit -m "feat(ui): add welcome message to welcome.txt"
   git push origin feat/add-welcome-message
```

2. **Bug Fix**:

```sh
   git checkout -b fix/fix-typo
   echo "Hello, World!" > greeting.txt
   git add greeting.txt
   git commit -m "fix(ui): fix typo in greeting message"
   git push origin fix/fix-typo
```

3. **Documentation**:

```sh
   git checkout -b docs/update-readme
   echo "Installation Instructions" > README.md
   git add README.md
   git commit -m "docs(readme): update installation instructions"
   git push origin docs/update-readme
```

4. **Refactor**:

```sh
   git checkout -b refactor/optimize-greeting
   echo "Hi, Team!" > greeting.txt
   git add greeting.txt
   git commit -m "refactor(backend): optimize greeting message logic"
   git push origin refactor/optimize-greeting
```

5. **Style**:

```sh
   git checkout -b style/reformat-code
   echo "Hello, World!" > greeting.txt
   git add greeting.txt
   git commit -m "style(auth): reformat greeting message code"
   git push origin style/reformat-code
```

6. **Performance**:

```sh
   git checkout -b perf/improve-query
   echo "Optimized Query" > query.sql
   git add query.sql
   git commit -m "perf(database): improve query execution time"
   git push origin perf/improve-query
```

7. **Test**:

```sh
   git checkout -b test/add-unit-tests
   echo "Test for greeting message" > test_greeting.txt
   git add test_greeting.txt
   git commit -m "test(api): add unit tests for greeting message"
   git push origin test/add-unit-tests
```

8. **Chore**:

```sh
   git checkout -b chore/update-dependencies
   echo "Updated dependencies" > dependencies.txt
   git add dependencies.txt
   git commit -m "chore(deps): update dependency versions"
   git push origin chore/update-dependencies
```

### Use Case: Corporate Audit Department

1. **Create a User Story**:

```sh
   git checkout -b feat/create-audit-checklist
   touch audit-checklist.txt
   echo "Initial checklist items" > audit-checklist.txt
   git add audit-checklist.txt
   git commit -m "feat: add initial audit checklist items"
   git push origin feat/create-audit-checklist
```

2. **Report a Bug**:
   
```sh
   git checkout -b fix/checklist-item-missing
   echo "Missing item added" >> audit-checklist.txt
   git add audit-checklist.txt
   git commit -m "fix: add missing item to audit checklist"
   git push origin fix/checklist-item-missing
```

3. **Update Documentation**:

```sh
   git checkout -b docs/update-checklist-docs
   echo "Updated checklist documentation" > checklist-docs.txt
   git add checklist-docs.txt
   git commit -m "docs(audit): update checklist documentation"
   git push origin docs/update-checklist-docs
```

4. **Optimize Performance**:

```sh
    git checkout -b perf/optimize-checklist-query
```