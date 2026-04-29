# LangChain Markdown Text Splitter
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green)](https://www.langchain.com/)
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![Data Processing](https://img.shields.io/badge/Pipeline-Markdown%20Parsing-orange)](https://python.langchain.com/docs/modules/data_connection/document_transformers/markdown_header_metadata)

## 🏗️ Project Overview
This repository focuses on **Syntax-Aware Data Chunking** for Retrieval-Augmented Generation (RAG). In the modern enterprise, the most valuable technical knowledge lives in Markdown (e.g., Notion, GitHub, docusaurus). Standard text splitters often ruin this data by slicing code blocks in half or breaking markdown links. This project demonstrates how to specifically parse Markdown syntax to preserve both the structure and the formatting of technical documentation.

---

## 🛠️ Key Technical Implementations

### 1. Header-Based Metadata Grouping
* **`MarkdownHeaderTextSplitter`:** Scraping a wiki page yields an enormous string of text. This implementation parses the `#`, `##`, and `###` tags to split the document into logical sections. 
* **Contextual Tagging:** It automatically maps the header titles to the `metadata` dictionary (e.g., `{"Header 2": "API Endpoints"}`). This is critical for downstream vector filtering, ensuring the AI knows exactly which section of a manual it is reading.

### 2. Syntax-Aware Recursive Splitting
* **`Language.MARKDOWN` Integration:** Even after splitting by headers, a single section might still be too large for an LLM's context window. We use `RecursiveCharacterTextSplitter.from_language(Language.MARKDOWN)` as a secondary pass.
* **Code Block Preservation:** This specific language configuration knows the hierarchy of Markdown syntax. It prioritizes keeping elements like ` ```python ... ``` `, tables, and lists completely intact, drastically reducing hallucination rates when asking an AI to analyze code or structured data.

### 3. Pipeline Readiness
* **Two-Stage Chunking:** Demonstrating the enterprise-standard pattern of chaining splitters: first splitting logically by headers, then splitting the resulting chunks recursively by Markdown syntax constraints.

---

## 💻 Tech Stack
* **Language:** Python 3.9+
* **Framework:** LangChain Text Splitters (`langchain-text-splitters`)
* **Environment:** `python-dotenv`

---

## 🚀 Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/langchain-markdown-text-splitter.git

2. **Install Dependencies:**
   ```bash
   pip install -U langchain langchain-text-splitters python-dotenv

3. **Run the Implementation:**
   ```bash
   python markdown_splitting.py
   
