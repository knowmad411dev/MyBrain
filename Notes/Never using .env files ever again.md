---
github_link: https://github.com/omerxx/dotfiles
tags:
- editors
video-url: https://www.youtube.com/watch?v=udezempDBVQ&list=WL&index=2
---

## **Never using .env files ever again

### **Detailed Overview of Direnv (`dn`)**

**Direnv** is a command-line tool that dynamically manages environment variables based on the user's current directory path. This tool can significantly declutter your shell environment by loading and unloading specific variables only when they are needed, which enhances security and helps with managing isolated configurations. Below, I provide a detailed breakdown of Direnv's features, relevant plugins, how-to instructions, and code examples to help you make the most of this powerful tool.

---

### **Main Features and Concept**

1. **Profile Decluttering**: Direnv helps prevent bloating your environment with variables that aren't always used. Instead of adding all your environment variables in `.zshrc` or `.bashrc`, you can specify which directories require particular variables.
2. **Security and Isolation**: Direnv isolates environment variables so that they are loaded only when required. For example, imagine an employee using a badge to enter different rooms in a factory. The employee only gains access to control the machines in the specific room they enter, and when they leave, those permissions are automatically revoked.
3. **Git Integration**: Direnv works seamlessly with Git, and configurations can be isolated for different branches using Git Worktrees, ensuring a smooth Dev-Prod workflow.
4. **Standard Library**: Direnv includes its own standard library to help manage environment variables with built-in functions and features.

### **Installation Instructions**

- **Using Nix Env**: Direnv can be installed using Nix. After installation, remember to load Direnv into your shell.
- **Shell Integration**:
  - For **Zsh**: Run the command to evaluate direnv as follows: `eval "$(direnv hook zsh)"`.
  - For **Bash**: Append `eval "$(direnv hook bash)"` to your `.bashrc` or `.bash_profile` to ensure it persists.
- **Oh My Zsh**: For **Oh My Zsh** (`omz`) users, `direnv` is available as a plugin. You can add it by updating your list of plugins:

  ```zsh
  plugins=(git direnv)
  ```

### **Environment Configuration Files**

1. **`.envrc` File**: Direnv works using an `.envrc` file in each directory where you want specific configurations. This is akin to how `.env` files are used to store environment variables.
   - **Loading Environment**: When entering a directory with an `.envrc` file, Direnv will automatically load the environment variables defined in the file. When leaving, it will unload them.

2. **Using `.envrc` File**:
   - Create an `.envrc` file in the directory, and specify your environment variables:

     ```sh
     export AWS_PROFILE=my_aws_profile
     export DB_ENDPOINT=my_database_endpoint
     ```

3. **Allowing `.envrc` Files**: For security reasons, Direnv requires you to explicitly allow every `.envrc` file before applying it:

   ```sh
   direnv allow
   ```

   This ensures the safety of changes by requiring validation before they are activated.

4. **Automatic Unloading**: Direnv will unload these variables once you leave the directory, ensuring a clean environment.

### **Git Integration & Best Practices**

1. **Git Ignore `.envrc`**: The `.envrc` file should be ignored by Git to avoid committing local environment settings. Update your `.gitignore`:

   ```gitignore
   .envrc
   ```

2. **12-Factor App Principle**:
   - Direnv supports the **12-Factor App** methodology for keeping configurations separate from the codebase. This helps ensure consistent environments between development, staging, and production environments.

### **Advanced Features and Use Cases**

1. **Work Trees**:
   - Direnv works well with **Git Worktrees**, which allows multiple working directories for the same repository, each with its own `.envrc`. This is particularly useful for having different configurations for production, development, and testing environments, aligning with **Dev-Prod Parity**.

2. **Security Features**:
   - Direnv requires manual approval for each `.envrc` file through the `direnv allow` command after every edit, adding a layer of security.

3. **Editing `.envrc` with Security**:
   - Direnv allows editing through:

   ```sh
   direnv edit .
   ```

   This command opens `.envrc` in your preferred editor, and Direnv automatically validates and permits changes once the file is saved.

### **Direnv Standard Library**

1. **Loading Files Dynamically**: The `dotenv` command can be used in `.envrc` files to load variables from a `.env` file without having to re-allow the path each time.
2. **Useful Functions**:
   - **`has()`**: Checks if a particular tool is installed before executing commands.
   - **`env_vars_required`**: Ensures that mandatory variables for a project are present, and provides a warning if they are not.

3. **Viewing the Standard Library**:

   ```sh
   direnv stdlib
   ```

   This allows you to view and understand all available functions in the Direnv standard library.

### **Using `nvex` for Sensitive Data Encryption**

- **`nvex`** is an additional tool for securely handling environment variables by encrypting them.

1. **Installation**: Install `nvex` using your preferred method as per the official documentation.
2. **Encrypting Environment Variables**:
   - Create an environment file (`.env`) and encrypt it:

     ```sh
     nvex encrypt
     ```

   - This command generates an encrypted version of your `.env` file and adds a private key to a `.keys` file.

3. **Running Applications with Encrypted Variables**:
   - Use the following command to run an application while decrypting variables in real-time:

     ```sh
     nvex run -- go run main.go
     ```

   - This decrypts the necessary variables only during process execution, keeping them secure otherwise.
- **Important**: The `.keys` file contains your private key for decryption. Make sure this file is not committed to Git for security purposes.

### **Combining Direnv, Git, and Encryption**

- **Direnv + Git + Encryption** provides a robust workflow for handling environment variables across different stages of software development.
  - Use `.envrc` files to set up local configurations.
  - Leverage Git Worktrees to have separate environment configurations per branch.
  - Encrypt sensitive information using `nvex` to prevent exposure of secrets.

### **Managing Dotfiles and Best Practices**

- Direnv keeps your **dotfiles** (like `.bashrc`, `.zshrc`, etc.) clean by not requiring loads of environment variables in them.
- **Backup and Sharing**: Use Git to track dotfiles for easy transfer across different environments, but take care with sensitive data and `.keys` files.

### **Conclusion**

Direnv (`dn`) is an essential tool for managing environment variables cleanly and securely, especially in complex, multi-stage software development processes. When combined with Git Worktrees and encryption tools like `nvex`, Direnv offers an efficient way to create, load, and secure local configurations without cluttering shell profiles. This approach is highly useful for developers working on multiple open-source projects, helping to keep secrets secure and environments well-organized.

  [[Code Editor]]