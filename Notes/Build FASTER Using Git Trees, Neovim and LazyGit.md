---
tags:
- github
- editors
video-url: https://www.youtube.com/watch?v=g9UaW5z-hn8&list=WL&index=2
---
## **Build FASTER Using Git Trees, Neovim and LazyGit

### **Overview of the Text: Keeping Git Histories Clean**

The content focuses on effective Git usage, particularly on keeping commit trees clean and using advanced Git techniques like **interactive rebasing** to simplify development workflows. Let's dive into the major components: related tools, plugins, how-to instructions, and all code examples.

### **GitHub Link and Creating Your Repo**

The video does not provide a specific GitHub link, but you can easily follow along by creating your own GitHub repository:

- **GitHub Link**: [https://github.com](https://github.com)
  - **Steps**: Create a new repository, clone it, and practice with the Git techniques outlined in this guide.

### **Key Concepts Discussed**

- **Filthy Commit Trees**: A lot of Git repositories become cluttered with unnecessary commits, making debugging and development cumbersome.
- **Why Cleanliness Matters**: Clean commit histories facilitate debugging, Git bisect operations, and efficient CI/CD pipeline runs.
- **Git Bisect**: A tool used to perform a binary search on commits to find when a bug was introduced.
- **Optimizing CI/CD**: By avoiding redundant merges and unnecessary builds, you can optimize your development workflow and save time and storage.
- **Interactive Rebasing**: Utilizing `git rebase -i` to clean up commit history before merging into the main branch.
- **Fast-Forward Merging**: Avoid creating extra merge commits by fast-forwarding whenever possible.

### **Plugins and Tools**

1. **Neogit**: A modern replacement for the Fugitive plugin, integrated into Neovim, that allows easy interaction with Git from the editor.
   - **GitHub Link**: [Neogit GitHub](https://github.com/TimUntersberger/neogit)
   - **Usage**: Handles various Git operations directly from the Neovim interface.

2. **LazyGit**: A terminal-based UI for handling Git commands interactively, which can also be integrated with Neovim.
   - **GitHub Link**: [LazyGit GitHub](https://github.com/jesseduffield/lazygit)
   - **Neovim Integration**: Can be used as a plugin to provide a floating terminal for seamless Git operations.

3. **LazyGit Neovim Plugin**:
   - **How to Install**: If using LazyVim or other package managers, add LazyGit to your Neovim configuration.
     ```lua
     use 'kdheepak/lazygit.nvim'
     ```
   - Alternatively, use a floating terminal to run LazyGit:
     ```vim
     :FloatermNew lazygit
     ```

### **How-To Instructions and Git Commands**

#### **Setting Up the Git Environment**

- **Checkout Feature Branch**
  ```bash
  git checkout feature-branch
  ```
- **Update Local Main Branch**
  ```bash
  git fetch origin
  git checkout main
  git merge origin/main
  ```
  - Alternatively, update without switching branches:
  ```bash
  git fetch origin main:main
  ```

#### **Rebasing for Clean Commit History**

- **Interactive Rebase**
  ```bash
  git rebase -i main
  ```
  - Open the editor and change `pick` to `squash` for the commits you want to merge. Squashing reduces clutter by combining small fixes into meaningful commits.

#### **Pushing Changes Safely**

- **Push with Force (Keeping Remote Changes Safe)**
  ```bash
  git push --force-with-lease
  ```
  - This prevents overwriting remote changes if someone else added commits in the meantime.

#### **Merging into Main with Fast-Forward**

- **Fast-Forward Merge**
  ```bash
  git checkout main
  git merge --ff-only feature-branch
  ```
  - This avoids unnecessary merge commits, ensuring a linear and readable commit history.

#### **Using Neovim and LazyGit Together**

1. **Installing LazyGit in Neovim**
   - Add to Neovim config:
     ```lua
     use 'kdheepak/lazygit.nvim'
     ```
   - Run LazyGit in a floating terminal:
     ```vim
     :FloatermNew lazygit
     ```

2. **Using LazyGit from Neovim**
   - Use LazyGit by opening it through `:LazyGit`. Squash commits (`S`), rebase (`r`), or view options (`?`) for additional commands.

### **Git Best Practices Highlighted**

1. **Rebase vs. Merge**
   - **Rebase**: Ideal for keeping a clean history; integrates changes by rewriting the commit history.
   - **Merge**: Adds merge commits, which can clutter history if overused.

2. **Use Fast-Forward Merges**
   - **Fast-Forward (`--ff-only`)** keeps history linear, avoiding redundant merge commits.

3. **Avoid CI/CD Redundancy**
   - Avoid triggering CI/CD pipelines unnecessarily by carefully handling merges and using clean commit practices.

### **Code Examples**

- **Interactive Rebase Example**
  - Running `git rebase -i main` opens an interactive file:
    ```plaintext
    pick 1234567 Commit message 1
    pick 89abcde Commit message 2
    ```
  - Change it to:
    ```plaintext
    pick 1234567 Commit message 1
    squash 89abcde Commit message 2
    ```
  - This combines both commits into a single commit, cleaning up the history.

### **Benefits of Keeping Git Clean**

- **Easier Debugging**: Clean history makes debugging easier with tools like `git bisect`.
- **Efficient CI/CD**: Avoiding redundant merges helps save time and resources in the CI/CD pipeline.
- **Reduced Storage**: Fewer artifacts to store means less disk space consumed.
- **Environmental Impact**: Reducing resource usage benefits the environment by saving energy.

### **Summary and Next Steps**

Keeping Git history clean isn’t just for aesthetics; it leads to better workflows, easier debugging, and reduced CI/CD costs. Using plugins like **Neogit** and **LazyGit** makes Git interactions smoother, especially when integrated with tools like **Neovim**. By leveraging interactive rebasing and fast-forward merging, you can significantly enhance your team's efficiency and workflow.

To proceed, try incorporating these plugins in your current project, practice rebasing your feature branches, and consider optimizing your CI/CD pipelines by eliminating unnecessary build runs. You'll notice a significant improvement in project maintainability and overall efficiency.

[[Neovim]]  [[Git]]  [[Code Editor]] 
