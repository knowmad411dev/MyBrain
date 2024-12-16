---
Video-URL: https://www.youtube.com/watch?v=ehjZUeTM7iE&list=WL&index=2
tags:
- obsidian
- github
---

## **Obsidian Git Plugin

**Detailed Summary: Setting Up the Obsidian Git Plugin for Automatic Vault Backups**

In the provided text, Mike walks through the process of installing and configuring the **Obsidian Git plugin** to automate the backup and synchronization of an Obsidian Vault using a remote Git repository. Below is a comprehensive summary that includes relevant links, step-by-step instructions, and example code snippets to help you replicate the setup.

---

## **1. Introduction to Obsidian Git Plugin**

**Obsidian Git Plugin** is a community plugin for Obsidian that leverages Git to manage backups and synchronization of your Vault. Key features include:

- **Automatic Backups:** Automatically commits changes at set intervals.
- **Remote Repository Syncing:** Pushes and pulls changes to/from a remote Git repository, ensuring your Vault is synchronized across multiple devices.
- **History View:** Provides a history log similar to `git log` for tracking changes.

**Limitations:**

- **Mobile Support:** The plugin is not well-suited for mobile versions of Obsidian.

**Useful Links:**

- [Obsidian Git Plugin GitHub Repository](https://github.com/denolehov/obsidian-git)
- [Obsidian Official Website](https://obsidian.md/)
- [GitHub](https://github.com/)
- [Download Git](https://git-scm.com/downloads)

---

## **2. Installation and Configuration**

### **a. Prerequisites**

Before setting up the Obsidian Git plugin, ensure you have the following:

1. **Obsidian Application:** Installed on your computer. [Download Obsidian](https://obsidian.md/)
2. **Git:** Installed on your system. [Download Git](https://git-scm.com/downloads)
3. **GitHub Account:** To host your remote repository. [Sign Up for GitHub](https://github.com/join)

### **b. Installing the Obsidian Git Plugin**

1. **Open Obsidian:**
    - Launch the Obsidian application on your computer.
2. **Access Community Plugins:**
    - Go to **Settings** > **Community Plugins**.
3. **Disable Safe Mode:**
    - If **Safe Mode** is enabled, disable it to allow the installation of third-party plugins.
4. **Browse and Install:**
    - Click on **Browse**.
    - Search for **Obsidian Git**.
    - Click **Install** next to the Obsidian Git plugin.
    - After installation, click **Enable** to activate the plugin.

### **c. Configuring the Obsidian [[Git]] Plugin**

1. **Open Plugin Settings:**
    - Navigate to **Settings** > **Community Plugins** > **Obsidian Git**.
2. **Set Backup Interval:**
    - Locate the **Backup Interval** setting and set it to `60` minutes (or your preferred interval).
3. **Set Author Details:**
    - Fill in the **Author Name** and **Author Email** fields. These details will be used in your Git commits.

        ```
```plaintext
        Author Name: Your Name Author Email: your.email@example.com
```

4. **Initialize Git Repository:**
    - In the plugin settings, click on **Initialize a New Repo**. This action sets up a local Git repository within your Obsidian Vault.

### **d. Setting Up the Remote GitHub Repository**

1. **Create a New Repository on GitHub:**
    - Go to [GitHub](https://github.com/) and log in to your account.
    - Click on the **+** icon in the top right corner and select **New repository**.
    - **Repository Name:** Enter a name for your repository (e.g., `BasVault`).
    - **Privacy:** Set the repository to **Private**.
    - Click **Create repository**.
2. **Copy Repository URL:**
    - After creating the repository, copy the repository URL provided by GitHub (e.g., `https://github.com/yourusername/BasVault.git`).

### **e. Linking Local Repository to GitHub**

1. **Open Terminal/Command Line:**
    - Navigate to your Obsidian Vault directory.

```bash
        cd path/to/your/Obsidian/Vault
```

2. **Initialize Git (if not already initialized):**
    - If you haven't initialized Git through the plugin, do so manually:

```bash
        git init
```

3. **Add All Files to Git:**
    - Stage all files for commit.

```bash
        git add .
```

4. **Commit Changes:**
    - Commit the staged files with a message.

```bash
        git commit -m "Initial commit"
```

5. **Add Remote Origin:**
    - Link your local repository to the GitHub repository.

```  bash
        git remote add origin https://github.com/yourusername/BasVault.git
```

6. **Push to GitHub:**
    - Push your local commits to the remote repository.

```bash
        git push -u origin master
```

### **f. Automating Sync with Obsidian Git Plugin**

1. **Automatic Pull on Startup:**
    - The Obsidian Git plugin is configured to pull changes from the remote repository whenever Obsidian starts. This ensures that your Vault is up-to-date across all devices.
2. **Automatic Commit and Push:**
    - Based on the backup interval set (e.g., every 60 minutes), the plugin automatically commits any changes and pushes them to the remote repository.
3. **Testing Sync:**
    - Make a change in your Vault (e.g., add a sentence to a note).
    - Wait for the backup interval to elapse or manually trigger a sync.
    - Verify that the changes appear in your GitHub repository.

**Example Commit Output:**

```plaintext
Committed 1,389 files
```

**Pushing Changes:**

```plaintext
Committed 2 files Pushed to remote repository
```

### **g. Viewing Commit History**

- The plugin provides a **History View** similar to `git log`, allowing you to track changes over time.
- Access this view through the Obsidian Git plugin interface to see commit messages and file changes.

---

## **3. Enhancements and Recommendations**

- **User Experience Improvements:**
    - Mike suggests adding a checklist or to-do section within the plugin to guide new users through the setup process.
    - Enhanced documentation and intuitive prompts could make the plugin more accessible to those unfamiliar with Git.
- **Target Audience:**
    - The plugin currently seems geared towards users with some Git experience. Beginners might find the setup process challenging without additional guidance.
- **Testing Backup Intervals:**
    - Mike set the backup interval to `1` minute for testing purposes but recommends using a longer interval (e.g., `60` minutes) for regular use.

---

## **4. Example Git Commands Used**

For reference, here are the Git commands Mike utilized during the setup process:

```bash
# Navigate to your Obsidian Vault directory 
cd path/to/your/Obsidian/Vault  
# Initialize a new Git repository 
git init  
# Add all files to the staging area 
git add .  
# Commit the staged files with a message 
git commit -m "Initial commit"  
# Add the remote GitHub repository 
git remote add origin https://github.com/yourusername/BasVault.git  
# Push the local commits to the remote repository 
git push -u origin master`
```

---

## **5. Supporting Resources**

- **Obsidian Git Plugin Documentation:** [GitHub - denolehov/obsidian-git](https://github.com/denolehov/obsidian-git)
- **Obsidian Community Forum:** Obsidian Forum

---

## **6. Conclusion**

The Obsidian Git plugin offers a powerful solution for backing up and synchronizing your Obsidian Vault using Git and GitHub. While the setup process requires some familiarity with Git, following the above steps can help streamline the process. Automating backups ensures that your notes are securely stored and accessible across multiple devices, enhancing your productivity and safeguarding your data.

[[Obsidian]]  [[GitHub]]  [[Git]]
