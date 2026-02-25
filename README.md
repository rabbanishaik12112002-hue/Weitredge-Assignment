🤖 AI Powered Support Assistant

A full-stack AI-powered support chat application built with React, Node.js, and SQLite.

The assistant answers user queries strictly based on provided documentation using LLM integration while maintaining session-based conversation history stored in SQLite.

👤 Author

Name: Shaik Rabbani
GitHub: https://github.com/rabbanishaik12112002-hue

Repository: https://github.com/rabbanishaik12112002-hue/Weitredge-Assignment

🚀 Tech Stack
Layer	Tech
Frontend	React.js (Vite)
Backend	Node.js (Express)
Database	SQLite
AI/LLM	OpenAI / Gemini / Mistral etc.
API Protection	express-rate-limit
🏗️ Project Architecture
Frontend (React)
        ↓
Backend API (Express)
        ↓
SQLite Database (Sessions + Messages)
        ↓
LLM (Prompt with Docs + Context)
📂 Project Structure
Weitredge-Assignment/
│
├── frontend/           → React application
│   ├── src/
│   │   ├── components/
│   │   ├── App.js
│   │   ├── index.js
│   │   └── api.js
│   └── package.json
│
├── backend/            → Express API
│   ├── routes/
│   ├── controllers/
│   ├── services/
│   ├── middleware/
│   ├── docs.json
│   ├── server.js
│   └── package.json
│
└── README.md
🗄️ Database Schema
Table: sessions
Column	Type	Notes
id	TEXT	Primary Key (sessionId)
created_at	DATETIME	Session creation timestamp
updated_at	DATETIME	Last activity timestamp
Table: messages
Column	Type	Notes
id	INTEGER	Auto-increment
session_id	TEXT	FK → sessions
role	TEXT	“user” or “assistant”
content	TEXT	Message text
created_at	DATETIME	Message timestamp
✨ Core Features

✔ Strict document-based question answering
✔ Context memory (last 5 user + assistant message pairs via SQLite)
✔ Persistent sessions using LocalStorage
✔ Rate limiting for API protection
✔ Clean JSON error responses
✔ Responsive chat UI

📄 Document-Based Answering

The assistant uses the docs.json file as the only source of truth.

Example docs.json:

[
  {
    "title": "Reset Password",
    "content": "Users can reset password from Settings > Security."
  },
  {
    "title": "Refund Policy",
    "content": "Refunds are allowed within 7 days of purchase."
  }
]
❗ Strict AI Rules

The assistant:

Uses ONLY information from docs.json

Uses last 5 user + assistant message pairs from SQLite as context

Does NOT hallucinate

Does NOT guess

If answer is not found:

“Sorry, I don’t have information about that.”

🧠 Prompt Construction Logic
You are a support assistant.
Only answer using the provided documentation.
If the answer is not found, say:
"Sorry, I don’t have information about that."

Documentation:
{relevant_docs}

Conversation History:
{last_5_pairs}

User Question:
{current_question}
🔌 API Endpoints
1️⃣ POST /api/chat

Request:

{
  "sessionId": "abc123",
  "message": "How can I reset my password?"
}

Response:

{
  "reply": "Users can reset password from Settings > Security.",
  "tokensUsed": 123
}

Errors:

{
  "error": "SessionId and message are required."
}
2️⃣ GET /api/conversations/:sessionId

Returns full conversation history (chronological).

Response example:

[
  {
    "role": "user",
    "content": "How can I reset my password?",
    "created_at": "2026-02-24T10:00:00Z"
  },
  {
    "role": "assistant",
    "content": "Users can reset password from Settings > Security.",
    "created_at": "2026-02-24T10:00:02Z"
  }
]
3️⃣ GET /api/sessions

Returns:

[
  {
    "sessionId": "abc123",
    "lastUpdated": "2026-02-24T10:00:02Z"
  }
]
🚦 Rate Limiting

Basic IP-based rate limiting is implemented using express-rate-limit on all /api routes.

If the limit is exceeded:

{
  "error": "Too many requests. Please try again later."
}
📱 Responsive UI

The chat interface supports:

✔ Mobile screens (responsive card layout)
✔ Medium screens (centered container)
✔ Desktop (scrollable history, clear chat interface)

⚙️ Setup & Run Instructions
🧰 Prerequisites

Ensure you have:

✔ Node.js (v18+)
✔ npm
✔ Git

Check versions:

node -v
npm -v
git --version
📥 Clone Repo
git clone https://github.com/rabbanishaik12112002-hue/Weitredge-Assignment.git
cd Weitredge-Assignment
🖥️ Backend Setup
cd backend
npm install

Create .env:

PORT=5000
OPENAI_API_KEY=your_api_key_here
CORS_ORIGIN=http://localhost:5173

Start backend:

npm run dev

Backend runs at:

http://localhost:5000
🌐 Frontend Setup
cd frontend
npm install
npm run dev

Frontend runs at:

http://localhost:5173
✅ Conclusion

This repository provides a clean, professional implementation of a full-stack document-based AI support assistant with:

✔ Modular architecture
✔ Persistent session memory
✔ Strict prompt rules
✔ Responsive UI
✔ API best practices
