# Eval Scorecard

Copy this file for each task you want to evaluate.
One file per task. One row per example.

---

## Task definition

| Field | Value |
|-------|-------|
| **Task name** | e.g. `pr-security-review` |
| **Description** | What you're asking Claude to do |
| **Prompt file** | Link to the prompt being evaluated |
| **Date** | When this eval was run |
| **Model** | e.g. `claude-sonnet-4-6` |

---

## Scoring rubric

Score each dimension 1–3:

| Score | Meaning |
|-------|---------|
| **3** | Good — I'd use this with light review |
| **2** | Acceptable — needs edits before use |
| **1** | Poor — wrong, incomplete, or misleading |

---

## Results

| # | Input summary | Correctness | Completeness | Format | Tone | Notes |
|---|--------------|:-----------:|:------------:|:------:|:----:|-------|
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

---

## Verdict

**Overall score:** `__` / 15 (sum of all dimensions across examples)

**Trust level:**
- [ ] Trusted — use with light review
- [ ] Trusted with review — always check before shipping
- [ ] Not trusted — needs significant prompt work or human ownership

**What works well:**
>

**What fails or needs improvement:**
>

**Changes to try next:**
>

---

## Example (filled)

| Field | Value |
|-------|-------|
| **Task name** | `dockerfile-generator` |
| **Description** | Generate a production-ready Dockerfile from a service README |
| **Prompt file** | `../../chain-of-thoughts/init.md` |
| **Date** | 2025-06-01 |
| **Model** | claude-sonnet-4-6 |

| # | Input summary | Correctness | Completeness | Format | Tone | Notes |
|---|--------------|:-----------:|:------------:|:------:|:----:|-------|
| 1 | Node 20 Express API | 3 | 2 | 3 | 3 | Missing HEALTHCHECK |
| 2 | Python FastAPI + Postgres | 3 | 3 | 3 | 3 | Solid, minor env var naming |
| 3 | Go binary, static build | 2 | 2 | 3 | 3 | Missed multi-stage build opportunity |
| 4 | Ruby on Rails + Sidekiq | 1 | 1 | 2 | 3 | Hallucinated a gem that doesn't exist |
| 5 | Java Spring Boot | 3 | 3 | 3 | 3 | Good, correct JVM flags |

**Overall score:** `11` / 15

**Trust level:**
- [ ] Trusted — use with light review
- [x] Trusted with review — always check before shipping
- [ ] Not trusted — needs significant prompt work or human ownership

**What works well:**
> Handles common stacks (Node, Python, Java) reliably. Format is always valid and clean.

**What fails or needs improvement:**
> Less common stacks (Ruby, Go multi-stage) need human review. One hallucination on a gem name — correctness is the weak point.

**Changes to try next:**
> Add a few-shot example with a Go multi-stage build. Add an explicit constraint: "do not invent package or dependency names — if unsure, leave a TODO comment instead."