---
tags:
- vscode
- editors
video-url: https://www.youtube.com/watch?v=VFaIq7PTIyU&list=WL&index=3https://www.youtube.com/watch?v=VFaIq7PTIyU&list=WL&index=3
---

## **Overview of NeoVim Setup and Transition Guide

Below is a detailed overview of the content, extracted how-to instructions, and all relevant code examples based on the provided transcript.

#### Personal Update and Content Direction

The creator provides a personal update on their life, discussing their recent burnout and plans for future YouTube content. They share their transition from VS Code to NeoVim, focusing on creating educational videos around learning Go, algorithms, and computer science concepts. The content's direction will move beyond just JavaScript libraries to more overarching computer science topics.

#### Transition from VS Code to NeoVim

The creator describes their frustration with VS Code, primarily due to perceived slowness and inefficiencies. They experiment with various Neovim configurations like **Dracula**, **LazyVim**, **LunarVim**, and others, before settling on a simpler, customizable setup with **AstroNvim**.

They emphasize that beginners can start with a pre-configured version like AstroNvim or Kickstart, which allows users to quickly familiarize themselves with NeoVim features before customizing further.

---

### Step-by-Step Instructions for NeoVim Setup

#### **1. Download and Install NeoVim**

- Clone the NeoVim configuration repository (**AstroNvim**):
  ```bash
  git clone https://github.com/AstroNvim/AstroNvim ~/.config/nvim
  ```
- Navigate to the configuration directory:
  ```bash
  cd ~/.config/nvim
  ```
- Launch NeoVim:
  ```bash
  nvim
  ```

#### **2. Install Nerd Fonts**

- Visit [Nerd Fonts](https://www.nerdfonts.com/) and download a preferred font (e.g., `Proton`).
- Set your terminal to use the installed font.

#### **3. Install Dependencies**

- On launching NeoVim, it will install plugins and set up dependencies automatically.

---

### Configuring Plugins

#### **Adding Plugins**

- **Add and Configure Plugins** in `community.lua` (AstroNvim config).
  - For TypeScript and TailwindCSS, add:
    ```lua
    { import = "astrocommunity.pack.typescript" },
    { import = "astrocommunity.pack.tailwindcss" },
    ```

#### **Set Up Diagnostics**

- Add and enable **trouble.nvim** for diagnostics:
  ```lua
  { import = "astrocommunity.diagnostics.trouble-nvim" },
  ```

#### **Enable AutoPairs**

- Ensure **auto-pairing** is activated for efficient coding:
  ```lua
  enable_auto_pairs = true
  ```

#### **Add a Smooth Scrolling Effect**

- Install **mini-animate** for visual enhancements:
  ```lua
  { import = "astrocommunity.scrolling.mini-animate" },
  ```

#### **Customize Hover Behavior**

- Add **hover.nvim** for hover previews:
  ```lua
  { import = "astrocommunity.utility.hover.nvim" },
  ```

#### **Set a Custom Color Scheme**

- Add a custom color scheme (e.g., **Rose Pine**):
  ```lua
  { import = "astrocommunity.colorscheme.rose-pine" },
  ```

---

### Common NeoVim Commands

#### **Basic Commands**

- **Quit NeoVim**:
  ```bash
  :q
  ```
- **Save File**:
  ```bash
  :w
  ```
- **Edit a New File**:
  ```bash
  :e <filename>
  ```

#### **File Tree and Search**

- **Open/close file tree**:
  ```bash
  SPACE + e
  ```
- **Use Telescope for fuzzy search**:
  ```bash
  SPACE + ff
  ```

#### **Navigate Buffers**

- **Search between open buffers**:
  ```bash
  SPACE + fb
  ```

#### **Insert Mode Escape**

- Quickly exit **insert mode** by typing `jj`:
  ```lua
  better_escape = true
  ```

---

### Advanced Features

#### **Auto-Completion and TailwindCSS Integration**

- **Activate TailwindCSS autocompletion** for better productivity:
  ```lua
  mason_lspconfig.setup({
    ensure_installed = { "tsserver", "tailwindcss" },
  })
  ```

#### **Git Integration**

- **View changes** like additions, deletions, and modifications in the sidebar.

#### **Customize Icons**

- Modify icons using **Nerd Fonts** and add custom mappings in the configuration.

#### **Prettier Integration**

- Automatically **format files** on save to maintain clean code:
  ```lua
  format_on_save = true
  ```

---

### Summary

- The creator recommends starting with **AstroNvim** for a hassle-free experience.
- Plugins like **trouble.nvim**, **hover.nvim**, and **mini-animate** enhance both productivity and aesthetics.
- Experimenting with NeoVim commands and key mappings helps in building muscle memory and improving efficiency.

This detailed overview condenses the original content into actionable steps for those looking to transition to NeoVim. Let me know if you need more details or assistance with any specific part of the setup!

[[VSCode]]  [[Neovim]]  [[Code Editor]]