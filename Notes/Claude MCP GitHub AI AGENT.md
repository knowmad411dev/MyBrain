---
tags:
- editors
- github
video-url: https://www.youtube.com/watch?v=FiirOCVrPOk&list=WL&index=3
---

[[Anthropic's New Agent Protocol]]  [[Claude Agents]]  [[GitHub]]  [[Code Editor]]  [[Python]] 

## **Claude MCP GitHub AI AGENT

**Detailed Overview of Enhanced GitHub MCP Server**

This guide provides a detailed overview, including key information, how-to instructions, and related code, on enhancing an "Anthropic Model Context Protocol (MCP) server" to automate tasks in GitHub.

### **Overview**

The video covers the expansion of an "Anthropic Model Context Protocol (MCP) server" to enhance its interaction with GitHub repositories. The presenter demonstrates how they modified an existing GitHub MCP server to automate tasks such as managing issues, merging pull requests, and adding features to repositories—all through prompts. The project integrates an AI agent (such as CLA or Cursor) to streamline GitHub repository management, making it more accessible, especially for those not proficient in Git.

The modifications allow for the following GitHub actions:

- **Creating a repository**
- **Adding code to the repository**
- **Merging pull requests**
- **Fetching and addressing issues**
- **Creating new features and adding them via pull requests**
- **Closing issues once they are fixed**
- **Generating README files**
- **Adding code for visualization using tools like `matplotlib`**

The entire project was created by cloning the GitHub MCP server, tweaking configurations, and adding new tools for GitHub automation.

### **Key Information and How-To Instructions**

1. **Setting Up the Enhanced GitHub MCP Server**:
   - Clone the existing MCP server repository.
   - Use a prompt-based approach with tools like CLA 3.5 to extend the server's capabilities.
   - Update the server configuration (`CLA desktop config.js`) to incorporate changes.

2. **How to Use the Expanded MCP Server**:
   - **Add New Tools**: The presenter added tools for managing issues and pull requests on GitHub. These tools were integrated by using prompts to modify and extend the server capabilities.
   - **Local Configuration**: After cloning the server, they configured paths, tokens, and other settings. This allowed the server to run locally with the added functionalities.

3. **GitHub Integration Demonstration**:
   - The enhanced GitHub MCP server was used to create a repository, add Python code, and handle other repository management tasks.
   - The presenter demonstrated how issues were automatically fetched and fixed by using AI agents that handled tasks end-to-end, such as:
     - Creating a repository named `BTC Price`.
     - Adding Python code to fetch Bitcoin prices using the CoinGecko API.
     - Creating and closing issues directly via prompts.
     - Adding visualization using `matplotlib`.

4. **Example Scenario**:
   - **Creating a Repository**: They started by creating a repository named `BTC Price`, which contained Python code for fetching Bitcoin price data.
   - **Issue Management**: They created an issue requesting an additional feature for converting Bitcoin prices to NOK (Norwegian Krone). The MCP server handled fetching and addressing the issue.
   - **Pull Request**: The MCP server then created a pull request with code improvements, such as adding visualization using `matplotlib` to display the latest Bitcoin price.

5. **Auto-Generated README**:
   - The server was prompted to generate a `README.md` file for the repository, resulting in a professional, well-structured file.
   - The `README` contained:
     - Project Overview
     - Installation Instructions
     - License Information

6. **Installation and Running the Code**:
   - Clone the GitHub repository.
   - Install the required dependencies using `pip`.
   - Run the Python code to see the output (including price visualization using `matplotlib`).

### **Code and Configuration**

Below are key components that were highlighted:

1. **Python Code to Fetch Bitcoin Price**:
   - Created a Python script named `price.py` that interacts with the CoinGecko API to fetch the Bitcoin price.
   - Dependencies are listed in a `requirements.txt` file that includes libraries such as `requests`.

   **Example Code**:
   ```python
   import requests

   def fetch_bitcoin_price():
       url = "https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd,nok"
       response = requests.get(url)
       if response.status_code == 200:
           data = response.json()
           return data["bitcoin"]
       else:
           return None

   if __name__ == "__main__":
       price = fetch_bitcoin_price()
       if price:
           print(f"Bitcoin Price in USD: {price['usd']}")
           print(f"Bitcoin Price in NOK: {price['nok']}")
       else:
           print("Failed to fetch Bitcoin price.")
   ```

2. **Adding Visualization Using `matplotlib`**:
   - A feature was added to visualize the Bitcoin price using `matplotlib`. The code was integrated into the existing repository by creating a new branch, modifying the code, and merging it through a pull request.

   **Example Code**:
   ```python
   import matplotlib.pyplot as plt

   def plot_bitcoin_price(prices):
       currencies = list(prices.keys())
       values = [prices[currency] for currency in currencies]

       plt.bar(currencies, values)
       plt.xlabel('Currency')
       plt.ylabel('Price')
       plt.title('Bitcoin Price Comparison')
       plt.show()

   if __name__ == "__main__":
       price = fetch_bitcoin_price()
       if price:
           print(f"Bitcoin Price in USD: {price['usd']}")
           print(f"Bitcoin Price in NOK: {price['nok']}")
           plot_bitcoin_price(price)
       else:
           print("Failed to fetch Bitcoin price.")
   ```

3. **README Generation**:
   - A `README.md` file was generated automatically with the following content:

   **Example `README.md`**:
   ```markdown
   # BTC Price Repository

   ## Overview
   This repository contains a Python script to fetch and display the Bitcoin price in multiple currencies, including USD and NOK, using the CoinGecko API.

   ## Installation

   1. Clone the repository:
      ```

      git clone <repo-url>

      cd BTC_Price

      ```

   2. Install the dependencies:
      ```

      pip install -r requirements.txt

      ```

   ## Running the Script
   Run the script to fetch and visualize the Bitcoin price:
   ```

   python price.py

   ```

   ## License
   MIT License. Data provided by CoinGecko.
   ```

### **Summary**

The enhanced GitHub MCP server allows for an AI-driven interaction to handle common GitHub tasks. This includes creating repositories, managing issues, handling pull requests, and even generating structured README files. The project illustrates how integrating tools like CLA 3.5 with GitHub can enhance productivity, especially for users who are less familiar with GitHub's command-line operations.

### **Key Takeaways**:

- The expanded GitHub MCP server makes GitHub automation more accessible.
- Key tasks like issue handling, merging pull requests, and even generating new code can be handled through AI agents.
- A combination of prompts, AI tools, and server configurations can significantly streamline repository management.

This setup provides an efficient way for those not fully comfortable with Git to leverage the power of automation to manage their projects on GitHub. Let me know if you need more details or further guidance on implementing something similar!


