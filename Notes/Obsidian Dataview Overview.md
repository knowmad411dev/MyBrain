---
tags:
- dataview
- obsidian
video-url: https://www.youtube.com/watch?v=6p5Eb1sqgIY&list=WL&index=2
---
## **Overview of Dataview

Dataview is a powerful plugin for Obsidian that allows you to query, filter, sort, and visualize data from your notes, treating them like a database. The plugin uses its own simple query language and can work with both built-in metadata and YAML front matter within your Markdown files. This makes it suitable for creating dynamic lists, tables, tasks, and calendars that automatically update as new notes are added or modified.

#### **Key Features of Dataview**

1. **Simple Query Language**: Dataview provides a query language that can be used to retrieve and display specific data from notes.
2. **Filter, Sort, and Group**: Queries can filter, sort, and group data based on tags, paths, links, or YAML front matter.
3. **Dynamic Outputs**: Queries refresh automatically, ensuring the data is always up-to-date without requiring manual intervention.
4. **Metadata Extraction**: Dataview can extract metadata from YAML front matter for advanced querying.
5. **Multiple Output Formats**: The query output can be presented in various forms such as lists, tables, tasks, and calendars.
6. **Community Support**: It has a strong community and many beginner guides, which makes learning easier.

#### **Dataview Query Types**

Dataview supports four main query types:

- **List**: Generates a list of notes.
- **Table**: Displays data in a table format.
- **Task**: Displays tasks from notes.
- **Calendar**: Creates a calendar view from date-based metadata.

### **Dataview Query Components**

1. **`FROM`**: Specifies the source of the data, such as specific tags, paths, or types of notes.
2. **`WHERE`**: Filters the data based on specific criteria, allowing you to only display results that match these conditions.
3. **`GROUP BY`**: Aggregates results based on a particular field, such as an author or category.
4. **`FLATTEN`**: Transforms a nested data structure into a single layer.
5. **`SORT`**: Sorts the output in ascending or descending order.
6. **`LIMIT`**: Restricts the number of results returned by the query.

### **Dataview Query Examples**

#### **1. List Query Example**

A list query can be used to list notes matching certain criteria. Here’s how you can create a simple list query:

````markdown
```dataview
list from #book
sort file.mtime desc
limit 5
```
````

This will:

- List notes that have the tag `#book`.
- Sort them by the last modified time in descending order.
- Limit the results to the latest 5 notes.

#### **2. Table Query Example**

To create a table listing authors from your notes:

````markdown
```dataview
table file.name as Title, category, topics, author
from ""
where author
limit 5
```
````

This query:

- Creates a table with columns for the note title, category, topics, and author.
- Retrieves data from all notes that have an `author` field.
- Limits the output to 5 rows.

#### **3. Task Query Example**

To display tasks across your vault:

````markdown
```dataview
task from ""
where file.name = "Data View Tasks"
group by file.link
```
````

This query:

- Displays tasks from the specified note.
- Groups them by the file they come from.

#### **4. Calendar Query Example**

To display a calendar view based on file modified times:

````markdown
```dataview
calendar file.mtime
from "note lab"
where file.tasks
```
````

This query:

- Shows modified times of notes from the folder "note lab".
- Filters to only include notes that have tasks.

### **Advanced Workflows for Dataview**

For users who want to go beyond the basics, it is helpful to create a dedicated directory within Obsidian to store learning notes and reference materials for Dataview. Here are a few practical workflows:

#### **1. Learning and Reference Directory**

- Create a directory named "Dataview Learning Notes".
- Inside the directory, store examples and reference notes to understand various aspects of Dataview.
- Each note can contain a brief summary, YAML property fields, and example queries for easy access.

#### **2. Using Dataview to Track Notes with Missing Content**

To find notes that are incomplete or have missing internal links:

- Create a query that identifies broken links within your vault.
- Use the output to help maintain the integrity of your note connections.

#### **3. Advanced Query Dashboards**

- Build dashboards using Dataview for tasks like tracking cycles, managing reviews, or curating summaries.
- For example, create a "System Engineer Wiki" dashboard by creating a query that pulls in all related notes, sorts them by custom attributes, and uses interactive buttons.

### **Best Practices and Tips for Using Dataview**

- **Use a Canvas**: Layout your Dataview learning notes and examples on an Obsidian canvas. This allows you to visualize different Dataview queries and organize them into groups.
- **Reference Queries**: Maintain a reference page that you can quickly use to copy and paste often-used queries into new notes.
- **Debugging Tips**: If you're facing issues with your queries, consider using an AI tool like ChatGPT to assist in debugging. Tools like these can often identify syntax issues and suggest improvements, making the learning process smoother.

### **How to Apply Dataview Basics**

To get started with Dataview:

1. **Install the Plugin**: Navigate to Obsidian’s community plugins, search for "Dataview", and install it.
2. **Create a Note**: Create a new note and title it "Dataview Basics".
3. **Start Querying**:
   - **List Query**: For listing notes in the folder "cards":
     ````markdown
     ```dataview
     list from "cards"
     ```
     ````
   - **Table Query**: To create a table view of concept notes:
     ````markdown
     ```dataview

table tags, type, related

from "cards/concepts"

limit 5

```
````
     This will generate a table showing tags, types, and related properties from notes in the specified folder.

### **Debugging Dataview Queries**

To learn Dataview:

- **Example Vault**: Consider using the "Obsidian Dataview Example Vault," a pre-configured vault that includes numerous examples.
- **AI Tools for Debugging**: AI tools like ChatGPT can be helpful to debug and improve Dataview queries.

### **Practical Considerations**

Dataview is a powerful tool but has some drawbacks, including:

- **Steep Learning Curve**: The query language takes time to learn.
- **Performance Issues**: Queries may cause performance problems, especially on slower computers or larger vaults.
- **Plugin Dependencies**: Compatibility with Obsidian updates can be an issue as Dataview is a third-party plugin.

### **Conclusion**

Dataview transforms your Obsidian vault into an organized, dynamic knowledge base. By utilizing Dataview’s query language to generate lists, tables, and calendars, you can effortlessly visualize and manage your notes. The plugin’s versatility and dynamic features are incredibly useful, although there is a learning curve involved. Starting with simple queries, building learning directories, and taking advantage of community resources will help you leverage Dataview to its fullest potential.

[[Obsidian]]
