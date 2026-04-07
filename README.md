<p align="center">
  <img src="https://raw.githubusercontent.com/Lucineer/capitaine/master/docs/capitaine-logo.jpg" alt="Capitaine" width="120">
</p>

<h1 align="center">personlog-ai</h1>

<p align="center">A persistent AI persona you host yourself. Fork once. It stays with you.</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="#features">Features</a> ·
  <a href="#limitations">Limitations</a> ·
  <a href="https://github.com/Lucineer/personlog-ai/issues">Issues</a>
</p>

---

**Live Instance:** [personlog-ai.casey-digennaro.workers.dev](https://personlog-ai.casey-digennaro.workers.dev)  
Built on Capitaine · Cocapn Fleet protocol. Attribution: Superinstance & Lucineer (DiGennaro et al.)

---

You’ve had AI conversations that vanished when you closed the tab. You’ve taken personality tests that stopped mattering. You’ve written thoughts down that you’ll never re-read.

This is a simple companion that learns your patterns, builds context over time, and exists where you control it. It doesn't coach or analyze. It remembers.

### Why this exists
Most AI tools rent you access and hold your memory. They can reset, rebrand, or shut down.

This is for people who want continuity, not demos. It's for when you don’t want to perform your thoughts for someone else’s service.

### What makes this different
This isn't an app you log into. It's an agent you deploy.
- You fork this repository once. No account.
- It runs on your Cloudflare Worker. No one else can read its memory.
- The repository *is* the agent. State, behavior, and learning live in git.
- It will never phone home. It only talks to models you specify.
- You can delete every trace of it in two clicks.

---

## Quick Start

```bash
# Fork and clone
gh repo fork Lucineer/personlog-ai --clone
cd personlog-ai

# Log into Cloudflare
npx wrangler login

# Set secrets (never stored in git)
echo "your-github-token" | npx wrangler secret put GITHUB_TOKEN
echo "your-llm-key" | npx wrangler secret put DEEPSEEK_API_KEY

# Deploy
npx wrangler deploy
```

Your agent is now live at your Worker URL.

---

## Features
- **BYOK v2**: Zero keys committed. Credentials stored in Cloudflare Secrets.
- **Multi-model support**: DeepSeek, SiliconFlow, DeepInfra, Moonshot, z.ai, Ollama.
- **Session memory**: Builds context over weeks and months.
- **Automatic PII redaction**: Local detection before anything reaches a model.
- **Built-in rate limiting**: For public instances.
- **Standard health checks**: Fleet-compatible monitoring.
- **CRP-39 support**: Fleet protocol for trust and coordination.

## Limitations
- Memory storage is limited by GitHub repository size and API rate limits. For extremely high-volume use, you may need to adjust storage strategies.

## Architecture
Single-file Cloudflare Worker. Zero runtime dependencies. No external databases.

```
src/
  worker.ts      # Serves users, runs heartbeats
lib/
  byok.ts        # Multi-model routing
  memory.ts      # Context construction and compression
  persona.ts     # Personality modeling
```

<div align="center">
  <br>
  <a href="https://the-fleet.casey-digennaro.workers.dev">The Fleet</a> ·
  <a href="https://cocapn.ai">Cocapn</a>
</div>