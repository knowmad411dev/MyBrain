---
github_link: https://github.com/omerxx/dotfiles
tags:
- editors
video-url: https://www.youtube.com/watch?v=LFBOLx5KiME
---
## **NuShell

### Overview of Nushell: A Data-Centric Shell Environment

The text is a personal reflection on exploring and using a new shell called **Nushell** (previously referred to as "Nell" due to a possible typo). The author initially used **Zsh** and **Fish**, but eventually found Nushell to be far more advanced. Nushell is not just a command-line shell, but a powerful data-processing environment, ideal for those working with structured data like **JSON**, **YAML**, and **CSV**. It aims to replace many command-line utilities and offers a unique approach to handling structured data, making it especially useful for tasks like Kubernetes management.

### Key Features of Nushell

1. **Beyond Traditional Shells**:
   - Nushell is designed to be more than a shell, with capabilities beyond the typical **Bash**, **Zsh**, or **Fish**. It is particularly adept at structured data processing, which makes it highly suitable for modern DevOps and cloud environments.

2. **Powerful Data Handling**:
   - Nushell makes working with data like **JSON**, **YAML**, and **CSV** effortless. It allows seamless conversion between data formats and has built-in commands for querying and manipulating these formats, often replacing tools like **jq** and **yq**.

3. **Useful Examples**:
   - **Kubernetes Data Parsing**: The author discusses using **kubectl** to fetch pod data, piping the output into Nushell for automatic column detection and filtering (e.g., finding pods older than 27 days).
   - **Interactive Data Exploration**: Commands like `explore` enable users to navigate and interact with JSON structures without needing to write complex queries.

4. **Custom Key Bindings**:
   - The author found **alt+backspace** didn’t work as expected and fixed it by modifying the Nushell configuration (`config.nu`). This customization allows typical shell behaviors such as word deletion, improving usability.

5. **Replacing Common Utilities**:
   - **jq/yq Replacement**: Nushell can parse **JSON** and **YAML** using commands like `from json` and `from yaml`, then convert between formats seamlessly.
   - **sed Replacement**: Simple text replacement in Nushell is handled via `str replace`, which is easier than the syntax-heavy **sed** utility.
   - **CSV Manipulation**: Nushell simplifies handling CSV files by converting them to structured tables for further querying or transformation.

6. **HTTP Requests**:
   - Nushell has built-in support for making **HTTP requests** directly from the command line (similar to **curl** or **Postman**), allowing parsed responses to be directly processed or queried.

### How-To Instructions with Example Commands

#### 1. Setting Up Custom Key Bindings

To remap **alt+backspace** to delete words as it does in other shells:

```shell
config nu where alt_backspace = some_function_remap
```

This customization makes the workflow smoother by allowing familiar key combinations.

#### 2. Handling JSON and YAML

Nushell makes it easy to manipulate structured data:

- To parse JSON from a file:
  ```shell
  open some_file.json | from json
  ```
- To convert YAML to JSON:
  ```shell
  open some_file.yaml | from yaml | to json
  ```
- To extract **Kubernetes** data:
  ```shell
  kubectl get pods | detect columns | where age == 27d
  ```

#### 3. Interactive Data Exploration

Nushell allows users to explore JSON interactively:

```shell
open some_file.json | from json | explore
```

This command provides a structured view, making it easier to inspect large, nested JSON data.

#### 4. Text Replacement (Replacing **sed**)

Replace text more intuitively compared to **sed**:

```shell
echo "Hello world" | str replace "world" "nushell"
```

This replaces "world" with "nushell" in a simple and straightforward way.

#### 5. HTTP Requests

To send an HTTP GET request:

```shell
http get https://api.example.com/data
```

The response is returned as a parsed structure, allowing further processing without extra parsing.

#### 6. Manipulating CSV Files

- Load a CSV and interact with it as a table:
  ```shell
  open users.csv | from csv
  ```
- Remove sensitive information, such as passwords:
  ```shell
  open users.csv | from csv | each { |row| update password { "" } }
  ```
- Select specific columns from the CSV:
  ```shell
  open users.csv | from csv | select username city
  ```

### Downsides of Nushell

- **Breaking Changes**: Many users experienced breaking changes with **pre-1.0** releases, as Nushell was evolving rapidly. Functions, operators, or commands users relied upon could change frequently.
- **Immaturity**: Some frustrations came from Nushell's immaturity during early phases, leading to a less stable experience compared to older, more established shells.

### Final Thoughts

Nushell is a powerful, data-centric shell environment that can:

- Replace numerous command-line utilities (such as **jq**, **yq**, **sed**, and **awk**).
- Allow interactive data exploration without complex syntax.
- Handle structured data (JSON, YAML, CSV) seamlessly.
- Execute HTTP requests directly from the command line.

If you work extensively with structured data and are comfortable with adapting to new tools, **Nushell** might be the perfect addition to your workflow. However, it might not be the best option if you need a time-tested, stable environment for production purposes.

### Example Nushell Commands Summary

Here is a summary of some Nushell commands discussed in the text:

| Command                                 | Description                                        |
|-----------------------------------------|----------------------------------------------------|
| `open file.json | from json`            | Read JSON from a file and parse it.                |
| `http get <url>`                        | Send a GET request and get a structured response.  |
| `open file.csv | from csv | select col` | Select specific columns from a CSV file.           |
| `str replace "old" "new"`               | Replace text within a string (easier than sed).    |
| `explore`                               | Interactive exploration of structured data.        |

### Conclusion

If you want a powerful and modern shell that makes handling structured data easy and efficient, **Nushell** offers a compelling set of features. While it requires a willingness to adapt to changes, Nushell can be an exciting option for those looking to push beyond traditional shell limitations.

[[Code Editor]]