---
tags:
- github
video-url: https://www.youtube.com/watch?v=HjfEg1pBpjI&list=WL&index=2
---

## **SECRET Git Tricks**

It looks like you've provided a transcript of a video or a piece of content discussing advanced Git features. I'll break down the content, provide Git commands, tips on using the features mentioned, and relevant GitHub links or plugin suggestions where applicable.

Let’s dive into the detailed overview:

### 1. **Overview of Git**

- **Git Origins**: Git was initially created by Linus Torvalds for Linux kernel development. It has grown into the most popular version control system with around 150 commands.
- **Command Categories**:
  - **Core Commands**: There are 82 core commands that developers typically don't touch directly.
  - **Main Commands**: You’re likely familiar with the 44 main commands like `commit`, `push`, `pull`.
  - **Manipulators**: These include commands like `config` (to set configurations) and `reflog`.
  - **Interrogators**: Commands like `git blame` that help investigate commits.

### 2. **Useful Git Configurations**

- **Git Config Basics**:
  - Use `git config` to set different types of configurations.
  - `git config -l` lists all local configurations.
  - Add the `--global` flag to set global configurations, like:
    ```sh
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    ```
  - View global configuration:
    ```sh
    git config --list --global --show-origin
    ```
- **Conditional Configs**:
  - **Use Case**: Set a different email for work and personal projects.
  - **Implementation**:
    - Add an "include" section to your global `.gitconfig`:
      ```bash
      [includeIf "gitdir:~/work/"]
          path = ~/work/.gitconfig-work
      ```
    - This sets configurations based on your project directory.

### 3. **Alias Functionality**

- **Creating Aliases**:
  - Aliases can simplify your Git workflows. Examples include:
    ```sh
    git config --global alias.stashall '!git stash --all'
    git config --global alias.co checkout
    ```
  - Example: The alias for `stash --all` named `stashall` will stash everything (tracked and untracked files).

### 4. **ReReRe - Reuse Recorded Resolution**

- **Feature**: Automatically resolves previously resolved merge conflicts.
  - Enable it:
    ```sh
    git config --global rerere.enabled true
    ```
  - This is particularly useful for long-lived branches or rebasing workflows.

### 5. **Interrogating Commits**

- **Advanced Git Blame**:
  - The `git blame` command can be enhanced with flags:
    - `-w`: Ignores whitespace changes to avoid irrelevant commits.
    - `-C`: Tracks moved code between files.
    - Usage:
      ```sh
      git blame -w file.txt
      git blame -C file.txt
      ```
    - `-C -C -C` helps trace code copies across the project’s entire history.
- **Search within Logs**:
  - Search for specific keywords within the commit messages:
    ```sh
    git log -S "bug"
    git log -S "bug" -p
    ```

### 6. **New and Advanced Git Features**

- **Signing Commits with SSH Keys**:
  - Now, you can sign commits using your SSH keys instead of GPG:
    ```sh
    git config --global gpg.format ssh
    git config --global user.signingkey /path/to/public/key
    ```
- **Git Maintenance**:
  - Add a cron job for periodic repository maintenance:
    ```sh
    git maintenance start
    ```
  - To run specific tasks like garbage collection, you can:
    ```sh
    git maintenance run --task=gc
    ```

### 7. **Safe Force Pushing**

- **Force Pushing with Safety**:
  - Avoid overwriting others' changes with `--force-with-lease`:
    ```sh
    git push --force-with-lease
    ```
  - Create an alias for this:
    ```sh
    git config --global alias.pfwl 'push --force-with-lease'
    ```

### 8. **Git Worktrees**

- **Git Worktrees**:
  - Worktrees allow you to work on multiple branches simultaneously without stashing or resetting:
    ```sh
    git worktree add ../feature_branch
    ```
  - This way, you can avoid the hassle of frequently switching branches.

### 9. **Advanced Branch Listing**

- **Branch Management**:
  - Display branches in columns:
    ```sh
    git branch --column
    ```
  - Sort branches based on committer date:
    ```sh
    git branch --sort=committerdate
    ```

### 10. **GitHub Links and Tools Mentioned**

- **GitHub**:
  - [GitHub Repository](https://github.com) (General access to GitHub resources).
  - GitHub founders are developing new Git utilities and interfaces, such as **Git Butler**.
- **Git Butler**:
  - A new Git interface that offers features like virtual branches.
  - Note: This may carry risks if working directly on it outside its UI, as the data loss was reported by users switching to CLI commands.
- **Worktrees**:
  - Recommended for users who want to manage multiple development streams natively and avoid third-party GUI risks.
  - **Setup Worktree**:
    ```sh
    git worktree add ../<branch-name> <branch>
    ```

### 11. **Recommended Plugins and Tools for Git Users**

- **LazyGit**:
  - A TUI (Terminal User Interface) for Git commands that simplifies working with Git from the command line.
  - [LazyGit GitHub Link](https://github.com/jesseduffield/lazygit)
- **VSCode Extensions**:
  - **GitLens**: Provides insights and more comfortable navigation through git commits.
  - [GitLens on GitHub](https://github.com/eamodio/vscode-gitlens)

### 12. **How-To Guides for Using Git Features**

- **Setting Up Conditional Configs**:
  1. **Edit Global Git Config File**:
     - Open your `.gitconfig` located typically in `~/.gitconfig`.
  2. **Add IncludeIf Clause**:
     - Example:
       ```bash
       [includeIf "gitdir:~/work/"]
           path = ~/work/.gitconfig-work
       ```
  3. **Create Config File for Work Projects**:
     - In `~/work/.gitconfig-work`:
       ```bash
       [user]
           email = "work.email@example.com"
       ```

- **Creating and Using Git Aliases**:
  1. **Add Alias to Global Config**:
     - Run:
       ```bash
       git config --global alias.stashall '!git stash --all'
       ```
  2. **Usage**:
     - You can now run `git stashall` to stash everything.

### 13. **Summary and Takeaways**

- **Practical Tips**:
  - Use Git aliases to create shortcuts for repetitive tasks.
  - Configure `rerere` for reusing recorded conflict resolutions.
  - Explore `git worktree` to work with multiple branches simultaneously.
  - Use advanced blame flags (`-w`, `-C`) to trace logical changes, and keep focus on critical commits.

### Final Thoughts

This overview touches on some of the advanced features and tips for using Git effectively. For more in-depth learning, consider:

- **Git Documentation**: [Git SCM Docs](https://git-scm.com/doc)
- **GitHub Learning Lab**: [GitHub Lab](https://lab.github.com/) - Free hands-on Git training.
- **YouTube Learning Resources**: Channels like *Traversy Media* and *The Net Ninja* offer useful Git tutorials.

If you need further help setting up these commands or any configuration, let me know!

[[Git]]   [[GitHub]]
