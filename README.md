
# 🧠 Simple RAG from Scratch

A lightweight Retrieval-Augmented Generation (RAG) chatbot built completely from scratch using Python, Ollama, and Hugging Face models. 

This project demonstrates the core mechanics of AI search and generation without relying on heavy external vector database frameworks (like Pinecone or Qdrant) or massive API wrappers (like LangChain). It was developed and tested in a Kaggle environment using dual Tesla T4 GPUs.

## ✨ Features
* **Custom In-Memory Vector Database:** Built purely with Python lists and dictionaries.
* **Mathematical Retrieval:** Uses raw Cosine Similarity to find the closest matching vectors.
* **Local Inference:** Runs open-source Hugging Face models locally via Ollama.
* **Anti-Hallucination Prompting:** Forces the LLM to answer *only* using retrieved context.

## 🛠️ Tech Stack
* **Language:** Python
* **Engine:** [Ollama](https://ollama.com/)
* **Embedding Model:** `CompendiumLabs/bge-base-en-v1.5-gguf` (Translates text into math)
* **Language Model:** `bartowski/Llama-3.2-1B-Instruct-GGUF` (Generates the final chatbot response)

## 🔍 How it Works
This project breaks down the RAG pipeline into three distinct phases:

1. **Indexing:** The code reads a custom text dataset (`cat-facts.txt`), treats each line as a "chunk", and uses the embedding model to convert each chunk into a mathematical vector. These are stored in a custom `VECTOR_DB`.
2. **Retrieval:** When a user asks a question, the question is converted into a vector. The system calculates the cosine similarity between the question vector and every fact in the database, returning the top 3 best matches.
3. **Generation:** The top 3 facts are injected into a strict System Prompt. The Llama 3.2 model reads the prompt and streams an answer back to the user based *only* on the provided context.

## 🚀 Running the Code

### Prerequisites
You need to have [Ollama](https://ollama.com/download) installed on your system (or running in your cloud/Kaggle environment).

### Setup
1. Start the Ollama server in your terminal:
   ```bash
   ollama serve
   ```
2. Pull the required Hugging Face models:
   ```bash
   ollama pull hf.co/CompendiumLabs/bge-base-en-v1.5-gguf
   ollama pull hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF
   ```
3. Install the Python client:
   ```bash
   pip install ollama
   ```
4. Run the generator script:
   ```bash
   python rag_generator.py
   ```

## 🙏 Acknowledgements
This project was inspired by and adapted from [ngxson's Hugging Face tutorial on coding RAG from scratch](https://huggingface.co/blog/ngxson/make-your-own-rag).
```
