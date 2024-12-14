---
tags:
- obsidian
- web
video-url: https://www.youtube.com/watch?v=rKSpK1dXn4E&list=WL&index=27
---

## **Obsidian Publish with NextJS

This video walks through an alternative method to publish an Obsidian vault using Next.js, which supports key Obsidian features like link previews, backlinks, and full-text search. Here's a detailed summary, including links, how-to instructions, and relevant code.

### Key Features:

1. **Obsidian Syntax Support**: Supports link previews and file linking through the "obsidian-export" library. URLs are organized based on folder structure, meaning the URLs correspond directly to the folder and file structure in your Obsidian vault.
2. **Backlinks and Metadata Support**: You can add backlinks even outside of markdown files. For example, a backlink can be added in the footer, which isn't part of the markdown file. This makes cross-referencing content straightforward.
3. **Full-Text Search**: Supports full-text search, allowing users or readers to search through published content.

### Publishing Obsidian Vault Using Next.js and Vercel

Here’s a step-by-step guide on how to publish your Obsidian Vault using Next.js and Vercel.

#### Step 1: Fork the Repository

- Start by forking the provided GitHub repository that contains the necessary code to publish Obsidian notes.
- Go to the repository and click the "Fork" button to create your own copy.

#### Step 2: Set Up Vercel Account

- Create an account on [Vercel](https://vercel.com/) or log in to your existing account.
- From your dashboard, click "Add New" to start creating a new project.
- Import the "link-blog-starter-md" repository that you just forked.

#### Step 3: Configure Vercel Settings

- Set the **framework preset** to **Next.js**. This step is important to ensure that Vercel uses the appropriate settings for your deployment.
- Click **Deploy** to deploy the project. At this stage, the deployment might fail because of incomplete configuration—this is expected.

#### Step 4: Disconnect Repository

- To move forward, you need to manually deploy it rather than using automatic integration.
- Go to the Vercel dashboard, click on your project, and disconnect the repository.

#### Step 5: Generate Project IDs and Tokens in Vercel

- Go to your Vercel account settings to obtain:
    1. **Project ID**: Found under the project settings.
    2. **Account ID**: Found under account settings.
    3. **Deployment Token**: Generate a new token by selecting full account scope and giving it no expiration.

#### Step 6: Add GitHub Secrets

- Go back to your forked repository on GitHub.
- Click on **Settings > Secrets and Variables > Actions**.
- Create new secrets for:
    - **Organization ID (Account ID)**.
    - **Project ID**.
    - **Vercel Token**.

#### Step 7: Enable Actions for GitHub Repository

- Enable GitHub actions to automate the deployment process.
- Once set up, whenever changes are committed to the repository (especially in the "publisher" directory), the notes will be automatically published online.

#### Step 8: Test Deployment

- Edit a markdown file (e.g., "home.md"), make a small change (e.g., change text to "Hello World"), and commit the change.
- Wait for a few minutes to let the GitHub Actions and Vercel deployment process complete.
- Once completed, visit the Vercel-provided domain to see the updated version of your published vault.

#### Tracking Deployment Progress

- You can track the deployment status through the **Actions** tab in GitHub, which will show step-by-step instructions on the progress.
- It usually takes around 3 minutes for the deployment to complete after changes are committed.

### Helpful Links:

- [Vercel](https://vercel.com/): To create your account and deploy your project.
- [GitHub](https://github.com/): To fork the repository and configure the deployment workflow.
- Next.js Documentation: For more information on the Next.js framework used in this project.

### Integrating Obsidian with Git for Direct Publishing

In the next video, the presenter shows how to integrate your Obsidian Vault with the **Obsidian Git Community Plugin**. This plugin allows you to publish notes directly from Obsidian to GitHub, which will then trigger automatic updates on your website. This makes the entire publishing workflow smoother, allowing you to publish with just one command.

### Code Examples

Here are some code snippets to guide through the setup:

#### GitHub Secrets Configuration

```yaml

# In your GitHub repository, go to Settings > Secrets and add the following:  
- name: VERSEL_ACCOUNT_ID   value: "<your_account_id_here>"    
- name: VERSEL_PROJECT_ID   value: "<your_project_id_here>"  
- name: VERSEL_TOKEN   value: "<your_vercel_token_here>"`
```

#### GitHub Actions Workflow File (`.github/workflows/deploy.yml`)

```yaml
name: Deploy to Vercel on:push: branches: - main  jobs: deploy: runs-on: ubuntu-latest steps: - uses: actions/checkout@v2  - name: Install Dependencies run: npm install  - name: Deploy to Vercel  run: npx vercel --prod  env:           VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }} VERCEL_ORG_ID: ${{ secrets.VERCEL_ORG_ID }} VERCEL_PROJECT_ID: ${{ secrets.VERCEL_PROJECT_ID }}
```

### Summary

- Fork the repository with the starter template.
- Create and configure a Vercel account.
- Generate necessary tokens and add them as GitHub secrets.
- Use GitHub actions to automatically deploy changes to Vercel.
- You can integrate this process with Obsidian Git for easier updates.

With this setup, you have an extendable, automated way to publish your Obsidian Vault that is more customizable than the native Obsidian Publish, leveraging the power of Next.js and Vercel.

[[Obsidian]]  [[GitHub]]