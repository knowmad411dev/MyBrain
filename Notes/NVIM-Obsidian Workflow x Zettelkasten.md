---
github_link: https://github.com/mg979/vim-visual-multi
tags:
- obsidian
- editors
- automation
video-url: https://www.youtube.com/watch?v=sVRPa6928Ws&list=WL&index=3
---
## **NVIM-Obsidian Workflow x Zettelkasten

### Overview of the Workflow

The user in this text is trying to:

1. Use terminal commands to manipulate Markdown (.md) files from Obsidian.
2. Gather the Zettels (atomic notes) and generate a sequence for their manuscript.
3. Edit the generated sequence by inserting or deleting items.
4. Use terminal shortcuts, Vim-style commands, and plugins to achieve this.


Here is the detailed overview broken into steps:

### Step 1: Prepare Command to List Markdown Files

- The user has a custom workflow for writing a manuscript from their notes, known as Zettelkasten.
- The workflow starts in the **terminal**, listing the files in the working directory.
- The command used is pasted into the terminal by pressing `Ctrl + Shift + V`.


#### Code Example to List Files Without Extensions

The command mentioned outputs a list of Markdown files without the `.md` extension. Let's summarize what it does:

```sh
ls | sed 's/.md$//' > info
```

**Explanation:**
- `ls` lists all the files in the current directory.
- The pipe `|` directs the output from `ls` to the next command.
- `sed 's/.md$//'` uses a stream editor (`sed`) to remove `.md` extensions from the filenames.
  - `'s/.md$//'`: This means substitute (`s`) `.md` at the end (`$`) with nothing (`//`).
- `> info` saves the output to a new file named **info**.

**Purpose:**
This command creates a new file named `info` that contains the list of Markdown filenames **without** their extensions.

### Step 2: View and Edit the Generated List in Terminal

- After creating the file `info`, the user looks at its contents and begins editing.
- The process involves **inserting new lines** or deleting unwanted lines in the list.

#### Vim-style Commands for Editing

The text references using some **Vim** commands:

- **`i` for insert**: This allows the user to enter insert mode and add content.
- **`dd` to delete**: Deletes the current line.
- **Escape (`Esc`)** to go back to normal mode.

**Example:**
1. **Open the file** in a text editor (likely Vim or a similar terminal-based editor).
2. **Insert mode (`i`)** is used to add new lines manually.
3. **Delete lines (`dd`)** that aren’t needed.
4. **Paste (`p`)** can be used to place the copied content elsewhere.


### Step 3: Reorder Notes

- The goal here is to create a new sequence of notes from the Zettels. By deleting, inserting, and moving items around, the user can structure the notes for their manuscript.
- **Never switch between tasks**: The user emphasizes efficiency by avoiding task-switching between tools (such as the terminal and another application).

### Step 4: Using a Plugin for Obsidian Integration

- The user uses a **special plugin** that allows for better integration between Obsidian and the terminal.
- This helps streamline the workflow, likely allowing commands to be executed directly from Obsidian or providing advanced navigation or editing options.

### How-to Instructions Summarized

Here’s a simplified guide based on the provided workflow:

1. **Navigate to Your Notes Directory** in the terminal.
   ```sh
   cd path/to/your/notes
   ```
2. **List Markdown Files Without Extensions**:
   - Run the command to get a list of your Markdown files, removing the `.md` extensions.
   ```sh
   ls | sed 's/.md$//' > info
   ```
3. **Open the File for Editing**:
   - Use a terminal-based editor (like Vim or Nano) to open the `info` file.
   ```sh
   vim info
   ```
4. **Edit the File**:
   - Press `i` to enter insert mode and add lines.
   - Use `dd` to delete lines you don’t need.
   - Press `Esc` to return to normal mode.
   - Use `p` to paste lines elsewhere if needed.
5. **Reorganize Notes for Your Manuscript**:
   - Create a meaningful sequence by editing directly in the terminal.
   - Insert or reorder lines to structure the content effectively.


### Useful Vim Commands Recap

- **`i`** - Insert mode.
- **`dd`** - Delete current line.
- **`p`** - Paste below the current line.
- **`Esc`** - Exit insert mode.

### Plugins and Additional Tools

The user mentions that they use a special plugin for Obsidian. While the plugin isn't specified here, it could be one that allows executing terminal commands or better navigating between Obsidian and a terminal environment.

### Additional Considerations

- The text encourages staying in **"normal mode"** and **avoiding switching between tasks** to maintain focus.
- There is an emphasis on productivity, using quick terminal commands, and avoiding context switching between multiple applications.
- Using `Ctrl + Shift + V` is a common terminal shortcut for **pasting** content, especially in Linux terminals.

### Conclusion

The workflow in this text is highly manual but powerful for managing and organizing large amounts of Markdown notes directly through the terminal. It uses **command-line tools**, **Vim commands**, and an **Obsidian plugin** to efficiently manipulate the sequence of Zettels for writing a manuscript. The approach takes advantage of the terminal’s power for quick text manipulations and supports productivity by minimizing task switching.

The **plugin** is mentioned but not explicitly identified. It likely plays a role in automating the integration between Obsidian and the terminal, helping to complete the workflow more effectively.

[[Obsidian]]  [[Neovim]]   [[Low-Code Automation]]