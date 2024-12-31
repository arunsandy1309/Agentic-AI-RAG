# Agentic-AI-RAG
This project, Multi-Agentic AI RAG, combines a vector database with AI agents to enable dynamic document parsing, indexing, and querying from PDFs. It offers context-aware, memory-persistent responses, ideal for research assistance, summarization, and seamless knowledge retrieval in scalable applications.

This repository contains two implementations of a Retrieval-Augmented Generation (RAG) system using multi-agentic AI capabilities:
1. **pdf_assistant_online**: Processes and retrieves data from a PDF URL.
2. **pdf_assistant_local**: Processes and retrieves data from locally stored PDFs.

The system uses PostgreSQL as the backend, integrated with the `pgvector` extension for efficient vector storage and querying. It provides seamless document parsing, indexing, and query capabilities for scalable applications.

---

## Features

- **Knowledge Base Integration**:
  - **Online Assistant**: Utilizes `PDFUrlKnowledgeBase` to load and query PDF data from a URL.
  - **Local Assistant**: Utilizes `PDFKnowledgeBase` to load and query PDF data stored locally.
  
- **Persistent Memory**: Run history is stored using `PgAssistantStorage` to enable continuity across sessions.

- **Advanced Search**: Integrates vector similarity search with `PgVector2`.

---

## Prerequisites

1. Install Docker to set up the PostgreSQL server with `pgvector`.
2. Install Python 3.8+ and pip.

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/multi-agentic-ai-rag.git
   cd multi-agentic-ai-rag
   ```

2. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Make sure you have the `.env` which contains the API keys for Groq and Phidata.
---

## Setting Up PostgreSQL with pgvector

Before running the Python code, ensure PostgreSQL with pgvector is up and running. Use the following Docker command to set it up:
  ```bash
    docker run -d \
    -e POSTGRES_DB=ai \
    -e POSTGRES_USER=ai \
    -e POSTGRES_PASSWORD=ai \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v pgvolume:/var/lib/postgresql/data \
    -p 5532:5432 \
    --name pgvector \
    phidata/pgvector:16
  ```

This command sets up a PostgreSQL database named ai with user ai and password ai.
The pgvector extension will be enabled, allowing for vector operations.
PostgreSQL will be accessible at localhost:5532.

---

## Running the Assistants

1. **Online Assistant**

   This assistant processes and retrieves data from a PDF URL. The PDF is fetched from the Phi S3 bucket and contains Thai recipes. 
   
   To run:
   
   ```bash
   python pdf_assistant_online.py
   ```
   ![image](https://github.com/user-attachments/assets/00464037-64e1-453e-820d-2408cdbb963c)


2. **Local Assistant**

   This assistant processes and retrieves data from locally stored PDFs. For this assistant, the Knowledge Base is populated with research papers on LLaMA, GANs, and Gemini stored in the `data/` directory

   To run:
   
   ```bash
   python pdf_assistant_local.py
   ```
   Ensure your PDF files are stored in the data/ directory.

   ![image](https://github.com/user-attachments/assets/ea9d8f9c-b2d0-4e3d-9957-6325ac21c53d)


---

## How It Works

### Agents Used

- **PDF Knowledge Base Agents**:
  - PDFUrlKnowledgeBase:
    - Loads and indexes PDF content from URLs.
    - Uses pgvector for similarity-based retrieval.
  - PDFKnowledgeBase:
    - Loads and indexes PDF content from a local directory.
    - Similar capabilities as the online assistant but for local files.

- **PostgreSQL Storage**:
  - PgAssistantStorage stores conversation history and run metadata in a PostgreSQL database.

- **Vector Database**:
  - PgVector2 enables vector similarity search for indexing and retrieving relevant content from PDFs.
