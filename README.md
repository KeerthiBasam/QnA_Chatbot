# QnA_Chatbot

A conversational Retrieval-Augmented Generation (RAG) chatbot built with **LangChain**, **Groq LLM**, **Hugging Face embeddings**, and **Chroma vector store**.  
This project loads web content, converts it into embeddings, stores it in a vector database, and answers user questions using retrieved context. It also supports **chat history**, so follow-up questions can be understood in context.

## Features

- Loads and parses web content using `WebBaseLoader`
- Splits documents into smaller chunks for better retrieval
- Creates embeddings using `all-MiniLM-L6-v2`
- Stores embeddings in **Chroma**
- Builds a basic **RAG pipeline**
- Supports **history-aware retrieval**
- Maintains session-based conversation memory with `RunnableWithMessageHistory`

## Tech Stack

- Python
- LangChain
- Groq (`llama-3.1-8b-instant`)
- Hugging Face Embeddings
- ChromaDB
- BeautifulSoup4
- dotenv

## Project Workflow

1. Load environment variables from `.env`
2. Initialize the Groq LLM
3. Load a web page using `WebBaseLoader`
4. Split the content into chunks
5. Generate embeddings for each chunk
6. Store chunks in Chroma vector store
7. Create a retriever from the vector store
8. Build a question-answer chain with a prompt
9. Create a retrieval chain for RAG
10. Add chat history support for follow-up questions
11. Manage session-based memory using `RunnableWithMessageHistory`

## Project Structure

```bash
.
├── qnachatbot.ipynb
├── README.md
├── .gitignore
└── .env
```

## Installation

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2. Create and activate a virtual environment
**Windows**
```bash
python -m venv venv
venv\Scripts\activate
```

**Mac/Linux**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

If you do not have a `requirements.txt`, install the main packages manually:

```bash
pip install langchain langchain-groq langchain-huggingface langchain-chroma langchain-community langchain-text-splitters beautifulsoup4 python-dotenv
```

## Environment Variables

Create a `.env` file in the project root and add:

```env
GROQ_API_KEY=your_groq_api_key
HF_TOKEN=your_huggingface_token
```

## How It Works

### Basic RAG
The chatbot first retrieves relevant chunks from the indexed web content and then sends them to the LLM along with the user’s question.

### History-Aware RAG
For follow-up questions like *"Tell me more about it?"*, the system uses the previous chat history to rewrite the question into a standalone form before retrieval.

### Session Memory
`RunnableWithMessageHistory` stores conversation history by `session_id`, allowing multiple independent chat sessions.

## Example Questions

- What is Self-Reflection?
- How do we achieve it?
- What is Task Decomposition?
- What are common ways of doing it?

## Example Code Flow

```python
response = conversational_rag_chain.invoke(
    {"input": "What is Task Decomposition?"},
    config={"configurable": {"session_id": "abc123"}}
)
print(response["answer"])
```

## Use Cases

- Website Q&A chatbot
- Conversational document assistant
- Blog or article question answering
- Context-aware follow-up question answering

## Future Improvements

- Add support for PDF, DOCX, and text files
- Build a Streamlit or FastAPI interface
- Store chat history in a database
- Add source citations in answers
- Deploy as a web application

## Notes

- This notebook uses a web article as the knowledge source.
- The retriever fetches relevant chunks from the vector store.
- Chat history improves handling of follow-up questions.

## Author

Built as a practice project for understanding:
- RAG pipelines
- conversational retrieval
- session-based memory in LangChain
