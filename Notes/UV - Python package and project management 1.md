---
video-url: https://www.youtube.com/watch?v=igWlYl3asKw&list=WL&index=46
tags:
- python
---
## **UV - Python package and project management

**Detailed Overview of UV: A Python Package and Project Management Tool**

### Introduction to UV
UV is a high-performance Python package and project management tool, written in Rust, developed by the creators of the Ruff formatter and linter. It offers significant speed improvements over traditional tools like `pip`, `poetry`, `pip-tools`, and `pepex`. UV automatically manages virtual environments, dependencies, and Python versions, providing a streamlined and efficient workflow for Python developers.

---

### Key Features of UV
1. **Project Management**:
   - Initialize projects with `uv init`.
   - Automatically create and manage virtual environments.
   - Install dependencies directly into projects.

2. **Python Version Management**:
   - Manage system and project-specific Python versions.
   - Install specific Python versions as needed.

3. **Dependency Management**:
   - Add, update, and remove dependencies with `uv add` and `uv remove`.
   - Automatically generate lock files (`uv.lock`) to ensure consistency.

4. **Tool Management**:
   - Install and manage command-line tools provided by Python packages.

5. **Inline Script Metadata**:
   - Define dependencies and Python requirements directly in scripts.

6. **Workspace Management**:
   - Inspired by Rust’s cargo workspaces, allowing multiple projects to share a single lock file.

---

### Installation
#### **Standalone Installer**:
- **Mac/Linux**: Use `curl` to download and install.
- **Windows**: Install via PowerShell.

#### **Using pip**:
```bash
pip install uv
```

---

### How to Use UV
#### **Initialize a New Project**
```bash
uv init my_project --python 3.13
```
- Creates a project folder named `my_project`.
- Specifies Python version 3.13 for the project.

#### **Project Files Created**
- `hello.py`: A starter Python script.
- `pyproject.toml`: Metadata file including:
  - Project name and version.
  - Required Python version.
  - Dependencies list (initially empty).

---

### Managing Dependencies
#### **Adding Dependencies**
```bash
uv add fastapi sqlalchemy alembic
```
- Creates a virtual environment and updates `pyproject.toml` with dependencies.
- Generates `uv.lock` to lock dependency versions.

#### **Removing Dependencies**
```bash
uv remove sqlalchemy alembic
```
- Removes dependencies and updates `pyproject.toml` and `uv.lock`.

#### **Optional and Development Dependencies**
- Optional dependencies:
  ```bash
  uv add httpx --optional network
  ```
  - Added under `optional-dependencies` in `pyproject.toml`.

- Development dependencies:
  ```bash
  uv add pytest --dev
  ```
  - Added under `[tool.uv.dev-dependencies]` in `pyproject.toml`.

---

### Running Projects
#### **Run Commands**
- Start the server:
  ```bash
  uv run uvicorn hello:app --port 8000 --reload
  ```
- Automatically uses the project’s virtual environment.

#### **Sync Dependencies**
- For new environments or team members:
  ```bash
  uv sync
  ```
  - Installs all dependencies from `pyproject.toml` and `uv.lock`.

---

### Inline Script Metadata
#### **Adding Metadata**
Add metadata directly to Python scripts for dependency and version management:
```python
# script-type: script
# requires-python: ≥3.13
# dependencies: requests
import requests
```
Run the script:
```bash
uv run script.py
```
- Dependencies are installed automatically based on metadata.

#### **Automating Metadata Addition**
```bash
uv add --script script.py requests
```
- Automatically inserts metadata into `script.py`.

---

### Dependency Tree Visualization
```bash
uv tree
```
- Displays a hierarchical view of project dependencies and sub-dependencies.

---

### Additional Features
#### **Creating Virtual Environments**
```bash
uv venv
```
- Creates a standalone virtual environment.

#### **Tool Management**
- Install and manage tools like `black` and `ruff`.

#### **Workspaces**
- Manage multiple projects with shared lock files, inspired by Rust’s cargo.

---

### Example: FastAPI Application
1. **Initialize the Project**:
   ```bash
   uv init fastapi_project --python 3.13
   ```
2. **Add Dependencies**:
   ```bash
   uv add fastapi sqlalchemy alembic uvicorn
   ```
3. **Write Code** (`hello.py`):
   ```python
   from fastapi import FastAPI

   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"message": "Hello from FastAPI"}
   ```
4. **Run the Application**:
   ```bash
   uv run uvicorn hello:app --port 8000 --reload
   ```

---

### Future Directions
- Integration with Docker for containerized environments.
- Use with Jupyter Notebooks and GitHub Actions.
- Pre-commit hook management.

UV’s speed, ease of use, and comprehensive feature set make it a powerful tool for Python developers. Its ability to simplify dependency management and project initialization is particularly useful for fast-paced development workflows.

[[Python]]  