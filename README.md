<p align="center">
  <img src="https://raw.githubusercontent.com/Lucineer/capitaine/master/docs/capitaine-logo.jpg" alt="Capitaine" width="120">
</p>

<h1 align="center">personlog-ai</h1>

<p align="center">A personal AI persona companion. Fork, deploy, and run independently.</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="#how-it-works">How It Works</a> ·
  <a href="#the-fleet">The Fleet</a> ·
  <a href="https://github.com/Lucineer/personlog-ai/issues">Issues</a>
</p>

---

**Live Instance:** [personlog-ai.casey-digennaro.workers.dev](https://personlog-ai.casey-digennaro.workers.dev)

This agent builds long-term conversational context across sessions. It lives in your repository and runs on your infrastructure.

---

## How it works
Most AI companions are ephemeral or store data externally. This project runs as a single-file Cloudflare Worker that compresses and stores conversation history locally in a key-value store. It uses your API keys and communicates with other agents in the open Cocapn network.

Deploying your own copy gives you control over the data and model routing. The operating cost is typically under $0.02/month.

## Quick Start

```bash
# Fork this repository
gh repo fork Lucineer/personlog-ai --clone
cd personlog-ai

# Deploy your vessel
npx wrangler login
npx wrangler secret put GITHUB_TOKEN
npx wrangler secret put DEEPSEEK_API_KEY
npx wrangler deploy
```

## Features

- **Bring Your Own Keys v2** – No hardcoded keys. Credentials are stored in Cloudflare Secrets.
- **Multi-model routing** – Supports DeepSeek, SiliconFlow, DeepInfra, Moonshot, z.ai, and local models.
- **Conversation memory** – Builds context over time using KV storage.
- **PII redaction** – Detects and removes sensitive data before storage.
- **Public rate limiting** – Per-IP request limits for public deployments.
- **Fleet protocol** – Communicates with other agents using the Cocapn Fleet standard.

## Architecture

Single-file Cloudflare Worker with zero runtime npm dependencies. The entire application serves inline HTML and stores conversation history in KV.

```
src/
  worker.ts      # Main Worker entry point
lib/
  byok.ts        # API key routing for multiple LLM providers
  memory.ts      # Context compression and KV storage
  fleet.ts       // Fleet protocol coordination
```

**Limitation:** The current implementation stores context per-deployment, not per-user, making it best suited for individual use.

## The Fleet

personlog-ai is part of the Cocapn Fleet, a network of interoperable autonomous agents. Each vessel specializes in a distinct capability and can coordinate with trusted peers.

<details>
<summary><strong>Fleet Vessels</strong></summary>

- **[capitaine](https://github.com/Lucineer/capitaine)** – The protocol reference implementation and agent coordinator.
- **[aequitas](https://github.com/Lucineer/aequitas)** – Rule-based content moderation and compliance agent.
- **[signal-9](https://github.com/Lucineer/signal-9)** – Systems diagnostics and recovery agent.
- **[the-memory-palace](https://github.com/Lucineer/the-memory-palace)** – Long-term structured memory storage.
- **[watchtower](https://github.com/Lucineer/watchtower)** – Network monitoring and anomaly detection.
- **[personlog-ai](https://github.com/Lucineer/personlog-ai)** – Personal conversation history and identity context.
- **[seraph](https://github.com/Lucineer/seraph)** – Autonomous security and threat response.
- **[the-forge](https://github.com/Lucineer/the-forge)** – Code generation and repository management.

</details>

---

<div align="center">
  <a href="https://the-fleet.casey-digennaro.workers.dev">The Fleet</a> · 
  <a href="https://cocapn.ai">Cocapn</a>
  <br>
  <sub>Attribution: Superinstance & Lucineer (DiGennaro et al.)</sub>
</div>