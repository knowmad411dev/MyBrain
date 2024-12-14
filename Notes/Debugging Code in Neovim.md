---
github_link: https://github.com/mfussenegger/nvim-dap
tags:
- editors
video-url: https://www.youtube.com/watch?v=djpMB9LPkBc&list=WL&index=3
---
## **Debugging Code in Neovim

### Overview of Debugging Setup in Neovim

The content focuses on using **Neovim (commonly abbreviated as "neim" or "nevim")** as a primary code editor to set up remote debugging using **DAP (Debug Adapter Protocol)** and plugins. Specifically, it uses **Packer** as a plugin manager, **Rust** as a demo language, and the debugging setup is centered around tools like **nvim-dap** and **nvim-dap-ui**.

### Requirements and Tools

- **Neovim version**: 0.10 or similar
- **Plugin Manager**: [Packer](https://github.com/wbthomason/packer.nvim)
- **Programming Language**: Rust (but the setup is compatible with other languages as well)
- **Debugging Plugin**: [nvim-dap](https://github.com/mfussenegger/nvim-dap)
- **UI Plugin**: [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui)
- **Packer Configuration**: Used to install, configure, and manage plugins.

### Step-by-Step How-To Instructions

#### 1. Install Plugin Manager (Packer)

If you haven't installed Packer yet, here are the steps:

1. **Install Packer**:
   ```sh
   git clone --depth 1 https://github.com/wbthomason/packer.nvim \
   ~/.local/share/nvim/site/pack/packer/start/packer.nvim
   ```
2. **Add Packer Configuration in `init.lua` or `init.vim`**:
   ```lua
   require('packer').startup(function(use)
       use 'wbthomason/packer.nvim' -- Packer can manage itself
       -- Add plugins here
   end)
   ```

#### 2. Install and Configure `nvim-dap`

Add `nvim-dap` to your Packer configuration:

```lua
require('packer').startup(function(use)
    use 'wbthomason/packer.nvim' -- Packer can manage itself

    -- Debug Adapter Protocol plugin for Neovim
    use 'mfussenegger/nvim-dap'
    use 'rcarriga/nvim-dap-ui'   -- UI for nvim-dap
end)
```

**Installing Plugins**: After saving the changes in your configuration file, run:

```vim
:PackerSync
```

This will install all the plugins added to your `Packer` configuration.

#### 3. Set Up Debug Adapter Protocol for Rust

1. **Install Debugger Adapter for Rust**:
   - Download the VS Code C++ tools extension that includes debugging tools for Rust.
   - Extract the `.vsix` file, which is available in the [C++ Extension GitHub page](https://github.com/microsoft/vscode-cpptools).

2. **Configure `nvim-dap`**:
   - Add the debugger in your Lua configuration file:

   ```lua
   local dap = require('dap')

   dap.adapters.cppdbg = {
       id = 'cppdbg',
       type = 'executable',
       command = '/path/to/vscode-cpptools/extension/debugAdapters/bin/OpenDebugAD7', -- Change this path
       name = 'cppdbg',
   }

   dap.configurations.rust = {
       {
           name = "Launch",
           type = "cppdbg",
           request = "launch",
           program = function()
               return vim.fn.input('Path to executable: ', vim.fn.getcwd() .. '/', 'file')
           end,
           cwd = '${workspaceFolder}',
           stopOnEntry = false,
           setupCommands = {
               {
                   text = '-enable-pretty-printing',
                   description = 'enable pretty printing',
                   ignoreFailures = false
               },
           },
       },
   }
   ```

3. **Add Key Mappings** for Common Debugging Actions:

   Add mappings to make debugging easier, like setting breakpoints, starting/stopping debugging, and stepping through the code:

   ```lua
   local dap = require('dap')
   vim.keymap.set('n', '<F5>', dap.continue, { noremap = true, silent = true })
   vim.keymap.set('n', '<F9>', dap.toggle_breakpoint, { noremap = true, silent = true })
   vim.keymap.set('n', '<F10>', dap.step_over, { noremap = true, silent = true })
   vim.keymap.set('n', '<F11>', dap.step_into, { noremap = true, silent = true })
   vim.keymap.set('n', '<F12>', dap.step_out, { noremap = true, silent = true })
   ```

#### 4. Integrate `nvim-dap-ui`

The plugin **nvim-dap-ui** adds an easy-to-use interface for `nvim-dap` to display variable values, stack frames, etc.

**Configure nvim-dap-ui**:

```lua
local dap, dapui = require("dap"), require("dapui")
dapui.setup() -- Uses default settings

dap.listeners.after.event_initialized["dapui_config"] = function()
  dapui.open()
end
dap.listeners.before.event_terminated["dapui_config"] = function()
  dapui.close()
end
dap.listeners.before.event_exited["dapui_config"] = function()
  dapui.close()
end
```

#### 5. Setup Project-Specific Debugging Configuration

To avoid retyping the file path each time for project debugging, create a project-specific configuration using `nvim-dap-projects` (or similar customization).

1. **Use a Project-Specific Config**:
   - Add a configuration Lua script inside your project:

   ```lua
   local dap = require('dap')
   dap.configurations.rust = {
       {
           name = "Launch Project Specific Binary",
           type = "cppdbg",
           request = "launch",
           program = function()
               return "target/debug/my_project_binary" -- Replace with your specific path
           end,
           cwd = '${workspaceFolder}',
           stopOnEntry = false,
       },
   }
   ```

2. This script ensures project-specific paths are configured without manually adding them each time.

#### 6. Add Key Mappings for UI Features and Visual Enhancements

1. **Toggle Debug UI**:
   - Add a key mapping to toggle the UI for nvim-dap:

   ```lua
   vim.keymap.set('n', '<leader>du', require('dapui').toggle, { noremap = true, silent = true })
   ```

2. **Add Visual Cues for Breakpoints**:
   - Update the breakpoint symbol with a Unicode character to make it visually appealing:

   ```lua
   vim.fn.sign_define('DapBreakpoint', {text='🔴', texthl='', linehl='', numhl=''})
   ```

3. This configuration will replace the default "B" sign for breakpoints with a red dot.

### Debugging Workflow Summary

1. **Set a Breakpoint**:
   - Press `F9` to toggle a breakpoint on the current line.

2. **Start Debugging**:
   - Press `F5` to start the debugging session.
   - Select the binary file when prompted or use preconfigured project-specific options.

3. **Step Through Code**:
   - Use `F10` to step over functions or `F11` to step into functions.

4. **View Variable Values**:
   - Press `<leader>du` to toggle the nvim-dap-ui panel and view the values of variables, registers, etc.

### GitHub Links and Useful References

1. **Packer** - [Packer Plugin Manager](https://github.com/wbthomason/packer.nvim)
2. **nvim-dap** - [nvim-dap GitHub Repository](https://github.com/mfussenegger/nvim-dap)
3. **nvim-dap-ui** - [nvim-dap-ui GitHub Repository](https://github.com/rcarriga/nvim-dap-ui)
4. **VS Code C++ Extension for Debugger** - [VS Code C++ Tools](https://github.com/microsoft/vscode-cpptools)

### Additional Improvements

- **Automatically Launch UI**: Modify the key mappings to open `dap-ui` when starting debugging.
- **Project Configuration Consistency**: Submit a pull request to improve how configurations inherit adapter settings, making sharing configs easier among team members.

### Conclusion

The setup of Neovim for debugging with `nvim-dap` and `nvim-dap-ui` is versatile and provides functionality similar to what you would expect from mainstream IDEs. By integrating these plugins, you can effectively debug languages like Rust and use features such as visual debugging cues, remote debugging, and customizable key mappings to enhance productivity. The provided GitHub links and plugin references can further guide you through configuring this setup for your specific needs.

If you are looking for further customization or want to extend the debugging features, check out the respective GitHub documentation linked above for detailed guides and more advanced configurations.

[[VSCode to Neovim]]  [[Neovim]]