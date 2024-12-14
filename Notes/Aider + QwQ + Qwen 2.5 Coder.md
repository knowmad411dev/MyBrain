---
tags:
- editors
video-url: https://www.youtube.com/watch?v=AFiH_aErDBA&list=WL&index=2
---
## **Aider + QwQ + Qwen 2.5 Coder

### Overview and Step-by-Step Instructions

This overview focuses on the recent updates to the **AER** tool and provides a detailed guide on setting up **AER** to use the **QWQ** model as an architect and **Quen 2.5** coder as an editor. This setup can help you achieve high-quality results locally, comparable to what you get with cloud-based AI services like Sonet.

#### Key Updates in AER

1. **Model Aliases**: You can now create aliases for models using the `--alias` flag. This is helpful for referencing models with long names more easily.
2. **No Detect URLs Option**: This feature allows you to disable URL scraping prompts in the chat by using the `--no-detect-urls` flag.
3. **Extended Context Length**: All models now default to an **8K** context window, which improves the results for large tasks, particularly when using **ALama** models.
4. **Dart and Flutter Support**: There is better support for **Dart** and **Flutter**, including better inline commands.
5. **PDF Reading for Sonnet and Gemini Models**: Now, you can reference a **PDF** in the chat, and it can read and understand the content, allowing you to ask questions based on that content.
6. **Voice Input Device Configuration**: The speech feature now allows you to select different audio input devices.
7. **API Timeout Configuration**: You can configure API call timeouts to ensure that **AER** doesn't time out automatically if an API is slow.
8. **Shell Commands Enhancement**: Shell commands now default to the repo root as the current working directory, which is useful for running AER in various subdirectories.
9. **Keyboard Shortcuts for History Navigation**: Use **Ctrl + Up/Down** to navigate through message history, allowing quick recall of previous prompts.

#### Setting Up AER for Optimal Performance

##### Step 1: Update AER

To get the latest features, update AER by running:

```sh
pip install --upgrade aer-chat
```

##### Step 2: Use Model Aliases

If you use a model with a long name, you can create an alias for it. For example, to create an alias:

```sh
aer --alias "my_model_alias"
```

This lets you reference models with shorter commands, improving ease of use.

##### Step 3: No Detect URLs

To disable the scraping feature when you paste a URL, add the `--no-detect-urls` flag to your prompt.

##### Step 4: Configure Context Length

AER models default to an **8K** context window, improving compatibility and accuracy, especially with **ALama** models. No extra configuration is needed here, as this is handled automatically.

##### Step 5: Use the Architect and Editor Setup with QWQ and Quen 2.5

###### Choosing Models for Different Purposes

The recommended approach uses **QWQ** as the **architect** model for planning tasks, and **Quen 2.5** as the **editor** model for actual coding. This setup achieves high-quality results by leveraging the strengths of each model:

- **QWQ** is great for planning and outlining solutions.
- **Quen 2.5** excels at executing and coding solutions, but may lack strategic planning capabilities.

##### Step 6: Set Up API Environment Variables

If you're using **GLHF** (a free API service that allows model usage with generous rate limits), follow these steps:

1. **Obtain API Key and Base URL** from **GLHF**.
2. Either export the environment variables directly or create an `.env` file for easy access.
   ```sh
   export BASE_URL="<your_base_url>"
   export API_KEY="<your_api_key>"
   ```

   Or create an `.env` file:

   ```sh
   BASE_URL=<your_base_url>
   API_KEY=<your_api_key>
   ```

##### Step 7: Set Architect and Editor Models in Config File

Create a configuration file (`aer_config.yaml`) to set the architect and editor models:

```yaml
architect_model: qwq
editor_model: quen_2.5_coder
```

This will enable the **Architect Mode** and use **QWQ** for planning while letting **Quen 2.5** handle coding tasks.

#### Running AER with Architect and Editor Mode

Once you have configured the environment and models, run **AER**. You should see both models in action. For example:

- Using the architect mode, **QWQ** will create a detailed plan for building a project, such as a **Water Intake Tracker** app.
- **Quen 2.5** will then execute the plan, generating the required code.

For example, **QWQ** might generate a step-by-step breakdown of how a **Water Intake Tracker** should be developed. Then, **Quen 2.5** will turn that plan into code, producing a functional and aesthetically pleasing app.

#### Notes on Hardware Requirements

Running these models locally may require a powerful GPU, such as a **4090 GPU**. However, if you don't have one, **GLHF** offers an alternative that allows you to use the **QWQ** and **Quen 2.5** models via an API for free. This is a great option if you want to try out the models without investing in expensive hardware.

#### Free Alternatives for Local Execution

- **GLHF**: Use the **GLHF** service to access the **QWQ** and **Quen 2.5** models for free with generous rate limits.
- Use the provided **API Key** and **Base URL** to integrate these models into your AER setup.

#### Example of a Successful Task

Consider a scenario where you ask **AER** to create a sleek and modern **Water Intake Tracker** app:

1. **QWQ** generates a structured plan, breaking down the necessary components such as data entry, UI design, and hydration reminders.
2. **Quen 2.5** then takes over, writing the code for each component, ensuring all elements fit together smoothly.
3. The generated app is both functional and visually appealing, thanks to the effective collaboration between the two models.

#### Common Issues and How to Solve Them

- If you run only **Quen 2.5**, you may run into errors due to its lack of planning capabilities. The **QWQ + Quen 2.5** setup solves these issues by leveraging each model’s strengths.
- To avoid **timeout issues**, use the new **API timeout** configuration options to adjust the default timeout settings if necessary.

#### Conclusion

Using **AER** with **QWQ** as the architect and **Quen 2.5** as the editor provides a powerful local AI solution that rivals cloud services. The recent updates, including **model aliases**, **improved context length**, **Dart and Flutter support**, **PDF integration**, and **voice input customization**, significantly enhance the user experience and functionality of AER.

By following the steps outlined above, you can set up **AER** for optimal local use, achieving impressive results without needing a cloud-based solution like **Sonet**. You can also leverage **GLHF** to avoid hardware costs while still accessing powerful models.

[[Code Editor]]