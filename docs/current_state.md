# Tusk — Current State

**Last updated:** 2026-06-22
**Project stage:** Discovery and definition
**Overall status:** Project foundation is being established before implementation begins.

## Completed

* GitHub repository structure has been created.
* Project working instructions have been defined in `instructions.md`.
* The initial project overview has been defined in `docs/project_overview.md`.
* The following core project principles have been confirmed:

  * deterministic processing for transformations, calculations, validations, workflow states, storage, and outputs;
  * controlled use of AI;
  * human accountability for approvals and judgment-based decisions;
  * traceability, versioning, and preservation of audit history;
  * modular separation between deterministic processing, workflow, storage, integrations, and AI assistance.

## Confirmed project scope

Tusk must support two recurring broker-provided Excel-file streams:

1. policy, risk, and premium bordereau;
2. claims bordereau.

The two streams:

* may belong to the same broker and reporting period;
* must be processed independently;
* do not currently require cross-file reconciliation;
* share only the common context of broker and reporting period.

A separate AI-assisted history and audit capability is also part of the confirmed project concept.

## Current activity

The immediate activity is to prepare the minimum essential project documentation required before beginning detailed discovery and development.

The essential files currently being prepared are:

* `docs/current_state.md`
* `docs/backlog.md`
* `docs/workflow_map.md`
* `docs/decisions.md`
* `docs/session_handoff.md`

## Not started

The following work has not yet started:

* representative broker-file review;
* current business-process analysis;
* detailed policy bordereau workflow;
* detailed claims bordereau workflow;
* conceptual data model;
* detailed validations and business rules;
* user-role and approval definition;
* proof-of-concept implementation;
* technology and deployment selection.

## Current blockers

There is no technical blocker preventing documentation work.

Implementation should not begin until representative files and the current business process have been reviewed.

## Important open questions

* Which broker and files will be used for the first representative-data review?
* What is the current manual processing workflow?
* What outputs are required after processing?
* Which employees perform reviews and approvals?
* Which downstream system or process receives the final output?
* What should be included in the first proof of concept?

## Active decisions

The following decisions are currently in effect:

* policy and claims files are separate processing streams;
* no cross-file reconciliation is currently required;
* deterministic processing is the system core;
* AI recommendations do not automatically become approved decisions;
* humans approve new mappings, material exceptions, rule changes, and final outputs;
* important inputs, decisions, processing runs, and outputs must be traceable and versioned.

These decisions should also be recorded formally in `docs/decisions.md`.

## Next recommended step

Create `docs/backlog.md` and define the ordered discovery tasks required to reach the first narrow deterministic proof of concept.
