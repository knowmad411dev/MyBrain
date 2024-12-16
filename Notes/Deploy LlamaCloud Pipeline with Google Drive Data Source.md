---
tags:
- llm
- python
- google
- automation
video-url: https://www.youtube.com/watch?v=i3tlWUDF-t4
---

## **Deploy LlamaCloud Pipeline with Google Drive Data Source

**Overview**
The process involves:
1. **Setting up a Llama Cloud Pipeline** using Google Drive as a data source.
2. **Querying the created index** from the pipeline.
3. **Deploying the workflow** using Llama Deploy.

---

### **Setup Requirements**

#### **1. Install Required Python Packages**

Use `pip` to install these packages:

```bash
pip install llama-index llama-index-indices-manage llama-cloud
```

These packages:

- Manage orchestration (`llama-cloud`).
- Handle indices (`llama-index`).

#### **2. Configure API Keys**

You need:

- OpenAI API key.
- Llama Cloud API key.
- Google Service Account key (in `.json` format).

**Instructions to obtain the Google Service Account key:**
- Visit the [Google Cloud Console](https://console.cloud.google.com/).
- Create a service account and download its key as a `.json` file.
- Grant the service account access to the specific Google Drive folder by sharing the folder with the service account email.

---

### **Step 1: Create and Set Up the Pipeline**

#### **Setup Files**

You need two primary Python scripts:

1. `setup_pipeline.py`
2. `workflow.py`

#### **1. Configure `setup_pipeline.py`**

- **Purpose:** Set up the pipeline and create an index on Llama Cloud.

**Key parameters:**
- `data_source_name`: Name for the data source.
- `folder_id`: The ID of the target Google Drive folder.
- `pipeline_name`: Index/pipeline name.
- `service_account_key_path`: Path to the Google Service Account key `.json` file.
- **Chunking Parameters:**
  - `chunk_size`: Size of text chunks.
  - `chunk_overlap`: Overlap between chunks.

**Code Example (`setup_pipeline.py`):**
```python
from llama_cloud import create_data_source, setup_pipeline

# Configuration
data_source_name = "MyDataSource"
folder_id = "your-google-drive-folder-id"
pipeline_name = "MyPipeline"
service_account_key_path = "path/to/service-account.json"
chunk_size = 1024
chunk_overlap = 50

# Create Data Source
data_source = create_data_source(
    data_source_name=data_source_name,
    folder_id=folder_id,
    service_account_key_path=service_account_key_path
)

# Set up the Pipeline
setup_pipeline(
    pipeline_name=pipeline_name,
    data_source=data_source,
    embedding_config={"model": "openai-embedding-model"},
    transform_config={"chunk_size": chunk_size, "chunk_overlap": chunk_overlap}
)

print("Pipeline setup completed!")
```

#### **2. Run the Script**

Execute `setup_pipeline.py` to create the index:

```bash
python setup_pipeline.py
```

---

### **Step 2: Query the Created Index**

#### **Purpose:**

Query the index to retrieve insights.

#### **File: `workflow.py`**

This script:

- Queries the index.
- Returns results in a dictionary format.

**Key Parameters:**
- `index_name`
- `project_name`
- `organization_id`

**Code Example (`workflow.py`):**
```python
from llama_cloud import query_index

# Query Configuration
index_name = "MyPipeline"
project_name = "default"
organization_id = "your-organization-id"

# Query the Index
query = "What is the revenue of Uber in 2021?"
response = query_index(index_name=index_name, project_name=project_name, organization_id=organization_id, query=query)

print(f"Query: {query}")
print(f"Response: {response}")
```

#### **Run the Script**

Execute `workflow.py` to query the index:

```bash
python workflow.py
```

---

### **Step 3: Deploy the Workflow**

#### **1. Configure Deployment YAML File**

Create a `deployment.yaml` file with:

- Workflow name (`llama-cloud-workflow`).
- Index and project details.
- Service paths and control plane configurations.

**Example (`deployment.yaml`):**
```yaml
workflow_name: llama-cloud-workflow
index_name: MyPipeline
project_name: default
organization_id: your-organization-id
service_paths:
  - /path/to/service
control_plane:
  - control-settings
```

#### **2. Deploy Using Llama CLI**

Use `LlamaCTL` to deploy:

```bash
# Start API Server
llama-api-server --config deployment.yaml

# Deploy Workflow
llama-ctl deploy --file deployment.yaml
```

---

### **Demonstration Steps**

1. **Setup the pipeline:**
   - Provide the data source name, folder ID, pipeline name, and service account `.json` file.
2. **Query the pipeline:**
   - Example query: "What is the revenue of Uber in 2021?"
3. **Deploy the workflow:**
   - Use `llama-ctl` to deploy with the `deployment.yaml`.

---

### **Common Debugging Steps**

1. **Check API Keys:**
   - Ensure OpenAI and Llama Cloud API keys are set in the environment:
     ```bash
     export OPENAI_API_KEY="your-openai-api-key"
     export LLAMA_CLOUD_API_KEY="your-llama-cloud-api-key"
     ```

2. **Folder Access:**
   - Verify the Google Drive folder is shared with the service account email.

3. **Config File Issues:**
   - Ensure `index_name`, `project_name`, and `organization_id` match the pipeline setup.

---

### **Summary Workflow**

1. **Install dependencies.**
2. **Configure pipeline and workflow files.**
3. **Run `setup_pipeline.py` to create the pipeline.**
4. **Query the index with `workflow.py`.**
5. **Deploy using `deployment.yaml` and `llama-ctl`.

This structured process creates and deploys a Llama Cloud pipeline, enabling seamless querying of Google Drive data.

[[LLM]]  [[Python]]