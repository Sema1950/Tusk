# Tusk — Decisions

**Last updated:** 2026-06-23

## Purpose

This file records material project decisions that have been approved.

Approved decisions must remain visible. If a decision changes, mark the earlier decision as superseded rather than deleting it.

---

## DEC-001 — Separate processing streams

**Status:** Provisional
**Date:** 2026-06-22

### Decision

Policy bordereau and claims bordereau must be processed as separate workflows.

They may share the same broker and reporting-period context, but one workflow must not depend on the completion or result of the other.

### Consequence

The two streams may share common components, but their processing runs, validations, exceptions, approvals, and outputs must remain independently traceable.

---

## DEC-002 — No cross-file reconciliation

**Status:** Provisional
**Date:** 2026-06-22

### Decision

Tusk does not currently require reconciliation between policy bordereau data and claims bordereau data.

### Consequence

Cross-file reconciliation must not be added unless it is later approved as a new requirement.

---

## DEC-003 — Deterministic processing core

**Status:** Confirmed
**Date:** 2026-06-22

### Decision

Transformations, mappings after approval, calculations, validations, workflow states, storage, versioning, and outputs must be handled through deterministic code or controlled system logic.

### Consequence

The same approved inputs, rules, configuration, and software version should produce the same result.

---

## DEC-004 — Controlled use of AI

**Status:** Confirmed
**Date:** 2026-06-22

### Decision

AI may assist with interpretation, mapping suggestions, comparison, exception analysis, historical search, explanation, and documentation.

AI must not independently approve mappings, business rules, material exceptions, corrections affecting final results, or final outputs.

### Consequence

AI recommendations must remain distinguishable from approved facts, deterministic results, and human decisions.

---

## DEC-005 — Human accountability

**Status:** Confirmed
**Date:** 2026-06-22

### Decision

Humans remain responsible for business judgment, approvals, new mappings, material exceptions, rule changes, and final outputs.

### Consequence

Tusk must support human review and approval rather than replace accountability with automated or AI-generated decisions.

---

## DEC-006 — Traceability and versioning

**Status:** Confirmed
**Date:** 2026-06-22

### Decision

Important source files, processing runs, mappings, rules, exceptions, approvals, outputs, and changes must be traceable and versioned.

### Consequence

Important history must not be silently overwritten. The system must preserve enough evidence to reconstruct how an approved result was produced.

---

## DEC-007 — Bias toward the thinnest working slice

**Status:** Confirmed
**Date:** 2026-06-22

### Decision

Once the immediate concept is clear enough to act on, the project should prefer the smallest end-to-end working slice using a representative approved file over additional speculative documentation.

### Consequence

Working software is a primary discovery method. Documentation should support implementation and preserve what is learned, not delay building unless a genuine blocking unknown exists.

---

## DEC-008 — Universal mapping engine with mapping-as-data

**Status:** Provisional
**Date:** 2026-06-23

### Decision

Broker bordereau files will be converted to the standard template by one reusable deterministic processing engine plus a separate mapping description for each broker format.

Mapping will be stored as versioned data, provisionally in JSON, and may reference only pre-implemented and tested transformation operations.

The engine must not execute arbitrary code from a mapping.

AI may propose mappings for new or changed formats but must not approve or apply them.

See `docs/mapping_concept.md`.

### Consequence

Broker-specific mappings and configuration belong outside the reusable engine rather than in separate complete processing scripts.

The deterministic engine must operate independently of AI.

A new engine operation may be introduced only when representative data demonstrates the need. It should be implemented as a reusable controlled operation rather than hidden broker-specific logic.

Exact implementation technologies remain provisional.

---

## DEC-009 — Source of truth for Stage 1

**Status:** Provisional
**Date:** 2026-06-23

### Decision

For the first thin slice, the standard insurance-company template is the reference for the required target structure.

Correctness of mappings and transformations must also be supported by confirmed business meaning or business clarification where the template alone does not establish the correct rule.

The existing Excel script and its output are evidence of the current process and a comparison baseline. They are not automatic truth because they may contain outdated rules or errors.

Material discrepancies must be investigated and classified as one of the following:

* new-engine error;
* old-script error;
* formatting-only difference;
* unconfirmed business rule;
* open question.

### Consequence

Matching the existing Excel script alone is insufficient for Stage 1 success.

The new result must conform to the required template structure and use mappings and transformations supported by confirmed meaning or clarification.

Unexplained discrepancies must not be silently accepted.
