---
tags:
- github
---

### Git: Overview

**Definition**: Git is a distributed version control system (VCS) that tracks changes to files, enabling multiple developers to collaborate on projects. It allows users to save snapshots of their code (commits) and revert to earlier versions if needed.

**Key Concepts**:

- **Repository**: A storage space for your project, containing all files, folders, and the history of changes.
- **Commit**: A snapshot of changes saved in the repository. Each commit has a unique ID and a message describing the changes.
- **Branch**: A separate line of development, allowing for parallel work without affecting the main codebase. Common branches include `main` (or `master`) and `feature` branches.
- **Merge**: The process of integrating changes from one branch into another, typically to combine work into the main branch.
- **Remote**: A version of the repository hosted on a server (e.g., GitHub, GitLab). Users can `push` changes to a remote repository or `pull` updates from it.
- **Distributed**: Unlike centralized systems, every user has a full copy of the repository, enabling offline work and decentralized collaboration.

**Core Commands**:

- `git init`: Initializes a new Git repository.
- `git clone`: Creates a local copy of a remote repository.
- `git add`: Stages changes for the next commit.
- `git commit`: Saves staged changes with a descriptive message.
- `git push`: Uploads local commits to a remote repository.
- `git pull`: Fetches and integrates updates from a remote repository.
- `git branch`: Lists, creates, or deletes branches.
- `git merge`: Combines changes from one branch into another.

**Use Cases**:

- **Version Control**: Track changes to code, documents, or other files, making it easier to revert to previous versions.
- **Collaboration**: Multiple contributors can work on different parts of a project without interfering with each other's work.
- **Backup**: Each local copy of a Git repository serves as a backup, ensuring project continuity.

**Benefits**:

- **Decentralization**: Each developer has a full copy of the project's history, enhancing collaboration and resilience.
- **Flexibility**: Supports complex workflows, including feature development, bug fixing, and release management.
- **Efficiency**: Lightweight operations and fast branching/merging enable efficient project management.

  [[VSCode]]  [[Python]]  [[Obsidian Git Plugin]]  [[GitHub]]
