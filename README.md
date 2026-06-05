# useful-prompts

A practical toolbelt for working effectively with LLMs — built in public, by a backend/devops developer learning the field and sharing the journey.

---

## What this is

This repository is a growing collection of prompting techniques, patterns, and frameworks, organized so that anyone with a technical background can pick it up, understand *why* things work — not just *what* to copy — and build on it.

It is not a list of clever one-liners. It is a structured body of knowledge, built incrementally as new things are learned and tested.

---

## Guiding principles

Four core competencies for working effectively with AI (see sources for attribution):

| Competency | What it means | Where it appears in this repo |
|------------|--------------|-------------------------------|
| **Delegation** | Deciding what work should be done by humans, what by AI, and how to split tasks strategically | `00-foundations/` |
| **Description** | Communicating effectively with AI — defining outputs, guiding processes, specifying behavior | `00-foundations/`, `01-prompting-techniques/` |
| **Discernment** | Critically evaluating AI outputs — assessing quality, accuracy, and what needs improvement | `05-evaluation/` *(coming soon)* |
| **Diligence** | Using AI responsibly — transparency, accountability, and ethical choices | Throughout, as a baseline assumption |

These four competencies don't map to four separate sections — they run through everything. They're a lens, not a checklist.

---

## Sources and acknowledgments

This repo draws from multiple learning sources, all cited where relevant:

- **Anthropic's free courses** — [claude.ai courses](https://anthropic.skilljar.com) — for foundational concepts on how to write effective prompts and think about AI collaboration
- **Academic research** — the **4D Framework for AI Fluency** by Professor Rick Dakan (Ringling College of Art and Design) and Professor Joseph Feller (University College Cork), and technique-level papers linked in each folder
- **Community knowledge** — r/PromptEngineering
- **Anthropic's prompt engineering documentation** — https://docs.claude.ai/en/docs/build-with-claude/prompt-engineering/overview

---

## Repository structure

```
useful-prompts/
├── 00-foundations/                  # Start here — mental models before techniques
│   ├── README.md
│   └── anatomy-of-a-prompt/        # The three components every prompt has
│       ├── README.md
│       └── template.md             # Reusable prompt template (Markdown + XML)
│
└── chain-of-thoughts/               # First technique: Chain of Thought (CoT)
    ├── init.md
    └── init.xml
```

---

## How to use this repo

**If you're new to prompting:** start with [`00-foundations/anatomy-of-a-prompt/`](./00-foundations/anatomy-of-a-prompt/README.md). Everything else builds on that mental model.

**If you're looking for a template:** [`00-foundations/anatomy-of-a-prompt/template.md`](./00-foundations/anatomy-of-a-prompt/template.md) has a reusable Markdown and XML prompt template you can copy.

**If you want to see a technique in practice:** [`chain-of-thoughts/`](./chain-of-thoughts/) is the first example, available in both Markdown and XML format.

---

## Roadmap

This is a work in progress, built and documented as learning happens.

- [ ] TODO: prompting techniques — few-shot, role prompting, output formatting, self-consistency
- [ ] TODO: system prompt patterns — persona definition, constraint layering, multi-turn context
- [ ] TODO: agentic patterns — ReAct, plan-and-execute, reflection loops
- [ ] TODO: RAG patterns — basic retrieval, chunking strategies
- [ ] TODO: evaluation — LLM-as-judge, prompt regression testing

Contributions, corrections, and suggestions are welcome.