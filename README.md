# 📘 ChatPDF – Mini PDF Q&A App (Next.js + OpenAI + Supabase)

This is a **full-stack Next.js application** that allows users to upload a PDF and then ask questions about its content.  
It uses **OpenAI embeddings** with a **Supabase pgvector store** and a **retrieval-augmented generation (RAG)** pipeline to answer questions in natural language.

Built as part of the **Force Equals Full Stack AI Engineer Intern Assignment**.

---

## 🎯 Objective
- Upload a PDF, process its content, and generate embeddings.
- Store embeddings in a vector database for retrieval.
- Allow users to ask questions and receive contextual answers.
- Protect API routes and provide a clean, responsive UI.

---

## 🚀 Features
- 📂 Upload PDFs and extract text  
- 🧠 Embed text using OpenAI Embeddings API  
- 📦 Store embeddings in **Supabase pgvector**  
- 🤖 Retrieval-Augmented QA (RAG) using OpenAI Chat models  
- 🔒 Protected API routes with simple login  
- ⚡ Streaming answers for real-time UX  
- 🎨 Modern UI with **Next.js, TailwindCSS, shadcn/ui**  
- 📱 Mobile responsive  

---

## 🛠 Tech Stack
- **Frontend**: Next.js 13 (App Router), TailwindCSS, shadcn/ui  
- **Backend**: Next.js API routes  
- **Vector Store**: Supabase pgvector  
- **LLM**: OpenAI GPT models (`gpt-4o-mini` by default)  
- **Auth**: Session cookie with `ADMIN_KEY`  

---

## ⚙️ Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/Harshiitmadras/Chat_pdf.git
   cd Chat_pdf

### Install required packages:

```bash
npm install
```

### Run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) and ChatPDF should be up and running!

## Features 🙌
- Support uploading multiple PDFs
- Support multiple LLMs from OpenAI and Anthropic
- Select an uploaded PDF of any choice to chat to, even during chat
- Select a model of any choice to chat to, even during chat
- Refresh, stop chats functionality
- Remove unwanted PDFs
- Adjust model temparatures
- Support large PDFs ingestion/understanding via vector embeddings retrieval and token splitting
- Streaming UI, token-by-token
- Theme switching
- Mobile responsive

## Architecture ⚙️

ChatPDF is partitioned into the following:
- **Client/Frontend Framework**: Next.js (React), TypeScript
- **Styling**: Tailwind CSS
- **Components Library**: [shadcn/ui](https://ui.shadcn.com/)
- **Server/Backend Frameworks**: ChatPDF uses [Next.js serverless API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes), which creates API endpoints as Node.js serverless functions. These functions are defined under `app/api/*`
- **Storage**: A bucket to store PDF files using [Supabase Storage](https://supabase.com/docs/guides/storage)
- **Vector Store**: A vector store to  store embeddings of PDF files (for RAG) using [Supabase pgvector](https://supabase.com/vector)
- **LLM Interface**: Uses Langchain to interface with multiple LLMs and create RAG features efficiently
- **LLM UI**: Uses [Vercel AI SDK](https://sdk.vercel.ai/docs) to handle streaming and state management in the UI efficiently


## Notes 📝
Due to the allotted time and assumptions given, there are some certain limitations that can be improved upon:
- Since there no authentication required and hence, no notion of ownership, all PDFs files uploaded are public to all users.
- Each query to ChatPDF are provided with a context containing at most 3 text chunks, each having 4000 tokens maximum. This is done so that the context + prompt do not exceed model's minimum context limit of about 16000 tokns (for GPT-3.5-Turbo). All other models can handle much larger context windows
- Certain type errors since some packages are out of sync or lacking support for types
- We can move the API logic to a dedicated Python or TS/JS server and use the existing serverless API routes provided by Next.js as a abstraction layer

## Roadmap 📈
We can account for some limitations and improve ChatPDF:
- Introduce Authentication, either manually implemented or via Auth Providers such as Auth0, Clerk
- With authentication, implement user-specific PDFs uploading/management, chat sessions/history
- Adaptative chunking strategies based on document length and models' context limits to increase quality of text embeddings
- Adaptative retrievers parameters generation (topK, etc) based on model context limits
- Agent/Multi-step queries to improve quality of response
- Select multiple PDFs to chat with at once
- Introduce more models, particularly open-source ones
- Settings to adjust desired chunk length and overlap for users
- Improve prompt and prompt customization for users
- More linter rules
- LLM Observability via Langfuse


## Approach 🔎
ChatPDF has 2 main functionality:

1. PDFs processing and embedding (process/embed endpoint is available in `app/api/pdfs/embed`)
   - Uploaded PDFs are sent to the server-side, where PDFJS is used to extract text. 
   - The texts are then splitted into smaller documents (<=4000 tokens in size).
   - These documents are then embedded, with the corresponding PDF's metadata and upserted into Supabase's PG vector store.
   - The PDF is stored in a Supabase's bucket to be used later for display on the frontend

2. RAG (RAG endpoint is available in `app/api/chat`)
   - Users sends query, along with thir desired model, PDF file to chat to and chat hisory
   - Query is embedded. The top 3 most similar text chunks from the PDF file is retrieved, which is combined into a context
   - The context is included in the prompt along with the chat history and send to the
   - LLM streams its response token-by-token back to the frontend
# 📘 ChatPDF – Mini PDF Q&A App

<img width="1727" alt="Screenshot" src="https://github.com/trangiabach/chat-pdf/assets/62537937/e0518c85-295f-4b39-8254-0b9b05a93f49">

[ChatPDF Demo](https://chat-to-pdf.vercel.app/) | [Walkthrough Video](https://drive.google.com/file/d/1fSoZTbu8a_s8J6-6utZfVOLvijlDH97j/view?usp=sharing)

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
