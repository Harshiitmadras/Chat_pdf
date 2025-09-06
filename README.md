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
---
##2. Install dependencies

npm install

###3. Setup environment variables

Create a file named .env.local in the root of your project:

OPENAI_API_KEY=your-openai-key
SUPABASE_URL=your-supabase-url
SUPABASE_KEY=your-supabase-service-role-key
ADMIN_KEY=your-secret-password

###4. Run the development server

npm run dev

Now visit http://localhost:3000 🚀


---

##⚙️ Approach & Architecture

#1. PDF Processing & Embedding (app/api/pdfs/embed)

Uploaded PDFs are processed server-side with pdfjs.

Text is split into smaller chunks (≤ 4000 tokens).

Each chunk is embedded with OpenAI and stored in Supabase pgvector along with metadata.

The raw PDF is stored in a Supabase bucket for later use.


#2. Retrieval-Augmented Generation (RAG) (app/api/chat)

User sends a query, along with the chosen PDF and model.

The query is embedded, and the top 3 most similar text chunks are retrieved.

These chunks are merged into a context window along with chat history.

The prompt + context are sent to the LLM.

The LLM streams back an answer token-by-token to the frontend.



---

#📂 Project Structure

Chat_pdf/
├── app/
│   ├── api/          # API routes (upload, embed, chat)
│   ├── components/   # Reusable UI components
│   ├── page.tsx      # Main UI page
├── lib/              # OpenAI + Supabase helpers
├── providers/        # Context providers
├── db/               # Supabase schema & connection
├── types/            # TypeScript types
├── public/           # Static assets
├── middleware.ts     # Protects API routes
├── .env.example      # Env template
└── README.md


---

#🔒 Authentication

API routes (/api/upload, /api/chat) are protected with a simple ADMIN_KEY.

On login, an HttpOnly cookie is set → required for further API access.

This is demo authentication only.

For production, consider NextAuth / Auth0 / Clerk.



---

#🛠️ Tech Stack

Frontend: Next.js (React, TypeScript), TailwindCSS, shadcn/ui

Backend: Next.js API Routes (Serverless)

Database: Supabase (pgvector + storage)

AI / LLM: OpenAI API, LangChain

Streaming: Vercel AI SDK



---
