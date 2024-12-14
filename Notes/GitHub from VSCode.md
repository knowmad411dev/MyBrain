---
Video-URL: https://www.youtube.com/watch?v=WBE8XTTyH6g&list=WL&index=2
tags:
- github
---

# GitHub from VSCode

The video provides a step-by-step guide on how to download or clone a GitHub repository and open it in Visual Studio Code (VS Code). The creator offers two methods: one for users with `git` installed and one for those without it. Here's a detailed summary with instructions:

## Method 1: Cloning the Repository Using Git

### 1. Ensure Git is Installed

- If you haven't installed `git`, refer to a link (provided in the video's description) for installation instructions.

### 2. Find and Copy the Correct GitHub Repository URL

- Navigate to the GitHub page of the desired repository.
- Make sure the URL follows the format: `https://github.com/<username>/<repository-name>`.
    - **Correct URL Example**: `https://github.com/user/project`
    - **Incorrect URL Example**: `https://github.com/user/project/tree/main/README.md` (avoid URLs with extra paths).
- Click on the **"Code"** button, and copy the repository's URL.

### 3. Clone the Repository Using Git Bash

- Go to the directory where you want to clone the repository.
- **Tip**: No need to create a new folder for the project; it will be created automatically during cloning.
- Hold **Shift + Right-click** in the desired directory, and choose **"Open Git Bash here"**.
- Run the following command:

    ```bash
    git clone <repository-url>
    ```

    - Replace `<repository-url>` with the URL you copied from GitHub.
- Git will clone the repository, and you will see a message confirming the cloning process (e.g., `Cloning into 'repository-name'...`).

### 4. Verify Cloning

- Navigate into the cloned repository folder. You should see all files from the GitHub repository.

## Method 2: Downloading the Repository Without Git

### 1. Download the Repository as a ZIP File

- If you don't have `git` installed, click on the **"Code"** button on the GitHub repository page.
- Select **"Download ZIP"**. This will download the entire repository as a `.zip` file.

### 2. Extract the Downloaded ZIP File

- Go to the location where the `.zip` file was downloaded.
- Right-click the `.zip` file and select **"Extract All..."**.
- **Note**: If you extract without specifying the folder, it will create nested folders (one inside another).
    - To avoid this, copy all files inside the extracted main folder and paste them into a preferred directory.

#### Example Steps for Extraction

- If nested folders are created:

    1. Navigate to the innermost folder.
    2. Select all contents with **Ctrl + A**.
    3. Cut the contents with **Ctrl + X**.
    4. Paste them into the desired directory with **Ctrl + V**.

- Delete any empty folders left behind after moving the contents.

## Opening the Project in Visual Studio Code

### 1. Launch VS Code

- Press the **Windows** key, type "Visual Studio Code," and open the application.

### 2. Open the Cloned/Extracted Folder in VS Code

- In VS Code, click on **"File"** > **"Open Folder..."**.
- Navigate to the directory where the project folder is located.
- Select the project folder and click **"Select Folder"**.

### 3. Trust the Authors (Optional)

- When prompted, choose whether to trust the authors of the code.
    - You can either click **"No, I don't trust the authors"** or **"Trust the authors"** depending on your preference.

### 4. Run the Project

- To run the project, click on **"Run"** in the menu.
- Select **"Run Without Debugging"**.
- Choose the browser in which you want to open the project (e.g., Chrome).

### 5. View the Project in Your Browser

- Once run, the project's `index.html` or main file will open in the selected browser, displaying the content.

## Summary

- **If you have** `**git**` **installed**: Clone the repository using `git clone <repository-url>`.
- **If you don't have** `**git**` **installed**: Download the repository as a ZIP file, extract it, and open it in VS Code.
- Use **VS Code** to open and run the project in your preferred browser.

[[GitHub]]  [[VSCode]]  [[Git]]   [[GitHub Project Download & Run]]

[[Obsidian Publish Sync with GitHub]]  [[Python]]
