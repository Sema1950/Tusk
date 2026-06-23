# Tusk — Backlog

**Last updated:** 2026-06-23

## Purpose

This file records the project work that has been agreed but is not yet complete.

It is not a complete project roadmap. Tusk will be developed incrementally, based on what is learned and approved during each working session.

## Working rule

At the end of a working session:

1. review what was completed or discovered;
2. identify the most appropriate next step;
3. obtain user approval;
4. add the approved work to this file.

Do not add speculative future work merely to outline the entire project.

## Current priority

Obtain the remaining reference artefacts and prepare the Stage 1 thin slice for one policy-bordereau broker using the universal-engine and mapping-as-data approach defined in `docs/mapping_concept.md`, DEC-008, and DEC-009.

## Next tasks

1. Obtain and review the remaining Stage 1 artefacts for the same broker:

   * standard insurance-company template;
   * existing Excel script for that broker format;
   * output produced by that script from the same representative source file.

Precondition:

* Stage 1 requires four artefacts in total: the source bordereau, standard template, existing Excel script, and script output.
* A representative anonymized source bordereau with authentic broker column names has already been provided and structurally reviewed.
* The source bordereau must be available in the Stage 1 implementation environment.
* Availability of the remaining three artefacts has not yet been confirmed.
* If a required artefact cannot be obtained, the Stage 1 plan must be reviewed and adjusted rather than silently assuming an equivalent substitute.

Acceptance conditions:

* The output file follows the required standard-template structure.
* Mapping is stored separately from engine code.
* The reusable engine contains no hidden broker-specific logic.
* The same source file, mapping version, engine version, configuration, and confirmed rules produce the same result.
* Every material discrepancy with the existing script output is explained and classified.
* Correctness is not based solely on matching the existing script.
* No transformation or validation is invented without evidence from the source file, template, existing process, or confirmed business clarification.

## Blocked

Stage 1 implementation is blocked until the remaining required artefacts are available:

* standard insurance-company template;
* existing Excel script;
* script output for the same representative source file.

## Deferred

No tasks are currently recorded as deferred.

