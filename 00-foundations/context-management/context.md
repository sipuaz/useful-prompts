# CONTEXT.md

## Project
[One sentence: what this codebase does and why it exists]

## Stack
- **Language/runtime:** [e.g. Python 3.12, Node 20, Go 1.22]
- **Framework:** [e.g. FastAPI, Express, Gin]
- **Infrastructure:** [e.g. Kubernetes on GKE, AWS Lambda, bare metal]
- **Key dependencies:** [e.g. PostgreSQL, Redis, Kafka — only what matters for decisions]

## Conventions
- **Style guide:** [e.g. PEP8, Google, Airbnb]
- **Test framework:** [e.g. pytest, Jest, go test]
- **Branch strategy:** [e.g. trunk-based, gitflow]
- **Other hard rules:** [anything the model must never violate]

## Decisions already made
<!--
List choices that are settled. The model should not relitigate these or suggest alternatives
unless explicitly asked. One line per decision.
-->
- [e.g. We use Redis for caching, not Memcached]
- [e.g. No ORM — raw SQL with asyncpg]
- [e.g. API versioning is path-based: /v1/, /v2/]

## Hard constraints
<!--
Explicit negative constraints. Things the model must never do in this project.
-->
- Do not suggest architectural changes without flagging them explicitly
- Do not invent package or dependency names — use a TODO comment if unsure
- Do not generate or run database migrations automatically

## Current focus
<!--
Optional. Update this at the start of each session to give the model a working frame.
Remove or leave blank when starting something new.
-->
[e.g. Refactoring the auth service to support OAuth2 — see src/auth/]