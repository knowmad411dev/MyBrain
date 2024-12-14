---
tags:
- obsidian
video-url: https://www.youtube.com/watch?v=zvI_XS-l4ko&list=WL&index=38
---

## **Obsidian - Metadata Properties

### Summary of Video: Enhancing Properties in Obsidian Using Plugins

The video introduces a new feature in Obsidian that allows you to manage metadata properties of notes in a user-friendly manner, similar to Notion. While this core feature brings significant improvements, it also has limitations. The presenter, John Maverick, discusses how to enhance this feature by using various Obsidian Community plugins, taking the viewer from a basic understanding of properties to more advanced, automated workflows.

#### **1. Understanding Core Properties in Obsidian**

- **Creating Properties**:
    - Open the command palette with `Ctrl/Cmd + P`.
    - Use "Add File Property" or press `Ctrl + ;` to add a new property to the note.
    - Properties appear as key-value pairs; the key is the property name, and the value is the content.
    - Various data types are available, like text, checkbox, and date, which can be edited easily.
- **Viewing Properties in the Sidebar**:
    - Access properties by searching "Show File Properties" in the command palette.
    - To see all properties across notes, use "Show All Properties".
    - Click on a property in the sidebar to filter notes by that property or use advanced search syntax (`property:value`) to filter more specifically.

#### **2. Enhancing Property Management with Templates**

- **Automatically Adding Properties Using Templates**:
    - Install the `Templater` plugin by enabling Community Plugins in Obsidian settings.
    - Create a `Templates` folder to store template notes.
    - Add predefined property fields to the template (e.g., URL, rating, checkboxes).
    - Configure `Templater` to trigger when creating new files in specific folders, automatically applying the template to new notes.

    **Example Setup**:
    - For `Podcast Notes`, the template might include properties like `URL`, `Podcast`, `Rating`, and `Finished`.
    - When creating a new podcast note, the properties are automatically populated.

#### **3. Using Variables for Dynamic Property Values**

- **Incorporating Dynamic Values in Templates**:
    - Templater supports variables for automating values, such as dates or note titles.
    - Example scenario: A daily note template includes properties like `Summary`, `Rating`, and `Week`.
    - Use variables (e.g., `tp.file.title`) to dynamically fetch and calculate values.
    - The `moment.js` library is used for date calculations, allowing you to derive properties like the week number based on the note's title.

    **Example Code for Week Calculation**:

```md
    `<% moment(tp.file.title, "YYYYMMDD").format("YYYY-[W]WW") %>`
```

    - This code converts the note title into a date and formats it to display the week of the year.

#### **4. Syncing Inline Fields with DataView and Custom Plugins**

- **Enhancing Inline Properties with DataView & Inline Fields Sync Plugin**:
    - Install the `DataView` plugin to display property fields within the body of the note instead of at the top.
    - Use the `Inline Font Matter Sync` plugin (currently under review or installable via `BRAT` Community Plugin) to sync these inline fields with the standard properties menu.
    - Inline fields are created by adding `::` after the field name (e.g., `Summary:: Today was a productive day.`).
    - These inline fields sync to the properties pane, making it easier to manage and display metadata within the content of your note.

    **Note**: The `Inline Font Matter Sync` plugin adds a prefix (e.g., `_FM_summary`) to prevent potential conflicts between fields.

#### **5. Creating Header Links for Enhanced Navigation**

- **Linking to Specific Sections in Notes**:
    - Use headers (`# Header Name`) to mark sections within notes (e.g., `# Summary`).
    - Create a property that links to these headers, allowing easy access from other notes.
    - Use the `[[NoteTitle#Header]]` syntax to link to a header within a note. Optionally, use `|` to add an alias (e.g., an emoji).
    - This enables previewing and direct access to specific sections from summaries or tables in other notes.

    **Example Code for Header Linking in a Template**:

```md
    `Summary Link:: [[<% tp.file.title %>#Summary|📝]]`
```

#### **6. Plugin Recommendations for Advanced Functionalities**

- **Templater**: Enables template-based automation with support for variables and JavaScript.
- **DataView**: Displays query results and creates inline properties.
- **Inline Font Matter Sync**: Syncs inline properties with the properties pane (installed via BRAT if not available).
- **BRAT**: A Community Plugin to install beta versions of plugins not yet released in the main plugin directory.

---

#### **Resources and References**

- **Templater Documentation**: [Templater Documentation](https://github.com/SilentVoid13/Templater)
- **Moment.js Documentation**: Moment.js Docs
- **DataView Plugin**: [Obsidian DataView](https://github.com/blacksmithgu/obsidian-dataview)
- **BRAT (Beta Reviewers Auto-update Tool)**: [BRAT on GitHub](https://github.com/TfTHacker/obsidian42-brat)

#### **Further Learning and Resources**

The video offers free downloadable templates and an email course to deepen your knowledge of Obsidian workflows. You can find these resources in the video description.

#### **Conclusion**

With these plugins and techniques, users can fully leverage Obsidian's properties feature to enhance metadata management, streamline workflows, and create dynamic, connected notes. By utilizing templates, variables, and inline field syncing, users can automate repetitive tasks and improve note organization and retrieval.

[[Obsidian]]