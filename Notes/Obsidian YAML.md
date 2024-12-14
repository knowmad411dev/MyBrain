---
tags:
- obsidian
video-url: https://www.youtube.com/watch?v=diZ4AFh-ZNI&list=WL&index=74
---

## **Obsidian YAML**

**Introduction**

In this comprehensive guide, we'll explore how utilizing YAML properties in your Obsidian notes can significantly enhance your note-taking experience. We'll delve into the benefits of YAML front matter, common mistakes to avoid, best practices, and step-by-step instructions on how to implement YAML properties effectively. Whether you're new to Obsidian or looking to optimize your workflow, this guide is designed to help you make the most out of YAML properties.

---

## Understanding Obsidian YAML Properties

### What is YAML?

YAML (Yet Another Markup Language) is a human-readable data serialization format that is commonly used for configuration files and metadata. In Obsidian, YAML front matter refers to the section at the top of a note enclosed between two sets of triple dashes (`---`). This section allows you to include structured metadata about your note.

### Key Features of YAML in Obsidian

- **Structured Metadata**: Store data such as titles, tags, categories, dates, and custom properties.
- **Integration with Plugins**: Works seamlessly with plugins like DataView, enabling advanced querying and visualization.
- **Templates and Consistency**: Helps maintain a consistent structure across all notes using templates.
- **Enhanced Search and Organization**: Improves the ability to filter, search, and organize notes based on metadata.

---

## The Pros and Cons of Using YAML Properties

### Pros

1. **Improved Organization**: Structured metadata allows for better organization and management of notes.
2. **DataView Integration**: Leverage the DataView plugin to create dynamic queries, reports, and visualizations.
3. **Enhanced Searchability**: Metadata improves the precision of searches and filtering by tags, categories, and other criteria.
4. **Consistency with Templates**: Ensures all notes follow a consistent format, aiding in organization.
5. **Flexibility**: Define custom key-value pairs tailored to your specific needs.
6. **Human-Readable Format**: Easy to read and edit without complex formatting.

### Cons

1. **Learning Curve**: Requires an initial understanding of YAML syntax, which can be challenging for new users.
2. **Formatting Sensitivity**: Small errors like incorrect indentation can lead to issues.
3. **Clutter**: Excessive metadata can make notes appear cluttered, affecting readability.
4. **Plugin Dependency**: Full benefits are realized when using plugins like DataView.
5. **Time Investment**: Setting up templates and adding YAML properties requires upfront time, especially for existing notes.

---

## Common Mistakes When Using YAML Properties

### Mistake: Not Using YAML Properties from the Start

When first using Obsidian, it's common to include metadata directly in the note body rather than in the YAML front matter. For example:

```
# David Allen
- **Link**: [Getting Things Done](http://example.com)
- **Topics**: Productivity, Time Management
- **Tags**: #productivity, #time-management
```

**Why This is a Mistake:**

- **Limited Querying**: Plugins like DataView can't access metadata that's not in the YAML section.
- **Inconsistency**: Harder to maintain a consistent structure across notes.
- **Extra Work Later**: Requires manual migration of metadata to YAML if you decide to use advanced features later.

### Correct Approach Using YAML

```YAML
---
author: David Allen
title: Getting Things Done
tags: [productivity, time-management]
topics:
  - Productivity
  - Time Management
link: http://example.com
---
```

---

## Best Practices for Using YAML Properties

### 1. **Use Templates**

Create standardized templates for different types of notes (e.g., authors, books, articles) that include predefined YAML properties.

**Example: Author Template**

```YAML
---
type: author
date_added: {{date}}
tags: [author]
books: []
topics: []
---
```

### 2. **Consistent Formatting**

- **Indentation**: Use consistent indentation for nested properties.
- **Quotations**: Enclose text in quotes if it contains special characters or starts with a special character.

### 3. **Leverage the DataView Plugin**

- Install and enable the DataView plugin to query and display data based on your YAML properties.
- **Example DataView Query:**

    ```
    TABLE author, topics
    FROM "Books"
    WHERE type = "book"
    SORT date_added DESC
    ```

### 4. **Minimal Necessary Metadata**

Include only the metadata you need to avoid clutter. Too much unnecessary metadata can make notes harder to read.

### 5. **Regular Maintenance**

Periodically review your YAML properties to ensure they are up-to-date and relevant.

---

## How to Create YAML Properties in Obsidian

### Step 1: Enable Core Plugins

1. **Open Settings**: Click on the gear icon in the left sidebar.
2. **Navigate to Core Plugins**: Scroll down to find "Properties".
3. **Enable Properties Plugin**: Toggle it on to enable the Properties feature.

### Step 2: Access the Properties View

1. Click on the **Properties** button in the right-hand pane (it looks like a list or info icon).
2. This opens up the Properties view where you can add, edit, or remove YAML properties.

### Step 3: Add YAML Properties

#### Method 1: Using the GUI

1. **Add Property**: Click on "Add property" in the Properties view.
2. **Enter Property Name**: Type the name of the property (e.g., `author`, `tags`, `date_added`).
3. **Select Property Type**: Choose the appropriate type (Text, List, Number, Checkbox, Date, Date and Time).
4. **Enter Value**: Provide the value for the property.

#### Method 2: Manually in Source Mode

1. Switch to **Source Mode** by clicking the pencil icon.
2. At the top of your note, add the YAML front matter:

    ```YAML
    ---
    property_name: property_value
    ---
    ```

**Example:**

```YAML
---
author: "David Allen"
title: "Getting Things Done"
tags: [productivity, "time management"]
date_added: 2023-10-22
---
```

### Step 4: Using Templates with YAML

1. **Create a Template File**: In your templates folder, create a new note (e.g., `Book Template`).
2. **Add YAML Front Matter**: Include all the necessary properties with placeholder values or Templater code.

    **Example:**

    ```
    ---
    ```

## type: book title: "{{title}}" author: "{{author}}" date_added: {{date}} tags: [book] topics: [] status: "unread"

````

3. **Apply the Template**: When creating a new note, apply the template to automatically include the YAML properties.

### Step 5: Editing Properties

- Use the Properties view to edit existing properties without switching to Source Mode.
- Click on the property value to edit it directly.

### Step 6: Advanced Properties

- **Lists**: For multiple values, use lists.

```yaml
topics:
 - Productivity
 - "Time Management"
````

- **Links**: To link to other notes, use double square brackets.

    ```
    related_notes:
      - [[Note Title 1]]
      - [[Note Title 2]]
    ```

- **Dates**: For date properties, use the date format `YYYY-MM-DD`.

### Step 7: Inline Metadata (Alternative Method)

- You can also add metadata inline using the `key:: value` syntax.

    **Example:**

    ```
    Habits:: Good practices to follow
    ```

- **Note**: Inline metadata is not displayed in the Properties view but can be used in DataView queries.

---

## Leveraging the DataView Plugin

### Installing DataView

1. **Open Settings**: Click on the gear icon.
2. **Community Plugins**: Navigate to the Community Plugins section.
3. **Browse Plugins**: Search for "DataView".
4. **Install and Enable**: Click install, then enable the plugin.

### Using DataView with YAML Properties

**Example: Display All Books by an Author**

```
TABLE title, date_added
FROM "Books"
WHERE author = "David Allen"
SORT date_added DESC
```

- This query will generate a table of all books by David Allen, displaying the title and the date added.

### Common DataView Queries

- **List of Books**

    ```
    LIST
    FROM "Books"
    WHERE type = "book"
    ```

- **Tasks with Specific Tags**

    ```
    TASK FROM "Tasks"
    WHERE tags = "#important"
    ```

---

## Troubleshooting Common Issues

### YAML Formatting Errors

- **Incorrect Indentation**: YAML is sensitive to indentation. Ensure proper spacing.
- **Missing Quotes**: Enclose strings with special characters in quotes.
- **Special Characters**: Escape characters like `:` or `-` if they appear in your text.

### Properties Not Recognized

- Ensure that the property names are consistent across notes.
- Check for typos in property names and values.
- Verify that the DataView plugin is installed and enabled.

---

## Conclusion

By correctly implementing YAML properties in your Obsidian notes, you unlock powerful organizational and querying capabilities, especially when combined with plugins like DataView. Starting with well-structured templates and consistent metadata practices will save you time and effort in the long run. Embrace the full potential of Obsidian by integrating YAML properties into your note-taking workflow.

---

**Additional Resources**

- [Obsidian YAML Front Matter Documentation](https://help.obsidian.md/Advanced+topics/YAML+front+matter)
- [DataView Plugin Documentation](https://github.com/blacksmithgu/obsidian-dataview)
- [YAML Syntax Guide](https://yaml.org/spec/1.2/spec.html)

**Note**: Always remember to backup your vault before making bulk changes to your notes or templates.

[[Obsidian]]