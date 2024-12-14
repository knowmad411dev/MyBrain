---
tags:
- vscode
- editors
- automation
video-url: https://www.youtube.com/watch?v=xbaVJbstDPs&list=WL&index=2
---
## **Developer Workflow With Tmux, Vim, and VSCode

**Detailed Overview of Workflow, How-to Instructions, and Code Examples**

---

### **Introduction**

The content describes a comprehensive development workflow, emphasizing tool usage and preferences. It begins with a critique of IntelliJ GoLand, transitions to workflow optimization, and concludes with a comparison of Neovim, VS Code, and GoLand.

---

### **Virtual Desktop Organization**

- **Setup**:
  - Each primary application resides in a dedicated virtual desktop.
  - Example desktop layout:
    - Desktop 1: Slack
    - Desktop 2: ARC browser
    - Desktop 3: Alacritty terminal
    - Desktop 4: VS Code
    - Desktop 5: Obsidian
- **Shortcut Assignments**:
  - Jump between desktops using shortcuts configured through Raycast.
  - Example shortcut mappings:
    - Alacritty: `Hyper Key + D`
    - ARC: `Hyper Key + S`
    - Obsidian: `Hyper Key + G`
- **Hyper Key Configuration**:
  - Hyper Key = Combination of `Control + Alt + Shift + Command`.
  - Configured using **Karabiner Elements** on macOS.
  - Example Configuration:
    ```json
    {
      "from": {
        "key_code": "right_command"
      },
      "to": [
        {
          "key_code": "right_command",
          "modifiers": ["control", "option", "command", "shift"]
        }
      ],
      "type": "basic"
    }
    ```

---

### **Terminal Workflow with Alacritty and Tmux**

- **Alacritty**:
  - Preferred terminal emulator for speed and rendering.
- **Tmux for Multiplexing**:
  - **Basics**:
    - Tmux allows multiple terminal sessions within a single window.
    - Commands:
      - Start session: `tmux`
      - Split panes:
        - Horizontal: `Ctrl-B %`
        - Vertical: `Ctrl-B "`
      - Resize panes: `Ctrl-B <Arrow Keys>`
      - Detach session: `Ctrl-B d`
      - List sessions: `tmux ls`
      - Attach session: `tmux attach-session -t <name>`

  - **Use Case**:
    - Upper pane: `k9s` for cluster monitoring.
    - Lower pane: Logs and deployments.
    - Example:
      ```bash
      # Monitor pods
      k9s

      # Deploy cluster
      kubectl apply -f deployment.yaml

      # Monitor logs
      kubectl logs -f pod-name
      ```

- **fzf Integration**:
  - Search through command history:
    ```bash
    history | fzf
    ```

---

### **Editor Workflow**

#### **Neovim with AstroVim**

- **Configuration**:
  - Based on AstroVim distribution.
  - Plugins added as needed.
- **Capabilities**:
  - Jump to definitions and references.
  - Search files:
    ```vim
    :Telescope find_files
    ```

#### **VS Code**

- **Why VS Code?**
  - Modern UI/UX with smooth scrolling.
  - Stable and rarely breaks after updates.
  - Extensive plugin ecosystem.
- **Vim Integration**:
  - VS Code’s Vim plugin provides essential Vim motions.
- **File Management**:
  - Add file: `A`
  - Delete file: `D`
  - Rename file: `R`
- **Code Navigation**:
  - Jump to definitions and references.
  - Search symbols within a file.
- **Git Integration**:
  - Inline Git blame.
  - Open file in GitHub:
    ```bash
    code --goto file:line
    ```

#### **Comparison with IntelliJ GoLand**

- **Disadvantages of GoLand**:
  - Heavier resource usage.
  - Less customizable shortcuts.
  - Fewer plugins compared to VS Code and Neovim.
  - Paid license (~$150/year).

---

### **Conclusion**

The discussed workflow emphasizes efficiency, lightweight tools, and effective shortcuts. While IntelliJ GoLand offers features tailored to Go development, the author’s preference for VS Code and Neovim stems from configurability, plugin support, and overall usability.

[[VSCode]]  [[Obsidian]]  [[Code Editor]]