---
tags:
- editors
- obsidian
video-url: https://www.youtube.com/watch?v=DgKI4hZ4EEI&list=WL&index=1
---
## **Perfect Neovim Note Takers Setup

### **Overview**

This detailed guide explains how to transform Neovim into a powerful markdown-based note-taking and writing tool, including the use of plugins and workflows to enhance your productivity. Here, we'll walk through core plugins, features, and the step-by-step instructions needed to set up and use them effectively.

---

### **Key Features & Plugins**

#### **1. Markdown Rendering in Neovim**

- **Plugin:** `markdown.nvim`
  - **Features:**
    - Enhanced visuals for markdown files: headings, numbered icons, lists, separators.
    - Syntax-aware rendering of tables, checkboxes, and callouts.
    - Integration with Tree-sitter for parsing markdown syntax.
    - Customization options for icons, nesting levels, and separators.
  - **Installation via Lazy.nvim:**
    ```lua
    -- Add this to your Lazy.nvim configuration
    use({
        'plugin/markdown.nvim',
        config = function()
            require('markdown').setup()
        end,
    })
    ```

#### **2. Live Markdown Preview**

- **Plugin:** `markdown-preview.nvim`
  - **Purpose:** Render markdown in a browser for real-time previews.
  - **Features:**
    - Tracks Neovim movements and synchronizes them in the browser.
    - Updates rendered markdown in real time.
  - **Installation:**
    ```lua
    use({
        'plugin/markdown-preview.nvim',
        config = function()
            require('markdown-preview').setup()
        end,
    })
    ```

  - **Usage:**
    Run the command `:MarkdownPreview` to start the live preview in a browser.

#### **3. CLI Markdown Renderer**

- **Tool:** `Glow`
  - **Features:**
    - Renders markdown files in the terminal.
    - Provides a fuzzy search interface to browse markdown files in a directory.
  - **Installation:**
    ```bash
    brew install glow  # On macOS
    sudo apt install glow  # On Linux
    ```

  - **Usage:**
    ```bash
    glow <file.md>  # Render a specific file
    glow            # Open fuzzy search mode
    ```

#### **4. Obsidian Integration**

- **Plugin:** `obsidian.nvim`
  - **Features:**
    - Synchronizes notes between Obsidian and Neovim.
    - Supports front matter injection for note classification.
    - Allows linking and navigating between notes directly in Neovim.
  - **Installation:**
    ```lua
    use({
        'plugin/obsidian.nvim',
        config = function()
            require('obsidian').setup()
        end,
    })
    ```

  - **Setup Conflict Resolution:**
    Disable conflicting markdown UI elements in Obsidian when using `markdown.nvim`.

#### **5. Blogging with Quartz**

- **Framework:** `Quartz`
  - **Purpose:** Publish markdown notes as a blog or local server.
  - **Features:**
    - Graph visualization for linked notes.
    - Rendered previews and tags.
    - Easy deployment to platforms like Cloudflare Pages.
  - **Setup:**
    ```bash
    # Clone Quartz repository
    git clone https://github.com/jackyzha0/quartz.git

    # Install dependencies
    npm install

    # Create content
    npx quartz create

    # Serve locally
    npx quartz build --serve
    ```

---

### **Step-by-Step Workflow**

#### **1. Enhancing Markdown in Neovim**

- Install and configure `markdown.nvim`.
- Customize visuals: icons, separators, nesting levels.

#### **2. Live Previewing Markdown**

- Add `markdown-preview.nvim` to Lazy.nvim config.
- Use `:MarkdownPreview` to open a browser with real-time synced rendering.

#### **3. Quick Terminal Rendering**

- Install and use `Glow` for quick markdown previews in the terminal.

#### **4. Syncing with Obsidian**

- Install `obsidian.nvim`.
- Synchronize notes between Neovim and Obsidian.
- Leverage linking and classification for a "second brain" system.

#### **5. Publishing Notes Online**

- Use Quartz for turning local markdown notes into a hosted blog.
- Follow Quartz setup instructions to configure and deploy.

---

### **Code Example**

#### Markdown.nvim Configuration

```lua
use({
    'plugin/markdown.nvim',
    config = function()
        require('markdown').setup({
            icons = {
                heading = "",
                list = "",
                nested = "",
            },
            separators = {
                line = "─",
                block = "━",
            },
        })
    end,
})
```

#### Obsidian.nvim Configuration

```lua
use({
    'epwalsh/obsidian.nvim',
    config = function()
        require('obsidian').setup({
            dir = "~/notes",
            mappings = {
                link = "gf",  -- Go to linked note
            },
        })
    end,
})
```

#### Quartz Deployment

```bash
# Deploy to Cloudflare Pages
npx quartz build
npx quartz deploy --cloudflare
```

---

### **Tips for Productivity**

- Customize Neovim to match your markdown workflow.
- Use Tree-sitter-powered plugins for advanced syntax highlighting.
- Combine plugins like `markdown.nvim` and `markdown-preview.nvim` for seamless writing and publishing.

---

### **Conclusion**

This guide demonstrates how to transform Neovim into a powerful markdown-centric note-taking and writing tool. The combination of plugins, live preview capabilities, and integrations like Obsidian and Quartz ensures that users can write, organize, and publish their notes effectively.

  [[Obsidian]]   [[Neovim]]