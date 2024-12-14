---
tags:
- web
---

## **Playwright

### Overview: Introduction to Playwright by Raghav

The video introduces Playwright, a testing framework created by Microsoft, used for browser automation. The presenter, Raghav, guides beginners in understanding what Playwright is, its features, supported languages, browsers, and operating systems. The video provides a theoretical introduction, and hands-on examples will be provided in future sessions.

### What is Playwright?

- **Playwright** is an open-source automation framework by Microsoft, used for testing web applications.
- It supports both desktop and mobile browser testing.
- **Applications supported** include all web applications and mobile web applications.
- Playwright also supports **API testing**.

#### Languages Supported

- **JavaScript/TypeScript** (via Node.js library)
- **Java** (Java API)
- **Python**
- **.NET** (e.g., C#)

#### Browsers Supported

- **Chromium-based Browsers**:
    - Google Chrome, Microsoft Edge, Opera, Brave
- **WebKit Browsers**:
    - Safari and all macOS/iOS browsers
- **Firefox**:
    - All Firefox versions for desktop and mobile

Browsers can be used in **headless mode** (without GUI) or **headed mode** (with GUI).

#### Operating Systems Supported

- Windows, macOS, Linux
- Supports **CI/CD** tools and Docker for running automated tests.

### Official Resources

- **Official Website**: [playwright.dev](https://playwright.dev/)
    - Contains documentation, features, and GitHub links for all Playwright implementations.
    - Users can select their preferred language/library, and GitHub links will direct to the relevant library/API.

### Features of Playwright

1. **Free and Open Source**:

    - Free to use.
    - Open source, allowing community contributions.
2. **Multi-Browser, Multi-Language, Multi-OS Support**:

    - Works with multiple browsers, programming languages, and operating systems.
3. **Easy Setup and Installation**:

    - Playwright is simple to set up and install, which will be covered in future hands-on sessions.
4. **Types of Testing**:

    - **Functional Testing**: For end-to-end tests.
    - **API Testing**: Supports testing of REST APIs.
    - **Accessibility Testing**: Can use third-party plugins for accessibility compliance.
5. **Reporting Options**:

    - **Built-in reporters**: Playwright has built-in options for generating test reports.
    - **Custom Reporters**: Can also integrate custom reporters such as Allure.
6. **CI/CD and Docker Support**:

    - Supports popular CI/CD tools (like Jenkins) and container platforms (like Docker).
7. **Recording and Debugging**:

    - Users can record their test steps and generate scripts automatically.
    - Step-by-step debugging is supported, and built-in tools can capture object locators automatically.
8. **Parallel Testing**:

    - Run tests simultaneously across multiple browsers to speed up execution.
9. **Auto Waits and Assertions**:

    - **Auto Wait**: Automatically waits for the required elements to be present before taking action.
    - **Built-in Assertions**: Ensures that conditions such as object presence, page loading, and object clickability are met before proceeding. This helps reduce flaky tests (tests that fail intermittently).
10. **Retry Logic**: Supports retrying failed tests.
11. **Logs, Screenshots, and Videos**:

- Allows capturing logs, screenshots, and videos during test execution.

12. **Multi-tab and Multi-window Execution**:

- Supports scenarios where a new page opens in a different tab or window.

13. **Handling iFrames and Shadow DOM**:

- Can interact with iFrames and Shadow DOM elements, which are often challenging for other automation tools.

14. **Device Emulation**:

- Emulate different devices and screen resolutions, which is useful for responsive testing.
- Can also **set geolocation** settings during tests.

15. **Data-Driven Testing**:

- Supports parameterization and can read data from files like CSV for data-driven testing.

16. **Speed**:

- Playwright is known for its speed, especially with **parallel execution**.

### Getting Started with Playwright

The presenter shares a step-by-step plan for future sessions:

1. **Prerequisites** for installing Playwright will be covered.
2. **Hands-on Installation**: Setting up Playwright and its required tools.
3. **Running Test Cases**: Learn to create and execute tests.

### How-to Instructions

1. **Device Emulation Using Chrome DevTools**:

    - Press **F12** to open Chrome Developer Tools.
    - Click on the **Devices** icon to select devices such as Galaxy, iPhone, Pixel, etc.
    - Set the resolution to test different screen sizes.
    - Playwright has built-in methods to achieve similar functionalities programmatically.
2. **Recording Tests**:

    - Use the recording feature in Playwright to automatically generate test scripts based on interactions.
3. **Step-by-Step Debugging**:

    - Future sessions will cover how to debug your tests effectively using Playwright's debugging tools.

### Key Links

- **Official Website**: [playwright.dev](https://playwright.dev/)
    - Documentation, features, GitHub links, etc.
- **GitHub Repositories**:
    - Node.js, Java, Python, and .NET implementations are accessible via GitHub.

### Summary of Playwright Features

- **Multi-browser, multi-language, and multi-OS support**.
- **CI/CD** integration and **Docker** support.
- **Accessibility**, **Functional**, and **API testing**.
- **Recording, debugging,** and **parallel execution** capabilities.
- **Auto wait and built-in assertions** for stability.
- **Logs, screenshots, videos**, and support for **multi-tab/window**.

### Note

- Viewers are encouraged to take screenshots of the features summary to refer to often.
- From the next session, the presenter will dive into hands-on work with Playwright.

### Conclusion

Raghav emphasizes that the series is suitable for beginners, and the next videos will include installation and setup of Playwright, followed by writing and running test cases. He encourages viewers to keep learning and refers them to his website for more resources.

[[Python]]  [[Browsers]]  [[Operating Systems]]