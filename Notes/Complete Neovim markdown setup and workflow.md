---
github_link: https://github.com/linkarzu/dotfiles-latest
tags:
- editors
video-url: https://www.youtube.com/watch?v=c0cuvzK1SDo&list=WL&index=2
---
## **Complete Neovim markdown setup and workflow

This markdown workflow video outlines the speaker's comprehensive use of plugins, key mappings, automation, and other optimizations for working with markdown files in an editor (likely Neovim, based on context). Below, I provide a detailed summary of each part, including explanations of plugins, links where applicable, and practical usage.

---

#### **1. Markdown Editing Enhancements: Bullet Points & Numbered Lists**

- **Automatic Bullet Point Continuation**:
  - When typing a bullet point (`-` or `*`), pressing Enter automatically continues to the next line with a new bullet.
  - If you add a colon (`:`) at the end of the line, the next bullet is indented.

- **Automatic Numbered Lists**:
  - Start with a number (e.g., `1.`), and pressing Enter continues with an incremented number.
  - The behavior can switch between bullets and numbers and can also drop to plain text after pressing Enter twice.

##### Plugin Related to Bullet Points:

- The plugin for "better bullet points" is integrated into the setup but wasn't explicitly named in the video. This could be **`mini.nvim`** or another plugin supporting markdown automation.

#### **2. Spell Checking in Markdown Files**

- The video shows how spelling can be toggled on or off manually using key mappings.
- **Spell Navigation & Correction**:
  - You can use key mappings to jump between misspelled words, correct them, or add them to a dictionary file.
  - There are also mappings to undo adding a word to the dictionary if needed.

##### Key Plugins and Commands for Spell Check:

- **LazyVim distribution** includes an auto-command that enables spell checking.
- **Tmux Configuration**: Users need to add specific configurations to their `.tmux.conf` to ensure spelling errors show properly.

  **Lines for Tmux Configuration File (`tmux.conf`)**:
  ```bash
  set -g terminal-overrides 'xterm-256color*:Tc'
  ```

  After adding these lines, users must kill the current Tmux session to apply changes.

- **Spell Dictionary Location**:
  - Located in `~/do_files` directory, recommended by John McBride.
  - Manually adding words is discouraged; instead, use mappings for the dictionary to be properly recompiled.

#### **3. Key Mapping for Faster Editing and Workflow Customization**

- **Custom Key Mappings** (`Leader` key used frequently):
  - **`Leader + M + S`**: Shows markdown options.
  - **`Leader + M + R`**: Repeats the last correction across the file.
  - **Undo Dictionary Addition**: Using the mapping `Leader + Ms + U`.

#### **4. Plugin Dashboard Integration and Restoring Sessions**

- **Dashboard Plugin** is used to restore previous sessions quickly.
  - Users should allow a few seconds after opening the dashboard before pressing keys to restore a session; otherwise, spelling check might be disabled.

#### **5. Plugin Settings and Configuration Files**

- **Dotfiles Repository**: Configurations for Tmux, dashboard plugins, and others are stored in dotfiles.
  - Users can download the dotfiles to replicate the setup.

##### How to Access:

- **Tmux Configuration Example**:
  - Navigate to `~/dotfiles/tmux.conf` and view the lines for terminal override settings for Tmux.


#### **6. Todo Management and Task Tracking**

- **Plugin for Task Management**:
  - Creating todo items using `Ctrl + Y`.
  - Marking tasks as done (`Leader + T + D`), and toggling them on and off using the same mapping.
  - Listing all todo items using `Leader + TL` which utilizes the Telescope plugin for easy navigation.

##### Plugin Used:

- **Telescope Plugin** is used to list todo items across files and navigate through them.

#### **7. Generating and Managing Markdown Table of Contents**

- **Table of Contents (TOC)**:
  - Generated at the top of the markdown file and updated automatically using a specific plugin.
  - Activated by pressing `Leader + M + T` (for Markdown TOC).

  ##### Plugin for TOC:
  - **Markdown TOC Plugin** (installed via LazyVim Extras).

#### **8. Markdown File Management**

- **Delete Current File**: `Leader + F + D`.
- **Create or Jump to Daily Notes**:
  - Using **Hyper Key (`Hyper TR`)** to jump to a specific daily note.
  - Automatically creates Tmux sessions with the note name.

#### **9. Viewing and Pasting Images**

- **Image Viewing**:
  - Images can be viewed and pasted within markdown using a plugin that handles different formats (e.g., APNG, WebP, PNG).

  ##### Plugin for Viewing Images:
  - **nvim-picgo** or similar to handle image links directly within the markdown document.

#### **10. Snippets for Markdown**

- **Common Snippets** (e.g., bash code, links, and todo items) are expanded using shortcuts like `Ctrl + Y`.

##### Plugin for Snippets:

- **LuaSnip or Snippy Plugin** configured in LazyVim.

#### **11. Bold Text and Surround Features**

- **Bold Text**:
  - Configured using `Leader + M + B` to quickly bold text.
  - For unbolding, pressing the same sequence again.

  ##### Plugin for Surround Text:
  - **Surround.nvim** or **mini.surround** helps wrap, replace, or delete surrounding characters (e.g., bold, quotes).

#### **12. Navigation Between Markdown Headings**

- **Navigate Headings**: `Leader + MFU` unfolds all headings.
- **Jump Between Headings** using `GJ` and `GK`.

#### **13. Folding and Unfolding Headings**

- Folding by level (`Leader + MFJ` for Level 1, `Leader + MFL` for Level 3).
- Specific configurations are required to avoid leaving headings without content in between them.

#### **14. Markdown Preview and Autosave**

- **Markdown Preview**:
  - Enabled with `Leader + MP` to preview in a browser or another pane.

  ##### Plugin:
  - **Markdown Preview Plugin**.

#### **15. Image Management Plugins**

- **Pasting Images**: Uses a plugin that saves screenshots or pasted images directly in the markdown file.

#### **16. Buffers and Navigation**

- **BuffExplorer Plugin**: `Shift + H` to navigate through the most recently used buffers.
- **Buffer Management**:
  - Uses `Leader + FB` to view buffers and `Leader + WD` to close them.

#### **17. Searching and Replacing Text**

- **Spectre Plugin**:
  - Search and replace across multiple files using `Leader + SR`.
  - Can selectively replace in specific files only.

#### **18. Markdown Linting and Formatting**

- **Linting Plugin (`markdown-cli2`)**:
  - Shows errors like duplicate headings or multiple `H1` headers.
  - Use `Leader + XX` to display warnings.

#### **19. Marks and Links Navigation**

- **Marks Management**:
  - Press `M + letter` to create a mark and `MD` to delete all marks.
- **Convert Selected Text to a Link**: `Leader + M + L`.

  ##### Plugin for Links:
  - Likely **Marksman** plugin or similar to enable markdown linking and navigation.

#### **20. File Path Operations**

- **Add File Path as Comment**: Use `Ctrl + Z`.
- **Copy File Path to Clipboard**: `Leader + F + P`.

#### **21. Markdown Plugins Summary**

- Plugins mentioned:
  - **Mini.AI**: Selects text easily (e.g., quotes).
  - **Stay Centered**: Keeps cursor centered.
  - **Outline.nvim**: For navigation by headings.
  - **Headlines.nvim**: Styles headings visually.
  - **Spectre**: Search and replace plugin.
  - **BuffExplorer**: For managing open buffers.
  - **Telescope**: Search and navigate through files.
  - **TreeSitter**: Syntax highlighting for different code blocks.
  - **LazyExtras**: Contains several useful plugins for Markdown handling.

##### Plugin URLs and Resources:

- Most plugins can be found on **GitHub** by searching for their names, and detailed configuration examples are in the user's **Dotfiles** repository. For a complete setup, users can clone the dotfiles and load them into their configuration.

---

### Conclusion

The video provides a highly detailed markdown editing workflow, utilizing various Neovim plugins, automation tools, and key mappings to enhance productivity. The key aspects include automatic bullet and numbering management, spelling checks, todo item tracking, TOC generation, snippet insertion, markdown linting, buffer management, and even image handling—all through a combination of key mappings and a robust set of plugins. The workflow makes extensive use of **LazyVim** and other plugins that facilitate markdown editing and navigation.

For users who wish to replicate this setup:

- **Dotfiles and Configurations**: Clone the dotfiles repository shared by the creator.
- **Tmux Configuration**: Ensure `.tmux.conf` has the correct settings for proper compatibility with the editor setup.
- **Plugins Installation**: Most plugins can be installed using **Lazy.nvim** or **Mason** (which is integrated with Lazy.nvim for additional plugin management).

This workflow is ideal for those who use markdown frequently for notes, project documentation, or other purposes, especially within an editor like Neovim. It emphasizes efficiency and minimal manual intervention, relying on automated tools and shortcuts to maintain consistency and improve productivity.

[[Neovim]]  [[Markdown]]