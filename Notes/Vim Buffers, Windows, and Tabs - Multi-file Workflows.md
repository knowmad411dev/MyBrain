---
tags:
- editors
url: https://neovim.io/doc/user/windows.html#_1.-introduction
video-url: https://www.youtube.com/watch?v=XRIhRhDj3_c&list=WL&index=5
---
## **Vim Buffers, Windows, and Tabs - Multi-file Workflows

## **Overview of Buffers, Windows, and Tabs in Vim**

Vim provides powerful ways to work with multiple files simultaneously through **buffers**, **windows**, and **tabs**. Here, we will explore how to use these features effectively, with detailed instructions and code examples for each.

### **1. Buffers**

**Buffers** are essentially files that Vim loads into memory, allowing you to work with their content without affecting the actual files until you explicitly save changes.

Here's a step-by-step guide on how to work with **buffers**:

- **Opening a File (Creating a Buffer):**
  - When you open a file in Vim, a new buffer is created for that file.
    ```vim
    :e <filename>  " This command opens a file and loads it into a buffer.
    ```

- **Viewing Buffers:**
  - You can view a list of all the currently open buffers using the command:
    ```vim
    :ls  " Lists all open buffers.
    ```

    Each buffer is assigned a unique **buffer number**, which helps in switching between them.

- **Switching Between Buffers:**
  - To switch to a different buffer by its **buffer number**:
    ```vim
    :b <buffer-number>  " Switch to a buffer by number.
    ```
    - For example:
      ```vim
      :b 2  " Switch to buffer number 2.
      ```

- **Cycling Through Buffers:**
  - You can cycle through buffers using:
    ```vim
    :bnext  " Move to the next buffer.
    :bprev  " Move to the previous buffer.
    ```

    Many users map these commands to make cycling more convenient:

    ```vim
    nnoremap <key> :bnext<CR>  " Maps a key to move to the next buffer.
    nnoremap <key> :bprev<CR>  " Maps a key to move to the previous buffer.
    ```

- **Removing Buffers:**
  - To **delete** a buffer and remove it from the list:
    ```vim
    :bd <buffer-number>  " Deletes the specified buffer.
    ```
  - You can also **delete all buffers except** the one you are currently viewing:
    ```vim
    :%bd|e#|bd#  " Deletes all buffers except the current one.
    ```

- **Quick Buffer Search:**
  - If you know part of the filename but not the buffer number, you can start typing and use **tab completion** to find the correct buffer:
    ```vim
    :b test  " Start typing part of the filename.
    ```

### **2. Windows**

**Windows** in Vim are **views** into buffers. You can open multiple windows to view and edit different files or different parts of the same file simultaneously.

Here's how to work with **windows**:

- **Splitting Windows:**
  - **Vertical Split** (splits the screen side-by-side):
    ```vim
    :vsplit <filename>  " Splits vertically and opens the file in a new window.
    ```
  - **Horizontal Split** (splits the screen into top and bottom panes):
    ```vim
    :split <filename>  " Splits horizontally and opens the file in a new window.
    ```

- **Resizing Windows:**
  - To adjust window size:
    - Resize vertically:
      ```vim
      Ctrl-w +   " Increase window height.
      Ctrl-w -   " Decrease window height.
      ```
    - Equalize all windows:
      ```vim
      Ctrl-w =   " Make all window sizes equal.
      ```

- **Navigating Windows:**
  - To navigate between windows, use:
    ```vim
    Ctrl-w w  " Move to the next window.
    Ctrl-w h  " Move left.
    Ctrl-w j  " Move down.
    Ctrl-w k  " Move up.
    Ctrl-w l  " Move right.
    ```

- **Closing Windows:**
  - To close the current window:
    ```vim
    :q  " Closes the current window.
    ```
  - To close all windows except the current one:
    ```vim
    Ctrl-w o  " Closes all other windows.
    ```

### **3. Tabs**

**Tabs** in Vim can be thought of as a container for one or more **windows**. Each tab can hold its own arrangement of windows.

Here's how to use **tabs** in Vim:

- **Creating Tabs:**
  - To open a new tab with a file:
    ```vim
    :tabedit <filename>  " Opens the file in a new tab.
    ```
  - You can also create a new empty tab:
    ```vim
    :tabnew  " Opens a new tab.
    ```

- **Navigating Tabs:**
  - To move to the next tab:
    ```vim
    :tabnext  " Moves to the next tab.
    ```
  - To move to the previous tab:
    ```vim
    :tabprevious  " Moves to the previous tab.
    ```
  - Shortcut to move between tabs:
    ```vim
    gt  " Move to the next tab.
    gT  " Move to the previous tab.
    ```

- **Closing Tabs:**
  - To close the current tab:
    ```vim
    :tabclose  " Closes the current tab.
    ```
  - To close all tabs except the current one:
    ```vim
    :tabonly  " Closes all other tabs.
    ```

### **Workflow Tips for Buffers, Windows, and Tabs**

1. **Efficient Buffer Cycling**:
   - Use mappings or commands like `:bnext` or `:bprev` to quickly switch between buffers.

2. **Working with Multiple Files**:
   - When comparing two related files (e.g., code and test), use **vertical windows** to see both files side-by-side:
     ```vim
     :vsplit file1
     :vsplit file2
     ```

3. **Using Tabs for Context Switching**:
   - Tabs are useful for switching **context**, such as working on two separate projects. Instead of opening all files in different windows or buffers, open them in **separate tabs** to maintain different arrangements.

4. **Avoid Overusing Tabs**:
   - Unlike GUI editors like VS Code or Atom, Vim’s tabs are not meant to function as a tab per file. Instead, rely on **buffers** for individual files, and use **tabs** for different workflows or larger tasks.

5. **Managing Directories with Tabs**:
   - Use different tabs to work on **different projects**. You can use the `:lcd` command to change the local directory for each tab.
     ```vim
     :lcd <directory-path>  " Set the local directory for the current tab or window.
     ```

### **Key Mappings for Common Tasks**

To make your workflow easier, here are some suggested key mappings:

- **Cycle Through Buffers**:
  ```vim
  nnoremap <Tab> :bnext<CR>     " Map Tab to move to the next buffer.
  nnoremap <S-Tab> :bprev<CR>   " Map Shift-Tab to move to the previous buffer.
  ```

- **Close All Buffers Except Current**:
  ```vim
  nnoremap <Leader>bd :%bd|e#|bd#<CR>  " Deletes all buffers except the current one.
  ```

- **Open and Close Windows Easily**:
  ```vim
  nnoremap <Leader>vs :vsplit<CR>   " Vertical split.
  nnoremap <Leader>hs :split<CR>    " Horizontal split.
  nnoremap <Leader>q :q<CR>         " Close current window.
  ```

### **Example Use Cases**

- **Working with Related Files**:
  - Suppose you are working on a code file and its corresponding test file. You can use a **vertical split** to see both files side-by-side:
    ```vim
    :vsplit code.py
    :vsplit test_code.py
    ```

- **Switching Projects with Tabs**:
  - Suppose you need to switch between two projects. Open each project in a different **tab**:
    ```vim
    :tabnew
    :lcd /path/to/project1  " Set the directory for the first tab.
    :e main.py              " Edit main file in this tab.
    
    :tabnew
    :lcd /path/to/project2  " Set the directory for the second tab.
    :e app.py               " Edit app file in this tab.
    ```

By understanding and effectively using buffers, windows, and tabs, you can tailor Vim to fit various workflows and improve your productivity. Buffers allow you to work on multiple files seamlessly, windows let you view multiple files simultaneously, and tabs help manage different work contexts without disrupting your workflow.

[[Neovim]]