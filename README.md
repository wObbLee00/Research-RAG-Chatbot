# 🚀 **RAG ChatBot for Research Papers**

*A Retrieval-Augmented Generation (RAG) system for querying academic PDFs using LLMs + Vector Databases*

---

## 📚 **Overview**

This project is an end-to-end **RAG (Retrieval-Augmented Generation) ChatBot** built to answer questions **based on your own research papers and academic PDFs**.

Unlike ChatGPT—which does *not* know your private documents—this chatbot:

* Loads your PDFs 📄
* Splits them into meaningful chunks ✂️
* Embeds them using vector embeddings 🔢
* Stores them in a vector database (ChromaDB) 🗄️
* Retrieves the most relevant chunks for any user query 🔍
* Feeds those chunks into an LLM (OpenAI GPT-4o) 🤖
* Generates accurate, context-grounded responses 🧠

This makes it ideal for **students, researchers, and professionals** who need to extract insights from large collections of academic papers.

---

## ✨ **Features**

### 🔍 **Accurate Retrieval**

The system searches your papers using semantic similarity — not keyword search.

### 📘 **Research-aware Chatbot**

It answers only using **information found inside your documents**, preventing hallucinations.

### 🎯 **Clean & Human-Friendly Responses**

A custom conversational prompt makes the assistant sound natural, clear, and concise.

### 🧩 **Metadata-Rich Sources**

Each answer displays **which paper** and **which page** the information was taken from.

### 🖥️ **Streamlit Frontend UI**

A simple but effective UI lets users:

* Enter questions
* View answers
* See source citations

### 🗂️ **Modular Code Structure**

Includes:

* `app/rag.py` → RAG logic
* `app/vectorstore.py` → Ingestion + embeddings
* `frontend/interface.py` → Streamlit UI
* `app/config.py` → Environment + paths

### 🔐 **Environment-Safe Configuration**

Uses a `.env` file to securely load API keys using `python-dotenv`.

---

## 🧠 **Architecture Diagram**

```
        ┌──────────────┐
        │    PDFs       │
        └──────┬───────┘
               │
      Load & Split into Chunks
               │
        ┌──────▼───────┐
        │ Embeddings    │  ← OpenAI Embeddings (text-embedding-3-small)
        └──────┬────────┘
               │
      Store in Vector DB
               │
        ┌──────▼──────┐
        │  ChromaDB    │
        └──────┬──────┘
               │
     Similarity Search (top_k)
               │
        ┌──────▼────────┐
        │ Retrieved Docs │
        └──────┬────────┘
               │
     Feed Into LLM w/ Custom Prompt
               │
        ┌──────▼────────┐
        │   GPT-4o       │
        └──────┬────────┘
               │
          Final Answer
```

---

## 📦 **Tech Stack**

### **Backend**

* Python 3.12
* LangChain 🦜
* ChromaDB
* OpenAI GPT-4o
* python-dotenv

### **Frontend**

* Streamlit

### **Utilities**

* PyPDFLoader (LangChain)
* RecursiveCharacterTextSplitter

---

## 🛠️ **How It Works (Step-by-Step)**

### **1️⃣ PDF Loading**

The system loads all PDF files from a configured directory:

```python
pages = PyPDFLoader(path).load()
```

### **2️⃣ Chunking**

Long text is broken into overlapping chunks for better retrieval:

```python
RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
```

### **3️⃣ Embedding**

Each chunk is converted into a vector using OpenAI Embeddings.

### **4️⃣ Vector Storage**

Embeddings + metadata are saved inside **ChromaDB** for persistent storage.

### **5️⃣ Retrieval**

When the user asks a question:

* The question is embedded
* Similarity search retrieves the most relevant chunks

### **6️⃣ RAG Prompting**

Chunks are inserted into a custom prompt that ensures the AI:

* Uses only the provided context
* Speaks conversationally
* Does not hallucinate

### **7️⃣ Answer Generation**

The LLM (GPT-4o) produces a natural, reader-friendly reply.

---

## 🎨 **Frontend Preview (Streamlit)**

The minimal UI provides:

* 🔎 A question input box
* ✏️ A formatted answer
* 📄 Source citations (paper titles + pages)

Run it with:

```bash
streamlit run frontend/interface.py
```

---

## 🧪 **Running the Project Locally**

### **1. Clone the Repo**

```bash
git clone https://github.com/<your-username>/RAG-Chat-Bot.git
cd RAG-Chat-Bot
```

### **2. Create a Virtual Environment**

```bash
python -m venv .venv
.venv\Scripts\activate  # Windows
```

### **3. Install Dependencies**

```bash
pip install -r requirements.txt
```

### **4. Create a `.env` File**

```
OPENAI_API_KEY=your_key_here
```

### **5. Run Ingestion (Build Vector DB)**

```bash
python -m app.rag
```

### **6. Launch UI**

```bash
streamlit run frontend/interface.py
```

---

## 📌 **Project Structure**

```
RAG-Chat-Bot/
│
├── app/
│   ├── config.py          # Environment variables + paths
│   ├── rag.py             # RAG chain + LLM logic
│   ├── vectorstore.py     # PDF loading, chunking, embeddings
│   └── cli.py             # Terminal interface
│
├── frontend/
│   └── interface.py       # Streamlit chatbot UI
│
├── vector_database/       # Persistent Chroma store
├── .env                   # API key
├── requirements.txt
└── README.md
```

---

## 🎯 **Why This Project Is Useful**

This RAG Chatbot can be used for:

* 📘 Summarizing research papers
* 📝 Extracting methodologies, results, and insights
* 🎓 Study assistance
* 🔬 Literature review automation
* 🧪 Academic research exploration

And can be extended to:

* Corporate document search
* Policy Q&A systems
* Legal document assistants
* Medical document explorers

