## 2026-06-22 — Conceptual architecture baseline accepted

`docs/architecture.md` was completed, reviewed, and accepted as the conceptual architecture baseline.

Confirmed:

* Tusk ends when the converted, load-ready file is produced.
* Policy and claims streams are independent.
* Human judgment, deterministic code, and removable AI assistance have separate responsibilities.
* Within-file reconciliation is separate from cross-stream reconciliation.

Next step: System Context Diagram.

## 2026-06-23 — Universal bordereau mapping concept accepted

The universal bordereau mapping concept was accepted as provisional and recorded in `docs/mapping_concept.md`.

Confirmed:

* One reusable deterministic processing engine will be separated from broker-specific mapping data.
* Mapping configurations may reference only pre-implemented and tested transformation operations.
* Mapping configurations must not execute arbitrary code.
* AI may propose mappings but must not approve or apply them.
* The deterministic engine must operate independently of AI.
* Accumulation of confirmed mapping examples will be explored before model fine-tuning.
* The standard insurance-company template defines the required target structure.
* Mapping and transformation correctness must also be supported by confirmed business meaning where necessary.
* Existing Excel scripts and their outputs are reference evidence and comparison baselines, not automatic sources of truth.
* A representative anonymized policy bordereau with authentic broker column names was provided and structurally reviewed.
* DEC-008 and DEC-009 record the approved provisional direction.

Unresolved:

* The detailed mapping approval workflow remains to be defined.
* It is not yet confirmed whether formulas, formatting, and other workbook characteristics are required parts of the final output.
* The standard template, existing Excel script, and reference script output are not yet available for Stage 1.

Next step: Obtain the standard template, existing Excel script, and script output for the same representative source file, then prepare the Stage 1 policy-bordereau thin slice.
