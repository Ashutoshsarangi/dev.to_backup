## What is an LLM?

A Large Language Model (LLM) is an instance of a foundation model, applied specifically to text and text-like data (such as code). LLMs are trained on large datasets of text, including books, articles, and conversations. Training these models involves using petabytes of data.

### Data Scale

- **178 million words** ≈ 1 GB of data
- **1 million GB** ≈ 1 PB of data

### Parameters

A parameter is a value the model can change independently as it learns.

### Core Components of LLM

LLM = Data + Transformer Architecture + Training

### Business Applications (Use Cases)

1. Customer Support
2. Content Articles
3. Software Development (e.g., Copilot)

Foundation models are pre-trained on large amounts of unlabeled and self-supervised data.

### Self-Supervised Data

Self-supervised data means the model learns from patterns in the data in a way that produces generalizable and adaptable output.

### Small vs. Large Language Models

- **Small Language Models (SLMs)** have a small number of parameters.
- **Large Language Models (LLMs)** have a large number of parameters.

#### Examples

- **Mistral 7B**: 7 billion parameters (SLM)
- **LLAMA 700B**: 700 billion parameters (LLM)

### LLM Use Cases

1. Code Generation
2. Document Analysis
3. Multilingual Translation

### Small Model Use Cases

1. On-Device AI
2. Everyday Summarization
3. Enterprise Chatbots

## What is an AI Agent?

LLMs can be part of a compound AI system, leading to the creation of AI agents.

### Traditional LLMs

If you ask a traditional LLM about your remaining vacations, it might generate an incorrect answer because it does not have access to your specific data.

### Compound AI Systems (RAGs)

In a compound AI system:

1. Query → Search Query (LLM) → Your Database → Generate (LLM) → Answer (Correct)

This system fetches the response from your database, ensuring accuracy.

However, if the query changes (e.g., asking about the weather in Limassol), the system might fail if the dedicated path breaks.

### Control Logic in Compound AI Systems

Control logic in compound AI systems is defined programmatically by a human programmer. Another approach is to put the LLM in charge of the logic, leveraging its advanced capabilities to handle complex problems and generate plans.

### Agentic Approach

When LLMs control the logic, we refer to this as an agentic approach. Let's break down the components of LLM agents:

#### LLM Agents

1. **Reasoning**: Ability to think
2. **Ability to Act**: Via external tools (e.g., web search, database access, calculator, code execution)
3. **Access Memory**

### Configuring Agents

One popular method is the ReAct approach, combining reasoning and action components.

#### ReAct Agent Configuration

1. User Query → Plan/Think (LLM) → Act (via Tool) → Observe the Answer (Iterate if Wrong) → Provide Correct Answer

## Retrieval-Augmented Generation (RAG)

### LLM Challenges

1. No Source
2. Outdated Knowledge

### Addressing the Challenges

When a user prompts an LLM, it may not have the latest information. Additionally, without sources, the truthfulness of the response cannot be ensured.

### RAG Framework

The RAG framework addresses these issues:

1. When a user writes a prompt, the LLM queries the document to find the answer from the provided data, rather than relying solely on pre-trained information.
2. A well-crafted prompt is essential to avoid hallucinations.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b9wiq6oxk72ulfqler40.png)

## CAG (Cache Augmented Generation)

rather than querying knowledge data base for answer the core idea to preload the entire knowledge base and load these information into the context window

RAG:-


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kou3movnj7f7b0eh90da.png)


CAG:-

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/btfjipj7k9gmfrzrfiwf.png)


Example:-

Rag:- Law research papers (10000 pages of documents)


CAG:- IT help desk (Product Manual of 100page)  Not frequently changing

Clinical Decision Support (Both RAG + CAG)

**How can we improve the Model's Answer?**

There are 3 ways
1. RAG
2. Fine Tuning
3. prompt Engineering


**Fine tuning**

for this we need 
1. Supervised learning: training the model
2. We need additional GPUs for the training

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2yvg8kwz4mlu79gh5li0.png)


**Prompt Engineering**

Well, in prompt engineering, we can say that "Think Step by Step". as it has transfer architecture. It will activate the Self attention, and without RAG/Finetuning we can achieve our result. 

Example:- Validate code (Wrong prompt)

Good Prompt:-
Validate code security by identifying inputs, checking memory management, and list potential vulnerabilities with their cuss scores. 
We can add role into the prompt.

## LangChain

LangChain is an orchestration framework for the development of applications that use large language models (LLMs), including multiple LLMs.

### Modules in LangChain

1. **LLM Support**
   - Nearly all LLMs can be added to LangChain, such as Llama2 and GPT-4.

2. **Prompts**
   - These are instructions given to LLM models. The `PromptTemplate` class in LangChain formalizes the composition of prompts without the need to manually hard-code context and queries.
   - A prompt template can contain instructions like: "Don't use technical terms in your response." We can specify output format and few-shot context.

3. **Chains**
   - Chains are the core of LangChain's workflow. They combine LLMs with other components, creating applications by executing a sequence of functions.
   - For example, an application might need to first retrieve data from a website, then summarize the text it gets back, and finally use that summary to answer user-submitted questions. This is a sequential chain where the output of one function acts as the input for the next function. Each function in the chain could use different prompts, parameters, and even different models (LLMs).

4. **Indexes**
   - To achieve certain tasks, LLMs might need to access specific external data sources not included in the training dataset, such as internal documents or emails. LangChain collectively refers to these documents as indexes.

   **Indexes:**
   - **Document Loader**: Works with third-party applications for importing data from sources like file storage services, Dropbox, Google Drive, MongoDB, and Pandas.
   - **Vector Database**: Represents data points by converting them into vector embeddings, which are numerical representations in the form of vectors with a fixed number of dimensions. This format is very efficient for retrieval.
   - **Text Splitters**: Split text into small, semantically meaningful chunks that can then be combined using methods and parameters of your choosing.

5. **Memory**
   - LLMs by default don't have long-term memory of prior conversations unless you pass the chat history as an input to your query. LangChain solves this problem with simple utilities for adding memory to your application.
   - You have options for retaining entire conversations or just a summarization of the conversation so far.

6. **Agents**
   - Agents can use a given language model as a reasoning engine to determine which actions to take. When building a chain for agents, you want to include inputs like a list of available tools, user input, prompts, and queries.

### LangChain Use Cases

1. Chatbots
2. Summarizations
3. Question Answering (e.g., Jira)
4. Data Augmentation

## LangGraph

LangGraph is designed for building stateful multi-agent systems that can handle complex, nonlinear workflows (asynchronous).


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p2mh3qn35m12lkhq0lfp.jpeg)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3d6gnb10e6xhqyn7zao2.jpeg)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bu7y915b9jfw0xu0mxs2.png)


## LangSmith

LangSmith is used for monitoring purposes in applications built with LangChain or LangGraph.

## LangFlow

LangFlow allows you to create a Minimum Viable Product (MVP) model of your ideas using a drag-and-drop component. However, it is not suitable for production use.

## What is a Vector Database?

A vector database represents data as mathematical vector embeddings. Vector embeddings are simple arrays of numbers that capture the semantic essence of the data. Similar items are positioned close together in vector space, while dissimilar items are positioned far apart. With a vector database, we can perform similarity searches using mathematical operations. We can store image files, text, and audio files by converting these complex files into vector embeddings, which can then be stored in the vector database.

### Example of Vector Embeddings

\[0.91, 0.15, 0.83, ..., N\]

## How are Vector Embeddings Created?

Vector embeddings are created using embedding models that have been trained on massive datasets. Each type of data has its own specialized embedding model.

### Examples of Embedding Models

- **CLIP** (images)
- **GloVe** (text)
- **Wav2Vec** (audio)

## Vector Indexing

When we have millions of records in our vector database, each containing thousands of pieces of information (vector embeddings), comparing a query vector to every single vector in the database would be very slow. Vector indexing uses approximate nearest neighbor (ANN) algorithms to quickly find vectors that are very likely to be among the closest matches.

### Examples of Vector Indexing Methods

- **HNSW** (Hierarchical Navigable Small World): Creates multi-layer graphs connecting similar vectors.
- **IVF** (Inverted File Index): Divides the vector space into clusters and only searches the most relevant clusters.

These indexing methods trade a small amount of accuracy for significant improvements in search speed. Vector databases are a core feature of Retrieval-Augmented Generation (RAG).

## MCP vs. API

### Introduction

For LLMs to be truly useful, they often need to interact with external data sources, services, and tools, which was typically done with APIs. In late 2024, Anthropic introduced a new open standard protocol called MCP (Model Context Protocol).

### MCP Components

1. **MCP Host**: Runs a number of MCP clients.
2. **MCP Clients**: Each client opens a JSON RPC 2.0 session using the MCP protocol, connecting to external MCP servers.
3. **MCP Servers**: Provide capabilities like access to databases, code repositories, or email servers.

### Capabilities of MCP

MCP addresses two main needs of LLM applications (AI agents):
1. **Context**: Provides contextual data.
2. **Tools**: Enables the usage of tools by AI agents.

MCP provides a standard way for AI agents to retrieve external context, such as documents, knowledge bases, and database records. It can also execute actions or tools, like running a web search, calling an external service, or performing calculations.

### Dynamic Self-Discovery

MCP servers have tools, resources, and prompt templates. An LLM model queries the MCP server to know what capabilities are available, allowing dynamic self-discovery.

### Standardization of Interfaces

Every MCP server, regardless of the service or data it connects to, speaks the same protocol and follows the same patterns.

### Note

Many MCP servers use traditional APIs to do their work. In many cases, an MCP server is essentially a wrapper around an existing API, translating between the MCP format and the underlying service's native interface.

### Example

The MCP GitHub server exposes high-level tools such as repository/list as MCP primitives and internally translates each tool call into the corresponding GitHub REST API.

MCP services are available for file systems, Google Maps, Docker, Spotify, and many more, allowing better integration into AI agents in a standardized way.

## Agentic RAG

Agentic RAG is an upgraded version of RAG, where the LLM decides the data source based on the user query, combining AI agents with RAG.

References:-

1. https://www.youtube.com/watch?v=T-D1OfcDW1M&ab_channel=IBMTechnology
2. https://www.youtube.com/watch?v=HdafI0t3sEY&ab_channel=IBMTechnology
3. https://www.youtube.com/watch?v=zYGDpG-pTho&t=16s&ab_channel=IBMTechnology
4. https://www.youtube.com/watch?v=1bUy-1hGZpI&ab_channel=IBMTechnology
5. https://www.youtube.com/watch?v=qAF1NjEVHhY&ab_channel=IBMTechnology
6. https://www.youtube.com/watch?v=F8NKVhkZZWI&ab_channel=IBMTechnology
7. https://www.youtube.com/watch?v=gl1r1XV0SLw&ab_channel=IBMTechnology
8. https://www.youtube.com/watch?v=7j1t3UZA1TY&ab_channel=IBMTechnology
9. https://www.youtube.com/watch?v=0z9_MhcYvcY&ab_channel=IBMTechnology

