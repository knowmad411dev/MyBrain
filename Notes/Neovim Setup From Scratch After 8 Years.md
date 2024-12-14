---
github_link: https://github.com/omerxx/dotfiles/tree/master/nvim
tags:
- editors
video-url: https://www.youtube.com/watch?v=x__SZUuLOxw&list=WL&index=2
---
## **Neovim Setup From Scratch After 8 Years

Here's a detailed overview of the provided text, focusing on the plugins used, how-to instructions, and some example code. The text gives a walkthrough of configuring Neovim (often abbreviated as `nvim`) by discussing plugins, file structure, and practical features. Let's break it down step by step to make it easier to follow.

### 1. **Understanding the Starting Point: Neovim Configurations**

The author suggests that beginners start with a basic Neovim setup using the **vim-sensible plugin**, which adds reasonable default settings for new users. Once comfortable, the author recommends building a more advanced setup that includes:

- **Telescope Pickers** for file searching.
- **Language Servers** for code assistance.
- **Git Integrations** for managing code versions.

To get started quickly with a powerful setup, the author mentions using **Kickstart.nvim**, a ready-made configuration crafted by TJ DeVries, a core Neovim contributor. This config includes many essential features of an IDE-like environment.

### 2. **File Structure of Neovim Configuration**

To keep things organized, the author uses a specific file structure:

- **`init.lua`**: The main configuration file, loading all other settings and plugins.
- **`lua/` subdirectory**: Contains:
  - **Mappings**: Custom keybindings.
  - **Editor Options**: Basic settings.
  - **Plugin Configurations**: Settings specific to each plugin, organized in individual files for easier access.

This structure allows each plugin to have its own configuration file under a specific folder, typically in `lua/plugins/`.

### 3. **Overview of Neovim Configuration File (`init.lua`)**

- **Order of Loading**:
  1. **Keymaps** are loaded first. These contain the custom keybindings for navigating and using the editor efficiently.
  2. **Lazy Plugin List**: Plugins are managed and configured using **lazy.nvim**.
  3. **Editor Options and Plugin Configurations** are loaded last.

### 4. **Key Plugins Used and Configured**

#### a. **Lazy.nvim**

- **Purpose**: Lazy.nvim is used for managing plugins. It handles installation, configuration, and updates.
- **Plugin Loading Strategy**: The author prefers to create separate configuration files for each plugin, which are loaded on demand to keep things modular.

#### b. **Git Plugins**

- **GitSigns**: This is a core plugin that integrates with **Git**. It provides visual cues for changes, deletions, staging, and unstaging within the editor.

Example Configuration for GitSigns:

```lua
require('gitsigns').setup {
  signs = {
    add = {hl = 'GitGutterAdd', text = '+'},
    change = {hl = 'GitGutterChange', text = '~'},
    delete = {hl = 'GitGutterDelete', text = '_'},
  },
}
```

#### c. **Lualine**

- **Purpose**: Lualine provides a customizable status line at the bottom of the editor.
- **Features**: Displays information such as:
  - **Buffers**: Open files.
  - **Git Branches**.
  - **Vim Mode**: Insert, normal, visual, etc.

Example Configuration:

```lua
require('lualine').setup {
  options = {
    theme = 'gruvbox',
    section_separators = {'', '⟢'},
    component_separators = {'⟡', '⟣'},
  },
}
```

#### d. **DAP (Debug Adapter Protocol)**

- **Purpose**: The DAP plugin is used for debugging within Neovim.
- **Configuration**: Supports different debuggers for various languages. The author has created their settings in a `dap.lua` file.

Example Setup for Python Debugging:

```lua
require('dap-python').setup('~/.virtualenvs/debugpy/bin/python')
```

#### e. **Telescope**

- **Purpose**: Telescope is a powerful fuzzy finder and search tool.
- **Features**:
  - **File Picker**: Shows files in a fuzzy-search format.
  - **Word Picker**: Searches for a word in all files.
  - **Buffer and Git Status Picker**: Lets you search through open buffers or see the Git status of files.

Example Picker Use:

```lua
vim.api.nvim_set_keymap('n', '<leader>ff', '<cmd>Telescope find_files<cr>', { noremap = true, silent = true })
```

This command sets `<leader>ff` to quickly search for files.

#### f. **Treesitter**

- **Purpose**: Enhances syntax highlighting and code navigation.
- **Features**: Adds text objects and custom navigation, such as jumping between functions.

Example Configuration:

```lua
require('nvim-treesitter.configs').setup {
  ensure_installed = {"python", "lua", "javascript"},
  highlight = {
    enable = true,
  },
  incremental_selection = {
    enable = true,
    keymaps = {
      init_selection = "gnn",
      node_incremental = "grn",
    },
  },
}
```

#### g. **Language Servers (LSP)**

- **Purpose**: Provides real-time diagnostics, autocompletion, and formatting for many programming languages.
- **Manager**: The author uses **Mason** to manage LSPs. Mason helps with installing, updating, and removing language servers from one interface.

Example LSP Setup:

```lua
require('lspconfig').pyright.setup{}
```

Mason can be installed and used to install servers as follows:

```lua
require("mason").setup()
```

#### h. **Trouble**

- **Purpose**: A quick diagnostic viewer that shows all the errors in a project.
- **Usage**: Allows you to navigate to each problem easily from a single pane.

Example Keybinding:

```lua
vim.api.nvim_set_keymap('n', '<leader>xx', '<cmd>TroubleToggle<cr>', { noremap = true, silent = true })
```

#### i. **[[Obsidian]] Integration Plugin**

- **Purpose**: For note-taking, integrated with **Obsidian**. This plugin allows creating, managing, and templating notes directly from within Neovim.
- **Features**:
  - Handles YAML front matter.
  - Unique note naming for quick access.

#### j. **Zen Mode**

- **Purpose**: Helps with focused work by hiding all distractions like status lines and sidebars.
- **Coupled with Twilight**: Highlights only relevant code, increasing focus on what's being worked on.

Example Use:

```lua
require("zen-mode").setup {
  window = {
    width = 0.85, -- percentage of screen width
  }
}
```

#### k. **Neogit**

- **Purpose**: A plugin inspired by Magit for Git integration, used to stage, commit, push, pull, and review code directly within Neovim.
- **Replaces Git Fugitive**: Offers a more modern interface and better integration for daily Git tasks.

#### l. **CodeSnap**

- **Purpose**: For taking beautiful snapshots of code to share with others.
- **Usage**: Copies code as an image to the clipboard.

#### m. **Noice**

- **Purpose**: Provides a custom command line interface for Neovim, visually indicating different commands or functions being run.

### 5. **Minor Plugins and Their Purpose**

- **Catppuccin**: A theme that provides color schemes to maintain visual consistency.
- **Vim-Autopairs**: Auto-closes brackets, braces, and quotes.
- **Todo Comments**: Labels TODOs in code and integrates with **Telescope** for quick searches.
- **Surround**: Adds commands to quickly surround words, lines, or selections with specific characters.

### 6. **Wrapping Up**

The author emphasizes that the Neovim configuration is not perfect but has evolved to suit their needs over time. They suggest tweaking it to fit one's workflow. They also point out their upcoming plans to share a detailed beginner's guide to starting from scratch, which would help those new to this level of customization.

### 7. **General Takeaways for Neovim Configuration**

- **Modular Setup**: Each plugin has its own file to keep the setup organized.
- **Start Simple**: Begin with a minimal setup like vim-sensible and gradually add plugins as you become more comfortable.
- **Use Plugin Managers**: Plugins like Lazy.nvim or Packer.nvim simplify installing, updating, and configuring plugins.
- **Use Telescope**: This plugin is a game-changer for navigating files, buffers, and codebase-wide searches.
- **Zen Mode for Writing**: Plugins like Zen Mode can make Neovim a minimalist writing tool when you're not coding.

### Example of `init.lua` File

Here is an example of what the `init.lua` file might look like based on the author's configuration strategy:

```lua
-- Load Keymaps
require('my_mappings')

-- Load Plugins
require('lazy').setup('plugins')

-- Load Editor Options
require('editor_options')

-- Load Specific Plugin Configurations
require('plugin.telescope')
require('plugin.lualine')
require('plugin.gitsigns')
-- etc.
```

This breakdown should help you get a comprehensive understanding of the discussed configuration, including what plugins are used, their purpose, and how they fit into a complete Neovim setup. Feel free to explore any of the suggested plugins, and modify them as per your needs to build a robust and efficient Neovim environment!

[[Neovim]]