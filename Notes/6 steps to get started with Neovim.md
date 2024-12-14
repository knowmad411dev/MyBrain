---
tags:
- editors
video-url: https://www.youtube.com/watch?v=gI-6n3Pq7TU&list=WL&index=1
---
## **6 steps to get started with Neovim

**Detailed Overview of Setting Up and Learning Neovim**

### Step 1: Install Neovim

1. Go to the official Neovim website at [https://neovim.io](https://neovim.io).
2. Click on "Install Now."
3. Scroll down to locate your operating system or distribution (e.g., Windows, MacOS, Linux) and follow the specific instructions to install Neovim. This typically involves downloading the appropriate package or running a package manager command.

### Step 2: Learn the Basics of Neovim

1. Open Neovim by typing `nvim` in your terminal.
2. To begin learning the basics, type `:Tutor` (note the capital "T").
   - This command will open a 30-minute tutorial that introduces you to navigation, file editing, searching, and other essential commands.
   - Completing this tutorial will give you a solid foundation on how to use Neovim effectively, including tasks like saving, quitting, and navigating through text.

### Step 3: Customize Your Neovim Setup

1. Visit the following link: [https://github.com/nvim-lua/kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim).
2. This repository is designed as an excellent starting point for configuring Neovim according to your personal preferences.
   - **Why Use This?** It offers a simple entry point for customization without the complexity of starting from scratch or the clutter of larger distributions that might be overwhelming.
3. You can fork this repository to have your own version, allowing you to modify and save changes, though this is optional.
4. Scroll down to the "Installation Guide" section and make sure you meet all requirements.
5. Follow the installation instructions for your operating system, but essentially you will:
   - Clone the repository into your Neovim configuration directory, usually located at `~/.config/nvim` for Linux/MacOS.
   - Run the command: `git clone https://github.com/nvim-lua/kickstart.nvim ~/.config/nvim`
6. Once cloned, open Neovim:
   - Plugins will automatically be installed using a package manager (like Lazy.nvim).
   - Exit Neovim after the installation is complete.
7. Navigate to your Neovim configuration directory and open the `init.lua` file:
   - This is the main configuration entry point.
   - Go through the file line by line; it has detailed comments that explain how everything works and what to modify to suit your preferences.

### Step 4: Read the User Manual

1. Now that you have a configured and powerful editor, it is crucial to understand its full capabilities.
2. To access the user manual, type `:help user-manual` in Neovim and hit enter.
3. To make it full-screen, type `:only` or combine the commands as `:help user-manual | only`.
4. To explore links within the manual, move your cursor to a link and press `Ctrl + ]`. This will take you directly to that section, allowing you to explore documentation interactively.
5. For those who prefer auditory learning, you can also watch TJ DeVries, a prominent Neovim contributor, reading the manual.

### Step 5: Enjoy Your New Editor

- Take the time to get comfortable using Neovim for everyday tasks.
- Practice editing text, moving around files, and utilizing the plugins that you installed earlier.

### Step 6: Become an Advanced User

- Learn more advanced topics to fully leverage Neovim:
  - Learn **Lua**, the scripting language used by Neovim, which will allow you to write your own plugins and extend Neovim’s functionality.
  - Read the entire Neovim documentation (`:help` command) to deepen your knowledge.
  - Consider contributing to Neovim's open-source community by submitting bug reports or contributing code.

### Step 7: Optional - Emacs Joke

- "Reach Enlightenment and learn Emacs." This step is mentioned jokingly, as Emacs is often considered a rival to Vim/Neovim. The author humorously dismisses it with "Just kidding, nobody got time for this."

### Step 8: Final Words

- If you found the tutorial helpful, subscribe, like, and comment on the creator's content.
- Have a good day and happy coding! The author signs off with a light-hearted message, "Made with ❤️".

[[Neovim]]