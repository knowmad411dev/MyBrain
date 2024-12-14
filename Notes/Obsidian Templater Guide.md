---
Video-URL: https://www.youtube.com/watch?v=kXeODjqvNAg&list=WL&index=3
tags:
- obsidian
---

# Obsidian Templater Combined Guide

This comprehensive guide covers the setup, usage, and advanced scripting possibilities of Templater in Obsidian, a powerful plugin for managing and automating workflows within your vault. It combines an overview of Templater, step-by-step tutorials for beginners, and practical scripts to boost productivity.

---

## **1. What is Templater?**

Templater is a plugin that extends Obsidian's capabilities for note templating. It provides advanced templating features, allowing users to insert dynamic values, automate repetitive tasks, and create powerful workflows within their notes. Unlike the core template plugin in Obsidian, Templater allows for more customization and automation using JavaScript.

- **Key Features**:
    - Insert dynamic data such as dates, metadata, or user inputs.
    - Automate tasks like creating daily notes, updating lists, or querying APIs.
    - Use JavaScript to create custom commands.

---

## **2. Installing and Setting Up Templater**

### **Step-by-Step Installation**

1. **Open Obsidian**: Launch your Obsidian application.
2. **Access Community Plugins**: Navigate to `Settings` → `Community Plugins`.
3. **Browse and Install**:

    - Click on `Browse`.
    - Search for **Templater**.
    - Click `Install` and then toggle the switch to `Enable` the plugin.

4. **Access Configuration**:

    - Click on the Templater plugin to open its configuration page.
    - Initial settings can typically be left at default to start exploring functionalities.

---

## **3. Understanding the Differences Between Core Templates and Templater**

- **Core Templates**: The built-in Obsidian template plugin allows users to insert predefined text into notes, but lacks automation.
- **Templater**: Offers enhanced capabilities such as conditionals, loops, JavaScript integration, and automatic actions that can save time and streamline note-taking.

---

## **4. Getting Started with Templater**

### **A. Basic Templater Syntax**

Templater commands are embedded within double curly braces `{{ }}`. Many commands use a percent sign `%` followed by the function name to invoke specific actions.

- **Example**:

    ```Templater
    {{% tp.date("YYYY-MM-DD") }}
    ```

    This command inserts the current date in the specified format.

### **B. Common Commands**

1. **Inserting Dates**: Insert today’s date, formatted as needed:

    ```Templater
    {{% tp.date("YYYY-MM-DD") }}
    ```

2. **Fetching Data from the Web** (e.g., a daily quote):

    ```Templater
    {{% tp.web("daily_quote") }}
    ```

3. **User Inputs**: Prompt for user input while creating a note:

    ```Templater
    {{% tp.prompt("What is your task?") }}
    ```

---

## **5. Advanced Templater Commands and Automation**

Templater's true power comes from its ability to integrate JavaScript for more advanced automation.

### **Using JavaScript in Templates**

Templater supports JavaScript, which allows users to create complex templates with conditionals, loops, and dynamic elements.

- **Setting Variables**:

    ```Templater
    <%* let currentDate = tp.date.now("YYYY-MM-DD"); %>
    ```

    The `<%* ... %>` syntax executes code without displaying it in the note, useful for setting up variables or performing operations.

- **Outputting Values**:

    ```Templater
    <%* let greeting = "Hello, Obsidian!"; %>
    <%= greeting %>
    ```

    `<%= ... %>` is used to output the result directly in the note.

---

## **6. Practical Script Examples**

### **A. Daily Note Template**

Create a daily note that includes the current date, a motivational quote, and space for daily tasks:

```Templater
# <% tp.date.now("YYYY-MM-DD") %> - Daily Note

## Quote of the Day
> <% tp.web("quote_api") %>

## Tasks
- [ ] Task 1
- [ ] Task 2
```

### **B. YouTube Metadata Fetcher**

Automate the extraction of metadata from a YouTube link. This example uses JavaScript to fetch the title, duration, and description:

```Templater
<%*
let url = await tp.system.prompt("Enter YouTube URL:");
let metadata = await tp.web.youtube(url);
let title = metadata.title;
let duration = metadata.duration;
-%>

# Video Details
- **Title**: <%= title %>
- **Duration**: <%= duration %>
```

### **C. Meeting Notes with Pre-filled Sections**

Automatically generate a meeting note with sections for agenda, attendees, and notes:

```Templater
# Meeting on <% tp.date.now("dddd, MMMM Do YYYY") %>

## Attendees
- Person 1
- Person 2

## Agenda
1. Topic 1
2. Topic 2

## Notes
- Discussion points...
```

---

## **7. Templater Best Practices**

1. **Keep Scripts Modular**: Break complex scripts into smaller, reusable snippets.
2. **Use Comments**: Comment your JavaScript code for easier understanding and maintenance.
3. **Test Regularly**: Ensure your scripts work correctly by testing them in smaller notes before applying them across your vault.

---

## **8. Additional Templater Use Cases**

### **A. Advanced Journal Prompts**

Create reflective journal prompts that adjust based on the day of the week.

```Templater
# <% tp.date.now("YYYY-MM-DD") %> - Journal

## Reflection
<%*
let dayOfWeek = tp.date.now("dddd");
if (dayOfWeek == "Monday") { %>
- What are your goals for this week?
<% } else if (dayOfWeek == "Friday") { %>
- What were your achievements this week?
<% } else { %>
- What did you learn today?
<% } %>
```

### **B. Automating File Creation**

Automatically create new notes from a template based on a project:

```Templater
<%*
let projectName = await tp.prompt("Enter project name:");
tp.file.create_new(tp.file.find_tfile("Project_Template"), projectName);
%>
```

---

## **9. Summary and Next Steps**

Templater is an incredibly versatile plugin that can enhance your productivity in Obsidian by automating note creation, providing dynamic templates, and allowing for advanced JavaScript customization. Start with simple templates and gradually introduce more complexity as you get comfortable.

- **Next Steps**:
    - Explore the [Templater Documentation](https://github.com/SilentVoid13/Templater) for more details.
    - Try creating custom templates to solve everyday repetitive tasks.
    - Engage with the community on the Obsidian forums for more ideas and inspiration.

---

 [[Obsidian]]   [[Obsidian Templater Snippets]]
