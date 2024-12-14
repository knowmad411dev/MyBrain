---
tags:
- editors
- agents
video-url: https://www.youtube.com/watch?v=5CmAKm1wWW0&list=WL&index=2
---
## **Claude Agents

The video transcript provided offers a detailed tutorial on how to use **Claude's mCP (Model Context Protocol) Update** to transform Claude (CLA) into a fully-functional API with the ability to run its own servers. Below, I provide an overview along with a step-by-step guide on how to achieve the desired automation with Claude, including the setup process, tools needed, and how to work with mCP for integrating various functionalities.

### Summary

The content outlines how to leverage Claude's new update called mCP (Model Context Protocol). mCP essentially turns Claude into an API, making it easier for it to interact with external tools, apps, and services. The presenter shows how to use Claude to automate tasks, allowing the development of AI-powered agents that can act as full-stack developers. This setup involves steps such as setting up mCP servers, obtaining API keys, and using tools like GitHub and Brave Search. The main components discussed are:

1. Setting up CLA Desktop
2. Configuring mCP Tools
3. Interacting with GitHub and Brave Search through mCP
4. Automating multi-step tasks with a single prompt

### Key Steps and Instructions

#### 1. **Download and Install CLA Desktop**

   - **Link to Download:** Go to CLAI's download page and select either the Mac OS or Windows version, depending on your system.
   - **Installation Steps:**
     - For Mac: Click to download, save the installer, and then move CLA into your Applications folder.
     - After installing, open Finder and navigate to **Applications** to run CLA, or simply search for it on your device.

#### 2. **Create a CLA Account**

   - If you don't already have a CLA account, create one. The video mentions that it’s a quick process and necessary to utilize CLA effectively.

#### 3. **Set Up CLA Configuration**

   - You will need to create a config file to connect CLA to various tools and services:
     1. **Open Terminal:**
        - Depending on your OS:
          - For Mac: Use Terminal.
          - For Windows: Use Command Prompt or PowerShell.
     2. **Create a Configuration File:**
        - Use two commands provided in the video description to create a new config file:
          1. **Open Folder Command**: Use the first command to open the folder where the configuration will be created.
          2. **Create Config File Command**: Use the second command to create a new file named `CLA Desktop config.js`.

   - **Edit Config File:**
     - Open the `config.js` file using a code editor (like VS Code, Notepad, or Cursor).
     - This file will be edited to include mCP server configurations.

#### 4. **Setting Up mCP for Brave Search**

   - To give CLA web search capabilities, you need to configure it with Brave Search:
     1. **Obtain Brave API Key:**
        - Go to the Brave Search API page, sign up or log in, and generate an API key.
        - You must select a subscription tier, even for the free plan. This helps ensure that the API usage doesn’t go beyond acceptable limits.
     2. **Add API Key to Config File:**
        - Copy the API key and paste it into the relevant section of your `config.js` file.

#### 5. **Testing CLA Desktop**

   - After configuring the mCP servers, restart CLA Desktop for changes to take effect.
   - Once restarted, you should see the **mCP tools icon** indicating the mCP servers are active and CLA now has enhanced functionality like Brave Search.

#### 6. **Setting Up GitHub mCP Server**

   - **Adding GitHub Integration:**
     1. Go to the provided GitHub repo for the mCP server configuration.
     2. Copy the provided JSON block and add it to your `config.js` file.
     3. Generate a **GitHub Personal Access Token**:
        - Navigate to your GitHub settings.
        - Create a new token with permissions for repositories and writing packages (but avoid unnecessary permissions like deleting repositories).
     4. **Insert GitHub Token**:
        - Replace the placeholder with your GitHub token in the `config.js` file.
   - Restart CLA Desktop again to apply the changes, allowing GitHub tools to be available via CLA.

#### 7. **Executing Multi-Step Automation with a Single Prompt**

   - Now that CLA is configured with GitHub and Brave Search, you can use a **multi-step prompt** to perform complex tasks. An example prompt shared in the tutorial is:
     ```
     Please do the following:
     - Make a simple HTML page.
     - Create a repo called new Society test.
     - Push the HTML page to the new repo.
     - Add some CSS to the HTML and push the changes.
     - Create an issue suggesting more content.
     - Create a branch called feature, fix the issue, and make a pull request.
     ```
   - CLA, now equipped with the mCP tools, can execute these tasks in sequence, functioning like a full-stack developer:
     1. **Create Repository**: CLA uses GitHub integration to create a repository.
     2. **Add HTML/CSS**: CLA creates the relevant files and commits them.
     3. **Manage Branches and Issues**: CLA can create branches, fix issues, and generate pull requests.

#### 8. **Using Brave Search During Workflow**

   - If CLA needs information not readily available, it can now leverage Brave Search to conduct web searches and gather information in real-time.

#### 9. **Potential Errors and Debugging**

   - During the automation process, there may be errors, such as incorrect arguments when making a pull request. CLA can attempt to correct itself or use Brave Search to find potential solutions.
   - Always monitor the commands being executed, especially if CLA has file system access.

#### 10. **Security Considerations**

   - CLA prompts you to approve actions like accessing files or repositories. This is an important step to prevent unintended changes or security risks, especially if CLA has the ability to modify local files.

#### 11. **Artifact Display Feature**

   - **Artifact Display**: After executing changes, you can use CLA's artifact feature to display a webpage as it would appear once deployed.
   - CLA can integrate multiple files (like HTML and CSS) and preview them, providing a holistic view of the completed project.

### Important Notes

- **Using API Keys Securely**: Treat API keys like passwords. Never share them publicly or commit them to a public repository.
- **Restarting CLA After Changes**: Each time you modify the `config.js` file, you must restart CLA Desktop for the changes to take effect.
- **Security Awareness**: Always verify what CLA is trying to access, especially if it involves file deletion or modification.
- **Multi-Tool Integration**: CLA mCP allows it to function as an AI agent that can manage different aspects of a developer's workflow, including browsing, coding, and committing changes.
- **Productivity Boost**: The video encourages viewers to use AI to boost productivity, emphasizing that those who adopt AI early will have an advantage in many fields.

### Code Examples and Commands Used

1. **Terminal Commands for Creating Configuration Files**:
   - Open a folder:
     ```
     # Command example provided in the video to open folder
     open <folder_path>
     ```
   - Create configuration file:
     ```
     touch CLA Desktop config.js
     ```

2. **JSON Configuration Example**:
   ```json
   {
     "servers": {
       "braveSearch": {
         "apiKey": "YOUR_BRAVE_API_KEY_HERE"
       },
       "github": {
         "accessToken": "YOUR_GITHUB_ACCESS_TOKEN_HERE"
       }
     }
   }
   ```
   - This configuration is used to link CLA with Brave Search and GitHub.

3. **Example Prompt for Multi-Step Task Execution**:
   ```
   Please do the following:
   - Make a simple HTML page.
   - Create a repo called new Society test.
   - Push the HTML page to the new repo.
   - Add some CSS to the HTML page and push it up.
   - Create an issue suggesting more content.
   - Create a branch called feature and make that fix.
   - Push the change and make a pull request.
   ```
   - This prompt demonstrates CLA's ability to handle complex workflows.

### Conclusion

The video outlines how to set up and utilize CLA’s new mCP feature to build powerful automation agents. By configuring the CLA Desktop with mCP tools like Brave Search and GitHub integration, users can transform Claude into an API that automates workflows typically handled by developers, all through simple prompts. The tutorial emphasizes the speed and efficiency gains made possible through this AI automation, positioning CLA as a powerful tool for developers and AI enthusiasts alike.

For those interested in leveraging CLA mCP, it’s crucial to be comfortable with setting up API keys, modifying JSON files, and using GitHub. Mastering these tools can significantly enhance productivity, enabling AI to automate and optimize complex workflows with ease.

[[AI Agents]]  [[Chatbots]] [[GitHub]]  [[Code Editor]]