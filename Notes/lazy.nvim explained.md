---
github_link: https://github.com/tjdevries/advent-of-nvim/
tags:
- editors
video-url: https://www.youtube.com/watch?v=_kPg0VBRxJc&list=WL&index=2
---

## **lazy.nvim explained

In this guide, we'll cover how to install and set up the "Lazy.nvim" package manager for Neovim, configuring some plugins along the way, and exploring core concepts behind plugin management. This is a step-by-step breakdown, including all code examples, to help you fully understand what each part of the process does.

### Overview of Lazy.nvim and [[Neovim]] Plugin Management

Lazy.nvim is a powerful package manager for Neovim that helps organize and load plugins efficiently. We'll explore how Neovim identifies plugins, what runtime paths are, and how we use Lazy.nvim to extend Neovim's capabilities while keeping our plugin configurations separate and maintainable.

#### Step 1: Install Lazy.nvim

First, you need to install Lazy.nvim. Here's how:

1. **Create Lua Folder:** Inside your Neovim configuration directory, you need to create a new folder to hold Lua files. Run the following command to create the folder:
   ```sh
   mkdir ~/.config/nvim/lua
   ```
2. **Create Config File:** Within the new Lua folder, create another folder called `config` and a new file named `lazy.lua`.
   ```sh
   mkdir ~/.config/nvim/lua/config
   touch ~/.config/nvim/lua/config/lazy.lua
   ```
3. **Require the File:** To load Lazy.nvim, we use the `require` function inside Lua. This function works like the import function in Python, instructing Neovim to locate and use Lua scripts.
   ```lua
   require('config.lazy')
   ```
4. **Edit Lazy.lua:** Open the `lazy.lua` file in your favorite text editor and add a print statement for testing purposes.
   ```lua
   print("This is getting required")
   ```

   When you start Neovim, you should see "This is getting required" printed to confirm that your Lua file is being loaded correctly.

#### Step 2: Setting Up Lazy.nvim with Bootstrap Code

Now that we have our Lua file ready, it's time to bootstrap Lazy.nvim by adding necessary configuration code.

1. **Locate the Lazy.nvim Path:** Neovim needs to know where to find the Lazy.nvim repository. You can do this with a few lines of code in your `lazy.lua` file:
   ```lua
   local lazypath = vim.fn.stdpath('data') .. '/lazy/lazy.nvim'
   if not vim.loop.fs_stat(lazypath) then
       vim.fn.system({'git', 'clone', 'https://github.com/folke/lazy.nvim', lazypath})
   end
   vim.opt.rtp:prepend(lazypath)
   ```

   This snippet:

   - **Checks if Lazy.nvim Exists:** Uses `vim.fn.stdpath('data')` to define the path where Lazy.nvim should reside. If it doesn’t exist, it clones the Lazy.nvim repository.
   - **Prepends Lazy.nvim to Runtime Path:** This tells Neovim to load Lazy.nvim by adding it to the runtime paths (`vim.opt.rtp`).

#### Step 3: Verifying Lazy.nvim Installation

To verify if Lazy.nvim has been installed correctly, you can use the command `:checkhealth lazy` in Neovim. This will provide feedback on whether the installation is successful, versions of dependencies, and possible issues.

#### Step 4: Installing a Plugin (Tokyonight Color Scheme)

With Lazy.nvim set up, you can start adding plugins. For example, let's install the popular "Tokyonight" color scheme plugin:

1. **Edit lazy.lua:** Add the following lines to specify that Tokyonight is a plugin that you want Lazy.nvim to install.
   ```lua
   require('lazy').setup({
       {
           'folke/tokyonight.nvim',
           config = function()
               vim.cmd('colorscheme tokyonight')
           end
       }
   })
   ```
   - This code tells Neovim to **clone the Tokyonight GitHub repository** and **apply the color scheme** when the plugin loads.
2. **Test Installation:** Open Neovim, and you should see that the colorscheme changes to Tokyonight if installed correctly. This means Lazy.nvim has successfully pulled the plugin and made it available to Neovim.

#### Step 5: Adding Advanced Plugins (Mini.nvim Example)

Next, let’s add a more advanced plugin, "Mini.nvim," which offers multiple mini-features for Neovim. In this example, we’ll add a status line using Mini.nvim.

1. **Directory Setup:** We’ll create a new directory to keep our plugin configurations organized. Run:
   ```sh
   mkdir ~/.config/nvim/lua/config/plugins
   touch ~/.config/nvim/lua/config/plugins/mini.lua
   ```
2. **Define Plugin Configurations:** Open `mini.lua` and add the following code to configure the status line plugin:
   ```lua
   return {
       'echasnovski/mini.nvim',
       config = function()
           require('mini.statusline').setup()
       end
   }
   ```
3. **Update lazy.lua to Include Mini.nvim:** Modify `lazy.lua` to look for plugin configurations inside the `plugins` directory.
   ```lua
   require('lazy').setup({
       { import = 'config.plugins' }
   })
   ```
   - This tells Lazy.nvim to import and load plugins from the `config/plugins` directory, allowing you to manage multiple plugin configurations more efficiently.
4. **Restart Neovim:** Now, when you start Neovim, Mini.nvim will be loaded, and the status line will reflect the new, enhanced configuration.

#### Additional Tips for Using Lazy.nvim

- **Disabling Plugins:** You can easily disable a plugin by adding `enabled = false` within its configuration block. For example:
  ```lua
  { 'folke/tokyonight.nvim', enabled = false }
  ```

  This is helpful when debugging issues caused by a plugin.

- **Avoid Over-Optimization:** Especially for beginners, don’t get overly focused on optimizing Neovim’s startup time by disabling everything. Instead, focus on learning how plugins work, exploring the basic concepts, and gradually tweaking your setup.
- **Separate Files for Configurations:** As your setup grows, create separate configuration files for each plugin or plugin category. This keeps your setup modular and easier to maintain.

#### Conclusion

Congratulations! You've successfully installed Lazy.nvim and used it to configure plugins for Neovim, such as Tokyonight and Mini.nvim. Understanding how runtime paths work, the importance of the `require` function, and Lazy.nvim’s setup functions will make your Neovim customization much more efficient and structured. With this setup, you're ready to explore more plugins, create your own configurations, and make Neovim truly yours.

Remember, the key to managing plugins effectively is to start small, understand the basics, and scale up as you get more comfortable. Don't worry too much about making Neovim load in milliseconds—focus instead on writing code, learning, and enjoying the power of Neovim!

[[Neovim]]