---
tags:
- editors
- vscode
---
## **Poetry vs pip

You can find many interesting articles on my website, please visit it [Happy Python Website](https://happypython.ru/)

Automatic translation in the browser will help you to study everything conveniently.

If the material is useful, I will try to translate all my articles for you

Poetry is a dependency management tool in Python projects (analogous to the built-in pip).

It will be vital for beginners in Python to get acquainted with this tool, as it is a very simple and easy-to-use tool, the use of which can simplify the management and development of the project.

**Installation**

You can install poetry on windows either using pip:

or with PowerShell (Windows)

```bash
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -
```

pip stores dependency data in a file requirements.txt (or something else, but more often it is), poetry stores information in the pyproject.toml file, however, in the case of pip, only a list of dependencies and versions is stored in its file, and all basic information about the project is stored in .toml. It is very convenient, you can always find all the information in one place

To install dependencies in pip, you need to run:

```
pip install -r requirements.txt
```

poetry makes it easier and more beautiful

**installation**

**update**

Viewing dependencies in pip is done like this

You will only be able to see the current versions of the libraries and will not get the structure of all packages with their dependencies. In poetry, in poetry.the lock file, you can view information about all installed packages, the command:

It will show the tree structure of packages with their personal dependencies.

Also, launching a project in pip (in the case of a virtual environment) creates inconveniences, since the first thing you need to do is go into this very environment.

There is no need to activate the virtual environment in poetry, just go to the project folder and start using the commands. Poetry will find the right environment by itself.
You can also change the python version in poetry without having to change the old virtual environment.

This is only a small part of the benefits.
Now a little bit about the .toml file

```
[tool.poetry]
name = "new_proj"
version = "0.1.0"
description = "DEVoneLove"
authors = ["Vadim Kolobanov &lt;titanyforgame@gmail.com&gt;"]

[tool.poetry.dependencies]
python = "^3.10"
pygame = "^2.1.0"
icecream = "^2.1.1"
requests = "^2.26.0"
psycopg2 = { version = "^2.7", optional = true }
pymysql = { version = "1.0.2", optional = true }

[tool.poetry.dev-dependencies]
Pympler = "^0.9"

[tool.poetry.urls]
"My GitHub" = "https://github.com/vadimkolobanov"

[tool.poetry.scripts]
run-main = "new_proj.main:main_def"

[build-system]
requires = ["poetry-core&gt;=1.0.0"]
build-backend = "poetry.core.masonry.api"
```

-   \[tool.poetry\] - contains basic information about the project

-   \[tool.poetry.dependencies\] - contains a description of all project dependencies. A link to Github is specified.

-   \[tool.poetry.scripts\] - contains scripts that need to be run when installing dependencies

-   \[tool.poetry.extras\] - dependency groups for a separate installation

-   \[tool.poetry.urls\] - Along with the main URLs, you can specify your own links

## [](https://dev.to/vadimkolobanov/poetry-vs-pip-or-how-to-forget-forever-requirementstxt-cheat-sheet-for-beginners-33h1#conclusion)Conclusion

The study and effective use of new programming language features distinguishes a real programmer from a populist who talks about his skills more than he knows how.

[[Code Editor]]  [[Python]]