PDF-RAG-Chatbot
📚 RAG Chatbot for Python Built-In Functions
A Retrieval-Augmented Generation (RAG) application that answers
questions about a PDF containing information about Python built-in
functions. It combines document loading, text chunking, Hugging Face
embeddings, Chroma vector search, a Groq-hosted language model, and a
Gradio chat interface.

🚀 Overview

This project lets users ask questions about the contents of a PDF and
receive answers based on retrieved document passages.
The notebook downloads the Python Built-In Functions PDF, extracts its
text with LangChain's UnstructuredFileLoader, splits the content into
chunks, generates embeddings, and stores them in a persistent Chroma
vector database. A retriever selects relevant chunks for each question.
The LangChain RetrievalQA chain sends the retrieved context to a
Groq-hosted chat model, and Gradio provides the interactive chat
interface.
Configured model: The notebook uses ChatGroq with
model_name="qwen/qwen3.8-27b" and temperature=0. Although the
notebook may be named after Llama 3 70B, the model specified in the code
is Qwen.
🔄 RAG Pipeline
Python Built-In Functions PDF
             ↓
     Document Loader
             ↓
       Text Extraction
             ↓
   Text Chunking (2000 chars,
      400-char overlap)
             ↓
  Hugging Face Embeddings
             ↓
       Chroma Vector DB
             ↓
       User Question
             ↓
    Retrieve Relevant Chunks
             ↓
  LangChain RetrievalQA Chain
             ↓
      Groq Chat Model
             ↓
     Answer + Source Details
             ↓
       Gradio Chat UI
✨ Key Features
- 📄 PDF Loading --- downloads a PDF about Python built-in
  functions.
- 🧹 Text Extraction --- extracts document content using
  UnstructuredFileLoader.
- ✂️ Text Chunking --- uses CharacterTextSplitter with a chunk
  size of 2,000 characters and 400-character overlap.
- 🧠 Embedding Generation --- converts text chunks into vectors
  using HuggingFaceEmbeddings.
- 🗃️ Persistent Vector Storage --- stores embeddings and document
  chunks in Chroma DB under vector_db.
- 🔎 Semantic Retrieval --- retrieves document chunks relevant to
  each user question.
- 🤖 Groq LLM Integration --- uses ChatGroq with the configured
  Qwen model.
- 💬 Context-Based Question Answering --- uses LangChain's
  RetrievalQA chain to generate answers from retrieved content.
- 📚 Source Information --- returns source documents and displays
  source information where available.
- 🌐 Gradio Chat Interface --- allows users to ask questions
  through a browser-based interface.
- 📖 Document Summarization --- supports questions asking for a
  summary of the PDF or its built-in functions.
🏗️ Architecture
             ┌────────────────────────┐
             │      Source PDF        │
             │ Python Built-In Funcs  │
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │   Unstructured Loader   │
             │     Text Extraction     │
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │ CharacterTextSplitter  │
             │ Chunk: 2000 / Overlap 400│
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │ Hugging Face Embeddings│
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │       Chroma DB        │
             │   Persistent Storage   │
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │      Retriever         │
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │  RetrievalQA + Groq    │
             │  qwen/qwen3.8-27b      │
             └────────────┬───────────┘
                          ↓
             ┌────────────────────────┐
             │    Gradio Chat UI      │
             │  Answers and Sources   │
             └────────────────────────┘
Note: RAG can help ground answers in the PDF, but it does not
guarantee that every answer is complete or correct. Check important
information against the original document.
📂 Project Structure
PDF-RAG-Chatbot/
│
├── RAG using LLAMA3-70B, GROQ API, CHROMA DB & LANGCHAIN.ipynb
├── python_inbuildfunction.pdf    # Downloaded source PDF
├── vector_db/                    # Chroma vector store created at runtime
└── README.md                     # Project documentation
The notebook filename above is an example based on the project
description. Keep the actual filename in your repository. The PDF is
downloaded by the notebook, and vector_db/ is created or populated
when the vector store is built.
🛠️ Tech Stack
- Language: Python
- Notebook Environment: Google Colab / Jupyter Notebook
- LLM Framework: LangChain
- LLM Provider: Groq API
- LLM Integration: ChatGroq
- Configured Chat Model: qwen/qwen3.8-27b
- Vector Database: Chroma DB
- Embeddings: Hugging Face HuggingFaceEmbeddings
- PDF Loader: UnstructuredFileLoader
- Text Splitter: CharacterTextSplitter
- QA Chain: RetrievalQA
- Frontend: Gradio
- HTTP Requests: requests
⚙️ Installation and Setup
1. Clone the Repository
Replace the placeholders with your actual GitHub repository URL and
folder name.
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
Alternatively, open the notebook directly in Google Colab or Jupyter
Notebook.
2. Install Dependencies
Run the following commands in a notebook cell or terminal:
pip install -U langchain langchain-community langchain-text-splitters langchain-chroma langchain-groq
pip install "unstructured[pdf]" sentence-transformers gradio requests
The notebook uses a PDF parsing integration that may require additional
system dependencies. The code also uses some LangChain APIs that produce
deprecation warnings in the captured notebook output; newer package
versions may require migration to updated integration packages.
3. Configure the Groq API Key
The notebook currently contains this assignment:
os.environ["GROQ_API_KEY"] = "GROQ_API_KEY"
"GROQ_API_KEY" here is a placeholder string, not a real API key.
The Groq model call needs a valid key available in the runtime
environment.
For Google Colab, store your key in Colab Secrets and retrieve it
securely, or use a hidden prompt for a temporary session:
import os
from getpass import getpass

os.environ["GROQ_API_KEY"] = getpass("Enter your Groq API key: ")
Do not paste your real key into the notebook source, README,
screenshots, or a public GitHub repository. Make sure the runtime has
the key set before initializing ChatGroq.
4. Run the Notebook
Run the notebook cells in order:
1. Mount Google Drive if needed for your workflow.
2. Install the required packages.
3. Import the LangChain, Chroma, embedding, and Groq integrations.
4. Configure the Groq API key securely.
5. Download python_inbuildfunction.pdf.
6. Load and split the document into chunks.
7. Generate embeddings and create the Chroma vector store.
8. Initialize the retriever and RetrievalQA chain.
9. Run a test question.
10. Launch the Gradio chat interface.
5. Open the Chat Interface
When the Gradio launch cell runs, open the URL printed in the notebook
output. In Google Colab, Gradio may create a temporary public sharing
URL. That URL is intended for testing and is not a permanent deployment.
🧪 Example Questions
Try these questions in the notebook or Gradio interface:
1. Ask Which Functions Are Included
What are the functions from this PDF?
Expected behavior: The RAG chain retrieves relevant passages and
lists function names found in the document.
2. Summarize the PDF
Give me a summary of all functions from this PDF.
Expected behavior: The model summarizes information from the
retrieved document passages.
3. Ask About a Specific Function
Explain the purpose of the enumerate() function.
Expected behavior: If relevant content is present and retrieved, the
chatbot explains the function based on the PDF.
The quality of the response depends on the source document, retrieval
results, and the configured chat model.
🔐 Security and Limitations
- Keep GROQ_API_KEY private and out of source control.
- Never commit a real API key to GitHub. If a real key has been
  exposed, revoke it and create a replacement.
- The notebook's current API-key assignment is a placeholder and must
  be replaced by secure runtime configuration before using Groq.
- The notebook output shows deprecation warnings for
  UnstructuredFileLoader and HuggingFaceEmbeddings; updated
  LangChain integration packages may be needed in future versions.
- The notebook uses a PDF downloaded from an external URL. Confirm
  that the source is trustworthy and appropriate for your use.
- The model can produce incorrect, incomplete, or unsupported answers.
  Verify important details against the source PDF.
- A temporary Gradio share link should not be used as a secured
  production deployment.
🔮 Future Improvements
- Allow users to upload their own PDF files.
- Support multiple PDFs and document collections.
- Add configurable chunk size and chunk overlap.
- Explicitly configure and evaluate different embedding models.
- Add reranking to improve retrieval relevance.
- Show source page numbers and more detailed citations where
  available.
- Add conversation history for follow-up questions.
- Add a FastAPI REST backend for integration with other applications.
- Add evaluation tests for retrieval relevance and answer quality.
- Improve dependency pinning and migrate deprecated LangChain APIs.
- Deploy through a production hosting service with secure secret
  management.
💼 Skills Demonstrated
Generative AI • Retrieval-Augmented Generation (RAG) • Python •
LangChain • Groq API • Hugging Face Embeddings • Chroma DB • Vector
Search • PDF Processing • Semantic Retrieval • Question Answering •
Gradio

👨‍💻 Author

Patan Fouzan Khan
B.Tech --- Computer Science and Engineering
Focus Areas: Artificial Intelligence | Machine Learning |
Generative AI | LLM Applications | Backend Development
⭐ If you find this project useful, consider giving the repository a
star!
