---
tags:
- editors
- github
video-url: https://www.youtube.com/watch?v=Ihg37znaiBo&list=WL&index=5
---

## **Lazygit

### Lazy Git: Overview and How-To Guide

Lazy Git is a terminal-based Git UI that simplifies working with Git, especially for those who prefer a keyboard-driven workflow. This guide will walk you through installation, usage, [[Neovim]] integration, and more.

#### Overview of Lazy Git

- **Simple UI**: Lazy Git provides an easy interface for managing Git repositories.
- **Neovim Integration**: It works well with Neovim, enhancing productivity.
- **Efficient Navigation**: Use keyboard shortcuts to navigate, commit, push, and resolve conflicts quickly.

#### Installation Instructions

**For Different Operating Systems**:
- **macOS**: Use Homebrew to install Lazy Git:
  ```sh
  brew install lazygit
  ```

  For the latest version with frequent updates, refer to the [official Lazy Git repository](https://github.com/jesseduffield/lazygit).

- **Linux/Windows**: Follow the instructions on the [official repository](https://github.com/jesseduffield/lazygit) for installation tailored to your system.

**Check Installation**:
```sh
lazygit --version
```

### Getting Started with Lazy Git

1. **Navigate to Your Git Repository**:
   Open your terminal and move to your Git project folder.

2. **Launch Lazy Git**:
   ```sh
   lazygit
   ```

   This opens the Lazy Git UI, which consists of multiple panes showing repository status, branches, logs, etc.

#### Navigating Lazy Git Interface

- **Navigate Between Panes**:
  - Use `Tab` to cycle through panes.
  - Use `Shift + Tab` to move backward.
  - Directly press the pane number (e.g., `4`) to switch instantly.
- **Tabs Within a Pane**:
  - Use `]` to move forward.
  - Use `[` to move backward.
- **Exit Lazy Git**: Press `Ctrl + C` to close.

#### Editing Files and Staging Changes

1. **Edit Files in Neovim**:
   Open Neovim to make changes:
   ```sh
   nvim .
   ```
   - Example: Edit `layout.svelte`, add a `console.log('Hello there')`, then save (`:w`) and exit (`:q`).

2. **Stage Changes**:
   - Launch Lazy Git again with `lazygit`.
   - Use `j`/`k` to navigate through files.
   - Press `Space` to **stage** or **unstage** a file.

3. **Stage All Changes**:
   - Press `a` to stage all files.
   - Press `a` again to unstage everything.

4. **Stage Hunks**:
   - Press `Enter` to view file changes.
   - Navigate to specific hunks using `j`/`k` and press `Space` to stage.
   - Press `Tab` to move to the right pane and unstage if needed.

#### Committing Changes

- **Create a Commit**:
  - After staging changes, press `c` to create a commit.
  - Type a commit message.
  - Use `Tab` to add a description if needed, then press `Enter` to finalize.

#### Pushing Changes to Remote

- **Push Changes**:
  - Press `?` to view keybindings, search for "push" (`/push`), and use `P` to push.
  - Press `P` (capital) to push to the remote repository.

#### Managing Branches

- **View Branches**:
  - Navigate to pane `3` to see branches. The branch marked with a star (`*`) is the current one.
- **Switch Branches**:
  - Use `j`/`k` to move and press `Space` to switch.
- **Create a New Branch**:
  - Press `n`, provide a branch name, and press `Enter`.

#### Merging and Resolving Conflicts

- **Simulate a Merge Conflict**:
  - Make changes on different branches.
  - Switch branches in Lazy Git to create conflicting changes.
- **Resolve Merge Conflicts**:
  - Press `Shift + M` to merge branches.
  - Press `Enter` on the conflicting file.
  - Use `j`/`k` to navigate through options, and press `Space` to select.
  - Press `b` to select all hunks from one side.

#### Searching and Filtering

- **Search for Specific Items**:
  - Use `/` to filter or search for branches, commits, etc.
  - Use `Escape` to exit search mode.
- **View Details**:
  - Press `Enter` on a selected item to see more information.
  - Press `Escape` to go back.

### Integrating Lazy Git with Neovim

1. **Configure Neovim**:
   - Navigate to the Neovim configuration folder:
     ```sh
     cd ~/.config/nvim
     nvim init.lua
     ```
   - Add Lazy Git as a plugin:
     ```lua
     use {
       'kdheepak/lazygit.nvim',
       requires = {
         'nvim-lua/plenary.nvim',
       }
     }
     ```
   - Set up a keymap to open Lazy Git within Neovim:
     ```lua
     vim.api.nvim_set_keymap('n', '<space>lg', ':LazyGit<CR>', { noremap = true, silent = true })
     ```

2. **Using Lazy Git in Neovim**:
   - Press `space + LG` to open Lazy Git inside Neovim.
   - Press `q` or `Ctrl + C` to close Lazy Git and return to Neovim.

### Summary of Key Shortcuts

| Action                           | Keybinding       |
|----------------------------------|------------------|
| **Stage/Unstage file**           | Space            |
| **Stage all files**              | a                |
| **Commit changes**               | c                |
| **Push changes**                 | P (capital)      |
| **Create a new branch**          | n                |
| **Merge branch**                 | Shift + M        |
| **Navigate panes**               | Tab / Shift + Tab|
| **Navigate list items**          | j/k or arrows    |
| **View keybindings**             | ?                |
| **Search/filter**                | /                |
| **View more information**        | Enter            |

### Conclusion

Lazy Git simplifies working with Git repositories, providing an intuitive and efficient way to manage version control from the terminal. The integration with Neovim further enhances productivity, offering seamless context-switching between editing and version control.

To get the most out of Lazy Git, start using it actively, explore keybindings (`?`), and customize your setup to fit your workflow.

[[Neovim]]  [[Git]]