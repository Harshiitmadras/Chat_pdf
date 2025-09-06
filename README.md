 
# 📘 ChatPDF – Mini PDF Q&A App

<img width="1727" alt="Screenshot" src="https://github.com/trangiabach/chat-pdf/assets/62537937/e0518c85-295f-4b39-8254-0b9b05a93f49">

[Walkthrough Video](https://drive.google.com/file/d/1fSoZTbu8a_s8J6-6utZfVOLvijlDH97j/view?usp=sharing)

---

## 🎯 Objective
This project is a **full-stack Next.js application** that allows users to:
- Upload PDF files and process their text
- Generate **OpenAI embeddings** and store them in a **Supabase pgvector** database
- Ask natural-language questions about the PDF
- Retrieve contextual answers using a **retrieval-augmented generation (RAG)** pipeline

Built as part of the **Force Equals Full Stack AI Engineer Intern Assignment**.

---

## 🚀 Features
- 📂 Upload one or multiple PDFs  
- 🧠 Extract and embed text using OpenAI Embeddings API  
- 📦 Store embeddings in **Supabase pgvector**  
- 🤖 RAG-based Q&A with OpenAI + LangChain  
- 🔒 Protected API routes with simple login  
- ⚡ Streaming answers (token-by-token)  
- 🎨 Modern responsive UI (Next.js + Tailwind + shadcn/ui)  
- 🌙 Theme switching (light/dark)  
- 📱 Mobile responsive  

---

## ⚙️ Local Development

### 1. Clone the repository
```bash
git clone https://github.com/Harshiitmadras/Chat_pdf.git
cd Chat_pdf
smaller documents (<=4000 tokens in size).
   - These documents are then embedded, with the corresponding PDF's metadata and upserted into Supabase's PG vector store.
   - The PDF is stored in a Supabase's bucket to be used later for display on the frontend

2. RAG (RAG endpoint is available in `app/api/chat`)
   - Users sends query, along with thir desired model, PDF file to chat to and chat hisory
   - Query is embedded. The top 3 most similar text chunks from the PDF file is retrieved, which is combined into a context
   - The context is included in the prompt along with the chat history and send to the
   - LLM streams its response token-by-token back to the frontend
