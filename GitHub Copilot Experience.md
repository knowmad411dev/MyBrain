---
tags:
- editors
---
## **GitHub Copilot Experience

## Overview of GitHub Universe Announcements

At GitHub Universe, numerous updates were announced, focusing on **VS Code** and **GitHub Copilot**. The highlights include:

1. **Copilot Edits**: Edit multiple files simultaneously with context-aware assistance.
2. **Intent Detection**: Automatically includes workspace context during chat sessions.
3. **Vision for Copilot**: Leverages image inputs to generate code and descriptions.
4. **Data Analysis for Copilot**: Enables intelligent analysis and visualization of CSV files.
5. **GitHub Issues and PR Integration**: Summarize issues, fix them with Copilot, and interact with GitHub pull requests directly.

This document covers each feature with detailed instructions and code examples.

---

## 1. Copilot Edits

### **Feature Overview**

Copilot Edits allows you to edit multiple files simultaneously with suggestions tailored to your intent.

### **How to Use**

1. Ensure **GitHub Copilot** is updated to the latest version in **VS Code**.
2. Open Copilot on the right-hand side of VS Code.
3. Drag files into the **working set** that you want to modify.
4. Provide a clear instruction or intent to Copilot.
5. Review, accept, or reject changes for each file.

### **Example: Creating a Login Route**

1. Drag the following files into the working set:
    
    - `main.js`
    - `App.vue`
    - `router/index.js`
2. Prompt Copilot:
    
    > "Create a login route."
    

**Changes Copilot Makes**:

- **`index.js`**: Add a new route for the login page.
    
    ```javascript
    import LoginView from '@/views/LoginView.vue';
    
    const routes = [
      { path: '/login', name: 'Login', component: LoginView },
      // other routes...
    ];
    ```
    
- **`App.vue`**: Add a link to the login page in the navigation.
    
    ```html
    <nav>
      <router-link to="/login">Login</router-link>
    </nav>
    ```
    

3. **Accept** changes, save, and test the route.

### **Styling the Login View**

1. Add the login view file (`LoginView.vue`) to the working set.
2. Prompt Copilot:
    
    > "Style the login form to look cleaner and modern."
    

**Output Example**:

```css
.login-form {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 8px;
}

.login-form input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}
```

3. Accept and save the changes.

---

## 2. Intent Detection

### **Feature Overview**

Copilot now detects intent and automatically includes workspace context if you don’t explicitly specify it.

### **How to Use**

1. Start a Copilot chat session in VS Code.
2. Provide a query without explicitly mentioning `@workspace`.
    - Example: _"What files are leftover from boilerplate?"_
3. Copilot analyzes your workspace and attaches the necessary context automatically.

**Example**:

- Input: "What files are leftover from boilerplate?"
- Copilot Response:
    
    > "The following files appear to be unused boilerplate: `HelloWorld.vue`, `exampleComponent.vue`."
    

---

## 3. Vision for Copilot

### **Feature Overview**

Copilot Vision allows you to use images as context for chat queries and generate relevant code or descriptions.

### **How to Use**

1. Open Copilot Chat in VS Code.
2. Drag an image into the chat or paste it from the clipboard.
3. Ask a relevant question, such as:
    - _"Generate HTML and CSS based on this design."_
    - _"Create alt text for this image."_

**Example: Generating Alt Text**

- Drag an image into the chat.
- Prompt Copilot: "Create alt text for this image."
- Output:
    
    > _"A cartoon raccoon wearing sunglasses and a black outfit."_
    

---

## 4. Data Analysis for Copilot

### **Feature Overview**

The **Data Analysis for Copilot** extension allows you to interact with and analyze CSV files.

### **How to Use**

1. Install the Data Analysis extension for Copilot.
2. Open a CSV file in VS Code.
3. Interact with the data using natural language queries.

### **Example Queries**:

1. **Count entries in a CSV**:
    
    > "How many total entries are there?"
    
2. **Generate a visualization**:
    
    > "Display a chart of unique artists per playlist."
    

**Sample Output (Visualization)**:

```plaintext
90's Music - 16 Artists
Pop Hits - 51 Artists
...
```

---

## 5. GitHub Issues and Pull Requests Integration

### **Feature Overview**

This integration allows you to:

- Summarize issues.
- Fix issues using Copilot.
- Interact with pull requests (PRs) directly within VS Code.

### **How to Use**

1. Open the **GitHub Issues** extension in VS Code.
2. Summarize an issue:
    - Right-click an issue > _"Summarize with Copilot."_
3. Fix an issue:
    - Select an issue > _"Fix with Copilot."_

### **Example: Fixing Hardcoded Emails**

1. **Summarize the issue**:
    
    > _"Summarize issue #31."_
    
    - Output: "Hardcoded reply-to email in `sendEmail` function."
2. **Fix the issue**:
    
    - Select _"Fix with Copilot."_
    - Copilot suggests replacing hardcoded emails with environment variables:
        
        ```javascript
        const sendEmail = (to, subject, body) => {
          const defaultReplyTo = process.env.REPLY_TO_EMAIL || 'no-reply@example.com';
          // Send email logic...
        };
        ```
        
3. Accept and save the changes.
    

### **Checking Open Issues**

- Query example: "How many issues do I have open for the November push milestone?"
- Output:
    
    > "There are 4 open issues: #31, #45, #47, and #52."
    

---

## Conclusion

The latest enhancements to GitHub Copilot make it more powerful and intuitive:

- **Copilot Edits** streamlines multi-file editing.
- **Intent Detection** eliminates manual workspace context management.
- **Vision for Copilot** enables image-based workflows.
- **Data Analysis** makes CSV handling seamless.
- **GitHub Issues Integration** simplifies issue management and fixes.

These features empower developers to work smarter and faster within VS Code.

Happy coding!

[[GitHub]]