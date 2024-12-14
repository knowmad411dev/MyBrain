---
github_link: https://github.com/VonHeikemen/lsp-zero.nvim/blob/v3.x/doc/md/guides/lazy-loading-with-lazy-nvim.md
tags:
- editors
video-url: https://www.youtube.com/watch?v=VljhZ0e9zGE&list=WL&index=1
---
## **Neovim Lazy Lua IDE

**Overview of Setting up Neovim as an IDE**

This setup guide will walk you through configuring Neovim as a powerful Integrated Development Environment (IDE). This setup uses modern tools like Lazy.nvim, Lua for configurations, and a variety of plugins to enhance the coding experience. Here's a breakdown of how to get started and customize your Neovim to create a developer-friendly environment.

### Prerequisites

- **Neovim**: Install the latest version of Neovim using your OS package manager. Make sure it is accessible by running `nvim` in the terminal.
- **Git**: Make sure a recent version of Git is installed, as it's required for managing plugins.
- **Ripgrep**: Install Ripgrep (`rg`) to enable fast file searching, required for the Telescope plugin.

### Step-by-Step Instructions

1. **Installing Neovim**
   - Install Neovim using your package manager.
   - Verify installation by restarting your terminal and typing `nvim`.
   - If Neovim isn’t recognized, add its location to your system PATH.

2. **Alias Setup**
   - For Unix-based systems, add an alias to easily launch Neovim by typing `vim`. Add the following line to your shell configuration file (`~/.zshrc` or `~/.bashrc`):
     ```sh
     alias vim='nvim'
     ```
   - Apply changes by restarting your terminal or sourcing the file (`source ~/.zshrc`).

3. **Creating the Configuration Folder**
   - Create a new directory in your Neovim configuration path, typically located in `~/.config/nvim/`.
   - Inside this directory, create a main file named `init.lua` and a Lua directory to hold additional configuration files (`keymaps.lua`, `options.lua`, etc.).
   - Use the following structure:
     ```sh
     mkdir -p ~/.config/nvim/lua
     touch ~/.config/nvim/init.lua ~/.config/nvim/lua/{keymaps.lua,options.lua}
     ```

4. **Basic Lua Configuration**
   - Open `init.lua` and set up Lua to require your keymaps and options:
     ```lua
     require('keymaps')
     require('options')
     ```
   - In `keymaps.lua`, set your leader key and add other desired key bindings.
     ```lua
     vim.g.mapleader = ' '
     ```
   - In `options.lua`, set options like line numbering:
     ```lua
     vim.opt.relativenumber = true
     ```

5. **Installing Lazy.nvim as the Plugin Manager**
   - Create a new directory for plugins: `~/.config/nvim/lua/plugins/`
   - Create `lazy.lua` inside this directory. Lazy.nvim will help manage plugins effectively.
   - Add Lazy.nvim setup script to `lazy.lua` by copying the installation instructions from [Lazy.nvim GitHub repository](https://github.com/folke/lazy.nvim).

6. **Adding Plugins**
   - Modify `init.lua` to include Lazy.nvim and configure plugins by adding:
     ```lua
     require('plugins.lazy')
     ```
   - Open `lazy.lua` and add plugins:
     ```lua
     return require('lazy').setup({
       'nvim-telescope/telescope.nvim',
       'catppuccin/nvim',  -- Theme plugin
       'kyazdani42/nvim-tree.lua',  -- File tree
       -- Add more plugins here
     })
     ```
   - Restart Neovim and type `:Lazy` to open the plugin manager and install plugins.

7. **Adding Telescope Plugin**
   - Telescope is a fuzzy finder for quickly locating files and searching content.
   - Add Telescope key mappings in `keymaps.lua`:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>fs', ':Telescope find_files<CR>', { noremap = true, silent = true })
     ```
   - To search for a string, use:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>fz', ':Telescope live_grep<CR>', { noremap = true, silent = true })
     ```

8. **File Tree and Buffer Management**
   - Install `nvim-tree.lua` to handle the file tree, enabling easy navigation.
   - Map keys for toggling the file explorer in `keymaps.lua`:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>e', ':NvimTreeToggle<CR>', { noremap = true, silent = true })
     ```
   - Install `bufferline.nvim` for efficient buffer navigation. Add it to `lazy.lua`.
   - In `keymaps.lua`, add:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>n', ':BufferLineCycleNext<CR>', { noremap = true, silent = true })
     vim.api.nvim_set_keymap('n', '<leader>p', ':BufferLineCyclePrev<CR>', { noremap = true, silent = true })
     vim.api.nvim_set_keymap('n', '<leader>x', ':bd<CR>', { noremap = true, silent = true })
     ```

9. **Setting Up LSP (Language Server Protocol)**
   - Install `nvim-lspconfig` for configuring language servers.
   - Use [lsp-zero](https://github.com/VonHeikemen/lsp-zero.nvim) to make setting up LSP servers easy. Add it to `lazy.lua`.
   - Add LSP-specific key bindings and configurations to enable autocompletion and diagnostics.

10. **Code Formatting**
   - Install `black` for Python code formatting.
   - Add a shortcut in `keymaps.lua` to run formatting:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>fmp', ':!black %<CR>', { noremap = true, silent = true })
     ```

11. **Markdown Preview**
   - Add a Markdown preview plugin like `iamcco/markdown-preview.nvim`.
   - Create a key binding for previewing Markdown:
     ```lua
     vim.api.nvim_set_keymap('n', '<leader>mp', ':MarkdownPreview<CR>', { noremap = true, silent = true })
     ```

12. **Auto Session**
   - Install `rmagatti/auto-session` for automatically saving and restoring sessions.
   - This helps resume work across multiple sessions, maintaining buffer and window states.

### Example GitHub Configuration

You can find a sample configuration in this GitHub repository:

[Zazen Codes Neovim Setup](https://github.com/zazencodes/neovim-setup).

### Plugins List Overview

- **Lazy.nvim**: Plugin manager for lazy-loading other plugins.
- **Telescope.nvim**: Fuzzy finder to search for files, text, and more.
- **Catppuccin Theme**: Aesthetic theme for Neovim.
- **nvim-tree.lua**: File tree sidebar for easier file navigation.
- **Bufferline.nvim**: Organize and navigate multiple open buffers.
- **nvim-lspconfig**: Integrate language servers for autocompletion, syntax highlighting, etc.
- **Markdown Preview**: Preview Markdown files in the browser.
- **Auto Session**: Automatically save and restore session states.

### How-To Run Neovim as an IDE

- After following all the setup instructions, start Neovim by running `nvim` in the terminal.
- Use `<leader>` (`Space` key) to quickly access features:
  - **File search**: `<leader>fs` opens Telescope file search.
  - **Toggle file tree**: `<leader>e` opens or closes the file explorer.
  - **Cycle buffers**: `<leader>n` and `<leader>p` to switch between buffers.
  - **Markdown preview**: `<leader>mp` to open a live Markdown preview.

With this setup, Neovim is transformed into a modern IDE, allowing you to code efficiently with powerful tools, all configurable through simple Lua scripts.

[[Neovim]]