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

This repository currently documents the platform. The platform has working implementations across local inference, FastAPI services, voice integration, and the read-only workspace adapter, running on the builder's own lab. Not every subsystem is enabled in every deployment — verify the running configuration before demos or claims. Live now: a hallucination guard in the backend — grounded chat answers plus reply scrubbing — wired to a YOLO person detector and vision yes/no answering — and an operator restart button in the UI (POST /admin/restart, polls /health until the backend is back). Console metrics are live too — the dashboard's Health/CPU/Memory/Disk/Net cards now read real values from the backend, and the live cognitive stream authenticates with the operator session token. The console was redesigned in November 2026 — one page with the Jewel orb as the centerpiece, the N.I.G.U.E.L banner beneath it, four information panels across the top (Runtime, Operational Notes, Agents alert summary, Health), and an action row (Commands, Restart Backend, Living World) — all values live from the backend, no mock data. A follow-up look round the same day swapped in the real particle-cosmos orb, holographic glass panels, animated conduits, a live-values ticker, and orb state controls. A final exact-transplant round the same night reproduced the mockup itself: four chamfered glass panels in one row, a re-implemented bright particle orb (dense stars, diamond center, rotating rings), one screen with no scrolling, and the lower sections moved to a console-details view — all values still live. An orb fix the next morning (November 10, 2026) cured the orb rendering invisible on the live console — a zero-width layout collapse in the browser — compacted the surrounding chrome so the orb takes a much larger share of the screen, and was proven with headless-browser screenshots of a throwaway harness before going live. A second orb round the same morning replaced the starfield orb with a blue plasma ball — electric filaments, a moving inner nebula, and a pulsing core that reacts to NIGUEL's state (idle drift, listening reach, thinking churn, speaking flare) — and sized it to the viewport so it stays big on short displays, proven with headless-browser screenshots before going live. A third orb round later that morning, from a video reference of a particle-mesh sphere with flowing inner energy, reworked the orb again into a blue particle sphere with flowing energy ribbons whose colors ease smoothly between states instead of snapping, proven with timed headless-browser screenshots before going live. A fourth orb round the same day, at the builder's direction to match the video exactly, densified the sphere to ten thousand points, widened the ribbons into broad smoky bands that fold over the sphere, added a drifting outer particle cloud, and slowed the motion to the video's unhurried pace, proven with timed screenshots and pixel measurements against the video frames before going live. A fifth orb round the same day applied a second code review's fixes — no more effect restarts, closed ribbon gaps, frame-rate-independent ripples, depth-faded outer cloud, wider hot core — and fixed a crash the review surfaced, where the outer-cloud loop iterated the wrong value and left the orb blank on the live console; proven bright again with timed screenshots before going live. A sixth orb round the same day, at the builder's "that doesn't look organic," cut the ribbon brightness roughly threefold so the bands read as soft translucent smoke with the sphere visible through them, faded the bands out at the rim, and redrew them as single smooth polygons after the per-segment version left a comb of radial teeth at the folds; proven against the video frames by pixel measurement (orb brightness now close to the reference, zero near-white pixels) before going live. A seventh orb round the same day applied a second Kimi code review's frame-by-frame gap analysis — the dot mesh now reads through the whole sphere including the back side, the frame rings are gone, ribbon edges are frayed with a high-frequency factor, folds carry sharp creases from a fourth harmonic, a dim filament thread runs inside the bands, and the center glow and outer cloud are dimmer still; proven against the video frames by timed screenshots and pixel measurements before going live. An eighth orb round the same day, at the builder's feedback that the geometry wasn't cohesive, the back-side lines popped in and out, the motion didn't read as responding, and no state labels were visible, replaced the hard front/back split with a soft depth fade so bands fade smoothly behind the sphere, made the state response obvious (idle calm and dim, speaking a clear bright flare with a breathing pulse), and added a visible IDLE / LISTENING / THINKING / SPEAKING label under the orb that fades between states; proven with timed screenshots at the true rack viewport and pixel measurements (idle brightness now matches the reference frame, speaking roughly 75% brighter, zero near-white pixels) before going live. A ninth change the same evening added the operator completion rating to the console — the action row's empty slot became a compact chip showing the daily 0–100% operator-completion score (42% at first read, amber band under 50%) that opens a full breakdown on the details view, with five weighted component bars, the date, and what moved since the last read; the rating is a daily judgment kept in a UI-side data file, no backend change; proven with headless-browser screenshots at the true rack viewport before going live once the tower came back online. A tenth change later the same evening fixed the retention root cause in the backend — the knowledge-block load caps rose from 400/800 to 2500 characters so the model finally sees the full sharpened directives, and a blocked or misclassified change proposal now falls through to the language model instead of swallowing a knowledge question as a refusal; the WordPress flaw (CVE-2026-119977, fix in 7.1.4+) that had been refused four times now answers live, and the earlier retention wins still hold; proven with a live voice probe (four of four correct) before the swap was declared done. An eleventh change on November 11, 2026 hardened the backend after two external code reviews: the reply scrub now covers the voice path as well as typed chat, missing or defaulted cluster secrets fail loud in production instead of falling back silently, voice authentication fails closed when unconfigured, the agent-to-agent endpoints require an operator token, and content arriving from the vault, web search, and tool output is marked as untrusted reference data before it reaches the model; proven with an import gate and functional smoke tests inside the candidate image, plus a live unauthenticated probe of the agent endpoints returning 401 after the swap. A follow-up the same night closed the reply scrub's last two pattern gaps — the bracketed ECP tag line and the full Evidence-Constrained Patch banner — verified against the scrub's whole test battery inside the candidate and again in the running container after the swap.

Roadmap: source publication, reproducible setup docs with a tested quickstart and health check, automated boundary/latency tests, demo clip, sanitized demo assets.

## About the builder

**Jamai Jamison — Technical Systems Engineer.** 10+ years in media/streaming technical operations and infrastructure (Prime Video, Disney, Sony, MLB/BAMTECH); now building local AI infrastructure, LLM orchestration, backend integration, and security-conscious automation. Previous work includes Emmy-recognized NBA production.

- LinkedIn: https://www.linkedin.com/in/jimai-jamison-35864899
- Website: https://allthathustle.com
