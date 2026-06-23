# Tusk — Decisions

**Last updated:** 2026-06-22

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
