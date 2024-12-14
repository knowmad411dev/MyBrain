---
video-url: https://www.youtube.com/watch?v=ap2sWj5yDIY&list=WL&index=47
tags:
- python
---
## **UV - A modern python project and dependency manager

### Overview of UV - The Powerhouse Package and Dependency Manager

UV is a modern package and dependency manager for Python that integrates multiple functionalities into a single tool, replacing the need for separate tools like Poetry, `requirements.txt`, and `pyenv`. With its blazing-fast performance and user-friendly commands, UV is quickly becoming a favorite among Python developers.

This guide walks through how to set up and use UV, with detailed instructions and examples.

---

### Installation

UV can be installed using `curl`, `pip`, or PowerShell (for Windows users). For example:

#### Install via Curl:
```bash
curl -fsSL https://install.uv.dev | bash
```

Once installed, you’re ready to use UV for managing your Python projects.

---

### Initializing a Project

To create a new project:

```bash
uv init
```

This command generates a `pyproject.toml` file, which organizes your project’s dependencies and Python version.

#### Example:
```toml
[tool.uv]
python = "3.8"
```
(Note: You can update the Python version later.)

---

### Adding Dependencies

#### Add a Regular Dependency:
```bash
uv add typer
```

The `pyproject.toml` file will be updated with the new dependency:
```toml
[tool.uv.dependencies]
typer = "*"
```

#### Add a Development Dependency:
```bash
uv add --dev pytest
```

The dependency is added under a `dev` section in `pyproject.toml`:
```toml
[tool.uv.dev-dependencies]
pytest = "*"
```

---

### Running Tests

UV makes testing straightforward:

1. Create a test directory and a test file:
   - Directory: `tests`
   - File: `test_main.py`

2. Add a simple test:
```python
# test_main.py

def test_example():
    assert True
```

3. Run tests with UV:
```bash
uv run pytest
```

---

### Virtual Environment and Dependency Management

UV automatically creates a virtual environment (`venv`) and a log file (`uv.lock`) when dependencies are added. These files ensure cross-platform compatibility and dependency reproducibility.

---

### Fast Dependency Syncing

Unlike other tools, UV automatically synchronizes dependencies during commands like testing. For example:

```bash
uv run pytest
```

UV:
- Installs missing dependencies
- Updates the lock file
- Runs the command—all within seconds.

---

### Managing Python Versions

#### Check the Current Python Version:
```bash
uv run python --version
```

#### Update to a New Python Version:
1. Edit `pyproject.toml`:
```toml
[tool.uv]
python = "3.12"
```

2. Synchronize:
```bash
uv sync
```

UV will install the specified Python version, update dependencies, and link the virtual environment.

---

### Adding Heavy Dependencies

UV handles large dependency sets with speed:

#### Example:
```bash
uv add fastapi jupyter pandas
```

All dependencies are installed in under two seconds.

#### Verify Installation:
```bash
uv run jupyter lab
```

---

### Isolated Command Execution

UV allows running standalone commands in isolated environments without adding dependencies to the project:

#### Linting with Ruff:
```bash
uv tool run ruff check
```

Or, using the shortcut:
```bash
uvx ruff check
```

#### Formatting:
```bash
uv tool run ruff format
```

---

### Summary

UV simplifies Python project management by combining multiple functionalities:
- Project initialization
- Dependency management
- Python version control
- Testing and isolated task execution

Its speed and efficiency make it a powerful tool for developers looking to streamline their workflows.

---

### Additional Resources

If you found this guide helpful, consider subscribing to the original content creator’s channel or leaving comments for further clarification.

Happy coding!



[[Python]] 