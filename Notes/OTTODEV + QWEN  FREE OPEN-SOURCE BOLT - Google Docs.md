---
tags:
- editors
---

## **OTTODEV + QWEN : FREE OPEN-SOURCE BOLT

Step 1: Install Git

1. Install Git from the official website: [https://git-scm.com/downloads](https://git-scm.com/downloads)

Step 2: Install Node.js

1. Go to the Node.js download page: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
2. Choose the prebuilt installer for Windows with LTS (Long Term Support) 

Step 3: Clone the Repo of OTTODEV

1. Run CMD with admin permissions
2. Type the following command and then press enter:

cd path\to\desktop

An example of what you could paste would be

cd C:\Users\guest\OneDrive\Desktop

3. Type the following command to clone the repository then press enter:

git clone https://github.com/coleam00/bolt.new-any-llm.git

4. Rename the downloaded folder OTTODEV

Step 4: Install Dependencies and Start the Application

1. Open CMD with admin permissions
2. Type the following command then press enter:

cd path\to\OTTODEV

3. Type the following command then press enter:

npm install -g pnpm

4. Type the following command then press enter:

pnpm install

5. Type the following command then press enter:

pnpm run dev

NOTE:

You will need the local host number for the next step, which will enable the browser to automatically open when running pnpm run dev.

Step 5: Configure the Dev Script (to open the browser automatically)

1. Locate and open the package.json file in the OTTODEV folder
2. Locate the dev line and modify it to add the following:

"dev": "remix vite:dev --host 0.0.0.0 --port 3000 --open"

The 3000 port number needs to be modified to the local host number of step 4.

Step 6: Add a shortcut to launch OTTODEV

1. Create a new text document file.
2. Add the following lines:

@echo off

cd path\to\OTTODEV

pnpm run dev

3. Save the file with a .bat extension, for example, OTTODEV.bat

You can double click on it to open everything once you finish all the steps. You can even modify its icon so it feels like an app on your device.

Step 7: Install Ollama

Install Ollama from the official website: [https://ollama.com/download](https://ollama.com/download)

You can confirm Ollama was installed correctly by looking in the system tray.

This is a good resource for many of the Ollama commands:

[https://medium.com/@sridevi17j/step-by-step-guide-setting-up-and-running-ollama-in-windows-macos-linux-a00f21164bf3](https://medium.com/@sridevi17j/step-by-step-guide-setting-up-and-running-ollama-in-windows-macos-linux-a00f21164bf3)

Step 8: Install Qwen 2.5 Coder

1. Open CMD
2. Type the following command(s):

To install Qwen 2.5 Coder 32B:

ollama run qwen2.5-coder:32b

 If you want to download another smaller model or just a normal LLM, you can use the info on this site to figure out the command: [https://ollama.com/library/qwen2.5-coder:32b](https://ollama.com/library/qwen2.5-coder:32b)

3. To verify it is installed correctly, it should appear when you type this in CMD: 

ollama list

Step 9: Increase the Ollama Context Window

1. Create a new txt file on Notepad. Name it "Modelfile". 
2. Add the following lines (example is for 32B):

FROM qwen2.5-coder:32b

PARAMETER num_ctx 32768

Just change the 32b to the same smaller model if you went with 14b or 7b

3. Open CMD and run this command:

ollama create -f path\to\Modelfile qwen2.5-coder-extra-ctx:32b

I got most of the instructions from here: [https://github.com/coleam00/bolt.new-any-llm](https://github.com/coleam00/bolt.new-any-llm)

[[Code Editor]]