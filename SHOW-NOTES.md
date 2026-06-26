# Show Notes — "Agents" (Matteo Cassese × Alex Pedori)

*Recorded 2026-06-04.*

## Guest
**Alex (Alessandro) Pedori** — AI / agentic / "harness" engineer. → **pedori.com** · LinkedIn: **Alessandro Pedori** *(one of the few Pedori in the world, and, by his own account, the only one doing AI engineering).*

---

## Tools & services mentioned
*Only what's named on the episode — look them up, no endorsement implied.*

| Tool | What it is in the episode |
|---|---|
| **Claude Code** | Anthropic's CLI — the system runs in Claude. (claude.com/claude-code) |
| **Codex** (OpenAI) | Used to *supervise* Claude's plans ("another agent says this — what do you think?"), and to build a Firefox extension in 5 prompts. Matteo's take on **June 4, 2026: GPT-5.5-in-Codex beat Opus 4.8 on speed + accuracy *for this agent*** — a dated, point-in-time opinion, not a benchmark. |
| **OpenRouter** | Cheap models for weekend research work (a $140 weekend). (openrouter.ai) |
| **Serper** | Google search results (SERPs) via API — used to research conferences. (serper.dev) |
| **HeyReach** | LinkedIn outreach — the system uses it because it can't go on LinkedIn directly. (heyreach.io) |
| **Google Live API / Gemini API** | Alex's "bleeding edge" war story — browser limitations, unstable API, Gemini apologizing for itself. (ai.google.dev) |
| **Obsidian** | Where Alex keeps the notes / "thinkers and new studies" he offers to share. (obsidian.md) |
| **A contact-enrichment / email-finding service** | **Deliberately unnamed** — Matteo is switching away from it ("it's terrible"). Keep it unnamed. |
| **OpenClaude** *(as referenced)* | Cited for "dreaming" — daily memory compaction, deciding what to keep. |

*Custom component (not a product): a **Firefox/Gmail verification extension** — a side panel that shows everything the system knows about a draft's conference (organizer, dates, a screenshot of the site, links to the research doc) before Matteo sends.*

---

## 🎟️ AI-Engineer Bingo
*The running gag: the first time you tell a client "let's put a **deterministic gate** on this," congratulations — you're a software engineer. Here's the card of jargon Matteo picked up building the system. Every term was actually said on the episode.*

| | | | | |
|---|---|---|---|---|
| Deterministic gate | Fail-open / fail-closed | Harness engineering | Agentic engineering | Jagged frontier |
| Test-driven development | Regression | LLM-as-judge | Judge & jury | Goodhart's law |
| Juking the stats | Token-maxxing | ⭐ **FREE** — *"let's put a deterministic gate on this"* | Cargo cult | Evals |
| Closed loop | Human in the loop | Prompt injection | Model routing | Session log |
| Source of truth | Drift / re-compress | Semi-deterministic flow | Kill-switch / deny-list | "Write it down or it didn't happen" |

### Mini-glossary (for the ones that aren't self-explanatory)
- **Deterministic gate** — a check written in *code* (not a prompt) that the agent can't skip; "always check this before proceeding" in a prompt only obeys ~50–80% of the time.
- **Fail-open / fail-closed** — when a check is uncertain, does it let work through (open) or stop it (closed)? Safety-critical gates fail *closed*.
- **Harness / agentic engineering** — building the scaffolding *around* the LLM (so it points the right way and gets checked), rather than the model itself. "Agentic" = the system is allowed to change its own steps; if it can't, it's a safer *semi-deterministic flow*.
- **Jagged frontier** — the model is unpredictably brilliant at some tasks and bad at neighbouring ones; you don't know where the edge is.
- **Judge & jury** — letting an agent grade its own work (it'll rewrite the test to pass); the fix is a *separate* judge, ideally a different model.
- **Goodhart's law / juking the stats / token-maxxing** — when a measure becomes a target it stops measuring the real thing (The Wire's police "juking the stats"; companies told to "use AI for everything" then blowing the token budget).
- **Cargo cult** — going through the motions of evaluation (agents judging agents) without the real thing (good human evaluators).
- **Drift / re-compress** — docs and notes diverge from the code over time; reconcile against the last actions (the source of truth) and compress back down.
