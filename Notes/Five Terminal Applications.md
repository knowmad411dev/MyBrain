---
tags:
- editors
- linux
video-url: https://www.youtube.com/watch?v=1QqvL-k11NE&list=WL&index=2
---

## **Five Terminal Applications

Let's dive into the detailed overview of the given text, covering everything from GitHub links to plugins, how-to instructions, and code examples. This guide will also explore the specific tools mentioned, their installation, usage instructions, and benefits.

### Overview of the Workflow

The scenario starts with a common incident: receiving a notification that your system might be compromised by a virus. This is when you need effective terminal tools that are already available, requiring no heavy installations or further risk of destabilizing your system. Here's how you can set up a security-centric command line that allows you to:

1. Encrypt files for security.
2. Monitor incoming and outgoing traffic.
3. Manage SSH connections with ease.
4. Scan for vulnerabilities using local tools.

### Tools and Techniques Mentioned

#### 1. **Age**: A Command-Line File Encryption Tool

- **GitHub Repository**: [Age GitHub Link](https://github.com/FiloSottile/age)
- **Description**: Age is a popular encryption tool with almost 16,000 stars on GitHub. It can use keys or passwords to encrypt files and is available on multiple platforms such as Homebrew, MacPorts, Alpine Linux, Fedora, and NixOS.
- **Installation**:
  - For **NixOS**, add it to your Home Flake or run:
    ```sh
    nix-env -i age
    ```
  - For **macOS** using Homebrew:
    ```sh
    brew install age
    ```
- **Usage Example**:
  - **Generate Key**:
    ```sh
    age-keygen -o key.txt
    ```

    This creates a key file containing both the public and private key.

  - **Encrypt a File**:
    ```sh
    echo "Hello World" | age -e -r <public_key> > secret.txt
    ```
  - **Decrypt a File**:
    ```sh
    age -d -i key.txt secret.txt > decrypted.txt
    ```

    This decrypts the encrypted file using the private key.

#### 2. **SSHS**: Terminal User Interface for SSH

- **GitHub Repository**: [SSHS GitHub Link](https://github.com/avakarev/sshs)
- **Description**: SSHS is a terminal-based user interface for managing SSH connections. It reads the SSH configuration file and displays all the servers you have configured, simplifying access.
- **Installation**:
  - For **Arch Linux**:
    ```sh
    sudo pacman -S sshs
    ```
  - For **NixOS**:
    Add it to your home flake.
- **Usage**:
  - Once installed, simply run:
    ```sh
    sshs
    ```
  - This command will present a list of configured servers for you to select and connect.

#### 3. **Termshark**: Terminal-Based Network Packet Analyzer

- **GitHub Repository**: [Termshark GitHub Link](https://github.com/gcla/termshark)
- **Description**: Termshark is a terminal-based interface for analyzing network packets. It’s a user-friendly TUI wrapper around `tshark`, making it easier to analyze live network data directly from the terminal.
- **Installation**:
  - For **Linux**:
    ```sh
    sudo apt install termshark
    ```
- **Usage**:
  - Run termshark to start monitoring packets:
    ```sh
    sudo termshark -i eth0
    ```
  - It shows the packet stream, which you can expand and explore.

#### 4. **HTTPie (AAC)**: Terminal API Client

- **GitHub Repository**: [HTTPie GitHub Link](https://github.com/httpie/httpie)
- **Description**: HTTPie is a CLI tool for making HTTP requests easier and more intuitive compared to `curl`. It works like a terminal Postman client.
- **Installation**:
  - Install via Homebrew:
    ```sh
    brew install httpie
    ```
- **Usage**:
  - Send a GET request to an API endpoint:
    ```sh
    http GET https://api.chucknorris.io/jokes/random
    ```
  - Send a POST request:
    ```sh
    http POST https://api.example.com/data name="John" age:=25
    ```

#### 5. **Ido**: Container Scanning Tool

- **Website**: [Ido.dev](https://ido.dev)
- **Description**: Ido provides scanning for container images, detecting vulnerabilities by calculating security scores and providing suggestions to fix issues.
- **Installation & Setup**:
  - Register on their website to create an account.
  - Link your container registry or repositories, which will then be automatically scanned.
- **Usage**:
  - **CLI Scanning**:
    ```sh
    ido scan local-container
    ```

#### 6. **Portal**: File Transfer Utility

- **GitHub Repository**: [Portal GitHub Link](https://github.com/charmbracelet/portal)
- **Description**: Portal is a terminal-based utility for transferring files securely between machines.
- **Installation**:
  - Install on both sender and receiver machines.
  ```sh
  brew install charmbracelet/portal
  ```
- **Usage**:
  - **Send a File**:
    ```sh
    portal send secret.jpg
    ```
  - On the receiving end, run:
    ```sh
    portal receive
    ```
  - This will automatically receive the file from the sender machine.

### Step-by-Step Instructions on Setting Up and Using the Tools

#### Encrypt Files Using Age

1. **Install Age** on your preferred platform (macOS, Linux).
2. **Generate a Key** using:
   ```sh
   age-keygen -o key.txt
   ```
3. **Encrypt Your Files**:
   ```sh
   age -e -r <public_key> myfile.txt > encrypted_file.txt
   ```
4. **Decrypt Encrypted Files**:
   ```sh
   age -d -i key.txt encrypted_file.txt > original_file.txt
   ```

#### Manage SSH Connections Using SSHS

1. **Install SSHS** using Homebrew or your preferred package manager.
2. **Add Servers to SSH Config** by editing:
   ```sh
   vim ~/.ssh/config
   ```
3. **Launch SSHS**:
   ```sh
   sshs
   ```

   Select your desired server from the list.

#### Monitor Network Traffic Using Termshark

1. **Install Termshark** from its GitHub releases or using apt:
   ```sh
   sudo apt install termshark
   ```
2. **Run Termshark** to view packet information.
   ```sh
   sudo termshark -i eth0
   ```

#### Send HTTP Requests Using HTTPie (AAC)

1. **Install HTTPie**:
   ```sh
   brew install httpie
   ```
2. **Make Requests**:
   - To get a Chuck Norris joke:
   ```sh
   http https://api.chucknorris.io/jokes/random
   ```
   - To send a POST request with data:
   ```sh
   http POST https://example.com/api name=Alice age:=30
   ```

#### Secure File Transfer with Portal

1. **Install Portal** on both sender and receiver.
2. **Send a File**:
   ```sh
   portal send secret.jpg
   ```
3. **Receive a File** on the target machine:
   ```sh
   portal receive
   ```

### Conclusion

These tools help you establish a robust, command-line-driven security and utility setup, enhancing your ability to handle potential system emergencies. Most of these tools are highly regarded on GitHub, easy to install, and work without interfering with your system stability. You can add them to your daily workflow and enjoy secure file transfers, manage SSH connections more conveniently, and even sniff packets—all from the comfort of your terminal.

To recap, the **terminal** is your first line of defense: it's versatile and full of tools waiting to be leveraged. With tools like **Age**, **Termshark**, **SSHS**, **HTTPie**, and **Portal**, you can transform your terminal into a comprehensive, open-source security hub that operates with minimal system impact.

[[Code Editor]]  [[Linux]]