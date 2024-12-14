---
tags:
- agents
---

## **Multi-Agent AI using Magentic-One

**Overview of AI Agents and Magentic-One**

A new multi-agent framework developed by Microsoft called **Magentic-One**, which aims to address some of the current challenges in building autonomous [[AI Agents]]. The goal of such agents is to be able to **make decisions, take actions, and complete tasks independently**. Magentic-One is positioned as a **generalist multi-agent system**, which can perform a wide variety of tasks without requiring precise, fine-grained, and step-by-step instructions for each one.

### Existing Challenges in AI Agent Frameworks

The video begins by explaining two main approaches that have been used so far in AI agent design:

1. **LLM-Centric Approach**:

    - In this approach, the **language model ([[LLM]])** is given control to make decisions as much as possible.
    - This is similar to early versions of frameworks like **CrewAI**, where LLMs often went off track, got stuck in loops, used the wrong tools, or made incorrect decisions. In these cases, there was no reliable way to prevent such issues.
2. **Strictly Controlled Engineering Flow**:

    - Another approach, like that seen in **[[LangGraph]]**, uses a **controlled, node-based graph** to determine the flow of operations.
    - This approach is more reliable but requires significant manual work to build the engineering flow, and the agents end up being highly **specialized** rather than flexible generalists.

### Introducing Magentic-One

Magentic-One from Microsoft aims to **strike a balance** between these two approaches. Its goal is to build a **generalist multi-agent architecture** that is capable of a wide variety of tasks without strict control over each step, while ensuring it does not fall into the same pitfalls as an LLM-centric approach (e.g., loops and errors).

#### Core Components of Magentic-One

Magentic-One's architecture has an **orchestrator** agent as the lead, which coordinates a set of specialized sub-agents:

1. **Orchestrator Agent**:

    - The orchestrator is responsible for **high-level planning**. It decides which sub-agent to use for each step of a given task and tracks the progress of each step.
    - One of its distinguishing features is the use of **two ledgers**:
        - **Task Ledger**: Maintains the overall plan for how to complete a task.
        - **Progress Ledger**: Tracks what's been done, what’s pending, and the progress for each step.
    - This dual-ledger system allows the orchestrator to **reflect** on progress, update plans if necessary, and assign subtasks effectively.
2. **Sub-Agents**:

    - **Web Surfer Agent**:
        - Based on a **Chromium browser** and **Playwright**, this agent can browse websites, extract and input information, click, type, read, summarize, and answer questions about web content.
    - **File Server Agent**:
        - Responsible for interacting with the **local file system**—reading files, navigating, and managing data stored locally.
    - **Coding Agent**:
        - A specialized agent for **writing and analyzing code**. It can take inputs from other agents, such as information from web documents, and use it to create new code or artifacts.
    - **Computer Terminal Agent**:
        - Capable of executing **shell commands** and installing new software packages or libraries.

### Planning, Reflection, and Progress Tracking

- The **orchestrator agent** not only makes the high-level plan for a task but also updates the plan as it proceeds. If the orchestrator encounters issues, it can **adapt the plan**, trying alternative approaches and optimizing as needed.
- A key feature of the orchestrator is its **reflective ability**—an **outer loop** updates the main plan, while an **inner loop** goes through each of the task steps, making decisions, and tracking progress via ledgers.

### Multi-LLM/Model Approach

Another key innovation in Magentic-One is the use of **multiple models**:

- The system can use different **specialized models** for specific agents—these could be **small language models (SLMs)** or **vision language models (VLMs)**.
- For example, the orchestrator might be based on a powerful model like **GPT-4**, while smaller, **fine-tuned models** are used for specialized sub-agents to complete targeted tasks. This multi-model strategy allows for scalability and efficient specialization.

### Practical Example

An example is provided in the video to explain how Magentic-One works in practice:

- The user asks for a description of the latest trends in the **S&P 500** using **Yahoo Finance**.
- The orchestrator decides to use:
    1. The **web surfer** to browse relevant data.
    2. The **coding agent** to create a Python script that processes the data using **YFinance**.
    3. An **executor** agent that runs the Python script and retrieves the required analysis.
- The orchestrator reflects on each step, checks progress, and makes decisions accordingly.

### Benchmarking and Microsoft's Contribution

Magentic-One is built on Microsoft's **AutoGen framework** for building agentic apps. In addition to introducing Magentic-One, Microsoft has also introduced **AutoGen Bench**:

- **AutoGen Bench** is a benchmark suite that allows researchers and developers to evaluate how well an agentic system performs.
- The goal is to move beyond merely measuring the **language model’s capability** and instead evaluate the **overall system**, including how well it utilizes tools and completes real-world tasks.

### Key Takeaways

1. **Generalist Agents**: Magentic-One takes steps toward creating a **generalist agent** that can handle a wide range of tasks without needing a detailed, manual flow for every new task.
2. **Ledger System**: The combination of a **task ledger** (for planning) and a **progress ledger** (for tracking and reflection) gives Magentic-One a unique ability to **adjust and adapt** plans dynamically.
3. **Multi-Model System**: Magentic-One utilizes different LLMs or specialized models, allowing each sub-agent to be optimized for the tasks it performs.
4. **Microsoft’s AutoGen Bench**: A new benchmark that assesses an agentic system's performance, bringing consistency to the measurement of AI agents.
5. **Learnings for Developers**: Developers can learn from how Microsoft built Magentic-One by analyzing their **prompt structures**, tool definitions, and agent configurations—providing insights that can help improve their own agent-building approaches.

### Conclusion

Magentic-One represents a new iteration in AI agent development, focusing on **generalist capabilities** while avoiding issues that current LLM-centric or strictly controlled systems face. This system’s **adaptive planning** and **multi-agent orchestration** pave the way for agents that can operate more independently and effectively across a broader range of tasks. The video encourages viewers to explore Microsoft’s **AutoGen repository**, examine the prompt designs, and experiment with these concepts in their projects.

---

### **Library Examples

Here's how a multi-agent system like Microsoft **Magentic-One** could be applied to support a library, enhancing both patron services and internal operations:

### 1. **Automated Reference Assistance**

- **Orchestrator Agent**: Acts as the main decision-maker that receives requests from patrons (e.g., "I need books about ancient Greek mythology" or "How do I use the library's digital resources?").
- **Web Surfer Agent**:
    - Searches through the library's **online catalog** or **partner databases** to find relevant resources, such as books, articles, or multimedia.
    - Retrieves related information from external sources (e.g., academic websites, public databases) if patrons have questions that go beyond the library’s collection.
- **Coding Agent**:
    - Writes **scripts** to interact with the library's **OPAC** (Online Public Access Catalog) or databases to gather requested information in a structured format.
- **File Server Agent**:
    - Locates and retrieves **digital copies** of resources (e.g., PDFs, audiobooks) from the library’s digital repository for patrons to access.
- **Computer Terminal Agent**:
    - Executes **commands** to check resource availability, update borrowing status, and manage reservations if the patron wants to borrow a book or resource.

### 2. **Interactive Self-Help Kiosk**

- An orchestrator agent could manage an **interactive self-help kiosk** in the library that provides real-time support for patrons.
- The **Web Surfer Agent** can navigate web resources to help patrons find answers to common questions, such as event schedules or library policies.
- **Coding Agent** can generate personalized instructions for accessing library digital resources (e.g., eBooks or databases).

### 3. **Patron Recommendation System**

- The system could act as a **personalized recommendation agent** for library patrons.
- **Orchestrator Agent**: Gathers information about the user’s interests and past borrowings.
- **Coding Agent**: Analyzes the data and suggests new books, audiobooks, or other resources based on user preferences.
- **Web Surfer Agent**: Retrieves information on new releases or upcoming books to enrich recommendations.

### 4. **Digitization and Cataloging of New Books**

- When new books arrive, the **orchestrator** could manage their processing.
- **File Server Agent**: Handles the **scanning** of new books or metadata (e.g., author, title, publication date).
- **Coding Agent**: Automatically creates **catalog entries** or updates the library’s database, including tagging keywords for easier search.
- **Computer Terminal Agent**: Executes tasks such as **adding new book records** to the library catalog or managing the transfer of information between systems.

### 5. **Managing Events and Programs**

- Libraries often host events, book readings, and workshops. The orchestrator could manage the setup and monitoring of these events.
- **Web Surfer Agent**: Updates event information on the library’s website and social media.
- **Coding Agent**: Sends **automated email notifications** or reminders to patrons who have registered for events.
- **File Server Agent**: Maintains a record of event registrations and feedback forms.

### 6. **Inventory and Resource Management**

- **Orchestrator Agent**: Coordinates **inventory management** processes, keeping track of borrowed and returned items, checking for overdue items, and ensuring proper resource distribution.
- **File Server Agent**: Accesses the **library database** to locate physical resources, update their status, and manage re-shelving.
- **Computer Terminal Agent**: Executes commands to **run diagnostic checks** on digital resources or **automate inventory audits** by interfacing with RFID tags on books.

### 7. **Specialized Research Support**

- For patrons requiring **detailed research assistance**, the orchestrator could assign tasks to sub-agents.
- **Web Surfer Agent**: Searches academic databases and credible sources, providing the user with curated information.
- **Coding Agent**: Compiles findings into an organized document, performing any **data analysis** required for complex requests (e.g., statistical analysis).
- This is particularly helpful for students or researchers needing assistance with literature reviews or academic papers.

### 8. **Managing Digital Library Resources**

- The **Web Surfer Agent** could monitor **digital resource usage** and availability, making sure patrons can access journals, eBooks, and databases.
- **Computer Terminal Agent** could be used to **install** updates for digital resources, ensuring smooth operation of the library’s **e-learning platforms**.

### 9. **Multi-LLM/Model System for Specialized Assistance**

- The library might have specialized sub-agents using smaller, **fine-tuned LLMs** to answer specific questions related to different domains, such as history, literature, or science.
- For example, a fine-tuned LLM specialized in **genealogy** could help patrons research their family history using library resources.

### Summary of Benefits

The application of a multi-agent system like Magentic-One could significantly enhance a library's ability to **serve patrons** efficiently while optimizing **internal operations**. It allows for:

- **Adaptive decision-making** through the orchestrator, which can flexibly adjust to various user requests and tasks.
- **Scalable and efficient services** by using specialized agents for different tasks, minimizing the need for manual intervention.
- **Better patron experiences** through automated reference assistance, personalized recommendations, and real-time event management.
- **Improved resource management**, including seamless inventory control, cataloging, and access to digital resources.

The flexibility, adaptability, and capability for **reflective planning** in Magentic-One would help create a smarter library system that is responsive to patron needs while automating many of the labor-intensive, repetitive tasks in library management.

----

### **CDE Example

The **Center for Digital Equity (CDE) in Charlotte, NC** focuses on bridging the digital divide, improving digital literacy, and ensuring that all community members have access to technology. A multi-agent system like **Magentic-One** could be instrumental in helping the Center achieve its mission by supporting its various initiatives and ensuring efficient service delivery. Here are several ways in which CDE could leverage such a system:

### 1. **Digital Literacy and Education Programs**

- **Orchestrator Agent**: Acts as the central coordinator for providing personalized **learning paths** based on individual needs and skill levels.
- **Web Surfer Agent**: Searches for and curates free or affordable online educational resources, such as courses, tutorials, or instructional videos on topics like basic computer skills, cybersecurity, or using productivity tools.
- **Coding Agent**: Develops custom **quizzes, exercises, and tutorials** based on curated content, allowing learners to practice their skills and test their knowledge.
- **File Server Agent**: Manages learning resources, stores progress reports, and makes these resources accessible to learners at any time.
- **Computer Terminal Agent**: Automates installations of educational software for community centers or workshops, ensuring that all computers have the necessary tools pre-installed.

### 2. **Community Engagement and Support Services**

- **Orchestrator Agent**: Handles **community support requests** and assigns the right agents to address each request, ensuring every individual gets the assistance they need.
- **Web Surfer Agent**: Finds information related to available **community resources**, such as internet subsidy programs or grant opportunities, and provides up-to-date information to those in need.
- **File Server Agent**: Keeps track of community member data (securely and with consent), allowing the CDE to understand the demographics and needs of the community better.
- **Computer Terminal Agent**: Sets up new technology installations in community centers, ensuring all systems are properly configured for use.

### 3. **Personalized Digital Support**

- The **orchestrator** could manage a **support chatbot** available for community members to ask questions and get real-time help.
- **Web Surfer Agent**: Retrieves information from the Center's website or partners to answer questions related to device setup, finding digital skills training, or accessing public Wi-Fi.
- **Coding Agent**: Develops **scripts and bots** that provide personalized troubleshooting guides based on user inputs, such as step-by-step instructions for setting up a home Wi-Fi network or using telehealth services.
- **Computer Terminal Agent**: Remotely executes commands to help community members install necessary software or updates, especially for those unfamiliar with doing it themselves.

### 4. **Resource Allocation and Inventory Management**

- **Orchestrator Agent**: Manages the allocation of **digital devices**, like laptops or tablets, to community members based on requests and available inventory.
- **File Server Agent**: Keeps track of all the devices distributed, software licenses, and the status of technology loans.
- **Computer Terminal Agent**: Installs updates or new software on devices before distribution to ensure they're ready for use.

### 5. **Training Workshops and Events Coordination**

- **Orchestrator Agent**: Coordinates **training workshops** and **events** by tracking attendance, planning schedules, and assigning resources.
- **Web Surfer Agent**: Updates event schedules on the Center’s website and social media pages to keep the community informed.
- **File Server Agent**: Manages and stores training material such as **presentations, handouts, and videos**, making them accessible online for participants.
- **Computer Terminal Agent**: Automates the configuration of computers or devices that will be used during the events, ensuring they have the appropriate software and access settings.

### 6. **Community Needs Analysis and Reporting**

- **Orchestrator Agent**: Collects **community feedback** and analyzes areas where additional support is needed (e.g., access to devices, digital literacy programs).
- **Coding Agent**: Generates **analytical reports** and visualizations from data collected during community surveys, helping CDE staff understand what services need scaling or improvement.
- **Web Surfer Agent**: Gathers data from external public datasets that could provide additional context to the challenges faced by the community, such as broadband availability in different neighborhoods.
- **File Server Agent**: Stores community survey results and other related data securely for further use in planning and advocacy.

### 7. **Grant Application Assistance**

- **Orchestrator Agent**: Helps community members identify and apply for **grants and funding opportunities** related to technology and digital equity.
- **Web Surfer Agent**: Searches for available grants and funding options that individuals or the Center could apply for, such as digital inclusion grants, state programs, or nonprofit funding opportunities.
- **Coding Agent**: Assists in preparing and filling out grant applications, including creating drafts, writing formal letters, and compiling necessary supporting documentation.

### 8. **Multi-LLM System for Specialized Assistance**

- The **orchestrator** could manage **specialized sub-agents** that use smaller, **fine-tuned LLMs** to answer questions related to specific needs:
    - A **financial literacy agent** helps community members learn about financial tools, digital banking, and online safety.
    - A **job skills agent** offers training resources for job applications, resume writing, and interview preparation.
    - A **technology usage agent** provides guidance for using commonly available tech resources like Google Docs, spreadsheets, or accessing remote work tools.

### Summary of Benefits for the Center for Digital Equity

A multi-agent system like **Magentic-One** would be valuable for the CDE in several ways:

1. **Scalable Service Delivery**: Multi-agent orchestration allows the Center to serve a larger community efficiently by **automating support** and providing personalized assistance at scale.
2. **Efficient Resource Management**: The system ensures that the Center’s **resources**—whether devices, funding, or staff—are used optimally and distributed based on current community needs.
3. **Empowered Community**: By providing **real-time digital support** and educational resources, the Center can empower community members to become more digitally literate and independent.
4. **Adaptability**: The **orchestrator-led architecture** provides flexibility in managing diverse requests—from applying for grants to installing software on distributed devices—ensuring responsiveness to the community's dynamic needs.
5. **Knowledge Sharing and Learning**: Through the **file server agent** and **coding agent**, the system would store knowledge and create custom learning tools, helping to build and reinforce **digital literacy** over time.

By utilizing such a system, the Center for Digital Equity can improve the **efficiency** and **effectiveness** of their initiatives, helping them to achieve their mission of providing equitable access to digital resources and skills to the Charlotte community. This technology would be a significant step in bridging the digital divide and empowering people with the skills and resources needed for success in a digitally connected world.

[[AI Agents]]  [[AI Coding Assistants]]