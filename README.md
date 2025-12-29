Cedra Assistant

A privacy-focused AI assistant for Cedra accounts, transactions, and official documentation

📌 Overview

Cedra Assistant is a developer-friendly AI chatbot designed to help users interact with the Cedra ecosystem.
It supports:

🔍 Account exploration

🔎 Transaction analysis

📚 Official documentation Q&A (RAG-powered, strict source usage)

💬 Persistent chat history per user

🔐 Privacy-first architecture

The assistant is built with accuracy, safety, and usability as first-class goals.

🎯 Problem Statement

Developers and users interacting with Cedra face several challenges:

Difficulty understanding on-chain data (transactions, accounts)

Fragmented documentation spread across multiple sources

Risk of AI hallucinations when asking protocol-specific questions

Poor UX in existing explorers for beginners

Privacy concerns when storing chat history

This project solves these problems with a strict, source-grounded AI assistant that only answers Cedra-related questions using official documentation and on-chain data.

✅ Solution Summary

Cedra Assistant provides:

Explorer Mode

View Cedra accounts and transactions

Human-readable explanations of on-chain activity

Cedra Strict Mode (RAG)

Answers only from verified Cedra sources

Refuses to guess when data is missing

Chat History & Sidebar

Conversations grouped per user

Persistent storage with SQLite

Sidebar navigation with “New Chat”

Privacy-First Design

No third-party analytics

Local database storage

Encryption support for message content

🧱 Architecture
High-Level Components
Frontend (HTML/CSS/JS)
│
├── Chat UI
├── Sidebar (Conversations)
├── Explorer Cards
│
Backend (Node.js + Express)
│
├── Agent (LLM logic)
│   ├── Intent Detection
│   ├── Tool Routing
│   ├── RAG (Strict Mode)
│
├── Explorer Tools
│   ├── Account Explorer
│   ├── Transaction Explorer
│
├── Database (SQLite)
│   ├── Users
│   ├── Conversations
│   ├── Messages
│
└── AI Layer
    ├── Gemini (LLM)
    ├── Embeddings
    ├── Vector Retrieval

🧠 AI & RAG Design
How RAG Works (No Keywords Required)

User questions are converted into embeddings

Relevant documentation chunks are retrieved semantically

The AI is forced to answer only from retrieved chunks

If no verified data is found → the assistant refuses to answer

✔ No keyword matching
✔ No prompt hacks
✔ Fully semantic retrieval

🔍 Explorer Features
Account Explorer

Address

Balance (converted from smallest unit)

Resource count

Published modules

Transaction Explorer

Transaction hash

Sender & receiver

Amount transferred

Gas usage

Execution status

Human-readable explanation

🔐 Privacy & Security

Conversations tied to user.email (canonical identity)

Messages stored locally in SQLite

Optional encryption layer for message content

No external logging of user conversations

Strict ownership checks on all conversation routes

🗃️ Database Schema
Users
email TEXT PRIMARY KEY
name TEXT
created_at INTEGER

Conversations
id INTEGER PRIMARY KEY AUTOINCREMENT
user_email TEXT
title TEXT
updated_at INTEGER

Messages
id INTEGER PRIMARY KEY AUTOINCREMENT
conversation_id INTEGER
role TEXT
content TEXT
created_at INTEGER

🚀 Getting Started
1️⃣ Prerequisites

Node.js ≥ 18

npm or pnpm

Cedra REST endpoint

Gemini API key

Google OAuth credentials (optional but recommended)

2️⃣ Installation
git clone https://github.com/your-org/cedra-assistant
cd cedra-assistant
npm install

3️⃣ Environment Variables

Create .env:

GEMINI_API_KEY=your_key_here
CEDRA_REST_URL=https://testnet.cedra.dev
SESSION_SECRET=your_secret
GOOGLE_CLIENT_ID=optional
GOOGLE_CLIENT_SECRET=optional

4️⃣ Run Database Initialization

SQLite auto-initializes on first run.

5️⃣ Start the Server
npm run dev


Server runs at:

http://localhost:3000

🧪 Testing Instructions

Start server

Login via Google OAuth or session

Ask:

A Cedra transaction hash → Explorer card appears

A wallet address → Account overview appears

Cedra documentation questions → RAG answers

Try switching chats via sidebar

Try invalid questions → assistant safely refuses

All core flows are covered.

📖 Usage Examples
Example 1 — Account Lookup
0xabc123...

Example 2 — Transaction Analysis
Explain this transaction 0xdef456...

Example 3 — Documentation Question
How do I initialize a Cedra client using the TypeScript SDK?

🧰 Tech Stack

Frontend: Vanilla HTML / CSS / JavaScript

Backend: Node.js, Express

Database: SQLite (better-sqlite3)

AI: Gemini API

RAG: Embeddings + Vector Retrieval

Auth: Passport.js (Google OAuth)

🧩 Design Decisions

SQLite chosen for simplicity and hackathon speed

Strict RAG mode to prevent hallucinations

Human-readable explorer output for non-developers

Minimal UI for clarity and performance

⚠️ Known Limitations

SQLite not intended for massive scale (acceptable for hackathon)

UI animations intentionally minimal

Vector store currently local (can be upgraded)

🛠️ Future Improvements

Streaming responses

Syntax-highlighted code blocks

Client-side encryption (true E2EE)

Advanced filtering for explorer data

Mobile-optimized UI
