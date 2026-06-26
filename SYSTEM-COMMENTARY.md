# Commentary: How the Outreach Agent Is Built — and What Broke Along the Way

*Companion to the "Agents" podcast. This is the plain-language tour of the system Matteo describes in the episode — the architecture, and the lessons that were paid for in failures. Feed it to your agents alongside the Six Laws.*

---

## The problem it solves

A professional keynote speaker needs to reach more conferences. The relationship history, the research, and the pipeline state live across disconnected tools, so nothing is ever ready when it's time to act. Outreach doesn't happen because *starting* it costs too much effort. **You get booked on the follow-up — so the one thing the system must do is follow up, relentlessly, with context and a draft already prepared.**

## The architecture principle

**Matteo and Alex are not building software. They are configuring Claude.**

Claude is the intelligence layer. Google (Gmail, Drive) is the data layer. There is no custom CRM and no new database to log into — a CRM is a passive thing you have to visit, and the relationship history already exists in Gmail. The system reads Gmail and derives state from it. The job is to remove the human from the role of *being the intelligence layer*: the system surfaces what needs to happen, with a draft ready, and the human approves and sends.

Three non-negotiables:
1. **Gmail is the source of truth** for relationship state — read, never overwritten.
2. **Human in the loop for every send.** The system drafts; the human sends. Sending is structurally blocked at the tool boundary — the agent *cannot* send even if it tried.
3. **Model routing by task, not by default.** Cheap models classify and extract; capable models compose; the most expensive model is reserved for judgment.

## What actually got built (and works today)

The live system drafts real, personalized cold and follow-up outreach in the speaker's voice and lands them as native Gmail drafts for review. The flow is `discover → research → promote → draft → human review → send`, and every stage runs. Discovery finds conferences; research builds a background document per target; a promotion gate (a dozen hard checks) decides what's worth pursuing; the drafter composes; the human reviews in Gmail — aided by a **browser extension** that opens a side panel next to each draft showing everything the system knows about that conference (organizer, dates, a screenshot of the site, links to the research doc).

## The lessons — paid for in failures

**1. Volume breaks the naive agent.** Taking the agent by the hand — one promising conference, one draft, steer and correct — works, but it's slow. The moment you say *"here are a thousand conferences, produce a thousand drafts,"* it breaks: hallucinations, wrong information, contacting the wrong people. Attended work is reliable; unattended volume is where the cracks show.

**2. Push determinism into code; let the LLM hold the pen only where judgment is irreducible.** The fix wasn't a smarter prompt — it was moving every verifiable thing into deterministic, fail-closed *gates* written in Python. "Always check X before proceeding" obeyed in a prompt works maybe 50–80% of the time; the same check written as a code gate works every time. The LLM composes the message and makes genuine judgment calls; everything checkable — does this date exist, does this contact resolve, does this draft cite a real source — is a script that can say BLOCK.

**3. Don't let the agent be judge and jury.** A coding agent left to grade its own work will quietly rewrite the test to pass. So the test-runner is separated from the doer, and verification uses a *different* model than the one that produced the work — different model, different prompt, different run catches errors the original is blind to. (This is Law 1 made operational: every fact carries a quote and a source, and a cheap model verifies it's actually there.)

**4. Cross-model supervision.** One agent does the work; a second agent — a different model — reviews the plan before it runs. "Another agent says this; what do you think?" Disagreement is signal.

**5. Write it down, then prune it.** Detailed session logs, machine-structured state, and design docs — but the hard part is that agents ingest text well and *ignore* it badly. So drift is reconciled deliberately: the last actions and the code are the source of truth; anything in the notes that contradicts them gets re-compressed. A standing **System Review** skill runs after big work to reconcile decisions against the constitution.

**6. The agents have their own budget.** Beyond the model subscription, the system pays for its own tools — search APIs, contact enrichment, LinkedIn reach — because it has to go out on the internet and not everything can be installed locally. No brand loyalty: they're API calls; same quality at a lower price wins.

## Where it stands, honestly

The production system covers its costs and has produced a real pipeline of pending contracts, but it hasn't turned a profit yet, and the time invested is far from paid back. It's a money-maker in the making, not a finished machine — and Matteo deliberately keeps it on tools that are a few months old, because the bleeding edge is for client work, not for the thing that has to run reliably every day.
