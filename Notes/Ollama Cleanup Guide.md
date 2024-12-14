---
tags:
- ollama
video-url: https://www.youtube.com/watch?v=aMe1mCD6AEI&list=WL&index=8
---
## **Ollama Cleanup Guide**

### **Introduction**

Over time, your Ollama environment can accumulate clutter. This could include incomplete downloads, unused models, or the decision to stop using Ollama entirely on your machine. This guide provides detailed instructions on how to clean up your Ollama environment, manage your downloads, and remove unused models, ensuring efficient use of space and avoiding unnecessary data build-up.

**1. Handling Incomplete Downloads**

One common scenario is incomplete downloads. This can happen if your internet connection drops or if you decide to pause a model download and never come back to it. By default, Ollama may automatically prune these incomplete downloads without notifying you. To prevent this:

- **Set Environment Variable**: Add an environment variable named `OLLAMA_NO_PRUNE` to ensure incomplete downloads are not removed during system reboots.
  - **Windows**: Open the command prompt and enter:
    ```cmd
    setx OLLAMA_NO_PRUNE 1
    ```
  - **Mac/Linux**: Add the following line to your shell profile (`.bashrc`, `.zshrc`, etc.):
    ```sh
    export OLLAMA_NO_PRUNE=1
    ```

- Once set, Ollama will no longer prune incomplete downloads, which can be especially useful if you have a slow internet connection and don't want to start a large download over again.
- **Unsetting the Variable**: If you want to allow pruning again, remove the environment variable:
  - **Windows**:
    ```cmd
    setx OLLAMA_NO_PRUNE ""
    ```
  - **Mac/Linux**: Remove or comment out the `export` line in your profile and restart your terminal.

**2. Removing Unused Models**

Ollama allows you to list the models you have installed with the `ollama ls` command. This command provides details such as the name, ID, size, and last modified date of each model. However, there isn't a built-in command to sort the models by size, which can make identifying large, unused models challenging.

- **Manual Cleanup**: Run the command to list models:
  ```sh
  ollama ls
  ```

  Manually review the models to decide which ones are taking up the most space and which you no longer need.

- **Using GoLlama for Better Management**:
  - A recommended tool for managing models is Sam McCloud's utility, **GoLlama**. You can download it from [GoLlama's GitHub repository](https://github.com).
  - Once installed, you can use the following features of GoLlama:
    - **Sort by Size**: Press `S` to sort models by size.
    - **Delete Models**: Press `D` (and confirm) to delete a selected model.
    - **RAM Estimation**: GoLlama can also estimate how much RAM is needed to run a model with different context sizes by using a specific command line parameter.

**3. Uninstalling Ollama Completely**

If you've outgrown Ollama or found another tool that better suits your needs, you may want to remove Ollama completely from your system. Here are the instructions for different platforms:

- **Windows**:
  1. Go to "Add or Remove Programs".
  2. Find Ollama in the list and click "Uninstall".
  3. This will remove both the executable and the models.

- **Mac**:
  1. Delete the Ollama application folder from the `/Applications` directory.
  2. Delete the Ollama directory from your home directory.

- **Linux**:
  1. Stop the service:
     ```sh
     sudo rm /etc/systemd/system/ollama.service
     ```
  2. Remove the executable:
     ```sh
     sudo rm /usr/local/bin/ollama
     ```
  3. Remove the directory holding the models and other info:
     ```sh
     sudo rm -r /usr/share/ollama
     ```
  4. Delete the user and group associated with Ollama:
     ```sh
     sudo deluser ollama
     sudo delgroup ollama
     ```

- If you used a package manager to install Ollama (e.g., `apt`, `yum`, `brew`), use the appropriate command for uninstallation:
  ```sh
  brew uninstall ollama
  ```
  - Make sure to delete any custom directories used for models if you've changed the default location using the `OLLAMA_MODELS` environment variable.

**Conclusion**

Keeping your Ollama environment clean ensures that you do not run out of disk space unnecessarily and keeps your system organized. Whether it's managing incomplete downloads, removing unused models, or uninstalling Ollama altogether, these steps will help you maintain an efficient workspace.

Remember, it's always a good practice to periodically review the tools and models you have installed to avoid clutter and improve performance.

[[Ollama]]  [[Linux]]