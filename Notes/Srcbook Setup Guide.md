---
tags:
- editors
video-url: https://www.youtube.com/watch?v=SYIBmZ73ZMM&list=WL&index=1
---
## **Srcbook Setup Guide

**How to Install and Use Sourcebook (SRC Book) Locally**

Sourcebook is an open-source TypeScript-centric app development platform that lets you create and iterate on web apps using AI assistance. It provides an interactive notebook interface to help developers write, edit, and execute code seamlessly. Let's dive into the step-by-step guide for setting up Sourcebook locally and using its features.

### Prerequisites

1. **Node.js (Version 18 or above)**: Sourcebook requires Node.js. You can use Node Version Manager (NVM) to manage your Node.js versions.
2. **Package Manager**: You can use either `npm` or `pnpm` as your package manager. The instructions below will demonstrate both.
3. **Git**: You will need [[Git]] to clone the Sourcebook repository.

### Step 1: Install Node.js

Use NVM to install Node.js 18:

```bash
nvm install 18
nvm use 18
```

Enable `corepack` to use package managers like `pnpm`:

```bash
corepack enable
```

### Step 2: Clone the Sourcebook Repository

Clone the Sourcebook repository to a folder of your choice (e.g., `repos` folder):

```bash
cd ~/repos
git clone https://github.com/sourcebook/sourcebook.git
```

Change directory into the Sourcebook folder:

```bash
cd sourcebook
```

### Step 3: Install Dependencies

You have two options to install dependencies:

- **Using npm**:

  ```bash
  npm install
  npm run start
  ```

- **Using pnpm**:

  ```bash
  pnpm install
  pnpm dlx sourcebook@latest start
  ```

The command will start the application locally on **localhost:2150**.

### Step 4: Access the Sourcebook Interface

Once the server is running, open your browser and go to:

```
http://localhost:2150
```

You will see the Sourcebook interface, which will allow you to create notebooks, apps, and more. Initially, you may be prompted to enter your API keys.

### Step 5: Set Up API Keys

- **Anthropic, OpenAI, or Custom Models**: Add your API key (e.g., for Anthropic or OpenAI).
- **Secrets Management**: Navigate to the "Secrets" tab to securely store your API keys.

### Step 6: Create Your First App

1. **Navigate to Apps Section**: Go to the "Apps" tab on the Sourcebook dashboard.
2. **Create a New App**: Click on "Create App" and enter the name and description of your app. For example:
   - **Name**: `Stride CRM`
   - **Description**: `A modern CRM application with contact management, interaction tracking, and more.`
3. **Generate Code**: Click on "Use AI to scaffold your app" to generate the boilerplate code. This will create a basic CRM application with features like contact lists, a sidebar, and more.

### Step 7: Create a Notebook

- **Notebooks**: Sourcebook allows you to create TypeScript notebooks, similar to Python's Jupyter notebooks, for testing and iterating on code.
- **Generate with AI**: Use the "Generate Notebook" button to create a new notebook with an AI prompt. For example, you can prompt Sourcebook to create a web browsing agent using LangChain and Puppeteer.

### Example Code: Web Scraping with Puppeteer

To create a web scraping script with Puppeteer:

1. **Generate Code in a Notebook**: Use the prompt below:

   ```
   Generate a TypeScript notebook that uses Puppeteer to scrape a website and take screenshots.
   ```

2. **Generated Script**:

   ```typescript
   import puppeteer from 'puppeteer';

   async function scrapeWebsite(url: string) {
       const browser = await puppeteer.launch();
       const page = await browser.newPage();
       await page.goto(url);
       await page.screenshot({ path: 'screenshot.png' });
       await browser.close();
   }

   scrapeWebsite('https://example.com');
   ```

### Step 8: Troubleshooting Common Issues

- **App Crashes on Start**: If the app crashes when running `npm run start` or `pnpm start`, it could be due to an incompatible Node.js version. Make sure you are using **Node 18** as required.
- **Dependencies Not Installing**: Try switching between `npm` and `pnpm` to see if that resolves the issue.
- **Hosted Version vs. Self-Hosted**: If the self-hosted version fails, consider using the hosted version at [https://sourcebook.com](https://sourcebook.com) while debugging the issue.

### Features and Interface

- **Hot Reloading**: Any changes made to the code are automatically reflected in the web preview.
- **Mermaid Diagrams**: Create flowcharts and diagrams using Mermaid syntax directly in notebooks.
- **Code Execution**: Run TypeScript code directly in notebooks to test different parts of your application.

### Example: Adding Dark Mode to Your App

To add more features like dark mode or other enhancements to your CRM app, use prompts like:

```
Make the CRM app support dark mode with a toggle button. Improve the design to make it modern and user-friendly.
```

### Uploading Images and Screenshots

Sourcebook also allows you to upload images as part of your app-building process:

1. **Take a Screenshot**: For instance, take a screenshot of a sample UI from Spotify.
2. **Upload to Sourcebook**: Use the "Upload Image" feature to upload the screenshot and use it as a reference for designing the UI.

### Example: Creating a Spotify Clone

To create a Spotify clone with Sourcebook:

1. **Prompt for a Spotify Clone**:

   ```
   Create a Spotify clone with basic functionalities like a music library, search, and playlist management.
   ```

2. **Generated Features**: The AI will generate components such as the sidebar, music player, search interface, etc.
3. **Edit the Sidebar**: Use AI prompts to make adjustments to the sidebar to improve navigation.

### Troubleshooting Tips

- **Crashes During App Creation**: If you experience crashes, try downgrading to **Node.js 18** or reinstalling your packages with `npm`.
- **Missing Notebook Feature in Hosted Version**: Note that the hosted version may not have the notebook feature enabled yet.

### Summary and Further Exploration

Sourcebook is a powerful TypeScript app development tool that combines the functionalities of a code editor, AI pair programmer, and interactive notebook. You can build, test, and iterate on applications quickly, and its integration of AI allows you to make complex changes effortlessly. Although it's still relatively new and has some quirks, it shows great potential for AI-assisted coding.

You can find more information and stay updated on Sourcebook by following their [Twitter page](https://twitter.com/sourcebook). If you encounter bugs, consider reaching out to the community or the development team for assistance.

Happy coding and enjoy building with Sourcebook!

 [[Python]]  [[Chatbots]]  [[Code Editor]]