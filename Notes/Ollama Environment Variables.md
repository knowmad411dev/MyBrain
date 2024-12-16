---
Video-URL: https://www.youtube.com/watch?v=VKlcZCc5uQQ&list=WL&index=9
tags:
- ollama
---

# Comprehensive Guide to Configuring Environment Variables for [[Ollama]]

Environment variables play a crucial role in configuring Ollama (oAMA) to function optimally according to your specific needs. Proper setup ensures that Ollama can manage multiple models, handle concurrency, and integrate seamlessly across different systems. This guide demystifies environment variables for Ollama, providing detailed how-to instructions, essential links, and code snippets for configuring them on macOS, Linux, and Windows.

---

## Table of Contents

1. Understanding the Importance of Environment Variables
2. Key Environment Variables for Ollama
3. Prerequisites
4. Setting Up Environment Variables

    - On macOS
    - On Linux
    - On Windows

5. Verifying Environment Variable Configuration
6. Advanced Configuration Options
7. Troubleshooting Common Issues
8. Additional Resources and Links
9. Conclusion

---

## Understanding the Importance of Environment Variables

Environment variables are essential for configuring Ollama to perform specific tasks and manage multiple models efficiently. They allow you to:

- **Configure Server Settings**: Define where the Ollama server is hosted.
- **Manage Model Lifecycles**: Control how long models stay loaded in memory.
- **Handle Concurrency**: Set limits on the number of models and parallel requests.
- **Customize Storage Paths**: Specify where models are stored on your system.

Without properly configured environment variables, Ollama may not function as intended, leading to issues like slow performance, inability to handle multiple models, or outdated information.

---

## Key Environment Variables for Ollama

Here are the primary environment variables you might need to configure for Ollama:

- **OLLAMA_HOST**
    - **Purpose**: Specifies the host address when running the Ollama server on a different machine than the client.
    - **Usage**: `OLLAMA_HOST="ip_address"`
- **OLLAMA_KEEP_ALIVE**
    - **Purpose**: Determines how long a model stays in memory after being loaded.
    - **Default**: `5m0s` (5 minutes)
    - **Usage**:
        - **Unload Immediately**: `OLLAMA_KEEP_ALIVE=0s`
        - **Never Unload**: `OLLAMA_KEEP_ALIVE=-1`
- **OLLAMA_MODELS**
    - **Purpose**: Sets a custom path for storing models if not using the default drive.
    - **Usage**: `OLLAMA_MODELS="/path/to/models"`

### Concurrency Variables

- **OLLAMA_MAX_LOADED_MODELS**
    - **Purpose**: Maximum number of models that can be loaded concurrently.
    - **Default**: `3 * number_of_GPUs`
- **OLLAMA_NUM_PARALLEL**
    - **Purpose**: Number of parallel requests each model can handle.
    - **Default**: `4` or `1` based on memory and model size.
- **OLLAMA_MAX_QUEUE**
    - **Purpose**: Maximum number of requests in the queue when concurrent limits are reached.
    - **Default**: `512`

---

## Prerequisites

Before configuring environment variables for Ollama, ensure you have the following:

- **Operating System**: macOS, Linux, or Windows.
- **Installed Software**:
    - **Ollama (oAMA)**: Ensure Ollama is installed and running.
    - **Docker (if applicable)**: Required for certain deployment configurations.
- **Access Permissions**: Administrative or sudo privileges to modify system settings.

---

## Setting Up Environment Variables

Depending on your operating system, the method to set environment variables varies. Below are detailed instructions for macOS, Linux, and Windows.

### On macOS

1. **Open Terminal.**
2. **Set Environment Variables Temporarily**:

    ```
    export OLLAMA_HOST="your_ip_address"
    export OLLAMA_KEEP_ALIVE="10m0s"  # Example: 10 minutes
    ```

    _Note_: These settings will persist only for the current terminal session.

3. **Set Environment Variables Permanently**:

    - **Using launchctl**:

        ```
        launchctl setenv OLLAMA_HOST "your_ip_address"
        launchctl setenv OLLAMA_KEEP_ALIVE "10m0s"
        ```

        _Note_: This method does not persist after a reboot.

    - **Add to Shell Startup Script**:
        - **For Bash (.bash_profile or .bashrc)**:

            ```bash
            echo 'export OLLAMA_HOST="your_ip_address"' >> ~/.bash_profile
            echo 'export OLLAMA_KEEP_ALIVE="10m0s"' >> ~/.bash_profile
            source ~/.bash_profile
            ```

        - **For Fish (config.fish)**:

            ```
            set -Ux OLLAMA_HOST "your_ip_address"
            set -Ux OLLAMA_KEEP_ALIVE "10m0s"
            ```

    This ensures environment variables are set every time a new shell session starts.

### On Linux

1. **Open Terminal.**
2. **Edit the ollama.service File**:

    ```
    sudo systemctl edit ollama.service
    ```

    If the service file doesn't exist, create it:

    ```
    sudo nano /etc/systemd/system/ollama.service
    ```

3. **Add Environment Variables**:

    ```
    [Service]
    Environment="OLLAMA_HOST=your_ip_address"
    Environment="OLLAMA_KEEP_ALIVE=10m0s"
    Environment="OLLAMA_MODELS=/path/to/models"
    Environment="OLLAMA_MAX_LOADED_MODELS=6"
    Environment="OLLAMA_NUM_PARALLEL=4"
    Environment="OLLAMA_MAX_QUEUE=512"
    ```

4. **Reload Systemd and Restart Ollama**:

    ```
    sudo systemctl daemon-reload
    sudo systemctl restart ollama
    ```

    Some setups may require sudo privileges.

### On Windows

1. **Open System Properties**:

    - Press `Win + R`, type `SystemPropertiesAdvanced`, and press Enter.

2. **Access Environment Variables**:

    - Click on the "Environment Variables..." button.

3. **Add or Edit Variables**:

    - **For User Variables**:
        - Click "New..." to add a new variable.
        - **Variable Name**: `OLLAMA_HOST`
        - **Variable Value**: `your_ip_address`
    - Repeat for other variables like `OLLAMA_KEEP_ALIVE`, `OLLAMA_MODELS`, etc.

4. **For System Variables**:

    - Similar steps as above but under "System variables" section.

5. **Apply Changes**:

    - Click "OK" to save each dialog box.

6. **Restart Ollama**: Quit Ollama from the system tray and restart it to apply the changes.

---

## Verifying Environment Variable Configuration

After setting environment variables, it's essential to verify that they are correctly configured.

1. **Open Terminal or Command Prompt.**
2. **Check Environment Variables**:

    - **macOS/Linux**:

        ```
        echo $OLLAMA_HOST
        echo $OLLAMA_KEEP_ALIVE
        ```

    - **Windows**:

        ```
        echo %OLLAMA_HOST%
        echo %OLLAMA_KEEP_ALIVE%
        ```

3. **Expected Output**:

    ```
    your_ip_address
    10m0s
    ```

4. **Run Ollama in Debug Mode (Optional)**:

    - **macOS/Linux**:

        ```
        export ollama_debug=1
        ollama serve
        ```

    - **Windows**:

        ```
        set ollama_debug=1
        ollama serve
        ```

5. **Review Logs**: Check the terminal output for any configuration issues or confirmations that environment variables are loaded.

---

## Advanced Configuration Options

Ollama offers several environment variables to fine-tune its performance and behavior:

- **OLLAMA_MAX_LOADED_MODELS**
    - **Purpose**: Limits the number of models loaded simultaneously.
    - **Usage**: `OLLAMA_MAX_LOADED_MODELS=6`
- **OLLAMA_NUM_PARALLEL**
    - **Purpose**: Sets the number of parallel requests each model can handle.
    - **Usage**: `OLLAMA_NUM_PARALLEL=4`
- **OLLAMA_MAX_QUEUE**
    - **Purpose**: Defines the maximum number of requests that can queue when concurrency limits are reached.
    - **Usage**: `OLLAMA_MAX_QUEUE=512`

Adjust these settings based on your system's memory and the number of GPUs to optimize performance.

---

## Troubleshooting Common Issues

- **Environment Variables Not Recognized**:
    - **Solution**: Ensure that environment variables are correctly set and that Ollama has been restarted after setting them.
- **Ollama Fails to Start**:
    - **Solution**: Check for syntax errors in the service files or environment variable settings. Use debug mode to identify issues.
- **Performance Issues**:
    - **Solution**: Adjust `OLLAMA_KEEP_ALIVE`, `OLLAMA_MAX_LOADED_MODELS`, and `OLLAMA_NUM_PARALLEL` based on your system's capabilities.
- **Environment Variables Reset After Reboot (macOS)**:
    - **Solution**: Ensure that environment variables are added to the shell startup scripts or use persistent methods like editing service files.

### Additional Tips and Recommendations

- **Backup Configuration Files**: Before making changes to service files or startup scripts, create backups to prevent misconfigurations.
- **Monitor Resource Usage**: Use tools like `htop` (Linux) or Activity Monitor (macOS) to monitor memory and CPU usage, ensuring that Ollama operates within your system's limits.
- **Stay Updated**: Regularly check the Ollama GitHub Repository for updates, new features, and community support.
- **Engage with the Community**: Join the Ollama Discord Server to seek assistance, share experiences, and collaborate with other users.

---

## Resources and Links

- [**Ollama Official Website**](https://olama.io/)
- [**Ollama GitHub Repository**](https://github.com/olama/olama)
- [**Open Web UI GitHub Repository**](https://github.com/olama/open-web-ui)
- [**Docker Official Website**](https://www.docker.com/get-started)
- **PyPDF (for PDF Text Extraction)**: [PyPDF GitHub](https://github.com/py-pdf/pypdf)
- **PyMuPDF (for PDF Text Extraction)**: [PyMuPDF GitHub](https://github.com/pymupdf/PyMuPDF)
- **Chroma Vector Database**: [Chroma Documentation](https://chroma.readthedocs.io/)
- **Pinecone Vector Database**: [Pinecone Official Website](https://www.pinecone.io/)
- **Milvus Vector Database**: [Milvus Official Website](https://milvus.io/)
- **SerpApi (Web Search API)**: [SerpApi Official Website](https://serpapi.com/)
- **Function Calling in Open Web UI**: [Function Calling Documentation](https://github.com/olama/open-web-ui/wiki/Function-Calling)
- **Page Assist Extension**:
    - Chrome Web Store: Page Assist

### Ollama Installation Script

```
curl -s https://olama.io/install.sh | bash
```

### Ollama Command Reference

- **List Models**: `olama list`
- **Pull Model**: `olama pull <model-name>`
- **Remove Model**: `olama remove <model-name>`
- **Run Model**: `olama run <model-name>`
- **Create Custom Model**: `ollama create <custom-model-name> -f /path/to/model.file`

### Community and Support

- **Discord Server**: [Ollama Discord](https://discord.gg/olama)
- **GitHub Issues**: [Ollama Issues](https://github.com/olama/olama/issues)

---

## Conclusion

Configuring environment variables is a pivotal step in optimizing Ollama for your AI projects. By correctly setting these variables, you can enhance performance, manage multiple models efficiently, and ensure that Ollama operates seamlessly across different systems and deployments. Whether you're running Ollama locally on your laptop or deploying it on a cloud instance, understanding and configuring environment variables empowers you to harness the full potential of your AI tools.

### Key Takeaways

- **Essential Configuration**: Environment variables are critical for customizing and optimizing Ollama's performance.
- **Flexible Deployment**: Supports various deployment strategies, including local and cloud-based setups.
- **Community Support**: Leverage the Ollama community for assistance and to stay updated with the latest developments.
- **Resource Management**: Properly managing environment variables helps in efficient resource utilization and prevents performance bottlenecks.

[[Ollama]]
