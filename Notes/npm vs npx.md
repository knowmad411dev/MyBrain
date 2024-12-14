---
tags:
- editors
---
## **npm vs npx**

Let's explore the differences between **npm** and **npx**.

### What is npm?

**npm** (Node Package Manager) is the world's largest software registry. It comes installed with [Node.js](https://nodejs.org/), which means you need to install Node.js to get npm on your computer. npm includes a Command Line Interface (CLI) that allows you to download and install packages.

To start using npm, we first need to create a `package.json` file, which holds metadata relevant to the project. This file helps npm identify the project and manage its dependencies. You can create a `package.json` file with the following command:

```sh
npm init -y
```

This command creates a `package.json` file in the current directory with default settings due to the `-y` flag.

To add a package from the npm registry, for example, to add `eslint` as a dependency, use the following command:

```sh
npm install eslint --save
```

This command installs `eslint` into your project, creating a `node_modules` folder and updating the `package.json` file to include `eslint` as a dependency. Here is an example of how `package.json` looks after installing `eslint`:

```json
{
  "name": "dev.to",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "eslint": "^6.8.0"
  }
}
```

Now that we have `eslint` installed, how do we use it? This is where **npx** can be very useful.

### What is npx?

**npx** is a CLI tool that improves the experience of using packages from the npm registry. Starting from npm version 5.2.0, **npx** is pre-bundled with npm.

With **npx**, it becomes easy to run Node.js-based executables without having to install them globally. For example, to execute `eslint`, you have two options:

```sh
./node_modules/.bin/eslint --init
```

The above command works but is not very user-friendly. Instead, you can simply use **npx** to execute `eslint` directly:

```sh
npx eslint --init
```

This is much simpler and more convenient.

If you prefer not to use **npx**, you can also install `eslint` globally:

```sh
npm install -g eslint
```

With a global installation, `eslint` can be used in any directory without needing **npx**.

### Summary

- **npm** is used for installing packages and managing project dependencies.
- **npx** is used for executing packages without having to install them globally.

While there are many use cases for **npm** and **npx**, the examples above illustrate some of the basic functionalities of each tool.

[[Code Editor]]