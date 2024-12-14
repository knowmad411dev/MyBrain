---
tags: 
- obsidian
---

## **Templater Code Rules

In Templater for Obsidian (or similar markdown editors), the syntax you use to embed JavaScript code determines how the code is executed and whether its output is inserted into your document. The `*` character in the `<%* ... %>` syntax plays a crucial role in this behavior.

### Understanding the Syntax

1. **Standard Code Block (`<% ... %>`):**

    - **Purpose:** Executes the JavaScript code within the block.
    - **Output Behavior:** If the code returns a value, that value is inserted into the document at the location of the code block.
    - **Use Case:** When you want the result of the code execution to appear in your document.

```templater
    <% let currentDate = new Date(); %> Current date and time: <%= currentDate %>
  ```

    In this example, `<% let currentDate = new Date(); %>` runs the code without outputting anything directly. The `<%= currentDate %>` specifically outputs the value of `currentDate` into the document.
    
2. **Silent Code Block (`<%* ... %>`):**

    - **Purpose:** Executes the JavaScript code within the block.
    - **Output Behavior:** **Does not** insert any output into the document, regardless of what the code returns.
    - **Use Case:** When you need to perform operations like setting variables, fetching data, or any other logic that shouldn't directly appear in the document.
    
```templater
    <%*    let videoUrl = await tp.system.prompt("Enter YouTube video URL");    
	    let metadata = await tp.user.ytmeta(`-j "${videoUrl}"`, ".");    
	    let title = metadata.title;    let description = metadata.description;    
	    let duration = metadata.duration;    
	    let chapters = metadata.chapters; -%>
  ```

    In your provided code, `<%* ... %>` is used because you're performing a series of operations:
    
    - Prompting the user for a YouTube URL.
    - Fetching metadata for that video.
    - Assigning various pieces of metadata to variables.
    
    None of these operations are intended to produce direct output in the document. Instead, they're likely setting up variables for later use in the template. Using `<%* ... %>` ensures that this code runs silently without inserting any unintended text into your note.
    

### Why Other Code Might Not Use `*`

If you have other code blocks that are meant to display results directly in your document, they would use the standard `<% ... %>` syntax or include expressions like `<%= ... %>` to output values. For example:

```templater
<% let greeting = "Hello, World!"; %> Greeting: <%= greeting %>
```

Here, the `greeting` variable is set silently, but its value is explicitly inserted into the document with `<%= greeting %>`.

### Summary

- **`<%* ... %>`**: Use this when you want to execute code **without** inserting any output into the document. Ideal for setting variables, fetching data, or performing logic operations.
- **`<% ... %>` and `<%= ... %>`**: Use these when you want to execute code **and** insert the result or specific values into the document.

By choosing the appropriate syntax, you can control both the execution of your scripts and the output that appears in your notes.

---

**References:**

- Templater Documentation
- [Obsidian Templater GitHub](https://github.com/SilentVoid13/Templater)

[[Obsidian]]
