# CONTEXT.md

## What this is

`CONTEXT.md` is a structured file you add to the root of any project where you work with an LLM. It gives the model persistent, shared knowledge about your project — so every session starts informed instead of blind.

Think of it as the machine-readable equivalent of a good project `README.md`. Where a `README.md` onboards humans, `CONTEXT.md` onboards the model.

This is the **Delegation** competency from the 4D Framework in practice: deciding what the model needs to know upfront so you can delegate work to it effectively.

---

## The problem it solves

Without a `CONTEXT.md`, every session starts cold. The model has to re-explore your codebase, rediscover your conventions, and make assumptions about decisions you've already made. This costs context space, produces inconsistent output, and forces you to repeat yourself across sessions and teammates.

| Problem | Without `CONTEXT.md` | With `CONTEXT.md` |
|---------|---------------------|-------------------|
| **Cold start** | Model guesses your stack and conventions | Model starts informed |
| **Context drift** | Decisions made in session A are invisible in session B | Decisions are persisted in the file |
| **Team sharing** | Each person re-explains the project differently | One source of truth, committed to version control |
| **Prompt bloat** | You repeat context in every prompt | Context is loaded once, referenced always |

---

## Relationship to anatomy-of-a-prompt

The [anatomy-of-a-prompt](../anatomy-of-a-prompt/README.md) template has a **Context** pillar — the part where you define your role, project, and relevant background before every prompt.

`CONTEXT.md` is the **persistent, reusable version of that pillar**. Instead of rewriting project context in every prompt, you maintain it once in a file and reference it at the start of each session.

```
Every prompt:  [CONTEXT.md content] + [task-specific context] + [task] + [constraints]
```

---

## How to use it

1. Copy [`CONTEXT.md`](./CONTEXT.md) into the root of your project
2. Fill in each section for your project — keep it concise
3. Commit it to version control so your team shares the same model context
4. At the start of each session, paste the contents or reference the file explicitly:

```
Read CONTEXT.md first, then help me with the following task:
[your task here]
```

5. Keep it updated as the project evolves — treat it like living documentation

---

## What goes in it

See [`schema.md`](./schema.md) for a field-by-field reference of every section and what belongs there.

The key principle: include only what the model needs to *not get wrong*. Don't paste your entire README — that wastes context space. Instead ask: "what would I tell a new contractor in the first five minutes?"

---

## See also

- [`CONTEXT.md`](./CONTEXT.md) — the template to copy into your project
- [`schema.md`](./schema.md) — field-by-field reference
- [`../anatomy-of-a-prompt/`](../anatomy-of-a-prompt/README.md) — the Context pillar this builds on