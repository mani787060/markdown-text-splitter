# LangChain Markdown Text Splitter

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green)](https://www.langchain.com/)
[![Text Splitting](https://img.shields.io/badge/Focus-Markdown%20Chunking-orange)](https://python.langchain.com/docs/concepts/text_splitters/)

A practical implementation of Markdown-aware text splitting using LangChain's `RecursiveCharacterTextSplitter`. This project demonstrates how to divide Markdown documents into smaller chunks while considering the structural patterns of Markdown syntax.

---

## 🏗️ Project Overview

Markdown is widely used for technical documentation, GitHub README files, project notes, and knowledge bases.

When preparing these documents for **Retrieval-Augmented Generation (RAG)** applications, large amounts of text need to be divided into smaller chunks before generating embeddings and storing them in a vector database.

However, ordinary character-based splitting may create chunks at inconvenient positions, potentially separating headings, lists, paragraphs, and code blocks.

This project explores how LangChain's `RecursiveCharacterTextSplitter` can use Markdown-specific splitting rules to create more meaningful text segments.

## 🛠️ Key Technical Implementations

### 1. RecursiveCharacterTextSplitter

The project uses LangChain's `RecursiveCharacterTextSplitter` to divide Markdown text into smaller chunks.

Unlike a basic character-based splitter, the recursive approach attempts to split text using a hierarchy of separators.

This helps preserve larger text structures whenever possible.

### 2. Markdown Language Configuration

The implementation uses:

```python
from langchain_text_splitters import (
    RecursiveCharacterTextSplitter,
    Language
)

splitter = RecursiveCharacterTextSplitter.from_language(
    language=Language.MARKDOWN,
    chunk_size=500,
    chunk_overlap=0
)
```

The `Language.MARKDOWN` configuration applies Markdown-specific separator rules during splitting.

This makes the splitter more suitable for Markdown content than using generic character-based separators.

### 3. Chunk Size Configuration

The `chunk_size` parameter controls the target maximum size of each chunk.

In this implementation:

```python
chunk_size=500
```

This configures the splitter to target chunks of approximately 500 characters.

### 4. Chunk Overlap Configuration

The `chunk_overlap` parameter controls how much content is shared between consecutive chunks.

In this implementation:

```python
chunk_overlap=0
```

No overlap is added between consecutive chunks.

For RAG applications, introducing a small overlap can sometimes help preserve context around chunk boundaries.

### 5. Text Splitting and Output

The `split_text()` method performs the actual splitting operation.

```python
chunks = splitter.split_text(text)

print(len(chunks))
print(chunks[0])
```

The implementation:
- Takes a sample Markdown document as input.
- Applies Markdown-aware recursive splitting.
- Generates smaller text chunks.
- Prints the total number of chunks.
- Displays the first generated chunk.

---

## 🔄 Project Workflow

```text
Input Markdown Document
          |
          v
RecursiveCharacterTextSplitter
          |
          v
Language.MARKDOWN Configuration
          |
          v
Apply Chunk Size and Overlap
          |
          v
Generate Smaller Text Chunks
          |
          v
Display Chunk Count and Content
```

---

## 💻 Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangChain | Text processing framework |
| langchain-text-splitters | Recursive Markdown text splitting |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/mani787060/markdown-text-splitter.git
```

### 2. Navigate to the Project Directory

```bash
cd markdown-text-splitter
```

### 3. Create a Virtual Environment (Recommended)

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS/Linux:

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -U langchain-text-splitters
```

### 5. Run the Implementation

```bash
python markdown_splitting.py
```

The script will process the sample Markdown text and display the number of generated chunks along with the first chunk.

---

## 📚 Why Markdown-Aware Splitting Matters in RAG

Markdown documents often contain different types of structured information:

- Headings and subheadings.
- Paragraphs and descriptions.
- Numbered and unordered lists.
- Code blocks.
- Technical documentation.

Using Markdown-aware splitting rules can help create more meaningful chunks for downstream retrieval.

In a RAG workflow, these chunks can later be converted into embeddings and stored in a vector database.

This can support applications such as:

- Documentation-based question answering.
- Technical knowledge-base search.
- Developer documentation assistants.
- Code documentation retrieval.
- Document-based conversational AI.

---

## 🎯 Learning Outcomes

By exploring this project, you will understand:

- Why text splitting is important in Generative AI.
- How recursive text splitting works.
- How to configure Markdown-specific splitting rules.
- The role of `chunk_size` and `chunk_overlap`.
- How to generate smaller text chunks using LangChain.
- How text preprocessing supports RAG applications.

---

## 🚀 Future Improvements

Possible extensions to this project include:

- Implementing `MarkdownHeaderTextSplitter` for header-based document segmentation.
- Extracting header information into document metadata.
- Combining header-based splitting with recursive Markdown splitting.
- Experimenting with different chunk sizes and overlap values.
- Processing external Markdown files instead of sample text.
- Converting generated chunks into LangChain `Document` objects.
- Integrating the chunks with embedding models and vector databases.

---

