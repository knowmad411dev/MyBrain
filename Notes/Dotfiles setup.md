---
github_link: https://github.com/logandonley/dotfiles
tags:
- editors
- github
url: https://www.chezmoi.io/
video-url: https://www.youtube.com/watch?v=-RkANM9FfTM&list=WL&index=2
---
## **Dotfiles setup

# Comprehensive Guide to Managing Applications and Configurations Across Devices Using Shamwa and Ansible

## Overview

This guide provides a detailed walkthrough on setting up a system to manage your application configurations and installed software across multiple machines. Using **Shamwa** (a dotfile manager) and **Ansible** (a configuration management tool), you can bootstrap new machines and ensure synchronization across devices efficiently.

---

## Setup Overview

1. **Dotfiles Management**: Shamwa handles configuration files and scripts.
2. **Application Management**: Ansible installs and configures applications.
3. **Synchronization**: Ensure consistent environments across devices.

---

## Prerequisites

- **GitHub Repository**: A repository to store dotfiles and configurations.
- **Basic Tools Installed**: Git and a terminal environment.

---

## Step-by-Step Instructions

### 1. Initialize Shamwa

1. **Clone Dotfiles Repository**:
    ```bash
    git clone <your-dotfiles-repo>
    cd <your-dotfiles-repo>
    ```

2. **Install Shamwa**:
    Shamwa simplifies managing and syncing dotfiles. Install Shamwa by following its [official documentation](https://shamwa.readthedocs.io) or use:
    ```bash
    curl -sL https://shamwa.install | bash
    ```

3. **Set GitHub Username**:
    ```bash
    export SHAMWA_USER=<your-github-username>
    ```

4. **Run Shamwa Setup Command**:
    ```bash
    shamwa
    ```

    This command:

    - Copies your configuration files.
    - Installs pre-defined applications.
    - Runs any scripts you’ve specified.

### 2. Manage Dotfiles with Shamwa

- **Add Files or Directories**:
    ```bash
    shamwa add <file-or-directory>
    ```

- **Check for Changes**:
    ```bash
    shamwa diff
    ```

- **Apply Changes**:
    ```bash
    shamwa apply
    ```

- **Edit Files**:
    ```bash
    shamwa edit <file>
    ```

- **View Shamwa Directory**:
    ```bash
    shamwa cd
    ```

### 3. Automate with Ansible

Ansible manages application installations and configurations.

1. **Install Ansible**:
    ```bash
    sudo apt install ansible  # For Ubuntu
    brew install ansible      # For macOS
    ```

2. **Create an Ansible Playbook**:
    Example YAML file:
    ```yaml
    ---
    - name: Setup applications and configurations
      hosts: localhost
      tasks:
        - name: Install packages
          apt:
            name:
              - git
              - vim
              - neovim
              - brave-browser
              - python3
            state: present

        - name: Install fonts
          ansible.builtin.shell: "fc-cache -fv"

        - name: Change default shell
          ansible.builtin.shell: "chsh -s $(which zsh)"

        - name: Install flatpak applications
          ansible.builtin.shell: |
            flatpak install -y flathub com.brave.Browser
    ```

3. **Run the Playbook**:
    ```bash
    ansible-playbook <playbook-file>.yaml
    ```

4. **Update Applications**:
    Modify the YAML file to add or remove applications and re-run the playbook.

### 4. Synchronize Changes

- **Push Changes to GitHub**:
    ```bash
    git add .
    git commit -m "Update configurations"
    git push origin main
    ```

- **Pull Changes on Another Machine**:
    ```bash
    shamwa update
    ```

---

## Advanced Features

### Run Once Scripts

- Scripts executed only during the first setup.
- Example: Initialize Oh-My-Zsh if not already installed.
    ```bash
    if [ ! -d "$HOME/.oh-my-zsh" ]; then
      sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    fi
    ```

### Detect Changes Automatically

- Shamwa monitors configuration changes using hashes.
- When a change is detected:
    - It applies updated scripts.
    - Ensures consistent state across machines.

### Debugging and Logs

- Use `shamwa diff` to check differences.
- Verify application installations by reviewing Ansible logs.

---

## Example Workflow

1. **Add a New Configuration File**:
    ```bash
    shamwa add ~/.config/myapp/config.json
    ```

2. **Push Changes**:
    ```bash
    git add .
    git commit -m "Add config for myapp"
    git push origin main
    ```

3. **Pull and Update on Another Device**:
    ```bash
    shamwa update
    ```

4. **Verify Changes**:
    ```bash
    ls ~/.config/myapp
    ```

---

## Benefits

- **Consistency**: Maintain the same environment across multiple devices.
- **Scalability**: Add or modify configurations easily.
- **Efficiency**: Bootstrap new machines in minutes.

---

This setup streamlines managing configurations and applications. With Shamwa and Ansible, you can ensure that your environments are always synchronized and ready for use.

[[Code Editor]]   [[Git]]  