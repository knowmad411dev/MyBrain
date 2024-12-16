---
tags: 
- github
- editors
video-url: https://www.youtube.com/watch?v=H5Nr-8bYvXU&list=WL&index=12
---

# GitHub Codespaces

## Summary of the Video: Setting Up GitHub Codespaces with AI Tools and Copilot Workspaces

This video discusses using **GitHub Codespaces** as a remote development platform, with additional AI tools for productivity and coding assistance. The presenter compares Codespaces to **Project IDX** and demonstrates how to configure Codespaces with various AI-powered tools such as **Super Maven** and **AER**, as well as using **Copilot Workspaces** to automate tasks.

---

## Main Topics Covered

1. **GitHub Codespaces Overview**

    - GitHub Codespaces allows easy cloud-based development, with the option to launch environments from any GitHub repo.
    - Users can choose from various machine types, including one with **16GB of RAM**, making it suitable for running lightweight language models.
    - Codespaces is free but limited to **120 core hours/month**, which auto-pauses when idle to conserve usage.

2. **Comparing Codespaces and Project IDX**

    - Codespaces is faster than Project IDX for spinning up environments and installing extensions.
    - While IDX includes AI features by default, Codespaces requires additional configuration for auto-completion and chat features.

---

## Step-by-Step Setup: Configuring GitHub Codespaces with AI Tools

### 1. Creating a Codespace

- **Option 1**: Create a Codespace directly from a **GitHub repo** (includes repo content).
- **Option 2**: Create a **blank template Codespace** for a fresh environment:

    1. Open the Codespaces menu from GitHub.
    2. Choose the **Blank Template** for speed and flexibility.
    3. Launch the Codespace (starts quickly compared to IDX).

---

### 2. Installing Essential Tools

#### Installing Auto-completion (Super Maven)

1. Open the **Extensions** tab in the Codespace.
2. Search for **Super Maven** and click to install.
3. Configure Super Maven:

    - Select the **free tier** and enter an email.
    - Autocomplete will now be active.

#### Installing and Configuring AI Coding Agents

- **Klein Setup**:

    1. Search for **Klein** in the Extensions tab and install it.
    2. Choose the **Gemini 1.5 flash model** for configuration (a multimodal model that is free to use).
    3. Optionally, switch between models like **Deep Seek** for efficiency based on tasks.

- **Installing AER (Coding Agent)**:

    1. In the **Terminal**, run:

        ```bash
        pip install aer-chat
        ```

    2. Export the relevant **API key** to connect with either OpenAI, Anthropic, or Gemini models:

        ```bash
        export API_KEY=<your_api_key_here>
        ```

---

### 3. Building a Simple To-Do App Using Codespaces and Copilot Workspaces

1. **Creating a To-Do App**

    - Use **Gemini’s multimodal abilities** to generate code based on a mockup.
    - Install the **Live Server extension** to preview the app:

        1. Right-click the HTML file → **Preview on Live Server**.
        2. Access the app through the **Open Ports** tab.
2. **Using AER for Another Project (Minesweeper)**

    - Ask AER to generate a Minesweeper game in the terminal.
    - Run the code to see the game in action.

---

## Copilot Workspaces Integration

- **Accessing Copilot Workspaces**:
    - This feature is currently in **preview mode** (requires being on the waitlist).
    - Even without a Copilot subscription, users in the preview can access the workspace.
- **How to Use Copilot Workspaces**:

    1. Open a **GitHub repo** and click the **Copilot button** under the Code menu.
    2. Provide a **prompt** to Copilot for the desired task.
    3. Copilot generates a **plan** and implements the changes across files automatically.
    4. Preview or merge the changes using:

        - **Pull Requests** (for collaboration).
        - **Push to Main Branch** (for personal repos).
- **Sync with Codespaces**: After making changes in Copilot, open the **same Codespace** to view live updates, eliminating the need for frequent pull-push cycles.

---

## Tips for Managing Codespaces Efficiently

- Use **one Codespace** and clone multiple repos inside it to avoid repeated setup.
- Regularly sync your work to prevent loss of progress across sessions.

---

## Video Outro and Additional Content

- The presenter encourages viewers to **comment ideas** and **like the video** if they want a follow-up app-building tutorial.
- They also promote a **membership plan** ($5/month) for access to exclusive content like an OpenAI swarm tutorial.

---

## How-To Summary & Useful Commands

### Creating a Codespace

1. From any repo → **Code menu** → **Codespace**.
2. Choose **Blank Template** (for fresh setups).

### Installing Extensions

- **Super Maven**: Search in Extensions → Install → Configure with email.
- **Klein**: Search in Extensions → Install → Configure with Gemini model.

### Installing AER via Terminal

```bash
pip install aer-chat
export API_KEY=<your_api_key_here>
```

### Running HTML Apps on Live Server

1. Install **Live Server Extension**.
2. Right-click HTML file → Preview on Live Server.

[[GitHub]]