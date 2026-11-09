# N.I.G.U.E.L. — Local AI Orchestration & Developer Infrastructure

> **Networked Intelligence for Generative Understanding, Execution, and Learning**
>
> A modular AI platform that runs local LLM inference, agent/tool orchestration, backend services, memory-oriented capabilities, voice integration, and controlled developer-workspace tooling — on self-owned hardware, with governed access boundaries.

## What it does

- **Local LLM inference:** Ollama serving models on local hardware (`mistral:latest`, `qwen2.5:1.5b`, `phi3:mini`, plus `nomic-embed-text` for embeddings).
- **Agent backend & orchestration:** Python/FastAPI services connecting inference, tools, and integrations as modular components — not a monolithic chatbot.
- **Controlled VS Code/workspace integration:** read-only adapter for listing/reading/searching workspace files, Git status/diffs, and diagnostics — with server-configured roots, path-traversal and symlink-escape rejection, and sensitive paths (`.git`, `.env*`, credentials) restricted.
- **Voice integration:** Alexa path via AWS Lambda and a custom backend; recorded backend latency **3.05s** against a 6-second response constraint.
- **Systems work:** model serving, Linux infrastructure, networking, diagnostics, and hardware/software integration on a self-built lab (Ryzen 7, AMD RX 9060 XT + RX 580, NUC-based services).

## Architecture at a glance

```text
                 Voice interface (Alexa / Lambda)
                        |
                        v
+----------------+   +---------------------------+   +------------------+
| VS Code        |-->| Python / FastAPI services |-->| Ollama           |
| read-only      |   | orchestration and APIs    |   | inference        |
| workspace tool |<--| tool governance/diagnostics|<--| inference        |
+----------------+   +-------------+-------------+   +------------------+
                                  |
                                  v
                     +---------------------------+
                     | Configured workspace and  |
                     | integration boundaries    |
                     +---------------------------+
```

## Tech

| Layer | Detail |
|---|---|
| Backend/API | Python, FastAPI |
| Local inference | Ollama (`mistral`, `qwen2.5:1.5b`, `phi3:mini`; `nomic-embed-text` embeddings) |
| Developer integration | TypeScript VS Code adapter; read-only workspace API |
| Voice | Alexa, AWS Lambda, custom backend |
| Environment | Linux, self-owned lab hardware |

## Status

This repository currently documents the platform. The platform has working implementations across local inference, FastAPI services, voice integration, and the read-only workspace adapter, running on the builder's own lab. Not every subsystem is enabled in every deployment — verify the running configuration before demos or claims. Live now: a hallucination guard in the backend — grounded chat answers plus reply scrubbing — wired to a YOLO person detector and vision yes/no answering — and an operator restart button in the UI (POST /admin/restart, polls /health until the backend is back). Console metrics are live too — the dashboard's Health/CPU/Memory/Disk/Net cards now read real values from the backend, and the live cognitive stream authenticates with the operator session token.

Roadmap: source publication, reproducible setup docs with a tested quickstart and health check, automated boundary/latency tests, demo clip, sanitized demo assets.

## About the builder

**Jamai Jamison — Technical Systems Engineer.** 10+ years in media/streaming technical operations and infrastructure (Prime Video, Disney, Sony, MLB/BAMTECH); now building local AI infrastructure, LLM orchestration, backend integration, and security-conscious automation. Previous work includes Emmy-recognized NBA production.

- LinkedIn: https://www.linkedin.com/in/jimai-jamison-35864899
- Website: https://allthathustle.com
