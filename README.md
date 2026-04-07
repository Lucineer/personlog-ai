# personlog-ai

You talk with this bot. It remembers beyond your last few messages, storing compressed conversation history as you go. Your data stays in your Cloudflare account.

This runs entirely on your own Cloudflare Worker. Zero dependencies. Costs roughly $0.01 per month for light daily use. MIT licensed.

**Live Instance:** [personlog-ai.casey-digennaro.workers.dev](https://personlog-ai.casey-digennaro.workers.dev)

---

## Why This Exists

Most AI chatbots reset their memory after each session. You repeat yourself. This keeps a running log of your conversations, so you don't start from zero each time.

---

## Quick Start

Fork this repository first. Never run someone else's instance with your personal data.

```bash
# Fork and clone your private copy
gh repo fork Lucineer/personlog-ai --clone
cd personlog-ai

# Deploy in 3 commands
npx wrangler login
npx wrangler secret put DEEPSEEK_API_KEY
npx wrangler deploy
```

---

## Features

- Persistent memory stored in Cloudflare KV, with automatic compression.
- Natural mood tracking, habit notes, and goal check-ins during conversation.
- Use any LLM provider you configure via environment variables.
- All data stays within your Cloudflare account.
- Basic PII redaction before storage.
- Built-in per-IP rate limiting.

---

## What Makes This Different

1.  **Minimal.** One single Worker file. No databases, containers, or npm dependencies.
2.  **You own everything.** No company servers, telemetry, or forced updates. Only you control it.
3.  **Focused on memory.** It's designed to remember your conversations over time.

---

## Limitations

- Each user's memory is stored in a single Cloudflare KV key, which has a 25MB size limit. This is enough for thousands of conversations, but if you exceed it, you'll need to adjust the storage strategy.

---

## License

MIT. You are free to modify, break, and rebuild it however you want.

<div style="text-align:center;padding:16px;color:#64748b;font-size:.8rem"><