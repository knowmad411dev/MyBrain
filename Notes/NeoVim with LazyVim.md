---
github_link: https://github.com/dispatch-yt/dot-files
tags:
- editors
video-url: https://www.youtube.com/watch?v=lojAgyGnzc0&list=WL&index=2
---
## **NeoVim with LazyVim

### LazyVim Setup for Neovim: A Comprehensive Overview

**LazyVim** is a modern plugin manager for Neovim, designed to simplify setup and provide an IDE-like experience. It supports extensive customization and comes with built-in documentation for easier configuration.

---

### Installation Steps

1. **Backup Existing Neovim Configuration:**
   - Ensure your current Neovim setup is backed up in case you need to revert changes.

2. **Clone the LazyVim Starter Repository:**
   ```bash
   git clone https://github.com/LazyVim/starter ~/.config/nvim
   cd ~/.config/nvim
   rm -rf .git
   ```
   - This allows you to integrate it into your own repository if needed.

3. **Launch Neovim:**
   ```bash
   nvim
   ```
   - LazyVim will initialize and display its dashboard for quick actions.

4. **Run Health Check:**
   ```bash
   :checkhealth
   ```
   - Ensure all dependencies are installed and working correctly.

---

### Key Features and Initial Setup

#### **Dashboard Overview:**

- LazyVim starts with a dashboard for quick actions like opening files or projects.

#### **Key Plugins:**

- **Which Key:** Displays available keymaps when pressing the leader key (`<Space>`).
- **Neo Tree:** File explorer accessible with `<Space> e`.
- **Mason:** Manage language servers, linters, and formatters using `<Space> cm`.

---

### Adding TypeScript and JSON Support

1. **Edit `lazy.lua` Configuration:**
   - Navigate to the `Lua/config` folder and uncomment the following lines in `lazy.lua`:
     ```lua
     { "typescript-language-server", "json-language-server" },
     { "mini.animate" },
     ```
2. **Restart Neovim:**
   ```bash
   nvim
   ```
   - Plugins for TypeScript and JSON will be installed automatically.

3. **Verify Installation:**
   - Use Mason (`<Space> cm`) to confirm the plugins are set up.

---

### Working with Files

1. **Search Files:**
   - Use Telescope to search files:
     ```
     <Space> f f
     ```
     - Preview appears on the right.

2. **Open Files:**
   - Open a specific file, such as `page.tsx`, and navigate with ease using `leap.nvim`.

3. **Edit and Rename:**
   - Rename variables with LSP:
     ```
     <Shift> k  # Hover for type info
     <Space> ca # Code actions
     ```

---

### Using Advanced Features

#### **Search and Replace with Spectre:**

1. Launch Spectre:
   ```
   <Space> s r
   ```
2. Configure the search:
   - Example: Replace `description` with `summary`.
   - Use file type filters (e.g., `.tsx` or `.css`).

#### **Change Color Schemes:**

- Switch themes using:
  ```
  <Space> U C
  ```

#### **Manage Buffers:**

- Toggle buffers:
  ```
  <Space> f b  # List buffers
  ] b          # Next buffer
  [ b          # Previous buffer
  ```

---

### Customizing LazyVim

#### **Add New Plugins:**

1. Add a new file for the plugin in the `plugins` folder, e.g., `file-browser.lua`:
   ```lua
   return {
     "nvim-telescope/telescope-file-browser.nvim",
     keys = {
       { "<Space> S B", function() require("telescope").extensions.file_browser.file_browser() end, desc = "File Browser" }
     }
   }
   ```
2. Install the plugin:
   ```
   :Lazy sync
   ```

#### **Customize the Dashboard:**

1. Create `alpha.lua` in the `plugins` folder:
   ```lua
   return {
     "goolord/alpha-nvim",
     opts = function(opts)
       opts.section.header.val = {
         "My Custom Neovim",
         "@MyTwitterHandle"
       }
       return opts
     end
   }
   ```
2. Reload Neovim to view changes.

#### **Disable Plugins:**

1. Create `disable.lua` in the `plugins` folder:
   ```lua
   return {
     { "nvim-pack/nvim-spectre", enabled = false }
   }
   ```
2. Verify by checking the missing keymap under `<Space> s r`.

---

### Additional Tips

#### **Splits and Navigation:**

- Create splits:
  ```
  <Space> |  # Vertical
  <Space> -  # Horizontal
  ```
- Navigate between splits:
  ```
  Ctrl+h/j/k/l
  ```

#### **Auto-completion and Snippets:**

- Use `<Ctrl> n` to select completions and `<Tab>` to navigate snippet placeholders.

#### **Keymap Search:**

- Search for keymaps:
  ```
  <Space> S K
  ```

---

### Summary

LazyVim offers a feature-rich Neovim setup that can be customized extensively. From managing plugins to tweaking UI and keybindings, LazyVim simplifies the process, making it accessible for both new and experienced users. For more advanced configurations and details, refer to the official documentation and experiment with your setup.

[[Neovim]]  [[Code Editor]]