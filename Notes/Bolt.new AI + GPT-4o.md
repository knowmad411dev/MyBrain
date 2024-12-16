---
github_link: https://github.com/coleam00/bolt.new-any-llm
tags:
- gpt
- editors
video-url: https://www.youtube.com/watchv=36UkRRPjgng&list=WL&index=1&t=15s
---

## **Bolt.new AI + GPT-4o

**Detailed Overview and Instructions for Setting Up Bolt with OpenAI**

This guide walks you through setting up **Bolt** on your local machine, connecting it with OpenAI, and running a sample project. By following these steps, you'll create a basic website using **React** and **Tailwind CSS**.

---

### Prerequisites

Before starting, ensure you have the following tools installed on your computer:

1. **Git**
2. **Node.js**

You can verify the installations by running:

```bash
# Check Git version
git --version

# Check Node.js version
node -v
```

---

### Step 1: Clone the Repository

1. Open your terminal.
2. Clone the repository (replace `<repo-link>` with the actual repository URL):

   ```bash
   git clone <repo-link>
   ```

3. Navigate to the cloned repository:

   ```bash
   cd <repository-name>
   ```

4. Open the project in **VSCode**:

   ```bash
   code .
   ```

---

### Step 2: Install PNPM

PNPM is a faster and more efficient package manager than NPM. To install PNPM globally:

```bash
npm install -g pnpm
```

---

### Step 3: Install Dependencies

Install all the required packages using PNPM:

```bash
pnpm install
```

This will download and set up all dependencies specified in the `package.json` file.

---

### Step 4: Modify Configuration Files

#### 4.1 Update Vite Command

1. Navigate to:
   ```
   app/lead/server/prompt
   ```

2. Locate the Vite configuration file and replace any outdated commands with the latest ones from the **Vite documentation**.

   Example:

   ```bash
   # Replace the command with the correct Vite installation command from the docs
   npm create vite@latest
   ```

3. Save the changes.

#### 4.2 Edit the Environment File

1. Open the `.env` file in the root directory.
2. Add your **OpenAI secret key**:

   ```
   OPENAI_API_KEY=<your-openai-key>
   ```

3. Save the file.

---

### Step 5: Run the Application

Start the server using PNPM:

```bash
pnpm run dev
```

By default, the application will run on `localhost:3000`. If not, ensure the server is configured to run on port 3000 by checking the server settings in the project configuration files.

---

### Step 6: Reload the Application

If you don't see the OpenAI key reflected initially:

1. Reload the application in your browser.
2. Check the OpenAI configurations and confirm the key is properly loaded.

---

### Step 7: Adjust Constants for Better Responses

1. Navigate to:
   ```
   app/lead/server/constants
   ```

2. Increase the response size constant to ensure you receive more comprehensive responses from OpenAI.
3. Save the file and restart the server.

---

### Step 8: Create a Simple Website

#### Set Up Tailwind CSS

1. Install Tailwind CSS by following the [official documentation](https://tailwindcss.com/docs/installation).
2. Add Tailwind directives to your CSS file:
   ```css
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```
3. Configure your Tailwind `config.js` as required.

#### Develop Your Website

1. Use **React** components to build your site.
2. Style the components using Tailwind CSS classes.

Example:

```jsx
import React from 'react';

const App = () => {
  return (
    <div className="bg-gray-100 text-center p-10">
      <h1 className="text-3xl font-bold">Welcome to Bolt</h1>
      <p className="text-lg">Your AI-powered application</p>
    </div>
  );
};

export default App;
```

3. Save and run the project:
   ```bash
   pnpm run dev
   ```

---

### Troubleshooting

1. **Common Errors During Installation**
   - Refer to the **Vite documentation** for resolving npm installation errors.
2. **API Response Issues**
   - Ensure the constant values are properly adjusted for larger responses.
3. **Server Not Running**
   - Verify that the server is set to port 3000.

---

### Final Thoughts

You have successfully set up Bolt, connected it to OpenAI, and built a simple React website styled with Tailwind CSS. For further customization, explore the project files and Tailwind utilities.

Thank you for following along!

[[Bolt.new]]    [[Code Editor]]  [[Python]]