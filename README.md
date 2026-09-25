# HR Assistant – Agentic AI Application

### Overview

As part of my continued learning journey in **Generative AI and Agentic AI**, I built an **HR Assistant** that combines **Retrieval-Augmented Generation (RAG), an AI agent, and deterministic business tools** to handle common HR-related questions and scenarios.

The objective was to move beyond a traditional RAG chatbot and explore how an AI agent can understand a user's intent, determine the appropriate action, invoke the right tool, and generate a grounded response through a conversational interface.

### Solution Approach

The HR Assistant uses three primary interaction paths:

**1. RAG – HR Policy & Knowledge Retrieval**
For general questions such as *"What is the casual leave policy?"*, the agent retrieves relevant information from an employee handbook using a vector database and generates a response based on the retrieved content.

**2. HR Tools – Calculations**
For questions requiring calculations, the agent invokes deterministic Python tools rather than relying on the LLM to perform arithmetic. Examples include probation-end dates, leave balance projections, gratuity calculations, notice-period shortfalls, and allowances.

**3. HR Tools – Validation & Eligibility**
For scenario-based questions, the agent invokes validation tools to determine whether a specific request or condition meets defined HR rules, such as leave eligibility, reimbursement validation, and promotion eligibility.

The solution includes **10 deterministic HR tools**, along with a handbook retrieval tool.

### Agent Architecture

The solution was implemented using **LangChain's agent framework**. The agent receives the employee's question and determines whether it should:

**User Query → Agent → RAG / HR Tool → Result → Agent → Response**

The agent is guided by routing instructions that distinguish between:

* General policy questions
* Specific calculations
* Specific validations or eligibility checks

I also implemented input validation so that the agent does not simply invent missing parameters. Where information is unavailable or a calculation requires an assumption, the system is designed to surface that explicitly rather than presenting an unsupported answer as fact.

### RAG Pipeline

The employee handbook is processed through a complete RAG pipeline:

**PDF → Text Extraction → Text Cleaning → Chunking → Embeddings → Chroma Vector Store → Similarity Retrieval**

I experimented with document cleaning and chunking strategies to improve retrieval quality, including removing repeated headers and footers and preserving meaningful policy sections during chunking.

### Testing & Validation

The application was tested end-to-end through a **Gradio conversational interface**.

Testing focused not only on the final response but also on:

* Whether the correct route was selected
* Whether the appropriate tool was invoked
* Whether the tool received the correct parameters
* How missing inputs were handled
* How undefined or ambiguous cases were communicated
* Whether calculations were performed by deterministic tools rather than the LLM
* Whether policy responses were grounded in retrieved handbook content

One of the key learnings from this project was that **prompting alone is not sufficient for reliable agent behavior**. Tool design, input validation, routing logic, grounding, and explicit handling of uncertainty all contribute to building a more dependable Agentic AI application.

### Technology Stack

**Python | LangChain | OpenAI | RAG | Chroma | Embeddings | Tool Calling | AI Agents | Gradio**

### Key Learning

This project gave me hands-on experience in moving from a conventional **GenAI/RAG application toward an Agentic AI architecture**, where an AI agent can combine retrieved knowledge with deterministic tools and business logic to solve different types of problems.

It also reinforced an important principle in enterprise AI development: **LLMs can provide reasoning and orchestration, while deterministic tools should handle calculations, validations, and business rules where accuracy and consistency are critical.**
