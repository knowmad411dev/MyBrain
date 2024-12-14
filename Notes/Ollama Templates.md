---
tags:
- ollama
---

## **Ollama Templates

The provided text is a tutorial-style explanation of how templates work in Ollama and how to create them. Here's a detailed review, including a breakdown of the instructions, concepts, and examples given:

### Summary and Structure of the Text

The text describes the role of templates in Ollama, focusing on how they make the platform user-friendly for both beginners and advanced users. It covers:

1. **Importance of Templates in Ollama:**
   - Templates, parameters, system prompts, and licenses are part of the model, making Ollama easier to use compared to other platforms.
   - Unlike other platforms where users may struggle to determine the right template for a model, Ollama integrates these templates directly.

2. **Handling HuggingFace Models:**
   - When importing HuggingFace models, users often need to create a valid template on their own, which can be challenging if unfamiliar with the original model's prompt format.

3. **Basic Template Introduction:**
   - The text provides an overview of how templates work in Ollama using Go Templates.
   - It explains the use of system prompts and user prompts, and how they are represented in templates using variables such as `.System` and `.Prompt` in double curly braces.

4. **Debugging Templates:**
   - Users can run the Ollama server in debug mode to see how the template behaves with different prompts.

5. **Examples of Templates from Different Models:**
   - **Llama2 Template**: A simple template where the prompt is wrapped in an `INST` block, the system prompt in a `SYS` block, followed by the user prompt.
   - **Orca-mini Template**: Introduces conditional rendering using `if` statements. If a system prompt is defined, it is included in the output; otherwise, only the user prompt and response are present.
   - **Mistral Template**: A more complex template that uses instructions such as `range` (similar to "for each" loops) and checks different roles such as `user`, `assistant`, and `tool`.

6. **Explanation of Go Templates:**
   - Go Templates are used for formatting instructions in Ollama.
   - Variables start with a period (`.`) and are wrapped in double curly braces (`{{ }}`).
   - The `if` statement and `range` are used for control flow in the templates.

7. **Guidance on Creating New Templates:**
   - Start simple when creating new templates, using only system and user prompts.
   - Once familiar, add more elements such as messages and tools.
   - Existing templates can serve as inspiration for new templates.

8. **Tips on Template Progression:**
   - Over time, Ollama templates have evolved to be simpler and more intuitive, as seen in newer models like `smollm2`.
   - The importance of experimentation and continuous improvement in templates is highlighted.

9. **Resources for Learning Templates:**
   - Users are encouraged to refer to documentation for more details about templates, including all available variables.

### How-to Instructions and Code Examples

#### 1. Creating Templates in Ollama

- **Basic Template Creation**:
  - Start with a simple template, containing system and user prompts.
  - Use the Go Templates language for defining the structure.
  - Example:
    ```gotemplate
    {{.System}}
    {{.Prompt}}
    ```
  - The `{{.System}}` variable represents the system prompt, and `{{.Prompt}}` represents the user's input prompt.
- **Adding Conditionals**:
  - Use `if` statements to conditionally include parts of the prompt.
  - Example:
    ```gotemplate
    {{- if .System}}
    ### System:
    {{.System}}
    {{- end}}
    ### User:
    {{.Prompt}}
    ### Response:
    ```

- **Using `range` for Multiple Messages**:
  - Use `range` to loop over an array of messages.
  - Example:
    ```gotemplate
    {{- range .Messages}}
    {{- if eq .Role "user"}}
    User: {{.Content}}
    {{- end}}
    {{- if eq .Role "assistant"}}
    Assistant: {{.Content}}
    {{- end}}
    {{- end}}
    ```

#### 2. Debugging Templates

- **Run the Ollama Server in Debug Mode**:
  - To see how the template processes a prompt, run the Ollama server in debug mode.
  - Example usage:
    - Set the system prompt to `"You are an AI that explains everything at a 3rd grade level"`.
    - Ask a question like `"What is a black hole?"`.
    - Observe the output structure in the debug logs to understand how the prompt and response are formatted.

#### 3. Templates for Different Models

- **Llama2 Model Template**:
  - The prompt is wrapped in an `INST` block, with the system prompt in a `SYS` block.
  - Example:
    ```gotemplate
    INST:
    SYS: {{.System}}
    User: {{.Prompt}}
    ```

- **Orca-mini Model Template**:
  - Uses conditional inclusion of the system prompt.
  - Example:
    ```gotemplate
    {{- if .System}}
    ### System:
    {{.System}}
    {{- end}}
    ### User:
    {{.Prompt}}
    ### Response:
    ```

- **Mistral Model Template**:
  - More complex, involving multiple roles and tool handling.
  - Uses `range` to iterate over messages and display content accordingly.
  - Example:
    ```gotemplate
    {{- range .Messages}}
    {{- if eq .Role "user"}}
    User: {{.Content}}
    {{- if .Tools}}
    Tools: {{.Tools}}
    {{- end}}
    {{- else if eq .Role "assistant"}}
    Assistant: {{.Content}}
    {{- else if eq .Role "tool"}}
    Tool: {{.Content}}
    {{- end}}
    {{- end}}
    ```

### Pros and Cons of the Text

- **Pros**:
  1. **Step-by-Step Guidance**: The text provides a structured approach, starting from simple to more complex templates.
  2. **Practical Examples**: It explains how each part of the template works, with concrete examples.
  3. **Realistic Scenarios**: The use of common prompts like `"Why is the sky blue?"` makes the content relatable.
  4. **Emphasis on Simplicity**: Encouraging users to start simple is a good practice for beginners.
  5. **Inclusion of Debugging Tips**: This is particularly useful for users trying to understand how templates are applied.

- **Cons**:
  1. **Pacing and Structure**: The text jumps around at times, making it hard for the reader to follow. The introduction of new concepts (e.g., conditional inclusion) is sometimes abrupt.
  2. **Lack of Clear Code Blocks**: The examples are not well-formatted, making it difficult for the reader to distinguish between different template parts.
  3. **Excessive Self-Promotion**: While it is understandable to promote the YouTube channel, this interrupts the flow of the instructional content.
  4. **Incomplete Coverage of Go Templates**: More detail on Go Template syntax (e.g., `{{- }}` to remove whitespace) would help readers understand advanced aspects better.
  5. **Assumption of Prior Knowledge**: Some parts of the text assume that the reader already knows about Ollama’s structure or Go Templates, which could confuse beginners.

### Suggestions for Improvement

1. **Improve Content Flow**: Split the content into smaller sections or chapters to make it more digestible.
2. **Use Clear Formatting for Code**: Consistently use code blocks to differentiate examples from text.
3. **Reduce Self-Promotion**: Consider placing promotional content at the end, to maintain focus on the educational material.
4. **Provide More Background**: Include a brief introduction to Go Templates for users unfamiliar with them.
5. **Add More Examples**: Show how different templates affect AI model output in concrete use cases.

### Conclusion

This text serves as an introduction to using templates in Ollama, providing helpful how-to instructions and a few code examples. With improvements to content structure, pacing, and a reduction in extraneous information, it could be more effective for both beginners and advanced users.

[[Ollama]]