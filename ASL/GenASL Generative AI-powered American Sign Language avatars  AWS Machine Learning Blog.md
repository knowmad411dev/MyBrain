---
tags:
- ASL
---

## **GenASL Generative AI-powered American Sign Language avatars AWS Machine Learning Blog

In today’s world, effective communication is essential for fostering inclusivity and breaking down barriers. However, for individuals who rely on visual communication methods like American Sign Language (ASL), traditional communication tools often fall short. That’s where GenASL comes in. GenASL is a [generative artificial intelligence (AI)](https://aws.amazon.com/generative-ai/)\-powered solution that translates speech or text into expressive ASL avatar animations, bridging the gap between spoken and written language and sign language.

The rise of foundation models (FMs), and the fascinating world of generative AI that we live in, is incredibly exciting and opens doors to imagine and build what wasn’t previously possible. AWS makes it possible for organizations of all sizes and developers of all skill levels to build and scale generative AI applications with security, privacy, and responsible AI.

In this post, we dive into the architecture and implementation details of GenASL, which uses AWS generative AI capabilities to create human-like ASL avatar videos.

## Solution overview

The GenASL solution comprises several AWS services working together to enable seamless translation from speech or text to ASL avatar animations. Users can input audio, video, or text into GenASL, which generates an ASL avatar video that interprets the provided data. The solution uses AWS AI and machine learning (AI/ML) services, including [Amazon Transcribe](https://aws.amazon.com/transcribe/), [Amazon SageMaker](https://aws.amazon.com/sagemaker/), [Amazon Bedrock](https://aws.amazon.com/bedrock/), and FMs.

The following diagram shows a high-level overview of the architecture.

![GenASL - Architecture Digram](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2024/08/17/ML-16116-arch.png)

The workflow includes the following steps:

1.  An [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2) (Amazon EC2) instance initiates a batch process to create ASL avatars from a video dataset consisting of over 8,000 poses using RTMPose, a real-time multi-person pose estimation toolkit based on MMPose.
2.  [AWS Amplify](https://aws.amazon.com/amplify) distributes the GenASL web app consisting of HTML, JavaScript, and CSS to users’ mobile devices.
3.  An [Amazon Cognito](https://aws.amazon.com/cognito) identity pool grants temporary access to the [Amazon Simple Storage Service](https://aws.amazon.com/s3) (Amazon S3) bucket.
4.  Users upload audio, video, or text to the S3 bucket using the AWS SDK through the web app.
5.  The GenASL web app invokes the backend services by sending the S3 object key in the payload to an API hosted on [Amazon API Gateway](https://aws.amazon.com/api-gateway).
6.  API Gateway instantiates an [AWS Step Functions](https://aws.amazon.com/step-functions) The state machine orchestrates the AI/ML services Amazon Transcribe and Amazon Bedrock and the NoSQL data store [Amazon DynamoDB](https://aws.amazon.com/dynamodb) using [AWS Lambda](https://aws.amazon.com/lambda) functions.
7.  The Step Functions workflow generates a pre-signed URL of the ASL avatar video for the corresponding audio file.
8.  A pre-signed URL for the video file stored in Amazon S3 is sent back to the user’s browser through API Gateway asynchronously through polling. The user’s mobile device plays the video file using the pre-signed URL.

As shown in the following figure, speech or text is converted to an ASL gloss, which is then used to produce an ASL video.

![Sample ASL translation](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2024/08/19/2024-08-18_20-45-33.gif)

Let’s dive into the implementation details of each component.

## Batch process

The [ASL Lexicon Video Dataset](http://dai.cs.rutgers.edu/dai/s/signbank) (ASLLVD) consists of multiple synchronized videos showing the signing from different angles of more than 3,300 ASL signs in citation form, each produced by 1–6 native ASL signers. Linguistic annotations include gloss labels, sign start and end time codes, start and end handshape labels for both hands, and morphological and articulatory classifications of sign type. For compound signs, the dataset includes annotations for each morpheme. To facilitate computer vision-based sign language recognition, the dataset also includes numeric ID labels for sign variants, video sequences in uncompressed raw format, and camera calibration sequences.

We store the input dataset in an S3 bucket (video dataset) and use [RTMPose](https://github.com/open-mmlab/mmpose/tree/dev-1.x/projects/rtmpose) and a PyTorch-based pose estimation open source toolkit to generate the ASL avatar videos. MMPose is a member of the [OpenMMLab Project](https://github.com/open-mmlab) and contains a rich set of algorithms for 2D multi-person human pose estimation, 2D hand pose estimation, 2D face landmark detection, and 133 keypoint whole-body human pose estimations.

The EC2 instance initiates the batch process that stores the ASL avatar videos in another S3 bucket (ASL avatars) for every ASL gloss and stores the ASL gloss and its corresponding ASL avatar video’s S3 key in the DynamoDB table.

## Backend

The backend process has three steps: process the input audio to English text, translate the English text to an ASL gloss, and generate an ASL avatar video from the ASL gloss. This API layer is fronted by API Gateway, which allows the user to authenticate, monitor, and throttle the API request. Because API Gateway has a timeout of 29 seconds, this asynchronous solution uses polling. Whenever the API gets a request to generate the sign video, it invokes a Step Functions workflow and then returns the Step Functions runtime URL back to the frontend application. The Step Functions workflow has three steps:

1.  Convert the audio input to English text using Amazon Transcribe, an automatic speech-to-text AI service that uses deep learning for speech recognition. Amazon Transcribe is a fully managed and continuously training service designed to handle a wide range of speech and acoustic characteristics, including variations in volume, pitch, and speaking rate.
2.  Translate the English text to an ASL gloss using Amazon Bedrock, which is used to build and scale generative AI applications using FMs. Amazon Bedrock is a fully managed service that offers a choice of high-performing FMs from leading AI companies like AI21 Labs, Anthropic, Cohere, Meta, Mistral AI, Stability AI, and Amazon through a single API, along with a broad set of capabilities to build generative AI applications with security, privacy, and responsible AI. We used Anthropic Claude v3 Sonnet on AWS Bedrock to create an ASL gloss.
3.  Generate the ASL avatar video from the ASL gloss. Using the ASL gloss created in the translation layer, we look up the corresponding ASL sign from the DynamoDB table. If the gloss is not available in the GenASL database, the logic falls back to fingerspelling each alphabet letter. The Lookup ASL Avatar Lambda function stitches the videos together, generates a temporary video, uploads that to the S3 bucket, creates a pre-signed URL, and sends the pre-signed URL for both the sign video and the avatar video back to the frontend through polling. The frontend plays the video in a loop.

## Frontend

The frontend application is built using Amplify, a framework that allows you to build, develop, and deploy full stack applications, including mobile and web applications. You can add the authentication to a frontend Amplify app using the Amplify command Add Auth, which generates the sign-up and sign-in pages, as well as the backend and the Amazon Cognito identity pools. During the audio file upload to Amazon S3, the frontend connects with Amazon S3 using the temporary identity provided by the Amazon Cognito identity pool.

## Best practices

The following are best practices for creating the ASL avatar video application.

### API design

API Gateway supports a maximum timeout of 29 seconds. Additionally, it’s a best practice to not build synchronous APIs for long-running processes. Therefore, we built an asynchronous API consisting of two stages by allowing the client to poll a REST resource to check the status of its request. We implemented this pattern using API Gateway and Step Functions. In the first stage, the S3 key and bucket name are sent to an API endpoint that delegates the request to a Step Functions workflow and sends a response back with the execution ARN. In the second stage, the API checks the status of the workflow run based on the ARN provided as an input to this API endpoint. If the ASL avatar is successfully created, this API returns the pre-signed URL. Otherwise, it sends a RUNNING status and the frontend waits for a couple of seconds, and then calls the second API endpoint again. This step is repeated until the API returns the pre-signed URL to the caller.

Step Functions supports direct [optimized integration](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html) with Amazon Bedrock, so we don’t need to have a Lambda function in the middle to create the ASL gloss. We can call the Amazon Bedrock API directly from the Step Functions workflow to save on Lambda compute cost.

### DevOps

From a DevOps perspective, the frontend uses Amplify to build and deploy, and the backend is uses [AWS Serverless Application Model](https://aws.amazon.com/sam) (AWS SAM) to build, package, and deploy the serverless applications. We used [Amazon CloudWatch](https://aws.amazon.com/cloudwatch) to build a dashboard to capture the metrics, including the number of API invocations (number of ASL avatar videos generated), average response time to create the video, and error metrics, to create a good user experience by tracking if there is a failure and alerting the DevOps team appropriately.

### Prompt engineering

We provided a prompt to convert English text to an ASL gloss along with the input text message to the Amazon Bedrock API to invoke Anthropic Claude. We use the few-shot prompting technique by providing a few examples to produce an accurate ASL gloss.

The code sample is available in the accompanying [GitHub repository](https://github.com/aws-samples/genai-asl-avatar-generator).

## Prerequisites

Before you begin, make sure you have the following set up:

-   **Docker** – Make sure Docker is installed and running on your machine. Docker is required for containerized application development and deployment. You can download and install Docker from [Docker’s official website](https://www.docker.com/get-started).
-   **AWS SAM CLI** – Install the AWS SAM CLI. This tool is essential for building and deploying serverless applications. For instructions, refer to [Install the AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html).
-   **Amplify CLI** – Install the Amplify CLI. The Amplify CLI is a powerful toolchain for simplifying serverless web and mobile development. For instructions, refer to [Set up Amplify CLI](https://docs.amplify.aws/cli/start/install/).
-   **Windows-based EC2 instance** – Make sure you have access to a Windows-based EC2 instance to run the batch process. This instance will be used for various tasks such as video processing and data preparation. For instructions, refer to [Launch an instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html#ec2-launch-instance).
-   **FFmpeg** – The video processing step in the GenASL solution requires a functioning installation of FFmpeg, a multimedia framework used by this solution to split and join video files. For instructions to install FFmpeg on the Windows EC2 instance, refer to [Download FFmpeg](https://www.ffmpeg.org/download.html#build-windows).

## Set up the solution

This section provides steps to deploy an ASL avatar generator using AWS services. We outline the steps for cloning the repository, processing data, deploying the backend, and setting up the frontend.

1.  Clone the GitHub repository using the following command:
2.  Follow the instructions in the dataprep folder to initialize the database:
    1.  Modify `genai-asl-avatar-generator/dataprep/config.ini` with information specific to your environment:
    2.  Set up your environment by installing the required Python packages:
    3.  Prepare the sign video annotation file for each processing run:
    4.  Download the sign videos, segment them, and store them in Amazon S3:
    5.  Generate avatar videos:
3.  Use the following command to deploy the backend application:
4.  Set up the frontend:
    1.  Initialize your Amplify environment:
    2.  Modify the frontend configuration to point to the backend API:
        1.  Open `frontend/amplify/backend/function/Audio2Sign/index.py`.
        2.  Modify the `stateMachineArn` variable to have the state machine ARN shown in the output generated from the backend deployment.
    3.  Add hosting to the Amplify project:
    4.  In the prompt, choose **Amazon CloudFront and S3** and choose the bucket to host the GenASL application.
    5.  Install the relevant packages by running the following command:
5.  Deploy the Amplify project:

## Run the solution

After you deploy the Amplify project using the amplify publish command, an [Amazon CloudFront](https://aws.amazon.com/cloudfront) URL will be returned. You can use this URL to access the GenASL demo application. With the application open, you can register a new user and test the ASL avatar generation functionality.

## Clean up

To avoid incurring costs, clean up the resources you created for this application when you no longer need them.

1.  Remove all the frontend resources created by Amplify using the following command:
2.  Remove all the backend resources created by AWS SAM using the following command:
3.  Clean up resources used by the batch process.
    1.  If you created a new EC2 instance for running the batch process, delete the instance using the Amazon EC2 console.
    2.  If you reused an existing EC2 instance, delete the project folder recursively to clean up all the resources:
4.  Empty and delete the S3 bucket using the following commands:

## Next steps

Although GenASL has achieved its initial goals, we’re working to expand its capabilities with advancements like 3D pose estimation, blending techniques, and bi-directional translation between ASL and spoken languages:

-   **3D pose estimation** – The GenASL application is currently generating a 2D avatar. We plan to convert the GenASL solution to create 3D avatars using the 3D pose estimation algorithms supported by MMPose. With that approach, we can create thousands of 3D keypoints. Using Stable Diffusion image generation capabilities, we can create realistic, human-like avatars in real-world settings.
-   **Blending techniques** – When you view the videos generated by the GenASL application, you may see frame skipping. There are some frame drops when we stitch the video together, resulting in a sudden change in the motion. To fix that, we can use a technique called _blending_. We are working on incorporating currently available partner solutions in order to create the intermediate frames to blend in and create smoother videos.
-   **Bi-directional** – The GenASL application currently converts audio to an ASL video. We also need a solution from the ASL video back to English audio, which can be done by navigating in the reverse direction. To do that, we can record a real-time sign video, take the video frame-by-frame, and send that through pose estimation algorithms. Next, we collect and combine the keypoints and search against the keypoints database to get the ASL gloss and convert that back to text. Using [Amazon Polly](https://aws.amazon.com/polly/), we can convert the text back to audio.

## Conclusion

By combining speech-to-text, machine translation, text-to-video generation, and AWS AI/ML services, the GenASL solution creates expressive ASL avatar animations, fostering inclusive and effective communication. This post provided an overview of the GenASL architecture and implementation details. As generative AI continues to evolve, we can create groundbreaking applications that enhance accessibility and inclusivity for all.

___

### About the Authors

![Alak Eswaradass](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2024/08/19/AlakEswaradass.jpg)**Alak Eswaradass** is a Senior Solutions Architect at AWS based in Chicago, Illinois. She is passionate about helping customers architect solutions utilizing AWS cloud technologies to solve business challenges. She is enthusiastic about leveraging cutting-edge technologies like Generative AI to drive innovation in cloud architectures. When she’s not working, Alak enjoys spending time with her daughters and exploring the outdoors with her dogs.

![Suresh Poopandi](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2024/08/19/Suresh-100-1.png)**Suresh Poopandi** is a Principal Solutions Architect at AWS, based in Chicago, Illinois, helping Healthcare Life Science customers with their cloud journey by providing architectures utilizing AWS services to achieve their business goals. He is passionate about building home automation and AI/ML solutions.

![Rob Koch](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2024/08/19/rob-koch.jpeg)**Rob Koch** is a tech enthusiast who thrives on steering projects from their initial spark to successful fruition, Rob Koch is Principal at Slalom Build in Seattle, an AWS Data Hero, and Co-chair of the CNCF Deaf and Hard of Hearing Working Group. His expertise in architecting event-driven systems is firmly rooted in the belief that data should be harnessed in real time. Rob relishes the challenge of examining existing systems and mapping the journey towards an event-driven architecture.

[[American Sign Language (ASL)]]  [[ASL Avatar for Zoom]]  [[ASL Project Brainstorm]]