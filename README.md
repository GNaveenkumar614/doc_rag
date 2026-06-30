# Doc RAG

Doc RAG is a lightweight document-based conversational retrieval system built with LangChain, FAISS, and modern LLM providers. It ingests documents such as PDFs, DOCX files, and plain text, splits them into manageable chunks, stores embeddings in a vector index, and answers questions using the most relevant retrieved context.

## Overview

This project is designed for scenarios where you want to chat with your own documents. Instead of relying only on general model knowledge, the application retrieves passages from your indexed files and uses them as grounding context for responses.

## Features

- Ingests local documents in PDF, DOCX, and TXT formats
- Splits documents into overlapping chunks for better retrieval
- Builds and updates a FAISS vector index
- Supports similarity search and MMR-based retrieval for diverse results
- Uses conversational question rewriting and chat history for multi-turn QA
- Configurable LLM and embedding providers via YAML and environment variables

## Project structure

- config/ - YAML configuration for embeddings, retrievers, and LLM settings
- src/document_ingestion/ - document ingestion and FAISS index creation logic
- src/document_chat/ - retrieval and conversational RAG pipeline
- utils/ - configuration and model loading helpers
- model/ - prompt and response model definitions
- prompt/ - prompt templates for contextualization and QA
- test.py - example script that demonstrates ingestion and chat flow

## Prerequisites

- Python 3.10+
- A Google API key for embeddings and/or LLM access
- A Groq API key if you plan to use the Groq-backed LLM option
- Access to a local or networked environment where the required Python packages can be installed

## Installation

1. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
# On Windows:
# .venv\Scripts\activate
```

2. Install the required dependencies:

```bash
pip install python-dotenv langchain langchain-community langchain-google-genai langchain-groq langchain-text-splitters faiss-cpu pydantic
```

## Configuration

Set the required environment variables in a `.env` file:

```env
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key
LLM_PROVIDER=google
```

You can adjust the default behavior in `config/config.yaml`, including:

- embedding model settings
- retriever settings such as top-k and search strategy
- LLM provider and model selection

## Usage

### 1. Prepare your documents

Place the documents you want to index in a location accessible to the script. The example workflow uses a PDF file path in `test.py`.

### 2. Run the example script

```bash
python test.py
```

The script will:

- ingest the configured document(s)
- create or update a FAISS index
- initialize the conversational RAG pipeline
- start an interactive chat loop in the terminal

### 3. Ask questions

Once the script is running, enter your question at the prompt. The assistant will answer using the retrieved document context.

## Example workflow

1. Update the file list in `test.py` with your own documents.
2. Run the script.
3. Ask questions about the indexed content.
4. Optionally modify the retriever settings in `config/config.yaml` to tune relevance or diversity.

## Notes

- The retrieval pipeline is configurable and can be switched between similarity search and MMR-based search.
- For best results, choose document chunk sizes that balance context coverage and retrieval accuracy.
- The example script is intended as a starting point for building a more complete application or service around this RAG flow.

