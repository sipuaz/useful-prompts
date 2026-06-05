# Evals (Evaluations)

## What this is

Once you can write a prompt, the next question is: **how do you know if it's actually good?**

Evals are systematic ways to test how well an LLM performs on a specific task that matters to you. Not in general — on *your* task, in *your* context, with *your* definition of quality.

This is the **Discernment** competency from the 4D Framework: the ability to critically assess outputs rather than just accept them.

---

## Why evals matter for engineers

LLMs are inconsistent in ways that differ from traditional software. A function either returns the right value or it doesn't. An LLM might give you a great answer 80% of the time, a mediocre one 15% of the time, and a subtly wrong one 5% of the time — and all three look plausible.

Without evals you are flying blind. You don't know:
- Whether your prompt is actually better after you change it, or just *feels* better
- Which tasks Claude handles well enough to trust, and which need human review
- Whether a prompt that works today still works after you've changed the context

Evals give you a feedback loop. They turn prompt engineering from intuition into something closer to engineering.

---

## A practical eval approach

You don't need infrastructure to start. Five to ten examples and a clear rubric is enough to build real intuition.

### 1. Pick one specific task

Don't evaluate "Claude in general." Pick one recurring task:

- Reviewing a PR for security issues
- Writing a Dockerfile for a given service description
- Summarising a long error log into a root cause hypothesis
- Generating a runbook section from a service's README
- Converting informal requirements into a set of acceptance criteria

### 2. Gather reference examples

Collect 5–10 real examples of that task with known-good outputs — things you've written yourself, reviewed and approved, or can judge confidently. These become your ground truth.

> If you don't have real examples yet, generate 5 outputs manually first, then use those as your baseline.

### 3. Write your test prompts

Using the [anatomy-of-a-prompt template](../anatomy-of-a-prompt/template.md), write the prompt you'd actually use for this task. Include the context you'd naturally have.

Run it against each of your reference inputs.

### 4. Score the outputs

For each output, ask:

- **Correctness** — is the information accurate? are there errors or hallucinations?
- **Completeness** — does it cover what matters? what's missing?
- **Format** — is the structure and length appropriate for how you'd use this?
- **Tone** — is it appropriate for the audience (team, stakeholder, production system)?
- **Trustworthiness** — would you ship this with light review, heavy review, or not at all?

Use the [`eval-template.md`](./eval-template.md) scorecard to record results consistently.

### 5. Refine and re-run

Based on what you find:
- If outputs are missing context → add it to the prompt's **Context** pillar
- If format is wrong → tighten the **Constraints** pillar
- If outputs are inconsistent → add examples (few-shot) to anchor the expected output
- If a task scores poorly across the board → flag it as needing human ownership, not AI delegation

Re-run after each change. If the score improves consistently across your examples, the change is real. If it only improves on one, you may have overfitted the prompt to a single case.

---

## What good looks like

A mature eval for a single task looks like:

- 5–10 representative input examples
- A filled scorecard for each
- A summary of what the prompt handles well and where it fails
- A clear verdict: trusted / trusted with review / not trusted

You don't need to formalise this beyond a markdown file or a small spreadsheet. The point is the habit, not the tooling.

---

## See also

- [`eval-template.md`](./eval-template.md) — scorecard template for a single task eval
- [`../anatomy-of-a-prompt/`](../anatomy-of-a-prompt/README.md) — how to write the prompts you'll be evaluating