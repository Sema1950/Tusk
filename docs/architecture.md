# Tusk — Conceptual Architecture

**Status:** Provisional
**Version:** 0.1

This document describes Tusk at the conceptual level only: what the system is made of and how a file moves through it. It does not select databases, languages, cloud platforms, APIs, or detailed workflows. Those are deferred until requirements and representative data support them.

---

## 1. Relationship to the project overview

Purpose, scope, processing streams, and the core principles (deterministic processing, controlled use of AI, human accountability, traceability) are defined in `project_overview.md` and are not repeated here.

This file covers only the architectural layer that the overview does not: the **components** the system is built from, the **process** a submission moves through, the **responsibility split** across human / deterministic code / AI, the **system boundary**, and the meaning of **within-file reconciliation**.

---

## 2. Components

Tusk is organized into four groups of components. The deterministic core is the spine; memory and AI hang off it; the human sits above it as control. AI is an attached, removable layer — if it is unavailable, the core still operates and a person performs mapping manually.

### 2.1 Deterministic core (the processing spine)

- **Intake** — receives and registers a submission, assigns identifiers, links it to broker, period, and stream.
- **Structure Analysis** — inspects the workbook layout (sheets, headers, ordering) and produces a structure profile.
- **Mapping Resolution** — determines how source fields correspond to internal fields, using approved mappings where known.
- **Transformation** — applies the approved mapping and normalizes source data into the internal format.
- **Validation & Calculation** — runs deterministic checks, calculations, and within-file control totals.
- **Output Generation** — produces the load-ready final file and its converted form.

### 2.2 Memory & storage

- **Mapping Registry** — stores approved mappings, organized by broker, stream, and format version, so a recognized format is reused without re-deciding it.
- **Audit & History** — an append-only record of files, versions, mappings, checks, exceptions, decisions, approvals, and outputs.
- **File Storage** — holds original, working, and output files, kept separately from structured records.

### 2.3 AI assistance (removable)

- **Mapping Interpreter** — proposes mappings for unfamiliar structures; proposals require human approval before they become reusable.
- **Audit Copilot** — read-only; helps authorized users investigate how a historical result was produced. It retrieves and explains existing evidence and never alters records or approves anything.

### 2.4 Human control

- **Review & Approval** — where people confirm new mappings, resolve exceptions, decide on broker clarifications, and confirm readiness when judgment or unresolved exceptions require human review. Humans remain accountable for all judgment-based decisions.

---

## 3. High-level process

A submission moves through the following stages:

File Receipt → Submission Registration & Versioning → Original File Storage → Technical Intake Validation → Structure Identification → Mapping & Normalization → Main Checks → Broker Questions & Exceptions → Corrections & Reprocessing → Final Checks & Within-File Reconciliation → Load-Ready Final File → Conversion

The flow is not strictly linear. **Corrections & Reprocessing loops back** to the checks rather than advancing, repeating until the submission either passes or is escalated. The primary human judgment points are mapping approval and exception resolution.

---

## 4. Responsibility at each stage

The table defines the responsibility of humans, deterministic code, and AI. AI never performs or applies — it only interprets, suggests, explains, or drafts.

| Stage | Human | Deterministic code | AI assistance |
|---|---|---|---|
| File Receipt | Sends / receives file | Registers file | — |
| Registration & Versioning | Reviews if needed | Creates IDs, versions, timestamps | — |
| Original File Storage | — | Saves unchanged original | — |
| Technical Intake Validation | Handles failed files | Checks readability, sheets, format | Explains unusual technical intake failures |
| Structure Identification | Confirms unfamiliar structure | Reads headers and layout | Describes the structure |
| Mapping & Normalization | Approves new mappings | Applies approved mappings and transformations | Suggests mappings for new formats |
| Main Checks | Reviews exceptions | Runs deterministic checks | Explains errors and patterns |
| Broker Questions & Exceptions | Chooses what to ask | Tracks question / exception status | Drafts and summarizes questions |
| Corrections & Reprocessing | Reviews answers, decides | Applies approved corrections, reruns | Interprets broker responses, suggests actions |
| Final Checks & Within-File Reconciliation | Resolves remaining issues | Runs final checks and control totals | Explains unresolved differences |
| Load-Ready Final File | Confirms readiness | Generates load-ready file | — |
| Conversion | — | Converts to required format | — |

---

## 5. System boundary

Tusk's responsibility ends when the converted, load-ready file is produced. The following activities are downstream and belong to the company, outside the primary Tusk boundary:

| Stage (outside Tusk) | Human | Deterministic code | AI assistance |
|---|---|---|---|
| Database Load | Data analyst initiates / monitors | Loads data | — |
| Post-Load Verification | Reviews failures | Confirms counts, totals, load results | Explains discrepancies |
| BI | Uses reports | — | — |

The boundary is defined by the system's responsibility: Tusk owns processing up to the converted, load-ready file. The main database and BI tools are company-owned; Tusk hands them a validated file and does not own their internals.

---

## 6. Within-file reconciliation

Within-file reconciliation refers only to totals and control values **inside a single processing stream** — for example, confirming that line-item premiums sum to a stated total within the same file.

It does **not** mean reconciliation between the policy bordereau and the claims bordereau. Cross-file reconciliation between the two streams is not currently required (see `decisions.md`, DEC-002).

---

## 7. What this document deliberately omits

Consistent with concept-first development, this version does not specify databases, programming languages, cloud platforms, storage technology, APIs, deployment, or detailed workflow states. These are introduced only when confirmed requirements and representative files support them, and are recorded as later, lower-level revisions of this architecture.