---
tags:
- python
- github
- google
- editors
---

### **Steps to Set Up and Run Your Project in Colab**

#### **1. Restart the Colab Runtime**

To start fresh, restart the Colab runtime:

1. Go to the **Runtime** menu.
2. Click **Restart Runtime**.

---

#### **2. Clone the Repository**

1. Remove any existing repository to avoid conflicts:
```bash
    !rm -rf ollama-update
```
2. Clone the repository from GitHub:

```bash
    !git clone https://github.com/knowmad411dev/ollama-update.git
```

3. Navigate into the cloned directory:

```bash
    %cd ollama-update
```
---

#### **3. Install Dependencies**

1. Install the packages listed in `requirements.txt`:

```bash
    !pip install -r requirements.txt
```

2. Install PyTorch separately to ensure compatibility:

```bash
    !pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

---

#### **4. Load `github_pat.txt` from Google Drive**

If your `github_pat.txt` file is stored in Google Drive, follow these steps to access it:

##### **Option 1: Mount Google Drive**

1. Mount your Google Drive:

```python
    from google.colab import drive drive.mount('/content/drive')
```

2. Verify the file location:

```bash
    !ls /content/drive/MyDrive
```

    Adjust the path if `github_pat.txt` is stored in a subfolder.

3. Copy the file into the working directory:

```bash
    !cp /content/drive/MyDrive/github_pat.txt .
```

##### **Option 2: Use `gdown`**

If mounting Drive doesn't work, use `gdown` to download the file:

1. Install `gdown` if not already installed:

```bash
    !pip install gdown
```

2. Download the file using its file ID:

```bash
    `!gdown "https://drive.google.com/uc?id=<FILE_ID>"`
```

---

#### **5. Run the Code**

1. Use the scripts provided in your repository. For example:

```bash
    `!python main.py`
```

2. Monitor the output for errors or logs.

---

#### **6. Update the Repository**

If you make changes and want to update the repository:

1. Stage the changes:

```bash
    !git add .
```

2. Commit the changes:

```bash
    `!git commit -m "Your commit message"`
```

3. Push the changes back to GitHub:

```bash
    !git push origin main
```

---

### **Additional Notes**

- **Environment Variables:** If you modify the `github_pat.txt` file, ensure it’s updated in Google Drive or re-uploaded.
- **Requirements Management:** Keep `requirements.txt` up to date with any new dependencies.
- **Debugging:** If a file or folder isn't found, use `!ls` to check the directory structure.

[[Python]]  [[GitHub]]