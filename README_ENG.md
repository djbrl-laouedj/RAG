## 🧠 Mini RAG

This project presents a complete **RAG (Retrieval-Augmented Generation)** system that allows querying a PDF document through an intelligent chatbot.  
It combines **LangChain**, **FAISS**, **BGE embeddings**, **reranking**, and **local generation Ollama**.

## 🚀 Features

- Automatic PDF loading (e.g. *Syntec Conseil – Data Jobs Glossary*)
- Intelligent text chunking
- Vectorization using the **BAAI/bge-m3** embedding model
- Semantic search with **FAISS**
- Passage reranking using **BAAI/bge-reranker-v2-m3**
- Local text generation with **mistral:instruct** (Ollama)
- Simple **Streamlit** interface to interact with the chatbot
- Optimized pipeline: **MMR + Reranker + Anti-hallucination prompt**

## Project Structure

MiniRAG/
│── My_Streamlit_app.py # Streamlit interface

│── MiniRAG_Djebril_LAOUEDJ.ipynb # Project notebook

│── requirements.txt # Exact tested dependency versions

│── README.md # Documentation (English)

│── README_FR.md # Documentation (French)

│── .gitignore # Ignored files

└── data/ # Example PDF (can be replaced by any PDF)

The provided PDF is:
`Syntec-Conseil_Glossaire-des-principaux-métiers-de-la-Data.pdf`,  
but **any PDF can be used**.

## RAG Pipeline Overview

The global logic of the project is as follows:

1. Load the PDF
2. Split the text into chunks
3. Generate embeddings (BGE-M3)
4. Index embeddings using FAISS
5. Retrieve relevant chunks (MMR)
6. Rerank results (BGE Reranker)
7. Generate the final answer with **mistral:instruct** (Ollama)

## Installation

### 1️⃣ Clone the repository

git clone https://github.com/djbrl-laouedj/MiniRAG.git

cd MiniRAG

2️⃣ Install dependencies

⚠️ Exact versions are required to avoid LangChain conflicts.
Please use the provided requirements.txt.

pip install -r requirements.txt

3️⃣ Install Ollama (if not already installed)
➡️ https://ollama.com/download

Then download the model used in this project:

ollama pull mistral:instruct

▶️ Run the Streamlit application

streamlit run My_Streamlit_app.py

The interface will automatically open in your browser.

### Running on Google Colab

Upload all project files to Colab

Install the dependencies using requirements.txt

Follow the steps below to expose Streamlit using ngrok

ngrok Configuration (Optional)

If you want to expose your Streamlit interface publicly:

Create an account: https://ngrok.com

Get your auth token: https://dashboard.ngrok.com/get-started/your-authtoken

Add the following code at the end of your script:

from pyngrok import ngrok
ngrok.set_auth_token("<YOUR_NGROK_TOKEN>")

Run Streamlit:

!streamlit run My_Streamlit_app.py &>/dev/null &

Expose the app:

public_url = ngrok.connect(8501)
public_url

To restart ngrok cleanly if needed:

from pyngrok import ngrok
try:
    ngrok.kill()
except:
    pass


### MiniRAG User Guide


1️⃣ Upload a PDF

<img width="230" height="174" src="https://github.com/user-attachments/assets/68d63482-dab0-4fd7-9da6-eb2c532127a1" />

2️⃣ Run the pipeline

<img width="228" height="73" src="https://github.com/user-attachments/assets/1283f0f6-4c97-4e82-8e59-24a076c70c15" />

3️⃣ Ask a question

Example: What is the role of a Data Engineer?

<img width="1599" height="809" src="https://github.com/user-attachments/assets/ecf844b9-4725-402d-8bd0-124febe23a01" />

4️⃣ Get the result (sources optional)

<img width="1550" height="694" src="https://github.com/user-attachments/assets/ba5e04cc-467a-40ae-8506-52ae47a5799f" />

5️⃣ If the answer is not found

When the information is not present in the document, the chatbot will respond accordingly:

<img width="1028" height="154" src="https://github.com/user-attachments/assets/fb838479-3c1a-4307-97ba-a94f3b706254" />

### Possible Improvements

Support multiple PDFs (multi-corpus RAG)

Improve the Streamlit UI

Add support for images and tables

Switch to a more powerful LLM (e.g. Llama 3.1 8B)

👤 Author

Project developed by Djebril Laouedj
5th-year student in Big Data & Artificial Intelligence – ECE Paris
