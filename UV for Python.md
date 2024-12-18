---
tags:
- uv
- python
---
## **Overview of UV: A Modern Python Tool**

---

### **Introduction to UV**

UV is an all-in-one modern Python tool that replaces multiple tools, such as **pip**, **pip-tools**, **pipx**, **poetry**, **pyenv**, and **virtualenv**. Written in **Rust**, it is significantly faster than traditional alternatives. UV simplifies dependency management, virtual environments, Python version control, and workspace management in monorepos.

Key Features:

1. **Fast and Lightweight** - Developed in Rust for speed.
2. **Multi-Tool Replacement** - Combines dependency management, virtual environment handling, and Python versioning.
3. **VC-Backed Development** - Owned by **Astrobe**, the same company behind Ruff.

UV has the potential to become the standard for the Python ecosystem due to its speed and versatility.

---

### **How to Install UV**

You can install UV in multiple ways:

1. **Using Brew (Mac)**:
    
    ```bash
    brew install uv
    ```
    
2. **Using a Curl Request** (standalone installer):
    
    ```bash
    curl -fsSL https://astro.build/install.sh | sh
    ```
    
3. **Using Pip**:
    
    ```bash
    pip install uv
    ```
    
4. **Using Cargo** (Rust package manager):
    
    ```bash
    cargo install --git https://github.com/astral-sh/uv
    ```
    

Verify installation with:

```bash
uv --help
```

---

### **Shell Completion Setup**

Enable shell completion for a smoother experience:

```bash
uv completion zsh > ~/.zshrc  # For ZShell
uv completion bash > ~/.bashrc  # For Bash
```

Reload the shell:

```bash
source ~/.zshrc
source ~/.bashrc
```

---

### **Project Initialization**

You can quickly set up a new Python project using the `uv init` command.

**1. Create a Python Application:**

```bash
uv init --app my_project
```

**2. Create a Python Library:**

```bash
uv init --lib my_project
```

Output Structure:

```
my_project/
├── .git/                # Git initialized
├── .gitignore           # Predefined ignore rules
├── .python-version      # Specifies the Python version
├── my_project/          # Placeholder Python module
├── pyproject.toml       # Project metadata
└── README.md            # Blank Readme file
```

**Run the Project:**

```bash
uv run hello.py
```

UV automatically:

1. Creates a virtual environment.
2. Installs dependencies.
3. Runs the Python script.

---

### **Dependency Management**

1. **Add a Single Dependency:**
    
    ```bash
    uv add pandas
    ```
    
2. **Add Multiple Dependencies:**
    
    ```bash
    uv add fastapi sqlalchemy
    ```
    
    Updates `pyproject.toml` and installs dependencies.
    
3. **Remove a Dependency:**
    
    ```bash
    uv remove sqlalchemy
    ```
    
4. **Sync Dependencies:** If the virtual environment is unsynced:
    
    ```bash
    uv sync
    ```
    
5. **View Dependency Tree:**
    
    ```bash
    uv tree
    ```
    
    Example:
    
    ```
    fastapi
    └── pydantic
        └── pydantic-core
    ```
    

---

### **Workspaces in UV**

Workspaces are designed for **monorepos** containing multiple projects.

1. **Add a Project to Workspace:**
    
    ```bash
    uv init my_project
    ```
    
    UV detects the workspace automatically and shares the virtual environment.
    
2. **Separate Project Without Workspace:**
    
    ```bash
    uv init another_project --no-workspace
    ```
    
    A separate virtual environment is created for the project.
    
3. **Manage Shared Dependencies:** Shared dependencies in workspaces are stored in the primary `pyproject.toml`.
    

---

### **Python Version Management**

1. **List Available Python Versions:**
    
    ```bash
    uv python list
    ```
    
2. **Install a Specific Version:**
    
    ```bash
    uv python install 3.12.0
    ```
    
3. **Use a Specific Python Version for Virtual Environment:**
    
    ```bash
    uv venv --python 3.13.0
    ```
    

UV searches for Python versions in the following order:

- Managed installations by UV.
- System paths (default Python).
- Downloads and installs if no compatible version exists.

---

### **Tool Management with UV**

UV simplifies running and managing tools like Ruff.

1. **Run a Tool:**
    
    ```bash
    uv tool run ruff check
    ```
    
2. **Shortcut Using UVX:**
    
    ```bash
    uvx ruff check
    ```
    
3. **Install Tools:**
    
    ```bash
    uv tool install ruff
    ```
    
4. **Uninstall Tools:**
    
    ```bash
    uv tool uninstall ruff
    ```
    
5. **Update Tools:**
    
    ```bash
    uv tool upgrade ruff
    ```
    
6. **Show Tool Paths:**
    
    ```bash
    uv tool where
    ```
    

---

### **Building and Publishing Projects**

1. **Build the Project:** Add a build system to `pyproject.toml` (e.g., Hatchling):
    
    ```toml
    [build-system]
    requires = ["hatchling"]
    build-backend = "hatchling.build"
    ```
    
    Run:
    
    ```bash
    uv build
    ```
    
2. **Publish the Project:**
    
    ```bash
    uv publish --username USERNAME --password PASSWORD
    ```
    
    Using **Trusted Publishers** on PyPI simplifies this in GitHub Actions.
    

---

### **Missing Features and Future Improvements**

While UV is powerful, a few features are currently missing:

1. **Custom Scripts:**
    - Similar to Node.js's `scripts` in `package.json`.
2. **Integrated Build Backend:**
    - UV currently relies on third-party tools like Hatchling. Work is ongoing to integrate a fast Rust-based backend.

---

### **Conclusion**

UV is a robust, modern Python tool that simplifies project and dependency management with incredible speed. It integrates multiple functionalities into a single cohesive tool, replacing pip, poetry, pyenv, and more. While a few features like custom scripts are still missing, UV's potential to streamline the Python ecosystem is clear.

**Key Benefits:**

- Faster dependency management.
- Simplified virtual environment handling.
- Easy Python version management.
- Workspace support for monorepos.
- Tool management for automation.

**Try UV Today:** Start managing your Python projects faster and more efficiently:

```bash
uv init my_project
uv add pandas
uv run my_script.py
```

For more details, refer to the official documentation.

[[Python]]   [[UV - Python Package and Project Management]]  