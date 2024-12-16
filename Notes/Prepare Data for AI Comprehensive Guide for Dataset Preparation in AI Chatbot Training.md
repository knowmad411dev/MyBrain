---
tags:
- data
- gpt
---

## **Dataset Preparation in AI Chatbot Training

By adhering to these guidelines regarding the Data preparation process and making iterative improvements, you can attain an accuracy level of 95% or higher for your AI application, chatbot, or virtual assistant.

Preparing data for AI might seem complex, but by understanding [what artificial intelligence means](https://ingestai.io/blog/what-is-artificial-intelligence) in data terms, you'll be able to prepare your data effectively for AI implementation. Check out our in-depth article for more guidance.

## How to Prepare Data for AI Virtual Assistants and AI Chatbots

After reviewing the Implementation Guide and establishing the business value, initial scope, and expectations, it is crucial to prepare your data. Achieving an acceptable accuracy rate for an AI model requires data scientists to devote up to 80% of their time to data wrangling, ensuring data quality. As Jeffrey Heer, a computer science professor at the University of Washington, stated: "It's an absolute myth that you can send an algorithm over raw data and have insights pop up." While IngestAI does not use your data to train new AI models, the quality of your data remains critical for optimal AI-app performance.

Preparing data for AI involves a meticulous data preparation process, which consists of the following stages:

### 1\. Data gathering

Collect relevant chatbot training data from various sources, such as databases, web blogs, articles, YouTube video transcriptions, podcasts, tweets, LinkedIn posts, and files of different formats, among others.

IngestAI ingests all of the following file formats:

<table><tbody><tr><td colspan="1" rowspan="1"><p>.txt</p></td><td colspan="1" rowspan="1"><p>.pdf</p></td><td colspan="1" rowspan="1"><p>.fb2</p></td><td colspan="1" rowspan="1"><p>.odp</p></td></tr><tr><td colspan="1" rowspan="1"><p>.csv</p></td><td colspan="1" rowspan="1"><p>.rst</p></td><td colspan="1" rowspan="1"><p>.htm</p></td><td colspan="1" rowspan="1"><p>.pot</p></td></tr><tr><td colspan="1" rowspan="1"><p>.doc</p></td><td colspan="1" rowspan="1"><p>.rtf</p></td><td colspan="1" rowspan="1"><p>.htmlz</p></td><td colspan="1" rowspan="1"><p>.potx</p></td></tr><tr><td colspan="1" rowspan="1"><p>.docx</p></td><td colspan="1" rowspan="1"><p>.tex</p></td><td colspan="1" rowspan="1"><p>.lit</p></td><td colspan="1" rowspan="1"><p>.pps</p></td></tr><tr><td colspan="1" rowspan="1"><p>.abw</p></td><td colspan="1" rowspan="1"><p>.wpd</p></td><td colspan="1" rowspan="1"><p>.lrf</p></td><td colspan="1" rowspan="1"><p>.ppsx</p></td></tr><tr><td colspan="1" rowspan="1"><p>.djvu</p></td><td colspan="1" rowspan="1"><p>.wps</p></td><td colspan="1" rowspan="1"><p>.mobi</p></td><td colspan="1" rowspan="1"><p>.ppt</p></td></tr><tr><td colspan="1" rowspan="1"><p>.docm</p></td><td colspan="1" rowspan="1"><p>.zabw</p></td><td colspan="1" rowspan="1"><p>.pdb</p></td><td colspan="1" rowspan="1"><p>.pptm</p></td></tr><tr><td colspan="1" rowspan="1"><p>.dot</p></td><td colspan="1" rowspan="1"><p>.azw</p></td><td colspan="1" rowspan="1"><p>.pml</p></td><td colspan="1" rowspan="1"><p>.pptx</p></td></tr><tr><td colspan="1" rowspan="1"><p>.dotx</p></td><td colspan="1" rowspan="1"><p>.azw3</p></td><td colspan="1" rowspan="1"><p>.prc</p></td><td colspan="1" rowspan="1"><p>.et</p></td></tr><tr><td colspan="1" rowspan="1"><p>.html</p></td><td colspan="1" rowspan="1"><p>.azw4</p></td><td colspan="1" rowspan="1"><p>.rb</p></td><td colspan="1" rowspan="1"><p>.numbers</p></td></tr><tr><td colspan="1" rowspan="1"><p>.hwp</p></td><td colspan="1" rowspan="1"><p>.cbc</p></td><td colspan="1" rowspan="1"><p>.snb</p></td><td colspan="1" rowspan="1"><p>.ods</p></td></tr><tr><td colspan="1" rowspan="1"><p>.lwp</p></td><td colspan="1" rowspan="1"><p>.cbr</p></td><td colspan="1" rowspan="1"><p>.tcr</p></td><td colspan="1" rowspan="1"><p>.xlr</p></td></tr><tr><td colspan="1" rowspan="1"><p>.md</p></td><td colspan="1" rowspan="1"><p>.cbz</p></td><td colspan="1" rowspan="1"><p>.txtz</p></td><td colspan="1" rowspan="1"><p>.xls</p></td></tr><tr><td colspan="1" rowspan="1"><p>.odt</p></td><td colspan="1" rowspan="1"><p>.chm</p></td><td colspan="1" rowspan="1"><p>.dps</p></td><td colspan="1" rowspan="1"><p>.xlsm</p></td></tr><tr><td colspan="1" rowspan="1"><p>.pages</p></td><td colspan="1" rowspan="1"><p>.epub</p></td><td colspan="1" rowspan="1"><p>.key</p></td><td colspan="1" rowspan="1"><p>.xlsx</p></td></tr></tbody></table>

Ensure that all content relevant to a specific topic is stored in the same Library. If splitting data to make it accessible from different chats or slash commands is desired, create separate Libraries and upload the content accordingly.

### 2\. Data detalization:

After uploading data to a Library, the raw text is split into several chunks. Subsequently, a chunk containing the most relevant chatbot training dataset to answer a user's query is retrieved through AI-search (also known as Semantic Search) and transformed into a human-like response using AI. Understanding this simplified high-level explanation helps grasp the importance of finding the optimal level of dataset detalization and splitting your dataset into contextually similar chunks.

Contextually rich data requires a higher level of detalization during Library creation. If your dataset consists of sentences, each addressing a separate topic, we suggest setting a maximal level of detalization. For data structures resembling FAQs, a medium level of detalization is appropriate. In cases where several blog posts are on separate web pages, set the level of detalization to low so that the most contextually relevant information includes an entire web page.

Higher detalization leads to more predictable (and less creative) responses, as it is harder for AI to provide different answers based on small, precise pieces of text. On the other hand, lower detalization and larger content chunks yield more unpredictable and creative answers.

> Note that while creating your library, you also need to set a level of creativity for the model. This topic is covered in the IngestAI documentation page (Docs) since it goes beyond data preparation and focuses more on the AI model.

### 3\. Data cleaning:

It is crucial to identify and address missing data in your blog post by filling in gaps with the necessary information. Equally important is detecting any incorrect data or inconsistencies and promptly rectifying or eliminating them to ensure accurate and reliable content.

In cases where your data includes Frequently Asked Questions (FAQs) or other Question & Answer formats, we recommend retaining only the answers. To provide meaningful and informative content, ensure these answers are comprehensive and detailed, rather than consisting of brief, one or two-word responses such as "Yes" or "No".

### 4\. Data transformation:

When working with Q&A types of content, consider turning the question into part of the answer to create a comprehensive statement. For instance, if you have a question like "Can I cancel my subscription during the trial period?" with the answer "Yes, you can", combining them as "Yes, you can cancel your subscription during the trial period" makes the information clearer. Evaluate each case individually to determine if data transformation would improve the accuracy of your responses.

For data in tabular formats, such as Excel sheets or relational databases, it is crucial to convert continuous or binary data into categorical data. For example, columns with binary data showing whether a customer has children or higher education (represented by "0" or "1") should be changed to "has children" or "has higher education" as "1" and "doesn't have children" or "doesn't have higher education" instead of "0". If the column displays numerical data like the number of children or years of work experience, it's recommended to present this information in a string format, such as "number of children: 3" or "work experience: 5 years" in each row. It's easy to do using Excel "Find and replace".

When dealing with media content, such as images, videos, or audio, ensure that the material is converted into a text format. You can achieve this through manual transcription or by using transcription software. For instance, in YouTube, you can easily access and copy video transcriptions, or use transcription tools for any other media. Additionally, be sure to convert screenshots containing text or code into raw text formats to maintain it's readability and accessibility.

### 5\. Data integration:

When uploading Excel files or Google Sheets, we recommend ensuring that all relevant information related to a specific topic is located within the same row.

Please note that IngestAI cannot navigate through different tabs or sheets in Excel files or Google Sheet documents. To resolve this, you should either consolidate all tabs or sheets into a single sheet or separate them into different files and upload them to the same Library.

In complex scenarios, such as integrating tabular structured data (Excel, Google Sheets, or relational databases like SQL) with text content (.docx, .txt, etc.) in the same Library, manual configuration by IngestAI may be required to achieve the best results. This customization service is currently available only in Business or Enterprise tariff subscription plans.

For data or content closely related to the same topic, avoid separating it by paragraphs. Instead, if it is divided across multiple lines or paragraphs, try to merge it into one paragraph.

As a reminder, we strongly advise against creating paragraphs with more than 2000 characters, as this can lead to unpredictable and less accurate AI-generated responses.

### 6\. Data reduction:

If you have paragraphs or rows in Excel or Google Sheets exceeding 2000 characters, we recommend using summarization or other prompt methods (available in IngestAI Prompt Engineering functionality) to reduce the maximum paragraph size to no more than 2000 characters. Always test first before making any changes, and only do so if the answer accuracy isn't satisfactory after adjusting the model's creativity, detail, and optimal prompt.

It is also crucial to condense the dataset to include only relevant content that will prove beneficial for your AI application.

In general, we advise making multiple iterations and refining your dataset step by step. Iterate as many times as needed to observe how your AI app's answer accuracy changes with each enhancement to your dataset. The time required for this process can range from a few hours to several weeks, depending on the dataset's size, complexity, and preparation time. Ideally, you should aim for an accuracy level of 95% or higher in data preparation in AI.

   [[GPT]]