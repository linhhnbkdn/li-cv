# Elffie Backend Engineer Assessment — Answers

## Question 1 — PR Review

### A) PR Comment 

*Assuming networking, authentication, and other infra concerns have already been verified.*

> **PR Comment (Suggestion — non-blocking):**
>
> Hey [name], logic looks good and I'm approving this for today's demo.
>
> One suggestion before merge — wrap the LLM call with a long timeout as a safety net so the app doesn't hang indefinitely if OpenAI is slow:
>
> ```python
> import asyncio
>
> async def call_llm_with_timeout(payload, timeout_seconds=90):
>     try:
>         return await asyncio.wait_for(
>             llm_client.complete(payload),
>             timeout=timeout_seconds,
>         )
>     except asyncio.TimeoutError:
>         raise HTTPException(status_code=504, detail="LLM request timed out, please retry.")
> ```
>
> Note: this fix only makes the request fail gracefully instead of hanging — it does **not** retry. The user will still get a 504 if OpenAI is slow. A proper retry mechanism against OpenAI (or any third-party LLM provider) is something we'll need to handle properly down the line. I'm treating this as tech-debt and will create a ticket for it.
>
> Once this is merged, I'll spin up a Slack channel to coordinate a quick smoke test with you and QA before we go into the demo.
>
> ✅ Approved.

During the demo, proactively tell the client:

> *"We have a known limitation with LLM response handling under load — we've already identified the fix and it's lined up for the next release."*

---

### B) Two architectural changes for production

Context: we need to release to prod on schedule next week. This is a simple request/response service — no queue, no retry. The goal is stability and reducing tight coupling to OpenAI, not a full rewrite.

**1. Refactor with Dependency Injection — inject the LLM client**

The immediate goal is clean code — business logic should not be responsible for constructing its own dependencies. Inject the LLM client from outside, keeping each layer focused on a single responsibility.

```python
class LLMService:
    def __init__(self, llm_client: LLMClient):
        self.llm_client = llm_client

    async def process(self, payload):
        return await self.llm_client.complete(payload)
```

**2. Circuit Breaker (singleton)**

When OpenAI is slow or down, fail-fast immediately instead of letting the user hang. The circuit breaker must be a **singleton** — it tracks failure state at the instance level, so if it is recreated per request the state resets every time and the breaker never actually trips.

```python
import pybreaker

# instantiated once at app startup, shared across all requests
llm_breaker = pybreaker.CircuitBreaker(fail_max=5, reset_timeout=30)

class OpenAIClient:
    def __init__(self, breaker: pybreaker.CircuitBreaker):
        self.breaker = breaker

    def complete(self, payload):
        return self.breaker.call(self._do_request, payload)
```

**Why no retry:** this is a pure request/response service with no queue. Adding retry here just means the user waits longer per attempt with no guarantee of success — it adds latency without real reliability gain. Retry belongs at the worker level when there is a queue to back it.

**Known trade-off:** the system remains synchronous — each request blocks while waiting for OpenAI. At low workload this is acceptable. When traffic scales up, a proper async migration will be required — that should be planned and prioritized before the next growth milestone.

**Future migration note:** the DI and Circuit Breaker changes above are deliberate groundwork. When the system migrates from sync to async (task queue + worker pool), the injected LLM client and breaker slot cleanly into the worker layer. That migration also unlocks: retry with exponential backoff, rate limiting, OpenAI API quota management, model switching (e.g. fallback from GPT-4 to GPT-3.5 under load), and horizontal scale-out of workers independently from the web layer.

---

## Question 2 — Technical Challenge with AI

### Recent challenge

I built a development workflow where Claude operates as the entire engineering team within a Scrum structure. Rather than using AI as a coding assistant, I run it as a system:

- **PO (Claude):** writes user stories, defines requirements and acceptance criteria per ticket
- **Dev squad (Claude):** three roles running in sequence —
  - *Tech Lead:* breaks down the ticket, makes architecture decisions, flags risks
  - *Developer:* implements the code based on TL's plan
  - *QA:* writes test scenarios and e2e test cases
  - *Tech Lead (final gate):* reviews the full output, decides if the ticket is done or needs rework
- **Scrum Master (Claude):** manages the sprint flow, surfaces blockers, keeps the process moving
- **Human:** reviews and approves at each checkpoint — the only role Claude does not fill

**AI tools used:**
- **Claude** as the primary engine running all exec roles above
- **Claude Code (agentic harness):** currently migrating the workflow to a fully agentic setup — Claude operates with tools, memory, and executes tasks end-to-end autonomously, with the human stepping in only to review and approve
- **Cursor** for in-editor implementation when Claude hands off the code

---

### When AI gives wrong advice

One concrete incident: the AI agent wrote a database migration file manually — created the file directly in the migrations directory instead of using Alembic to generate it (`alembic revision --autogenerate`). The file looked correct in isolation. The problem surfaced when another developer ran Alembic to generate a new migration — Alembic's version chain had a gap because the manually written file was not properly registered in the revision history. The result was a broken migration sequence that the ORM could no longer manage reliably.

This is exactly the kind of mistake that is invisible until someone else touches the same system.

From this I built checkpoints into the workflow. Before any code is written, the Tech Lead output must include:
- High-level architecture diagram
- Low-level sequence diagram
- List of files to be changed and why
- Implementation summary

I review all of this before giving the green light. When something is wrong, I correct it at that checkpoint — not after the code is already written. After the fix, I ask Claude to summarize the mistake and save it as a rule, doc, or reference so it feeds back into the workflow and doesn't repeat across future tickets.

---

### One task I refuse to let AI do without heavy supervision

**Database migrations and any destructive SQL operations.**

AI can write the migration scripts and I will review them — but it will never execute them autonomously. This is a hard rule in my workflow.

Specifically, `DELETE` statements and ORM-level delete operations triggered by an AI Agent are strictly forbidden. Data loss is irreversible. An AI does not know the actual data distribution, does not understand the downstream impact of removing records, and cannot judge whether a rollback is feasible in time. A migration that looks correct can lock a table for minutes on prod, or silently orphan data across related collections.

Every destructive operation goes through: human review of the script, a dry-run against a staging environment with a prod-like data snapshot, a documented rollback plan — and only then manual execution by a human.
