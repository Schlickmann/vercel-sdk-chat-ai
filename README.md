<div align="center">

# 🤖 Chat AI — Vercel AI SDK + OpenAI

**A real-time streaming chat app built with Next.js 13, the Vercel AI SDK, and GPT-3.5 Turbo.**

[![Next.js](https://img.shields.io/badge/Next.js-13-black?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.1-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vercel AI SDK](https://img.shields.io/badge/Vercel_AI_SDK-2.x-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://sdk.vercel.ai/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--3.5_Turbo-412991?style=for-the-badge&logo=openai&logoColor=white)](https://platform.openai.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.3-06B6D4?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

</div>

---

## ✨ Features

- 🌊 **Real-time streaming** — responses stream in token by token, just like ChatGPT
- ⚡ **Edge Runtime** — API route runs on Vercel's Edge Network for low-latency, globally distributed responses
- 💬 **Conversation history** — full multi-turn chat context sent with every request
- 🎨 **Clean UI** — scrollable message feed with user and AI avatars, built with shadcn/ui
- 🔒 **Server-side API key** — your OpenAI key stays on the server, never exposed to the client
- 📱 **Responsive** — centered card layout that works on any screen size

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Framework | [Next.js 13](https://nextjs.org/) (App Router) |
| Language | [TypeScript](https://www.typescriptlang.org/) |
| AI / Streaming | [Vercel AI SDK](https://sdk.vercel.ai/) (`ai` package) |
| LLM | [OpenAI GPT-3.5 Turbo](https://platform.openai.com/) via `openai-edge` |
| UI Components | [shadcn/ui](https://ui.shadcn.com/) (Radix UI primitives) |
| Styling | [Tailwind CSS](https://tailwindcss.com/) |
| Icons | [Lucide React](https://lucide.dev/) |
| Runtime | [Vercel Edge Runtime](https://vercel.com/docs/functions/edge-functions) |

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- An [OpenAI API key](https://platform.openai.com/api-keys)

### 1. Clone the repo

```bash
git clone https://github.com/Schlickmann/vercel-sdk-chat-ai.git
cd vercel-sdk-chat-ai
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env.local` file in the root of the project:

```bash
cp .env.example .env.local
```

Then add your OpenAI API key:

```env
OPENAI_API_KEY=sk-...your-key-here...
```

> You can get an API key from [platform.openai.com/api-keys](https://platform.openai.com/api-keys).

### 4. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser. Start chatting! 🎉

---

## 📁 Project Structure

```
vercel-sdk-chat-ai/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── chat/
│   │   │       └── route.ts      # Edge API route — streams GPT-3.5 responses
│   │   ├── globals.css           # Global styles
│   │   ├── layout.tsx            # Root layout
│   │   └── page.tsx              # Home page — renders <Chat />
│   ├── components/
│   │   ├── ui/                   # shadcn/ui primitives (Avatar, Button, Card…)
│   │   └── Chat.tsx              # Main chat component (client-side)
│   └── lib/
│       └── utils.ts              # Utility helpers (cn, etc.)
├── .env.local                    # Your secrets (not committed)
├── next.config.js
├── tailwind.config.js
└── tsconfig.json
```

---

## 🔍 How It Works

```
User types a message
       │
       ▼
[Chat.tsx — useChat hook]   ← manages messages state & input
       │  POST /api/chat
       ▼
[route.ts — Edge Runtime]   ← sends messages to OpenAI
       │  GPT-3.5 Turbo stream
       ▼
[OpenAIStream]              ← converts OpenAI chunks → Web ReadableStream
       │
       ▼
[StreamingTextResponse]     ← streams tokens back to the browser in real-time
       │
       ▼
[useChat]                   ← appends tokens to message as they arrive
       │
       ▼
UI renders streamed response live ✨
```

The Vercel AI SDK handles all the streaming plumbing. The `useChat` hook on the client and `OpenAIStream` + `StreamingTextResponse` on the server do the heavy lifting, so the only business logic you need to write is the OpenAI API call itself.

---

## 🌐 Deploy to Vercel

The fastest way to deploy is with the button below. You'll be prompted to add your `OPENAI_API_KEY` environment variable during setup.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/Schlickmann/vercel-sdk-chat-ai&env=OPENAI_API_KEY&envDescription=Your%20OpenAI%20API%20key&envLink=https://platform.openai.com/api-keys)

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">
  Built by <a href="https://github.com/Schlickmann">Julian Schlickmann</a> ·
  <a href="https://vercel-sdk-chat-ai.vercel.app">Live Demo</a> ·
  <a href="https://sdk.vercel.ai/docs">Vercel AI SDK Docs</a>
</div>
