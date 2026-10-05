# Python RAG Chatbot

A document-based **Retrieval-Augmented Generation (RAG) chatbot** built with Python, Streamlit, LangChain, Hugging Face embeddings, FAISS, and Ollama.

The application allows users to upload a PDF document and ask questions about its contents. The application extracts the document text, splits it into smaller chunks, converts the chunks into embeddings, retrieves relevant content using similarity search, and generates an answer using a local LLM.

## Features

- 📄 Upload PDF documents directly through the Streamlit interface
- 🔎 Extract text from uploaded PDF files
- ✂️ Split documents into smaller chunks for retrieval
- 🧠 Generate document embeddings using Hugging Face
- 🗂️ Store and search embeddings using FAISS
- 🔍 Retrieve relevant document sections using Maximum Marginal Relevance (MMR)
- 🤖 Generate responses using the local `gemma3:4b` model through Ollama
- 💬 Ask questions about the uploaded document
- 🔒 Answers are instructed to use only information retrieved from the uploaded document

## How It Works

The application follows a basic RAG pipeline:

```text
        PDF Upload
             ↓
      PDF Text Extraction
             ↓
       Text Chunking
             ↓
    Hugging Face Embeddings
             ↓
        FAISS Vector Store
             ↓
      Similarity Retrieval
             ↓
       Relevant Context
             ↓
        RAG Prompt
             ↓
       Ollama LLM
             ↓
          Answer
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Streamlit | Web application interface |
| LangChain | RAG pipeline and LLM orchestration |
| pdfplumber | PDF text extraction |
| Hugging Face | Text embeddings |
| BAAI/bge-small-en-v1.5 | Embedding model |
| FAISS | Vector database / similarity search |
| Ollama | Local LLM execution |
| Gemma 3 4B | Language model |

## Project Structure

```text
Python_Chatbot/
│
├── ragchatbot.py
├── requirements.txt
├── README.md
├── .gitignore
└── venv/                 # Local virtual environment - not committed
```

## Prerequisites

Before running the application, make sure you have:

- Python 3.x
- Ollama
- The `gemma3:4b` model available in Ollama

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/NiranjangoudaPatil/python-rag-chatbot.git
cd python-rag-chatbot
```

### 2. Create a virtual environment

Windows:

```powershell
python -m venv venv
```

Activate it:

```powershell
venv\Scripts\activate
```

### 3. Install dependencies

```powershell
pip install -r requirements.txt
```

> **Note:** The current project imports `langchain_huggingface` and `langchain_ollama`. If these packages are not already installed in your environment, install them with:

```powershell
pip install langchain-huggingface langchain-ollama
```

### 4. Install and prepare Ollama

Make sure Ollama is installed and running.

Then download the model used by the application:

```powershell
ollama pull gemma3:4b
```

## Run the Application

Start the Streamlit application with:

```powershell
streamlit run ragchatbot.py
```

Streamlit will provide a local URL where you can open the chatbot in your browser.

## Usage

1. Start the application.
2. Upload a PDF using the sidebar.
3. Wait for the document to be processed.
4. Enter a question about the uploaded document.
5. The application retrieves relevant document content.
6. The retrieved context is passed to the LLM.
7. The chatbot generates an answer based on the document context.

## RAG Pipeline Details

### 1. Document Extraction

`pdfplumber` extracts text from each page of the uploaded PDF.

### 2. Text Chunking

The extracted text is divided into chunks using LangChain's `RecursiveCharacterTextSplitter`.

Current configuration:

```text
Chunk size: 1000
Chunk overlap: 200
```

### 3. Embeddings

The application uses:

```text
BAAI/bge-small-en-v1.5
```

through Hugging Face embeddings to convert document chunks into numerical vectors.

### 4. Vector Search

The generated embeddings are stored in a FAISS vector store.

The retriever uses **MMR (Maximum Marginal Relevance)** with:

```text
k = 4
```

to retrieve relevant document chunks.

### 5. LLM Generation

The retrieved context is provided to a local Ollama model:

```text
gemma3:4b
```

The prompt instructs the assistant to answer using the provided document context and to indicate when the requested information is not present in the context.

## Example

Upload a PDF containing a report, book, documentation, or other text-based material.

You can then ask questions such as:

```text
What is the main objective of this document?
```

```text
Summarize the key findings.
```

```text
What methodology was used?
```

```text
What are the important conclusions?
```

## Future Improvements

Potential improvements for the project include:

- Persistent FAISS indexes
- Support for multiple document uploads
- Chat history and conversational memory
- Source/page references for retrieved answers
- Improved document preprocessing
- Support for additional document formats
- Better UI/UX
- Deployment as a hosted application

## Author

**Niranjangouda Patil**

GitHub:  
https://github.com/NiranjangoudaPatil

## License

This project is available for educational and development purposes.