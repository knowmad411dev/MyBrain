---
Video-URL: https://www.youtube.com/watch?v=qbimJu-ej3Q&list=WL&index=2
tags:
- github
- obsidian
---

## **Obsidian Sync with [[GitHub]]

### **Synchronizing Obsidian with GitHub: A Comprehensive Guide**

In this guide, we'll walk you through the process of synchronizing your Obsidian vault with GitHub. This setup ensures that your notes are version-controlled and backed up in a remote repository. Whether you're a beginner or looking to refine your workflow, this step-by-step tutorial covers everything from repository creation to integrating Obsidian with GitHub using the Obsidian Git plugin.

---

#### **Table of Contents**

1. [Prerequisites](#prerequisites)
2. [Step 1: Create a GitHub Repository](#step-1-create-a-github-repository)
3. [Step 2: Install Git on Your Computer](#step-2-install-git-on-your-computer)
4. [Step 3: Generate a Personal Access Token on GitHub](#step-3-generate-a-personal-access-token-on-github)
5. [Step 4: Install the Obsidian Git Community Plugin](#step-4-install-the-obsidian-git-community-plugin)
6. [Step 5: Clone the Repository to Your Local Machine](#step-5-clone-the-repository-to-your-local-machine)
7. [Step 6: Configure the Obsidian Git Plugin](#step-6-configure-the-obsidian-git-plugin)
8. [Step 7: Synchronize Your Notes](#step-7-synchronize-your-notes)
9. [Additional Resources](#additional-resources)
10. [Support the Channel](#support-the-channel)

---

### **Prerequisites**

- **Obsidian**: Ensure you have Obsidian installed. Download Obsidian
- **Git**: Install Git on your computer. [Download Git](https://git-scm.com/downloads)
- **GitHub Account**: If you don't have one, [sign up for GitHub](https://github.com/join).
- **Basic Git Knowledge**: Familiarity with Git commands is beneficial.

---

### **Step 1: Create a GitHub Repository**

1. **Log in to GitHub**: Navigate to [GitHub](https://github.com/) and log in to your account.
2. **Create a New Repository**:

    - Click the **"+"** icon in the top-right corner and select **"New repository"**.
    - **Repository Name**: Choose a name for your repository, e.g., `my-obsidian-vault`.
    - **Description** (Optional): Add a description like "Obsidian Vault Sync".
    - **Public/Private**: Decide if you want the repository to be public or private.
    - **Initialize Repository**: You can add a README or leave it empty.
    - Click **"Create repository"**.

    _Example Repository:_ [your-username/my-obsidian-vault](https://github.com/your-username/my-obsidian-vault)

---

### **Step 2: Install Git on Your Computer**

If you haven't installed Git yet:

1. **Download Git**: Visit [Git Downloads](https://git-scm.com/downloads) and choose the appropriate installer for your operating system.
2. **Install Git**: Follow the installation prompts. Default settings are generally sufficient.
3. **Verify Installation**:
    - Open your terminal or command prompt.
    - Run:

```bash
        git --version
```

        You should see the installed Git version.

---

### **Step 3: Generate a Personal Access Token on GitHub**

GitHub requires a personal access token (PAT) for authentication instead of a password.

1. **Navigate to Settings**:

    - Click on your profile picture in the top-right corner.
    - Select **"Settings"**.
2. **Access Developer Settings**:

    - On the left sidebar, click **"Developer settings"**.
3. **Personal Access Tokens**:

    - Click **"Personal access tokens"**.
    - Select **"Tokens (classic)"**.
    - Click **"Generate new token"**.
4. **Configure the Token**:

    - **Note**: Add a descriptive name, e.g., `Obsidian Sync Token`.
    - **Expiration**: Set to **"No expiration"** for continuous access.
    - **Scopes**: Check **`repo`** to grant full control of private repositories.
5. **Generate and Save the Token**:

    - Click **"Generate token"**.
    - **Important**: Copy the token immediately. You won't be able to view it again.

---

### **Step 4: Install the Obsidian Git Community Plugin**

1. **Open Obsidian**.
2. **Access Community Plugins**:

    - Click on the **"Settings"** gear icon.
    - Navigate to **"Community plugins"**.
    - Toggle **"Safe mode"** off to allow third-party plugins.
3. **Browse and Install**:

    - Click **"Browse"** and search for **"Obsidian Git"**.
    - Select **"Obsidian Git"** by **"Granitelt"** and click **"Install"**.
4. **Enable the Plugin**:

    - After installation, click **"Enable"**.

---

### **Step 5: Clone the Repository to Your Local Machine**

1. **Create a Folder for the Repository**:
    - Decide where you want to store your repository locally, e.g., `~/Documents/ObsidianVault`.
2. **Open Terminal/Command Prompt**:
    - Navigate to the desired parent directory:

```bash
        cd ~/Documents
```

    - Clone the repository using the URL from GitHub. Replace `your-username` and `my-obsidian-vault` accordingly:

```bash
        git clone https://github.com/your-username/my-obsidian-vault.git ObsidianVault
```

        _Alternatively, using SSH:_

``` bas
        git clone git@github.com:your-username/my-obsidian-vault.git ObsidianVault
```

3. **Verify Cloning**:
    - Navigate to the cloned folder:

```bash
        cd ObsidianVault
```

    - List files to ensure the repository has been cloned:

```bash
        ls
```

---

### **Step 6: Configure the Obsidian Git Plugin**

1. **Open Your Obsidian Vault**:
    - In Obsidian, click **"Open another vault"** and select the cloned repository folder (`ObsidianVault`).
2. **Access Plugin Settings**:
    - Go to **"Settings"** > **"Community plugins"** > **"Obsidian Git"**.
3. **Set Up Git Integration**:
    - **Git Executable Path**: Ensure Obsidian can locate Git. Typically, this is set automatically. If not, specify the path manually (e.g., `/usr/bin/git` on Linux or `C:\Program Files\Git\bin\git.exe` on Windows).
    - **Commit Message**: Define a default commit message format, e.g., `Sync notes on {date}`.
    - **Remote URL**: Enter your repository's HTTPS URL (e.g., `https://github.com/your-username/my-obsidian-vault.git`).
4. **Authenticate with GitHub**:
    - When prompted, enter your **Personal Access Token** generated in Step 3 as the password.

---

### **Step 7: Synchronize Your Notes**

1. **Make Edits in Obsidian**:

    - Create or modify your notes as usual within Obsidian.
2. **Create a Backup (Commit and Push)**:

    - Open the **Command Palette**:
        - **Windows/Linux**: Press `Ctrl + P`.
        - **Mac**: Press `Cmd + P`.
    - Type and select **"Git: Commit and Push"** or **"Obsidian Git: Create Backup"**.
    - The plugin will:
        - **Stage Changes**: Add modified files to the staging area.
        - **Commit Changes**: Commit with the predefined message.
        - **Push to GitHub**: Upload the commits to your remote repository.
3. **Verify on GitHub**:

    - Visit your GitHub repository page to ensure the latest changes are reflected.

---

### **Additional Tips**

- **Automate Synchronization**:
    - Configure the Obsidian Git plugin to automatically commit and push changes at set intervals.
- **Pulling Updates**:
    - If you make changes from another device, use **"Git: Pull"** to fetch and merge updates.
- **Conflict Resolution**:
    - Be cautious of merge conflicts. Always ensure only one device edits the vault at a time or handle conflicts manually.

---

### **Sample Code Snippets**

**Cloning a Repository:**

```bash
git clone https://github.com/your-username/my-obsidian-vault.git ObsidianVault
```

**Configuring Remote URL:**

```bash
git remote set-url origin https://github.com/your-username/my-obsidian-vault.git
```

**Committing and Pushing Changes:**

```bash
git add . git commit -m "Sync notes on 2024-04-27" git push origin main
```

---

### **Useful Web Links**

- **Obsidian Git Plugin Repository**: [Obsidian Git on GitHub](https://github.com/denolehov/obsidian-git)
- **Obsidian Community Plugins**: Obsidian Plugins
- **GitHub Personal Access Tokens Documentation**: [Creating a PAT](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- **Git Documentation**: [Git Docs](https://git-scm.com/doc)

---

### **Conclusion**

Synchronizing Obsidian with GitHub not only provides a robust backup solution but also leverages Git's powerful version control features. By following this guide, you can ensure your notes are safely stored and easily accessible across multiple devices. Happy note-taking!

[[Obsidian]]   [[GitHub]]  [[Obsidian Git Plugin]]  [[GitHub from VSCode]]
