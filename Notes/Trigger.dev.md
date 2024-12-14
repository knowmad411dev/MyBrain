---
tags:
- automation
video-url: https://trigger.dev/docs/video-walkthrough
---

## **Getting Started with Trigger.dev

This guide will walk you through setting up Trigger.dev in a Next.js application, creating a basic task, deploying it, and then building a more advanced real-world example using Fal.ai to generate images. Additionally, it covers real-time features for user updates, utilizing fan-out tasks, and deploying to Trigger.dev Cloud.

### Initial Setup

1. **Create a Next.js App**: Start by setting up a Next.js application.
2. **Trigger.dev Dashboard**: On the Trigger.dev dashboard, start the onboarding process by running the initialization command provided.
3. **Install Trigger.dev**: Copy the provided project key and run the command in your terminal. For example:

    ```
    npx trigger.dev init
    ```

    During installation, specify the folder to install Trigger.dev, such as `/src`. This creates a "trigger" folder within your Next.js project, which includes a configuration file and a sample "Hello World" job.

4. **Run the Dev Command**: To run Trigger.dev, execute the following:

    ```
    npm run dev
    ```

    This starts the Trigger.dev server and connects it to your Next.js application.

### Creating and Testing Your First Task

- **Hello World Example**: Navigate to the "Hello World" task created during initialization. It logs "Hello, world!" to the Trigger.dev dashboard, waits for five seconds, and then returns "Hello, world!".
- **Test the Task**: To run a test:

    1. Click **Test** on the Trigger.dev dashboard.
    2. Select the "Hello World" task, hit **Run Test**.
    3. Watch the logs as the task runs, displaying the message "Hello, world!" after a delay.

### Creating a More Complex Task

The next example uses **Fal.ai** to convert an image and uploads it to **Cloudflare**. This task demonstrates using a **Server Action** to trigger the task.

1. **Set Up the Task**:

    - Start by setting up multiple terminals:
        - **Trigger.dev Terminal**: Run the Trigger.dev server using:

            ```
            npx trigger.dev@latest
            ```

        - **Dev Server Terminal**: Run your Next.js app with:

            ```
            npm run dev
            ```

        - **Curl Command**: Use a `curl` command to hit an endpoint for processing an image (e.g., a Corgi picture). This triggers the task.

2. **Monitor the Task**:

    - In the Trigger.dev dashboard, you will see the logs of the running task.
    - Fal.ai processes the image, transforming it into a cartoon in Pixar style, which then gets uploaded to a Cloudflare bucket.

3. **The Code Breakdown**:

    - **POST Endpoint**: The first file defines a POST endpoint that accepts an image URL and forwards it to the server action.
    - **Validations with Zod**: Use the **Zod** schema to validate URLs and filenames.
    - **Trigger Task**: The task itself is stored in the "trigger" folder. The task is defined with an ID (`imageToCartoon`), using Fal.ai to generate an image and upload it to Cloudflare.

### Fan-Out Task Example Using Trigger.dev Realtime

This example demonstrates how to use Trigger.dev's real-time feature to manage multiple subtasks running in parallel.

1. **Overview**:

    - **File Upload**: A file is uploaded using **UploadThing**, which triggers a **handle upload task** in Trigger.dev.
    - **Fan-Out to Subtasks**: The main task fans out to three subtasks, each running a **Fal.ai model** in parallel.
    - **Realtime Updates**: The app subscribes to all tasks using Trigger.dev Realtime, updating the UI as each subtask progresses.

2. **Set Up the Task**:

    - **UploadThing Router**: This router handles file uploads and triggers the main task, `handleUploadTask`.
    - **Task Fan-Out**: The `handleUploadTask` triggers three **runFalModel** tasks, running in parallel.
    - **Public Access Token**: After triggering the task, a **public access token** is generated and passed back to the client. This token allows the frontend to safely subscribe to task updates.

3. **Frontend Integration**:

    - **Next.js Client Component**: The frontend uses the **public access token** to authenticate requests to Trigger.dev.
    - **UseRealtime Hook**: The React component uses the `useRealtimeRun` hook from the Trigger.dev `react-hooks` package to subscribe to all tasks with a specific tag, displaying real-time updates.

4. **ElectricSQL Integration**:

    - **ElectricSQL**: Trigger.dev uses **ElectricSQL** to listen for changes in a PostgreSQL database. This integration allows real-time updates to propagate from the backend to the frontend seamlessly.

### Enhancing the Task: Real-Time Feedback

To improve user experience, you can add real-time progress updates for the task:

1. **Trigger.dev Realtime**: Add real-time progress visibility for users on the frontend, leveraging **Trigger.dev Realtime** features.
2. **Run Example**:

    - You can see task execution progress in real-time, such as the image generation progress.
    - Use the **Realtime Hook** (`useRealtimeRun`) from the `react-hooks` package to access the task run data and update the UI accordingly.

3. **Frontend Integration**:

    - The Next.js app takes an image URL and a prompt.
    - The server action receives this form data and triggers the Trigger.dev task, subsequently redirecting the user to the page displaying the progress.

### Deploying to Trigger.dev Cloud

1. **Deployment**:

    - Split the terminal and run the deployment command:

        ```
        npx trigger.dev@latest deploy
        ```

    - The command compiles, bundles, and registers the task as a new version in the Trigger.dev Cloud.

2. **Environment Variables**:

    - Set up any necessary environment variables, such as API keys for **Fal.ai**.
    - For instance, add environment variables like `TRIGGER_SECRET_KEY` to Vercel or another cloud provider where you deploy the app.

### Real-World Testing

After deploying to production (e.g., on Vercel), you can run a test in the live environment:

- **Example Test**: Upload an image and run the process again (e.g., transforming the dog picture for Easter).
- Monitor progress on the Trigger.dev dashboard to verify the live functionality.

### Summary

This walkthrough covered:

- Setting up Trigger.dev in a Next.js project.
- Creating a basic "Hello World" task and running it.
- Building and testing a more complex image generation task using **Fal.ai**.
- Adding real-time progress feedback for frontend users.
- Deploying tasks to Trigger.dev Cloud.
- Utilizing fan-out tasks with real-time progress updates using Trigger.dev Realtime and ElectricSQL.

For more detailed information, consult Trigger.dev documentation or reach out for support. The full video walkthrough includes timestamps for all key parts of the tutorial.

[[Workflow]]