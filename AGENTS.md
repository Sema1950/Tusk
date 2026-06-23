# Tusk Agent Guide

`AGENTS.md` is the working file for coding agents such as Codex and Cursor.
`instructions.md` remains the methodology reference for project-reasoning work.

## Core Rules

- Deterministic code performs transformations, validations, calculations, and approved mappings; the same inputs must produce the same output.
- AI may only suggest, explain, or draft. AI must never alter financial or policy values, including premium, policy number, amount, or limit.
- Humans approve new or changed mappings and material exceptions.
- Audit and history are append-only; never silently overwrite them.
- Tusk has two processing streams: policy bordereau and claims bordereau. They are processed independently; cross-file reconciliation between them is not currently planned and remains provisional.
- Do not invent requirements, business rules, schemas, technologies, roles, workflows, validations, integrations, or implementation details.
- Approved files in `docs/` are the source of truth. If files conflict, surface the conflict instead of choosing silently.
- Make only the requested change. Do not expand scope. For step-by-step work, wait for approval before continuing.
- Never commit confidential customer data, production insurance data, passwords, API keys, tokens, private certificates, or other secrets.

## When To Read More

Do not load the full `instructions.md` on every routine coding task.

Consult `instructions.md` and relevant `docs/` files only when the task involves project concepts, decisions, scope, documentation, architecture, workflows, data meaning, approvals, or unresolved requirements.

For routine coding inside an already-approved task, use this file plus the relevant code and tests.
