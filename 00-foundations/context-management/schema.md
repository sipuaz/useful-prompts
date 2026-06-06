# CONTEXT.md Schema Reference

Field-by-field reference for every section in `CONTEXT.md`.
Use this when filling in the template for the first time or reviewing an existing file.

---

## Project

**What it is:** A single sentence describing what the codebase does and why it exists.

**What to include:** The domain, the core function, and the intended user or system.

**What to omit:** History, team structure, business context — the model doesn't need it.

**Good example:**
```
A REST API that handles webhook events from Stripe and writes normalized payment records to PostgreSQL.
```

**Bad example:**
```
Our main backend service (started in 2021, migrated from monolith).
```

---

## Stack

**What it is:** The technical environment the model is operating in.

**What to include:** Language and version, framework, infrastructure, and any dependency that
affects decisions (e.g. the database driver matters; a logging library usually doesn't).

**What to omit:** Everything the model doesn't need to make correct choices. If it doesn't
affect how code should be written, leave it out.

**Good example:**
```
- Language/runtime: Python 3.12
- Framework: FastAPI
- Infrastructure: AWS Lambda behind API Gateway
- Key dependencies: asyncpg (PostgreSQL), boto3 (S3), pydantic v2
```

---

## Conventions

**What it is:** The rules the model must follow when generating code or documentation.

**What to include:** Style guide, test framework, branch strategy, and any project-specific
hard rules (naming conventions, folder structure, import order).

**What to omit:** Preferences you'd accept being overridden on — only include rules that,
if violated, would cause a PR to be rejected.

**Good example:**
```
- Style guide: PEP8, enforced by ruff
- Tests: pytest, all tests in tests/ mirroring src/ structure
- Branch strategy: trunk-based, feature flags for incomplete work
- Hard rule: all database queries go through the repository layer, never inline in routes
```

---

## Decisions already made

**What it is:** A list of settled architectural or technical choices.

**Why it matters:** Without this, the model will often suggest alternatives to choices you've
already made — wasting your context and its reasoning on relitigating closed questions.

**What to include:** Any decision that took non-trivial effort, has tradeoffs, or that a
reasonable engineer might question and suggest changing.

**Format:** One line per decision, phrased as a statement of fact.

**Good example:**
```
- We use Redis for caching, not Memcached — TTL-based expiry is sufficient for our use case
- No ORM — raw SQL with asyncpg for performance and query control
- All background jobs go through Celery, not async tasks in the web process
```

---

## Hard constraints

**What it is:** Explicit negative constraints — things the model must never do in this project.

**Why it matters:** This is the scope control layer. Without it, the model may helpfully suggest
things that are correct in general but wrong for your context: auto-generating migrations,
installing new dependencies, or refactoring outside the scope of the task.

**Format:** Imperative statements starting with "Do not" or "Never".

**Good example:**
```
- Do not suggest architectural changes without flagging them explicitly
- Do not invent package or dependency names — use a TODO comment if unsure
- Do not generate or run database migrations automatically
- Do not modify files outside the current feature's scope
```

---

## Current focus

**What it is:** An optional field describing what you're working on right now.

**Why it matters:** It narrows the model's frame of reference for the session. Without it,
the model has to infer scope from the task alone — which can lead to suggestions that are
technically correct but contextually irrelevant.

**How to use it:** Update this at the start of each session. Clear it or leave it blank when
starting something completely new.

**Good example:**
```
Refactoring the auth service to support OAuth2 alongside existing API key auth.
Relevant files: src/auth/, tests/test_auth.py
Do not touch the payment service during this session.
```

---

## General principles

**Keep it short.** Every line in `CONTEXT.md` consumes context window space in every session.
The goal is maximum signal per token, not comprehensive documentation.

**Update it.** A stale `CONTEXT.md` is worse than none — it gives the model confidently wrong
information. Treat it like living documentation and update it when decisions change.

**Commit it.** `CONTEXT.md` should be in version control. It is team infrastructure, not a
personal note.

**Don't duplicate your README.** If something is already documented elsewhere, reference
the location rather than copying the content.