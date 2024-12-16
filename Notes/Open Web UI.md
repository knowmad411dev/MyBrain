---
tags:
- ollama
- docker
---

## **Open Web UI

1. **Run the Docker Container:** After building the image, run the Docker container with the following command:

```bash
    `docker run -p 5000:5000 open-webui`
```

    This command starts the container and maps port 5000 of the container to port 5000 on your host machine, allowing you to access Open WebUI at `http://localhost:5000`.

**Additional Considerations:**

- **Verify the Entry Point:** Ensure that the `app.py` file (or the specified entry point) is correctly configured to start Open WebUI.
- **Dependencies:** The `requirements.txt` file in the `open-webui` directory should list all necessary Python dependencies. The `RUN pip install -r requirements.txt` command in the Dockerfile will install these dependencies during the image build process.

[[Ollama]]