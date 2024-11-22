---
tags: [obsidian, GitHub]
---
## Sync Obsidian with GitHub: Step-by-Step Guide

If you're looking to back up your Obsidian notes to GitHub or collaborate on notes using version control, this guide will walk you through all the necessary steps to set up syncing between Obsidian and GitHub.

### 1. Create a Repository on GitHub

- **Log into GitHub:** Go to [GitHub.com](https://github.com) and log into your account. If you don't have one, create an account first.
    
- **Create a Repository:** Click on the **New** button to create a new repository.
    
    - **Repository Name:** Give your repository a name, e.g., "obsidian-notes".
        
    - **Privacy Settings:** You can choose to make the repository **Public** or **Private** depending on your preference.
        
    - **Initialize Repository:** You can leave it empty for now; there’s no need to add a README or other files. Click **Create Repository** to finalize.
        

### 2. Clone the Newly Created Repository to Your Local Machine

- **Install Git:** If you haven't installed Git on your computer, download and install it from [Git SCM](https://git-scm.com/).
    
- **Clone the Repository:** Open a terminal (Command Prompt, PowerShell, or Terminal on Mac/Linux).
    
    - Run the following command to clone your newly created GitHub repository to your local machine:
        
        ```
        git clone https://github.com/your-username/obsidian-notes.git
        ```
        
        Replace `your-username` with your actual GitHub username.
        
- **Navigate to the Cloned Folder:** Once the cloning is complete, navigate to the folder using:
    
    ```
    cd obsidian-notes
    ```
    

### 3. Open Obsidian and Set Up the Vault

- **Open Obsidian:** Launch the Obsidian app on your computer.
    
- **Set Vault Location:** When prompted to open or create a vault, choose **Open Folder as Vault**.
    
    - **Select Cloned Repository Folder:** Navigate to the directory where you cloned your GitHub repository (`obsidian-notes`) and select it. This will make your GitHub repository the vault for Obsidian.
        

### 4. Install the Obsidian Git Plugin

- **Access Community Plugins:** In Obsidian, click on the **Settings** icon (gear icon in the bottom left corner).
    
    - Go to **Community Plugins** and click on **Browse**.
        
- **Search and Install Git Plugin:** Search for "Git" in the community plugins and click on **Install**.
    
- **Enable the Plugin:** Once installed, make sure to click **Enable** to activate the plugin.
    

### 5. Configure the Obsidian Git Plugin

- **Access Git Settings:** In the **Settings** menu, scroll down to find **Obsidian Git** and click on it.
    
- **Set Local Directory Path:** Make sure that the **Local Repository Path** is correctly set to the location of your cloned GitHub repository (`obsidian-notes`).
    
- **Configure Sync Settings:** Here are some key settings to adjust according to your preferences:
    
    - **Auto Pull Interval:** Set how often Obsidian should automatically pull updates from GitHub (e.g., every 30 minutes).
        
    - **Auto Push on Change:** Enable this to automatically push your changes to GitHub whenever a change is detected.
        
    - **Commit Message Template:** Set a default commit message if you prefer to automate your commits.
        

### 6. Test the Syncing Setup

- **Create a Test Note:** In Obsidian, create a new note and add some content.
    
- **Commit and Push Changes:** Click on the **Obsidian Git** icon in the left sidebar (or use the hotkey `Ctrl+P` / `Cmd+P` and type "Git: Commit and Push").
    
    - This will commit your changes and push them to your GitHub repository.
        
- **Verify on GitHub:** Go back to GitHub, navigate to your repository, and confirm that the new note appears there.
    

### 7. Regular Use and Syncing

- **Manual Syncing:** You can manually **pull** or **push** changes from/to GitHub using the Git commands available in the Obsidian Git plugin.
    
- **Conflict Management:** If there are changes made on GitHub while you're also editing locally, the plugin will prompt you to resolve conflicts. Carefully choose which version of the note to keep or merge them as needed.
    

### Tips for Effective Syncing

- **Frequent Commits:** Make small, frequent commits to ensure you don't lose any changes.
    
- **Internet Connection:** Make sure you have an active internet connection when syncing to avoid issues.
    
- **Backup Strategy:** Consider also setting up other backup strategies to avoid data loss.
    

With these steps, you should now have a fully functioning system for syncing Obsidian with GitHub, allowing for seamless backups and version control of your notes.

[[Obsidian]]   [[GitHub]]  
