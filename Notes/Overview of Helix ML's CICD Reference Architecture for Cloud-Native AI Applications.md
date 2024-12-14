---
tags:
- cloud
- machine-learning
video-url: https://www.youtube.com/watch?v=noilYeBqNUA&list=WL&index=2
---
### Overview of Helix ML's CICD Reference Architecture for Cloud-Native AI Applications

Helix ML's reference architecture provides a CICD (Continuous Integration and Continuous Deployment) workflow tailored for AI applications using cloud-native tools like Kubernetes, Flux, and GitHub Actions. The workflow is intended to help developers, regardless of experience with AI engineering, easily iterate on AI models, prompts, API integrations, and related applications by leveraging Git-based automation. Here's a breakdown of the workflow and the setup process, including key features and code examples.

#### Key Features

1. **AI Application Workflow**: Developers work on AI applications (e.g., an exchange rates app) using GitOps, making changes in branches, and using GitHub Actions for CI and Flux for CD.
2. **Automated Testing & Deployment**: Uses GitHub Actions to test changes with LLMs before merging, and Flux to manage deployments.
3. **Ephemeral Testing Environments**: Changes are tested in a separate namespace using a Kubernetes operator before merging to main.
4. **Self-hosted Setup**: The architecture can be run entirely on local Kubernetes clusters using tools like Kind (Kubernetes in Docker), Docker Compose, or cloud-hosted setups.

#### Workflow Summary

1. **Development Workflow**:
   - Edit and update AI configurations (like prompts or models).
   - Push changes to a branch and test using GitHub Actions.
   - Deploy changes to a test namespace using Flux.
   - Merge changes to main when tests pass and deploy to production.

2. **AI Application Example**: The example used is an exchange rate application, which makes API calls to provide the current exchange rate for different currencies. The AI integrates with an API using Swagger specifications.
3. **Issue Handling**:
   - Testing failures (e.g., incorrect output for the requested exchange rate).
   - Debugging the AI model prompts and updating configurations.
   - Re-testing the application and ensuring changes are correct before deploying.

### How-To Instructions for Setting Up the System

1. **Set Up the Environment**
   - Start by installing necessary components such as Kubernetes (Kind) for local development, Git, Docker, and Helm.

2. **Configure the Kubernetes Cluster**:
   - Tear down any old clusters:
     ```bash
     kind delete cluster --name <your-cluster-name>
     ```
   - Create a new Kubernetes cluster with Kind:
     ```bash
     kind create cluster --name <your-cluster-name>
     ```
   - Keycloak is deployed initially for user access management:
     ```bash
     helm install keycloak stable/keycloak
     ```
   - Deploy Helix Control Plane:
     ```bash
     helm install helix-control-plane helix/control-plane-chart
     ```

3. **Helix ML Setup**:
   - Use Helm to set up the Helix Operator:
     ```bash
     helm install helix-operator helix/operator-chart
     ```
   - Port forward to access the Helix interface locally:
     ```bash
     kubectl port-forward service/helix 8080:80
     ```
   - Sign up and create an admin account.

4. **Setup GitHub Actions for CI**:
   - Use Enro (a tunneling tool) to allow GitHub to access your locally running Helix setup for CI jobs.
   - Configure the GitHub repository by updating the action's secrets:
     - Add the URL as a variable.
     - Update the API key in the GitHub Actions secrets.

5. **Use Flux for Continuous Deployment**:
   - Install Flux:
     ```bash
     flux install
     ```
   - Create a Git Source for Flux:
     ```bash
     flux create source git <source-name> --url=https://github.com/<username>/<repository>.git --branch=main
     ```
   - Apply the customization to reconcile changes:
     ```bash
     flux create kustomization <name> --target-namespace=<namespace> --source=<source-name> --path="./path/to/yaml"
     ```

6. **Work on the Exchange Rates Application**:
   - Example YAML to represent an AI application within Kubernetes:
     ```yaml
     apiVersion: helix.ml/v1
     kind: AIApp
     metadata:
       name: exchange-rates
     spec:
       model: "gpt-3"
       prompt: "Provide exchange rates"
       integration:
         - api: "exchange-rate-api"
           swagger: "/path/to/swagger.yaml"
     ```
   - Edit configurations using the Helix editor to update prompts, model specifications, etc.

7. **Debugging and Running Tests**:
   - Edit the prompt logic for handling API requests.
   - Update the request handler code in Helix:
     ```python
     # Modify the LLM prompt to handle currency pairs like USD-GBP
     request_template = """
     If the user asks for a currency pair like USD-GBP, split it and search for the non-USD currency.
     """
     ```
   - Run tests locally before committing:
     ```bash
     helix test --app exchange-rates
     ```
   - Set API keys for the tests:
     ```bash
     export API_KEY=<your-key>
     ```

8. **Commit and Merge Changes**:
   - Create a new branch:
     ```bash
     git checkout -b "improve-currency-handling"
     ```
   - Push changes to GitHub:
     ```bash
     git push origin improve-currency-handling
     ```
   - Create a pull request and merge after the GitHub Actions tests have passed.

9. **Deployment with Flux**:
   - Flux monitors GitHub changes and updates Kubernetes resources:
     ```bash
     kubectl get aapps -n flux-system
     ```
   - After merging, Flux will automatically apply the latest changes, and the Kubernetes operator will update the AI application in production.

10. **Verification**:
    - Run the application (e.g., query "USD-GBP"):
      ```python
      # The app now properly responds with USD to GBP only, no extraneous currencies.
      ```
    - Check that Flux has reconciled the update:
      ```bash
      flux get kustomizations -A
      ```

### Key Information and Takeaways

1. **Developer-Friendly AI Application Workflow**: The architecture aims to make it easy for developers without deep AI knowledge to iterate on AI models, prompts, and integrations. Developers only need to be familiar with Git, making contributions accessible.
2. **GitOps for AI**: Using Git as the source of truth for AI model configurations and prompts ensures consistency, versioning, and easy recovery from failures.
3. **LLM for Testing**: Helix ML uses an LLM as a judge for evaluating tests. This means that rather than hard-coded logic, tests are evaluated based on how well responses meet expected outcomes.
4. **Ephemeral Namespaces for Testing**: Before deploying to production, changes are tested in a separate namespace, reducing the risk of issues reaching production.
5. **Automated Deployment with Flux**: Flux automatically applies changes in Kubernetes when they are merged to main, making continuous deployment seamless.

### How to Recreate This Environment from Scratch

- **Tear Down the Environment**: Run a script that destroys the current cluster, including the Kind cluster and Kubernetes resources.
  ```bash
  kind delete cluster --name helix
  ```
- **Rerun the Setup Script**: The script rebuilds everything from scratch, including deploying Keycloak, Helix control plane, and initializing user access.

### Final Remarks

This CICD architecture supports a developer in iterating on AI models and their integration with other systems, providing a seamless experience using GitOps principles. The use of LLMs as judges, ephemeral testing, and fully automated deployment makes it a powerful reference setup for cloud-native AI solutions.

If you're interested in setting this up, visit the GitHub repository (`https://github.com/helix-ml/gen-cicd-ref`) or join their Discord for support (`https://helix.ml`).

[[LLM]]
