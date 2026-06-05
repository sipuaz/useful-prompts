# Anatomy of a Prompt

## What this is

Before learning any specific prompting technique, you need a mental model for what a prompt actually *is* and what its parts do. This section covers that foundation.

A prompt is not just a question. It is a **context package** — everything the model knows about your situation before it produces a response. The quality of that package determines the quality of the output.

---

## The three pillars

Every effective prompt, regardless of technique, is built from three components:

### 1. Context (Stage-setting)
*Who are you, what is the situation, what does the model need to know?*

This answers the implicit question the model has before it can respond: **"What world am I operating in?"**

Without context, the model fills in the blanks itself — and its defaults may not match your needs.

**Examples of context:**
- Your role: `"I'm a backend engineer reviewing a PR"`
- The project: `"This is a Python microservice using FastAPI and PostgreSQL"`
- Relevant constraints: `"We follow the Google style guide"`
- Prior state: `"We've already decided to use Redis for caching"`

**Why it works:** LLMs generate text that is statistically consistent with the input. The more precisely you define the context, the narrower and more appropriate the output distribution becomes. Vague context = generic output.

---

### 2. Task (Action definition)
*What do you want the model to do?*

This is the most obvious part, but also the most commonly underspecified. The key is to use **strong action verbs** and be explicit about scope.

**Weak task definition:**
> "Tell me about error handling"

**Strong task definition:**
> "Review the following function and identify any unhandled edge cases that could cause a silent failure in production"

**Common task verbs and what they signal to the model:**
| Verb | What it implies |
|------|----------------|
| `Write` | Produce new content from scratch |
| `Analyze` | Break down and explain something existing |
| `Review` | Evaluate against criteria, flag issues |
| `Refactor` | Improve structure without changing behavior |
| `Summarize` | Compress, extract key points |
| `Compare` | Find similarities and differences, often with a recommendation |
| `Explain` | Teach a concept, assume a specific audience level |
| `Draft` | First version expected, iteration will follow |

---

### 3. Constraints (Rules and style)
*How should the model respond? What are the boundaries?*

This pillar is where most beginners leave value on the table. Constraints shape the *form* of the response, not just the content.

**Types of constraints:**

**Format constraints** — how should the output be structured?
- `"Respond in bullet points"`
- `"Use markdown with headers"`
- `"Return only a JSON object, no explanation"`
- `"Keep the response under 200 words"`

**Tone/style constraints** — who is the intended reader?
- `"Write for a senior engineer, skip the basics"`
- `"Use plain language, no jargon, the reader is non-technical"`
- `"Be direct and opinionated, not neutral"`

**Scope constraints** — what should the model *not* do?
- `"Do not suggest architectural changes, only fix the bug"`
- `"Do not rewrite the code, just explain the problem"`
- `"Ignore performance for now, focus only on correctness"`

**Example constraints** — show what good looks like:
- Attach an example of the output format you want
- Reference a style: `"Format this like a Kubernetes YAML manifest"`

---

## How the three pillars interact

Think of it like a function call:

```
response = llm(
    context="who you are + the situation",
    task="the specific action",
    constraints="format + tone + scope + examples"
)
```

Each pillar narrows the space of valid responses. **Context** sets the domain. **Task** sets the goal. **Constraints** set the shape. Leave one out and the model has to guess — and it will.

---

## Common failure modes

| Problem | Missing pillar | Fix |
|---------|---------------|-----|
| Response is too generic | Context | Add your role, the project, relevant background |
| Model does the wrong thing | Task | Use a more specific action verb, add scope |
| Output is in the wrong format | Constraints | Specify format explicitly, add an example |
| Response is too long / too short | Constraints | Add a length constraint |
| Model includes unwanted content | Constraints | Add a negative constraint (`"do not..."`) |
| Response reads for the wrong audience | Constraints | Specify the reader's expertise level |

---

## Relationship to other techniques

Every technique in this repository is a specialization of this base structure. For example:

- **Chain of Thought** adds a constraint: *"show your reasoning step by step before giving the answer"*
- **Few-shot prompting** adds to context: *"here are examples of correct input/output pairs"*
- **Role prompting** extends context: *"you are a [specific expert]"*
- **ReAct** structures the task: *"reason, then decide on an action, then act"*

Knowing this structure makes every other technique easier to understand, combine, and debug.

---

## See also

- [`template.md`](./template.md) — a reusable prompt template based on the three pillars
- [`../README.md`](../README.md) — foundations overview
- Anthropic prompt engineering guide: https://docs.claude.ai/en/docs/build-with-claude/prompt-engineering/overview