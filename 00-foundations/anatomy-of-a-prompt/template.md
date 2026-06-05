# Prompt Template

A fill-in-the-blank template based on the three-pillar structure.
Copy this as a starting point for any new prompt.

---

## Template (Markdown)

```
## Context
- **My role:** [e.g. backend engineer, tech lead, devops engineer]
- **Project/system:** [e.g. Python FastAPI service, Kubernetes cluster on GKE]
- **Relevant background:** [anything the model needs to know before acting]

## Task
[Strong action verb] + [specific object] + [scope if needed]

e.g. "Review the following function and identify unhandled edge cases that could cause silent failures in production"

## Constraints
- **Format:** [bullet points / markdown / JSON / plain prose / code only]
- **Tone/audience:** [senior engineer / non-technical stakeholder / concise and direct]
- **Scope:** [what to include and, importantly, what to exclude]
- **Length:** [one paragraph / under 200 words / as long as needed]
- **Example of desired output:** [attach or describe one if available]
```

---

## Template (XML)

XML is preferable when your prompt content contains special characters, code blocks,
or nested structure that could be ambiguous in Markdown.

```xml
<prompt>
  <context>
    <role>backend engineer</role>
    <project>Python FastAPI service using PostgreSQL and Redis</project>
    <background>We follow Google style guide. Performance is not a concern for this task.</background>
  </context>

  <task>
    Review the following function and identify unhandled edge cases that could cause silent failures in production.
  </task>

  <constraints>
    <format>Bullet list, one issue per bullet</format>
    <tone>Direct, senior engineer audience, skip obvious basics</tone>
    <scope>Focus only on correctness and error handling. Do not suggest refactors.</scope>
    <length>As many bullets as needed, no padding</length>
  </constraints>

  <input>
    [PASTE YOUR CODE OR CONTENT HERE]
  </input>
</prompt>
```

---

## Worked example

### Before (typical beginner prompt)
```
Can you check my function for bugs?
```

### After (three-pillar structure)
```
## Context
- My role: backend Python developer
- Project: FastAPI REST API, deployed on AWS Lambda, Python 3.12
- Background: This function handles payment webhook events from Stripe.
  It must be idempotent — we may receive duplicate events.

## Task
Review the following function and identify any bugs or edge cases that could
cause incorrect behavior in production, particularly around idempotency and
error handling.

## Constraints
- Format: Numbered list, one issue per item, with a brief explanation of the risk
- Tone: Senior engineer, be direct, skip style comments
- Scope: Correctness and reliability only. Do not suggest performance improvements.
- Length: Only real issues, no filler

[FUNCTION CODE HERE]
```

### Why the second version is better

| Aspect | Before | After |
|--------|--------|-------|
| Model knows your stack | No | Yes (FastAPI, Lambda, Python 3.12) |
| Model knows the stakes | No | Yes (payments, idempotency) |
| Output format is predictable | No | Yes (numbered list) |
| Scope is bounded | No | Yes (no performance, no style) |
| Audience is set | No | Yes (senior, direct) |

---

## When to use XML vs Markdown

| Situation | Recommendation |
|-----------|---------------|
| Simple text prompts | Markdown is fine |
| Prompt contains code blocks | XML (avoids ambiguity with backticks) |
| Prompt is used in an API/system context | XML (more parseable, less ambiguous) |
| Prompt contains angle brackets or special chars | XML (wrap content in CDATA if needed) |
| Human-readable / stored in a repo for reading | Markdown |

---

## See also

- [`README.md`](./README.md) — full explanation of the three pillars and why they work