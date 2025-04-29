# 🔍 Code Review Assistant using LangChain, OpenAI, and Chroma

This project implements a **code review assistant** powered by [LangChain](https://www.langchain.com/), [OpenAI GPT-3.5-Turbo](https://platform.openai.com/docs/models/gpt-3-5), and [Chroma vector store](https://www.trychroma.com/). It loads Python code from a GitHub repository, chunks the code, indexes it with vector embeddings, and enables LLM-based retrieval and analysis to generate code review feedback.

---

## 🚀 Features

- Clones a public GitHub repository containing Python source code.
- Parses Python files into documents using LangChain’s `GenericLoader`.
- Splits and embeds the code using `RecursiveCharacterTextSplitter` and `OpenAIEmbeddings`.
- Stores vectors in a Chroma database.
- Enables retrieval-augmented generation (RAG) using `ChatOpenAI`.
- Generates contextual code reviews and improvement suggestions from retrieved chunks.

---

## 📦 Requirements

Install the necessary dependencies:

```bash
pip install python-dotenv langchain langchain-openai langchain-community langchain-chroma gitpython
```

---

## 🔐 Environment Setup

To securely manage your OpenAI API key, create a `.env` file in the same directory as the notebook:

```
OPENAI_API_KEY=your-openai-api-key
```

Then load the environment variables with:

```python
%pip install python-dotenv
import dotenv
%load_ext dotenv
%dotenv
```

---

## 🧱 How It Works

1. **Clone a Repository**  
   Clones the LangChain GitHub repository into a local folder using GitPython.

2. **Load and Parse Files**  
   Loads all Python files (excluding non-UTF-8) using LangChain's `GenericLoader` and `LanguageParser`.

3. **Split into Chunks**  
   Splits code into manageable chunks using a language-aware splitter (`RecursiveCharacterTextSplitter`).

4. **Vector Embedding and Storage**  
   Embeds the chunks with OpenAI and stores them in a local Chroma vector store.

5. **Retrieve and Review**  
   Retrieves the most relevant code chunks using Max Marginal Relevance (MMR) and generates review suggestions using GPT-3.5.

---

## 🧪 Example Usage

```python
response = retrieval_chain.invoke({
    "input": "Can you review and suggest improvements for the RunnableBinding code?"
})

print(response["answer"])
```

---

## 📁 Project Structure

```
.
├── test_repo/               # Cloned GitHub repository
├── .env                     # Contains your OpenAI API key
├── Solucao RAG.ipynb        # Main Jupyter Notebook
```

---

## 📝 Notes

- You can change the repository or target folder by modifying the `repo_path` and `clone_from()` call.
- This setup is optimized for Python code but can be adapted to other languages supported by LangChain.
- Only UTF-8 encoded files are processed.
