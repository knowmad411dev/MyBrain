---
github_link: https://github.com/nvim-lua/kickstart.nvim
tags:
- editors
video-url: https://www.youtube.com/watch?v=m8C0Cq9Uv9o&list=WL&index=4
---
## **Get Started with Neovim

It looks like you've shared a detailed transcript from a YouTube video about setting up and customizing Neovim using a project called "Kickstart." This walkthrough describes setting up a Neovim environment, plugin management, configurations, and more, particularly through the use of Lua, which is the configuration language for Neovim. I'll break down the key aspects of what was shared, including plugin links, how-to guides, and code examples for customization.

### **Overview of Neovim Kickstart Project**

**Kickstart Project** is essentially a template configuration for Neovim aimed at helping new users set up and begin customizing Neovim with plugins, LSPs (Language Server Protocols), Treesitter, and other tools. Unlike other distributions, which can be overwhelming and opaque, Kickstart aims to provide a minimal but extensible starting point, encouraging you to learn as you configure. It’s designed to be simple yet powerful, and easy for you to extend.

#### **Key Features and Components**:

1. **Core Configuration File**:
   - The Kickstart project focuses on a single configuration file (`init.lua`), which keeps the process simple and easy to follow.
   - The configuration is written in Lua, Neovim’s scripting language, which offers extensive flexibility.

2. **Plugins and Plugin Management**:
   - Plugins are managed via **Lazy.nvim**, a lightweight and efficient plugin manager for Neovim.
   - The script automatically checks for and installs Lazy.nvim if it's not already installed.
   - After installing Lazy.nvim, you can easily add, update, or remove plugins.

3. **Tutorial for New Users**:
   - If you’re new to Neovim, Kickstart recommends running `tutor` inside Neovim for basic navigation and command knowledge.
   - **Tutor** is an interactive Neovim tutorial that teaches you the basics, including how to quit the editor.
   - Running `:help` is also encouraged for understanding configuration options.

### **Key Concepts Explained in the Walkthrough**

#### **1. Leader Key and Keymaps**

- **Leader Key**: The `leader` key is used to map custom commands. In Kickstart, it's set as a namespace for all your custom mappings.
- **Keymaps**: These are customized keyboard shortcuts to make development easier. For example, pressing `Space + s + h` searches the help system.
- Example:
  ```lua
  vim.g.mapleader = " "
  -- Keymap to search the help
  vim.keymap.set('n', '<leader>sh', vim.cmd.help, { desc = 'Search help' })
  ```

#### **2. Options and Settings**

- **Options in Neovim**: Set options like line numbering, relative numbering, etc., using Lua.
- Example:
  ```lua
  vim.o.number = true
  vim.o.relativenumber = true
  ```

#### **3. Autocommands**

- **Autocommands** are similar to event listeners in JavaScript and automatically run some commands when certain events occur.
- Example: Highlight yanked text temporarily after yanking.
  ```lua
  vim.api.nvim_create_autocmd('TextYankPost', {
    callback = function() vim.highlight.on_yank { higroup = 'IncSearch', timeout = 150 } end
  })
  ```

#### **4. Plugins Setup and Lazy.nvim**

- **Lazy.nvim** is the plugin manager, and its setup script checks whether Lazy.nvim is already installed or not.
- Plugin example configuration:
  ```lua
  require('lazy').setup('plugins')
  ```

- Example of installing a plugin from GitHub:
  ```lua
  {
    'nvim-telescope/telescope.nvim',
    requires = { {'nvim-lua/plenary.nvim'} }
  }
  ```

#### **5. Telescope - Fuzzy Finder**

- **Telescope** is a powerful fuzzy finder that helps you locate files, keymaps, symbols, diagnostics, etc., using a simple keybinding.
- Keymaps for Telescope:
  ```lua
  vim.keymap.set('n', '<leader>ff', require('telescope.builtin').find_files, { desc = 'Find files' })
  vim.keymap.set('n', '<leader>fg', require('telescope.builtin').live_grep, { desc = 'Grep through files' })
  ```

#### **6. Language Server Protocol (LSP) Setup**

- **Language Server Protocol (LSP)**: This protocol allows editors like Neovim to communicate with language servers for features like autocomplete, go-to-definition, etc.
- **Mason** is used to install LSPs.
  - Example:
    ```lua
    require('mason').setup()
    require('mason-lspconfig').setup {
      ensure_installed = { 'lua_ls', 'pyright', 'tsserver' }
    }
    ```
- Setting up capabilities:
  ```lua
  local capabilities = require('cmp_nvim_lsp').update_capabilities(vim.lsp.protocol.make_client_capabilities())
  ```

#### **7. Completion with `nvim-cmp`**

- **nvim-cmp** is a completion plugin that integrates with LSP, file paths, snippets, etc.
- Configuring `nvim-cmp`:
  ```lua
  local cmp = require('cmp')
  cmp.setup {
    mapping = {
      ['<C-n>'] = cmp.mapping.select_next_item(),
      ['<C-p>'] = cmp.mapping.select_prev_item(),
      ['<C-y>'] = cmp.mapping.confirm({ select = true })
    },
    sources = {
      { name = 'nvim_lsp' },
      { name = 'path' },
    }
  }
  ```

#### **8. Treesitter for Syntax Highlighting**

- **Treesitter** provides better syntax highlighting and additional features like text objects.
- Example setup for Treesitter:
  ```lua
  require'nvim-treesitter.configs'.setup {
    ensure_installed = { "lua", "python", "javascript" },
    highlight = { enable = true },
    indent = { enable = true },
  }
  ```

### **Kickstart GitHub Repository and Plugins**

- **Kickstart Repository**: You can find the Kickstart configuration project on GitHub.
  - [Kickstart GitHub Repo](https://github.com/nvim-lua/kickstart.nvim)
- **Plugins Mentioned**:
  1. **Lazy.nvim**: Plugin manager used in Kickstart.
     - [Lazy.nvim GitHub](https://github.com/folke/lazy.nvim)
  2. **Telescope.nvim**: Fuzzy Finder.
     - [Telescope GitHub](https://github.com/nvim-telescope/telescope.nvim)
  3. **Mason.nvim**: Manages external tools and LSPs.
     - [Mason GitHub](https://github.com/williamboman/mason.nvim)
  4. **nvim-treesitter**: Syntax highlighting and parsing.
     - [Treesitter GitHub](https://github.com/nvim-treesitter/nvim-treesitter)
  5. **nvim-cmp**: Completion engine.
     - [nvim-cmp GitHub](https://github.com/hrsh7th/nvim-cmp)
  6. **Which-key.nvim**: Keybinding helper.
     - [Which-Key GitHub](https://github.com/folke/which-key.nvim)

### **Getting Started with Kickstart**

**Step-by-Step Instructions**:

1. **Install Neovim** (if not already done):
   - Head to [Neovim's official website](https://neovim.io/) to download and install the latest version.

2. **Clone Kickstart.nvim Configuration**:
   ```bash
   git clone https://github.com/nvim-lua/kickstart.nvim ~/.config/nvim
   ```

3. **Run Neovim**:
   ```bash
   nvim
   ```

   This will trigger the Lazy.nvim installation, and you should see Neovim fetching plugins.

4. **Install LSP servers**:
   - After launching Neovim, open Mason to install LSPs.
   ```vim
   :Mason
   ```

   Then select the LSP servers you need.

5. **Run Tutorial**:
   - Learn the basics of navigating Neovim by running:
   ```vim
   :Tutor
   ```

### **Recommended Learning Resources**

- **Learn Lua**: Check out "Learn X in Y Minutes" for a quick introduction to Lua:
  - [Learn Lua in Y Minutes](https://learnxinyminutes.com/docs/lua/)
- **Neovim Help**:
  - Run the command `:help` to learn about each feature discussed above.

### **Conclusion and Tips**:

- **Kickstart is Just the Beginning**: The main goal of Kickstart is to provide a base that you can adapt to your needs. It’s not a one-size-fits-all distribution but a well-documented template.
- **Key to Mastery**: Spend time with `telescope` and `LSP` to navigate and understand your code better.
- **Lua is Your Friend**: Understanding a bit of Lua will take you a long way in customizing Neovim and making it feel like home.

### **Final Note**:

Kickstart encourages you to explore and make Neovim your own. Feel free to experiment with different plugins, tweak settings, and create keybindings that work best for you. The community is vast, and you can find a lot of helpful information and inspiration from others using Neovim.

You can also support the creator by visiting their GitHub sponsors page or simply sharing the video for wider reach.

[[VSCode to Neovim]]  [[Neovim]]