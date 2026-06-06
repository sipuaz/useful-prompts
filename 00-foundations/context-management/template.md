# generate-context.md

A prompt to instruct an LLM or agent to generate or update the `CONTEXT.md` file
for your project, following the schema defined in `schema.md`.

Run this at the start of a new project, or when the existing `CONTEXT.md` is stale.

---

## When to use this prompt

| Situation | Action |
|-----------|--------|
| New project, no `CONTEXT.md` yet | Run as-is — the model will generate from scratch |
| Existing `CONTEXT.md`, project has evolved | Paste current `CONTEXT.md` into the prompt — the model will update it |
| Onboarding to an unfamiliar codebase | Run against the existing code — the model will infer what it can |

---

## The prompt

```
## Context
- My role: [your role, e.g. backend engineer, devops engineer]
- Task: generate or update the CONTEXT.md file for this project

## Task
Read the project files available to you and produce a filled CONTEXT.md following
the schema below exactly. For each field:
- Infer what you can from the codebase (package files, configs, existing docs)
- Leave a [TODO: brief description] placeholder for anything you cannot determine
  from the available files — do not guess or invent values
- If a CONTEXT.md already exists (provided below), update it rather than
  replacing it: preserve existing decisions and constraints, and only change
  fields where you have clear evidence from the codebase

## Schema
Each section must appear in this order. Do not add sections not in the schema.

### Project
One sentence: what this codebase does and why it exists.

### Stack
- Language/runtime:
- Framework:
- Infrastructure:
- Key dependencies: (only what affects decisions — db drivers, queues, auth libs)

### Conventions
- Style guide:
- Test framework:
- Branch strategy:
- Other hard rules: (only rules that would cause a PR rejection if violated)

### Decisions already made
One line per settled decision. Phrased as a statement of fact.
Only include decisions with real tradeoffs that a reasonable engineer might question.

### Hard constraints
Explicit things the model must never do in this project.
Format: "Do not..." or "Never..."

### Current focus
Leave blank. The engineer will fill this in at the start of each session.

## Constraints
- Output only the filled CONTEXT.md content — no explanation, no preamble
- Use the exact section headers from the schema
- Do not invent values — use [TODO: description] for anything uncertain
- Keep each section as concise as possible — every line costs context space
- Do not duplicate content already in README.md — reference the file instead

## Existing CONTEXT.md (if updating)
[PASTE CURRENT CONTEXT.md HERE — or remove this section if generating from scratch]

## Available project files
[LIST KEY FILES OR PASTE CONTENTS HERE — e.g. package.json, pyproject.toml,
docker-compose.yml, existing README.md, folder structure]
```

---

## Usage notes

**For an agent (e.g. Claude Code):** paste the prompt and let the agent read
the codebase directly. Remove the "Available project files" section — the agent
will explore on its own.

**For a chat session:** paste the prompt and attach or paste the key files manually:
`package.json` / `pyproject.toml`, `docker-compose.yml`, top-level folder structure,
and any existing `README.md`. These are usually enough for the model to infer the stack,
conventions, and decisions.

**After generation:** review every field before committing. Pay particular attention to:
- `Decisions already made` — the model may miss implicit decisions that live in your head
- `Hard constraints` — add anything project-specific the model couldn't infer from files
- `[TODO]` placeholders — fill these in manually before the file goes to version control