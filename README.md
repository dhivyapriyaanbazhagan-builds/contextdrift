# ContextDrift

> A proof-of-concept tool that detects topic drift in AI chat sessions and extracts focused, clean threads — ready to continue in a new window with zero noise.

---

## The problem

Most people don't realise that mixing topics in one AI chat window actively degrades the model's responses.

Every LLM processes your **entire conversation history** on every response. That history lives inside a fixed-size **context window**. When topics mix — a roadmap discussion, then a user research question, then a stakeholder email — three things break down:

| Problem | What's happening |
|---|---|
| **Attention dilution** | Transformer attention is distributed across all tokens. Irrelevant turns pull weight away from what matters. Responses become generic or hedged. |
| **System prompt erosion** | The "lost in the middle" effect (Liu et al., Stanford 2023) — LLMs recall context at the edges of a window better than content buried in the middle. Your early instructions fade. |
| **Token waste** | Every API call re-processes the full history. You're paying compute cost on noise unrelated to your current question. |

No AI chat product has solved this natively yet.

---

## What this does

**ContextDrift** reads a mixed conversation, uses Claude to semantically cluster messages by topic, and lets you extract a clean, linear thread — formatted and ready to paste into a new chat as focused context.

```
Mixed conversation (12 messages, 3 topics)
        ↓
Claude clusters by semantic similarity
        ↓
You select a theme
        ↓
Clean extracted thread (4 messages, 1 topic)
        ↓
Paste into new chat → model only sees what's relevant
```

---

## Tools in this repo

| File | What it does |
|---|---|
| `chat-thread-sorter (1).html` | Paste any conversation → detect themes → export a focused thread 

---

## Quick start

No installation. No backend. No framework.

1. Clone or download this repo
2. Open any `.html` file in your browser (or via VS Code Live Server)
3. Add your Anthropic API key at [console.anthropic.com](https://console.anthropic.com)
4. Paste the key into the field in the sidebar

> **Note:** The Anthropic API requires separate credits from a Claude.ai Pro subscription. A $5 top-up is enough for extensive testing — each conversation analysis costs roughly $0.01–0.03.

---

## Demo without an API key

Open `chat-thread-sorter (1).html` — it includes a built-in demo mode in the sidebar that walks through the full flow using a pre-analysed PM conversation. No API key needed to see how it works.

---

## Why this should be a native feature

Power users of AI tools inevitably drift across topics in long sessions. The chat UI treats every conversation as a single coherent thread. It isn't.

A **"Split thread by theme"** feature — one button — would:
- Improve response quality for long-session users
- Reduce token cost per query
- Make the product feel like it understands how people actually work

It doesn't exist in Claude, ChatGPT, or Gemini yet.
