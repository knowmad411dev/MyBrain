---
tags:
- obsidian
- editors
video-url: https://www.youtube.com/watch?v=pCzSPHrLBoU&list=WL&index=1
---
## **Obsidian to Neovim

### Overview

The video presents a detailed comparison between using **Obsidian** and **Neovim** (the presenter calls it "NE of them") as note-taking and editing tools. The presenter explains why they switched from Obsidian to Neovim and outlines how Neovim can now support many of the features they once relied on Obsidian for. The speaker provides a practical demonstration of various capabilities within both applications, discussing the reasons for their shift and how they overcame obstacles to make Neovim their primary note-taking tool.

### Key Differences Highlighted

1. **Context Switching**
   - **Obsidian** was used as a note-taking tool, while other text-editing tasks were handled in **Neovim**.
   - The constant need to switch between these two contexts disrupted productivity.
   - **Neovim** in the terminal allows seamless workflow without needing to leave the terminal environment.

2. **Image Support**
   - Initially, the speaker stuck with **Obsidian** because **Neovim** could not handle images.
   - By using **Kitty** (a terminal emulator), they were able to view and paste images in Neovim, just like they could in Obsidian.
   - The **Kitty** terminal provided support for different image formats like AVIF, WebP, PNG, and JPG.
   - **Automatic Image Saving**: Images pasted in Neovim using Kitty are saved in AVIF format by default for better quality and reduced file size, but other formats can be configured.

3. **Folding Headings**
   - Neovim's ability to handle "folds" was a major reason for the switch.
   - **Headings Folding**: The presenter demonstrated folding/unfolding headings of different levels in Neovim (e.g., level 2, level 3).
   - **Custom Keymaps**: Custom keybindings were set to control folding/unfolding at different heading levels. For example:
     - **`mfu`**: Unfold everything.
     - **`mfk`**: Fold everything up to level 2.
     - **`mfl`**: Fold everything up to level 3.

4. **Outline Navigation**
   - In Neovim, headings can be navigated efficiently without using an outline plugin, leveraging the folding structure.
   - The **outline plugin** in Obsidian is less necessary in Neovim, where keybindings facilitate navigation.
   - Custom keybindings were configured for navigating between headings:
     - **`GK`**: Go to the previous heading.
     - **`GJ`**: Go to the next heading.

5. **Linking Notes**
   - Neovim supports linking notes similar to **Obsidian's wiki links**.
   - Using the command **`GD` (go to definition)** in Neovim, the user can jump to linked notes or headings.
   - Pressing **`Ctrl+O`** will return them to the previous link.

6. **Advanced Text Manipulation**
   - **Neovim's Vim Motions** allow more powerful editing features compared to **Obsidian**:
     - Code formatting:
       - **`GSA ~`**: Format selected text as code.
     - Replacing text:
       - **`GSR ~`**: Replace with quotes or different characters.
     - Bullet points:
       - **`MD`**: Toggle bullet points on and off.

7. **Daily Notes & Journal**
   - The speaker uses a custom keybinding (**`Hyper+TR`**) to create or access **daily notes** in Neovim.
   - The setup automatically creates a new note for the current day or switches to it if it already exists.
   - Daily notes are autosaved, just like in Obsidian, making it easy for the user to journal or keep daily records.

8. **Git Integration**
   - **Obsidian** was being used to auto-sync with **GitHub** using a plugin that automatically commits and pushes changes.
   - In Neovim, the speaker initially pushed commits manually but plans to configure automated git integration.

9. **Additional Plugins and Features in Neovim**
   - **Frenzy Telescope** plugin: This plugin allows efficient file searching. Frequently accessed notes are ranked higher.
   - **Snip Plugin**: The user can navigate between buffers using single key presses:
     - For instance, pressing **`F`** moves to a specific file.
     - **`Space+Space`** is configured to alternate buffers quickly.
   - **Telescope Search**: The presenter uses **`SG`** to search within all notes in a directory.
   - **TAC Sessions**: The user organizes their notes using sessions:
     - **Daily Note Session**: Created automatically when pressing **`Hyper+TR`**.
     - Switching to the **daily note** or other sessions happens with these keybindings.

10. **Blogging and Publishing**
    - **Neovim** also became the primary tool for editing blog posts.
    - Using folds and other advanced editing capabilities, writing blog posts is similar to editing markdown files.
    - The speaker contrasts this with **Obsidian's** **Obsidian Publish** feature, which they chose not to use.

11. **Graph View in Obsidian**
    - The presenter briefly mentions **Obsidian's Graph View** but dismisses its usefulness, describing it as more cosmetic than practical.

12. **Search and Navigation**
    - **Telescope Plugin** in Neovim helps search for notes based on content, similar to Obsidian’s search capabilities.
    - **Frenzy Plugin** ranks and shows frequently used notes at the top.
    - The **snip plugin** and **telescope search** allow smooth navigation between open buffers and search results.

### How-To Instructions

1. **Image Viewing & Pasting with Kitty**
   - Install **Kitty Terminal**: Kitty is a terminal emulator that supports image viewing.
   - Configure Neovim to save images automatically in **AVIF format** by default or another format as desired.
   - Paste images into Neovim to see them rendered directly in Kitty.

2. **Fold and Navigate Headings in Neovim**
   - **Fold Headings**: Use **custom key mappings** to fold/unfold:
     - **Enter** on a folded heading to expand or collapse.
   - **Navigate Headings**:
     - Use **`GK`** to go up a heading.
     - Use **`GJ`** to go down a heading.
   - **Fold All to Specific Levels**:
     - **`mfk`**: Fold all to level 2.
     - **`mfl`**: Fold all to level 3.

3. **Linking Notes**
   - Use **`[[Note Name]]`** to link between markdown files in Neovim.
   - To navigate, press **`GD` (go to definition)** to follow a link, and use **`Ctrl+O`** to return.

4. **Advanced Editing with Vim Motions**
   - To **format text as code**:
     - **`GSA ~`** selects and formats the text as code.
   - To **replace**:
     - **`GSR ~`** with the desired character (e.g., replace with quotes).
   - To **toggle bullet points**:
     - **`MD`** can add or remove bullet points.

5. **Accessing Daily Notes**
   - Use **`Hyper+TR`**: Create or access daily notes.
   - The setup creates a new note if it does not exist or switches to the existing note if it does.

6. **GitHub Integration**
   - For automated GitHub commits and pushes, configure **git plugin** in Neovim.
   - Alternatively, commits can be done manually from within Neovim.

7. **Efficient File Search and Navigation**
   - Use **`Telescope Freeny`** to search files efficiently.
   - Frequently used notes appear at the top when searching.
   - **Snip Plugin**: Use **Shift+L** to switch between open buffers quickly.

8. **Blog Writing**
   - Blog posts can be edited just like markdown files.
   - Create folds to organize sections and navigate them efficiently.

### Summary

The video showcases the speaker’s journey and reasons for transitioning from **Obsidian** to **Neovim** as their primary markdown editor. They moved to Neovim to avoid context switching, leverage the terminal’s power, and utilize plugins like Kitty and Telescope for advanced features. They addressed the challenge of **image viewing**, implemented **daily note creation**, set up **folds for organized navigation**, and demonstrated **advanced editing capabilities** with **Vim Motions**.

While Obsidian offers a powerful and user-friendly markdown editor, Neovim's customizable environment in the terminal ultimately provided the presenter with a more streamlined and productive workflow. The video highlights the freedom that comes with **key mapping** and customizing an open-source tool to fit personal workflow needs, minimizing distractions and enhancing productivity. The speaker also emphasizes that while **Obsidian** is a great tool, their preference for terminal-based work led them to fully migrate to **Neovim**.

[[Obsidian]]  [[Neovim]]