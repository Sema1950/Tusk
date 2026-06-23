Tusk — Backlog

Last updated: 2026-06-22
Current project stage: Discovery and definition

Current priority

Prepare the minimum project foundation required to begin structured discovery and representative-file analysis.

Priority 1 — Complete essential project documentation
1. Create docs/current_state.md

Status: Completed locally, not yet pushed.

Purpose:

record the current project stage;
summarize completed work;
identify blockers and open questions;
define the next recommended step.
2. Create docs/backlog.md

Status: In progress.

Purpose:

define the ordered project work;
make priorities and dependencies visible;
separate immediate work from later work.
3. Create docs/workflow_map.md

Status: Not started.

Purpose:

define the initial high-level policy bordereau workflow;
define the initial high-level claims bordereau workflow;
show shared context and independent processing;
identify actors, states, reviews, exceptions, and outputs;
clearly mark unknown steps as provisional or to be defined.
4. Create docs/decisions.md

Status: Not started.

Purpose:

Record the project decisions already confirmed, including:

policy and claims files are separate processing streams;
no cross-file reconciliation is currently required;
deterministic processing is the core;
AI output is advisory unless explicitly approved;
humans retain responsibility for material decisions;
versioning, lineage, and audit history are required;
a separate AI history and audit capability is part of the project concept.
5. Create docs/session_handoff.md

Status: Not started.

Purpose:

summarize the current project position;
identify completed files;
identify the active priority;
allow a future session to continue without relying on chat history.
Priority 2 — Prepare representative-data discovery
6. Select the first representative broker

Status: Not started.

Required outcome:

identify which broker will be used for initial analysis;
confirm that representative policy and claims files are available;
confirm whether the files may be used for development and testing.

Dependency: Essential documentation should be prepared first.

7. Collect representative source files

Status: Not started.

Required files should include, where available:

one or more policy bordereau versions;
one or more claims bordereau versions;
examples containing known errors or exceptions;
any available expected outputs;
relevant mapping sheets or processing instructions.

Use sanitized, anonymized, synthetic, or formally approved data.

8. Document the current manual process

Status: Not started.

For each file stream, determine:

who receives the file;
how it is identified and registered;
how worksheets and columns are reviewed;
how fields are mapped;
how data is cleaned and transformed;
which validations are performed;
how exceptions are handled;
when the broker is contacted;
who approves the result;
what final output is produced;
where the final output is sent or loaded;
which records are retained.
9. Identify the first proof-of-concept boundary

Status: Not started.

The proof of concept should be narrow, deterministic, and testable.

The scope must be selected only after representative files and the current process have been reviewed.

Priority 3 — Define the first processing workflow
10. Define policy bordereau workflow requirements

Status: Not started.

Define:

trigger;
actors;
input conditions;
workflow states;
extraction steps;
mappings;
transformations;
validations;
exceptions;
human approvals;
outputs;
audit events;
correction and reprocessing paths.
11. Define claims bordereau workflow requirements

Status: Not started.

Define the same workflow elements independently for the claims stream.

Do not introduce cross-file reconciliation unless a later approved requirement changes the current decision.

12. Define shared broker and reporting-period context

Status: Not started.

Determine how both independent file streams reference:

broker;
reporting period;
file type;
submission;
file version;
processing run.
Priority 4 — Define data and rules
13. Create the conceptual data model

Status: Not started.

Define business concepts and relationships before selecting a physical database schema.

Likely concepts to investigate include:

broker;
reporting period;
submission;
source file;
file version;
worksheet;
source row;
processing run;
mapping;
rule version;
validation result;
exception;
approval;
output;
audit event.

This list is provisional and must be validated against representative data and workflows.

14. Define mappings and transformation governance

Status: Not started.

Determine:

how approved mappings are stored;
how new mappings are proposed;
who approves them;
how mapping versions are tracked;
how historical runs retain the mapping version used.
15. Define validations and exception categories

Status: Not started.

Determine:

structural validations;
required-field validations;
format validations;
duplicate checks;
business-rule validations;
warning versus error behaviour;
which exceptions require human review;
how corrected files are reprocessed.

Do not invent business validations before source evidence and process owners confirm them.

Priority 5 — Design and build the first proof of concept
16. Define proof-of-concept acceptance criteria

Status: Not started.

Acceptance criteria should be based on the selected representative files and approved workflow.

17. Select implementation technologies

Status: Not started.

Technology selection must follow requirements, representative-data analysis, and proof-of-concept scope.

Do not select hosting, databases, frameworks, or AI providers prematurely.

18. Build deterministic file inspection

Status: Not started.

Potential capability:

read workbook metadata;
identify worksheets;
inspect headers;
preserve source references;
produce a repeatable structural profile.
19. Build deterministic transformation and validation

Status: Not started.

Implement only approved mappings, rules, and validations within the selected proof-of-concept scope.

20. Add controlled human review

Status: Not started.

Support review and approval of:

unfamiliar structures;
proposed mappings;
material exceptions;
corrections affecting final output.
21. Generate controlled output

Status: Not started.

The output format and destination remain to be defined.

22. Preserve lineage and audit evidence

Status: Not started.

The proof of concept should retain sufficient evidence to reconstruct how each output was produced.

Priority 6 — Add selected AI capabilities
23. Define the first approved AI-assisted use case

Status: Not started.

Possible use cases include:

unfamiliar-field mapping suggestions;
file-version comparison;
exception summaries;
evidence-grounded processing explanations.

AI should not be added until the deterministic workflow and human approval boundaries are clear.

24. Define AI evaluation criteria

Status: Not started.

Evaluate AI separately from deterministic processing for:

evidence grounding;
unsupported claims;
uncertainty handling;
consistency;
human-review requirements;
prompt and model version effects.
25. Design the history and audit assistant

Status: Not started.

The assistant should explain existing historical evidence and must not alter records or invent missing facts.

Deferred until requirements are confirmed

The following items are deliberately deferred:

production architecture;
physical database schema;
cloud or hosting provider;
production integrations;
final security and retention policy;
performance targets;
operational support model;
full user-role model;
advanced AI capabilities;
scaling strategy.
Completed foundation
Repository structure created.
instructions.md created.
docs/project_overview.md created.
docs/current_state.md prepared locally.