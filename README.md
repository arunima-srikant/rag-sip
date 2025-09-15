# Document-Aware Chatbot with RAG

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline to build a **document-aware chatbot**. The chatbot can read technical documentation and answer user questions based only on the document content. Unlike a typical LLM that might “guess” answers, this approach ensures responses are accurate and grounded in source material.

---

## How It Works

1. **Document Loading**

   * `.docx` files are parsed using `python-docx`.
   * Extracted text is wrapped into `Document` objects for processing.

2. **Chunking / Splitting**
   Since large documents cannot be passed directly into a model, they are split into smaller pieces (chunks):

   * **SemanticSplitterNodeParser** → splits based on meaning, so related ideas stay together.
   * **TokenTextSplitter** → splits by token length with configurable size & overlap.
The code is structured in such a way that you can choose to run either the block that executes the token-based splitter, or the semantic splitter.

3. **Embeddings**

   * Each chunk is converted into a **vector representation (embedding)** using the **`bge-m3`** model.
   * Embeddings allow similarity comparison between user queries and document content.

4. **Retriever & Query Engine**

   * A `RetrieverQueryEngine` searches the document for the most relevant chunks.
   * These chunks are then passed to the language model for generating an answer.

5. **Answer Generation**

   * Uses **LlamaIndex** as the framework.
   * Runs the local model **`hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF`** via **Ollama**.
   * Ensures data privacy since the model runs on the local machine.

6. **Interactive Loop**

   * The notebook supports repeated querying.
   * For each user question → retrieve relevant chunks → generate grounded answer.

---

## Tools and Frameworks

* **Python**
* [LlamaIndex](https://www.llamaindex.ai/) – framework for RAG pipelines
* [Ollama](https://ollama.com/) – run LLMs locally
* **Embedding Model**: `bge-m3`
* **LLM**: `Llama-3.2-1B-Instruct-GGUF`
* `python-docx` for document parsing

---

## Features

* Load and process `.docx` documents
* Compare semantic vs token-based chunking
* Build embeddings for document search
* Run fully **offline/local** RAG chatbot
* Interactive query loop for repeated use

---


## Keywords

`Retrieval-Augmented Generation (RAG)`, `Document Chatbot`, `Embeddings`, `LlamaIndex`, `Ollama`, `Local LLM`, `Document Processing`
