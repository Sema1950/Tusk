# Tusk — Backlog

**Last updated:** 2026-06-22
**Project stage:** Concept definition
**Current priority:** Define the conceptual architecture of Tusk.

## Completed foundation

* Repository structure created.
* `instructions.md` created.
* `docs/project_overview.md` created.
* `docs/current_state.md` created.
* Initial project concept documented.

## Priority 1 — Conceptual architecture

### 1. Define the major parts of Tusk

**Status:** Next

Define, at a conceptual level:

* the deterministic processing core;
* the human-review capability;
* project data and history storage;
* audit and traceability capability;
* integrations with external systems;
* controlled AI assistance;
* the separate history and audit assistant.

Do not select technologies or define detailed implementation.

### 2. Define responsibility boundaries

**Status:** Not started

Clarify:

* what belongs to deterministic processing;
* what requires human judgment;
* what AI may assist with;
* what AI must never approve or control;
* how the two file-processing streams remain independent;
* how shared broker and reporting-period context is represented conceptually.

### 3. Approve the conceptual architecture

**Status:** Not started

Review the architecture for:

* consistency with the project overview;
* separation of deterministic logic, AI, and human responsibility;
* traceability and versioning;
* modularity;
* security and privacy considerations;
* ability to evolve as requirements become clearer.

Record approved architectural decisions in `docs/decisions.md`.

## Priority 2 — Capabilities and scope boundaries

### 4. Define major system capabilities

**Status:** Not started

Identify the capabilities Tusk must eventually provide without defining detailed workflows or technology.

### 5. Define scope boundaries

**Status:** Not started

Clarify:

* what is in scope;
* what is out of scope;
* what remains provisional;
* what is deliberately deferred.

## Priority 3 — High-level workflows

### 6. Define the policy bordereau workflow

**Status:** Not started

Create a high-level business workflow only after the conceptual architecture and capability boundaries are approved.

### 7. Define the claims bordereau workflow

**Status:** Not started

Create this as an independent workflow.

Do not introduce cross-file reconciliation unless a later approved requirement changes the current decision.

## Priority 4 — Main data concepts

### 8. Define the conceptual data model

**Status:** Not started

Identify the main business concepts and relationships.

Do not create a physical database schema at this stage.

### 9. Define traceability and versioning concepts

**Status:** Not started

Clarify conceptually how Tusk should connect:

* source information;
* processing history;
* rules and mappings;
* human decisions;
* approvals;
* outputs;
* historical explanations.

## Priority 5 — Discovery and representative data

### 10. Review the current business process

**Status:** Not started

Document how the work is currently performed.

### 11. Review representative files

**Status:** Not started

Analyze approved representative policy and claims files after the conceptual foundation is established.

### 12. Validate architecture and workflows

**Status:** Not started

Use evidence from the current process and representative files to confirm, change, or reject provisional concepts.

## Priority 6 — First proof of concept

### 13. Define the proof-of-concept scope

**Status:** Not started

Select one narrow, deterministic, testable capability.

### 14. Define acceptance criteria

**Status:** Not started

Base acceptance criteria on confirmed requirements and representative data.

### 15. Select implementation technologies

**Status:** Not started

Choose technologies only after the proof-of-concept requirements are sufficiently understood.

### 16. Build and test the proof of concept

**Status:** Not started

Implementation details will be defined later.

## Deferred

The following items are intentionally deferred:

* detailed workflow states;
* detailed validation rules;
* detailed exception categories;
* user-role and permission model;
* physical database schema;
* hosting and deployment architecture;
* production integrations;
* final security and retention policies;
* detailed AI prompts and evaluations;
* production scaling and support model.


