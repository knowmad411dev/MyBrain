---
github_link: https://github.com/langchain-ai/report-mAIstro
tags:
- langchain
video-url: https://www.youtube.com/watch?v=wSxZ7yFbbas&list=WL&index=2
---
## **Multi-agent research and report writing

In this detailed walkthrough, Lance from LangChain builds a custom research and summarization agent from scratch, demonstrating its capabilities to create automated reports. The agent processes and structures input topics into comprehensive markdown reports, formatted based on user specifications, with web research included. Here is an overview of how the agent works, the different approaches to building it, and all relevant code examples.

### 1. **The Purpose and Benefits of the Agent**

   - **Target Audience**: AI professionals needing structured research reports.
   - **Use Case**: The agent automates report writing based on input topics, generating markdown files that can include formatted bullet points, sections, sources, and summary tables.
   - **Output Examples**: Examples provided include a breakdown of agent frameworks (like Lang Graph, Crew AI, etc.), technical takeaways, and a summary of AI observability tools, showing how each agent was used for research.
   - **Benefits**: Customizable report formatting, varying structures, and user-defined styles to fit different needs (e.g., intro and conclusion sections, comparison tables).

### 2. **Three Phases of Report Writing**

The report writing process is broken down into three phases: **Planning, Research, and Writing**.

#### **Phase 1: Planning**

   - **Approaches to Planning**:
     1. **Subtopic Expansion**: Break the main topic into several subtopics to independently research, similar to what "GPD Researcher" uses.
     2. **Outline Generation**: Generate an upfront skeletal outline (inspired by "Storm Paper"), often following a Wikipedia-like structure.
   - **Data Model**:
     - A data model (via Pydantic) is created to handle the sections, with each section having attributes like name, description, need for research, and content. This is essential for aligning the output from LLMs with a structured format.

#### **Phase 2: Research**

   - **Strategies for Research**:
     1. **Simple Query Retrieval**: Create search queries and retrieve data from sources, either from the web or using a retrieval-augmented generation (RAG) system.
     2. **Iterative Query Evaluation**: Conduct searches and then evaluate results for relevance, iteratively refining the process.
     3. **Multi-Turn Interviews**: Simulate an AI analyst persona interviewing an AI search engine to retrieve comprehensive information.
   - **Best Practice**: Lance prefers simple, parallelized search queries for efficiency. Generating multiple subqueries for each section theme allows for fast, batch data retrieval.

#### **Phase 3: Writing**

   - **Section-by-Section Writing**: Writing each section individually allows for better quality compared to writing the entire report at once.
   - **Parallel Writing**: Sections requiring independent research are written in parallel to save time.
   - **Sequential Writing for Final Sections**: Introductory and concluding sections are written after main body sections to ensure cohesive conclusions.

### 3. **Implementation Details**

#### **Step-by-Step Implementation**

1. **Define the Data Model**:
   - Lance defines a **section data model** using Pydantic, which includes the attributes for each section, like name, description, and research requirement.
   - Another data model is created for **search queries**.

2. **Planning Phase**:
   - This phase involves generating subtopics for research using two LLM calls:
     - First LLM generates **search queries** for planning.
     - Second LLM helps generate a **detailed report plan** (outline).
   - **Code Example**:
     ```python
     def generate_report_plan(state):
         # Generate search queries for planning
         queries = generate_queries(state['topic'])
         # Perform web search for context
         results = perform_web_search(queries)
         # Generate report sections based on user input and search results
         sections = generate_sections(state['topic'], results)
         return sections
     ```

3. **Research and Writing Phase**:
   - **Section State**: Each section has its own **state** and **subgraph**, enabling independent research and writing.
   - **Section Writing**: Lance emphasizes customizable prompts for better quality output and incorporates **Claude 3.5** for writing.
   - **Parallel Processing**: Parallelized research and writing for all sections using LangChain's **send API**. Each section with research requirements runs in parallel, optimizing speed.

4. **Final Synthesis**:
   - **Intro and Conclusion Writing**: Uses previously written sections as context, ensuring they synthesize information well.

#### **Prompt Engineering**

- **Query Writer Prompt**: Generate unique search queries that cover different aspects of the section.
- **Section Writer Prompt**: Give detailed instructions (e.g., style, length, accuracy) for writing each section.

### 4. **LangChain Studio Usage**

   - **LangChain Studio**: Lance uses this for easy interaction with the agent.
   - **Assistants Setup**: Different assistants can be created for different report types. For example, a "Business Strategy" assistant is tailored to write reports related to business case studies.
   - **Configuration Example**: Report structures and styles are defined by simply pasting them into the assistant configuration.

### 5. **Products Used**

   - **LangChain**: Core framework used for orchestrating LLM calls and building the agent workflow.
   - **Claude 3.5**: Utilized for writing tasks, preferred due to its strength in generating high-quality long-form content.
   - **Tavily Search API**: Used for retrieving web data, preferred for ease of use and efficient scraping capabilities.
   - **LangChain Studio**: Tool for managing different agent assistants and configurations.

### 6. **Customization and Flexibility**

   - **User-Defined Structure**: Input topic and preferred report structure are provided by the user, and the agent adapts accordingly.
   - **Parallel Processing**: Most of the heavy lifting in terms of research and writing is parallelized, significantly speeding up the process.
   - **Interactive Testing**: Individual sections can be tested in isolation, ensuring output quality before running the full report generation.

### 7. **Complete Code Example**

```python
from pydantic import BaseModel

class Section(BaseModel):
    name: str
    description: str
    needs_research: bool
    content: str = ""

# Data model for search queries
class SearchQuery(BaseModel):
    topic: str
    subqueries: list[str]

# Generate report plan
state = {}
state['topic'] = "Comparative analysis of AI agent frameworks"
state['structure'] = "Introduction, analysis of each framework, conclusion with comparison"
sections = generate_report_plan(state)

# Writing phase - each section in parallel
for section in sections:
    if section.needs_research:
        research_results = perform_web_search(section.description)
        section.content = write_section_with_research(research_results, section)
    else:
        section.content = write_section_without_research(section)

# Finalize report
final_report = compile_report(sections)
```

### 8. **Lessons Learned**

- **Pre-planning is Essential**: Laying out the report structure in advance allows for customizable formats and parallel research.
- **Simple Parallelized Research**: Helps save tokens and manage latency better compared to complex multi-turn interviews or iterative search methods.
- **Section-by-Section Writing**: Produces better quality and coherence in each part of the report, while maintaining speed through parallel execution.

### 9. **Summary**

Lance’s tutorial effectively showcases how to build a research and summarization agent capable of producing high-quality, automated reports. The use of a structured planning phase, parallel research, and independent writing of sections enables rapid and flexible report generation. By employing LangChain and Claude 3.5, the workflow becomes seamless, allowing users to easily customize and generate research-based content tailored to their needs.

[[LangChain]]  [[AI Agents]]  [[Python]]  