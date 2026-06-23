# Tusk — Project Overview

## 1. Purpose

Tusk is an internal insurance data-processing and workflow-automation system.

Its purpose is to receive recurring broker-provided insurance files, process them in a controlled and repeatable way, support human review and approval, preserve a complete audit history, and produce reliable outputs for downstream use.

The project should reduce repetitive manual work without removing human accountability for business decisions.

---

## 2. Business problem

Insurance data often arrives from brokers in Excel files with inconsistent structures, naming, formatting, and data quality.

Manual processing may require employees to:

* inspect incoming files;
* identify the file type and reporting period;
* map broker fields to internal fields;
* clean and normalize data;
* validate required information;
* investigate exceptions;
* communicate with the broker;
* correct and rerun processing;
* approve final results;
* prepare data for loading or other downstream use;
* explain later why a historical result was produced.

This creates operational risk, inconsistent handling, limited traceability, and unnecessary manual effort.

Tusk is intended to make this process more controlled, transparent, repeatable, and auditable.

---

## 3. Confirmed input streams

Tusk must support two recurring broker-provided Excel-file streams:

1. **Policy bordereau**

   * policy information;
   * insured risks;
   * premiums;
   * related policy or exposure data.

2. **Claims bordereau**

   * claims information;
   * claim status and values;
   * related loss data.

These files may relate to the same broker and reporting period, but they must be processed as separate workflows.

No cross-file reconciliation between the policy bordereau and claims bordereau is currently required.

The two streams share only the common business context of broker and reporting period.

---

## 4. Core system responsibilities

Tusk is expected to support the following high-level capabilities:

* receive and register incoming files;
* identify the broker, reporting period, and file stream;
* preserve the original file;
* create versioned processing records;
* inspect workbook and worksheet structure;
* apply approved mappings and transformation rules;
* normalize source data into controlled internal structures;
* validate required fields, formats, and business rules;
* identify errors, warnings, and exceptions;
* route material issues for human review;
* support correction and reprocessing;
* preserve approvals and decisions;
* generate controlled outputs;
* maintain complete processing lineage and audit history.

Detailed workflow steps and business rules remain to be defined.

---

## 5. Deterministic processing principle

The core processing system must be deterministic.

The same approved inputs, configuration, rules, and software version should produce the same output.

Deterministic code or controlled system logic should be used for:

* file ingestion;
* workbook and worksheet reading;
* data transformation;
* calculations;
* validations;
* mappings after approval;
* workflow-state transitions;
* output generation;
* storage;
* versioning;
* logging;
* integrations.

Important processing results must not depend on uncontrolled AI behaviour.

---

## 6. Controlled use of AI

AI may be used where interpretation or explanation provides value.

Potential uses include:

* suggesting mappings for unfamiliar broker fields;
* comparing new file structures with historical versions;
* summarizing exceptions;
* helping users understand processing issues;
* searching historical evidence;
* explaining why a result was produced;
* supporting documentation and review.

AI output must remain distinguishable from:

* approved business rules;
* deterministic results;
* confirmed facts;
* human decisions.

AI recommendations must not automatically become approved mappings, rules, exceptions, or business decisions.

The deterministic core must continue operating if AI is unavailable, disabled, or replaced.

---

## 7. Human accountability

Humans remain responsible for decisions requiring business judgment.

Human approval is expected for matters such as:

* new field mappings;
* material exceptions;
* rule changes;
* unusual source structures;
* corrections that affect final results;
* approval of final outputs;
* decisions requiring insurance or operational judgment.

Tusk should support human review rather than hide or replace it.

---

## 8. Auditability and history

Tusk must preserve sufficient evidence to explain what happened during processing.

The audit history should connect, where relevant:

* original broker files;
* later file versions;
* processing runs;
* workbook structures;
* extracted source values;
* mappings;
* transformation rules;
* calculations;
* validations;
* errors and warnings;
* exceptions;
* user actions;
* approvals;
* broker questions and responses;
* corrected data;
* final outputs;
* software and configuration versions.

Important history must not be silently overwritten.

---

## 9. AI history and audit assistant

A separate AI-assisted history and audit capability is part of the Tusk concept.

Its purpose is to help authorized users answer questions such as:

* Why did this historical value appear in the final output?
* Which source file and source cell produced this result?
* Which mapping or rule was applied?
* Was the result changed after broker clarification?
* Who approved the exception?
* Which file version was ultimately used?
* Why did one processing run differ from another?

The assistant should retrieve and explain existing evidence.

It must not invent missing facts, alter historical records, or independently approve decisions.

Its answers should identify the evidence used and distinguish confirmed facts from interpretations.

---

## 10. Traceability and versioning

Important project and processing artefacts should be versioned.

This includes, where applicable:

* source files;
* normalized data;
* mappings;
* rules;
* configurations;
* processing runs;
* outputs;
* approvals;
* exceptions;
* project decisions;
* technical documentation.

The system should support reconstruction of how an approved result was produced.

---

## 11. Modularity

The system should keep the following concerns sufficiently separated:

* file intake;
* data extraction;
* transformation and normalization;
* validation;
* business rules;
* workflow management;
* human review;
* storage;
* audit logging;
* integrations;
* AI assistance;
* reporting and outputs.

This separation should allow components to change without requiring the entire system to be redesigned.

---

## 12. Security and privacy

Tusk will process confidential insurance information.

The project must therefore consider:

* access control;
* least-privilege permissions;
* secure credential handling;
* protection of source and processed data;
* environment separation;
* audit logging;
* retention;
* backup and recovery;
* secure integrations;
* authorized access to AI-assisted features.

Final security, privacy, and retention policies are still to be defined.

---

## 13. Current scope status

### Confirmed

* internal insurance data-processing system;
* recurring policy bordereau processing;
* recurring claims bordereau processing;
* independent processing of the two streams;
* deterministic processing core;
* human approval for judgment-based decisions;
* versioning and traceability;
* controlled use of AI;
* dedicated AI history and audit capability.

### Provisional

* exact workflow stages;
* exact review and approval roles;
* exact exception categories;
* exact normalized data model;
* exact output formats;
* exact integration approach;
* exact AI features beyond history and audit support.

### To be defined

* supported brokers in the first implementation;
* representative input files;
* required downstream systems;
* user roles and permissions;
* detailed business validations;
* storage architecture;
* deployment model;
* security and retention policies;
* first proof-of-concept scope;
* acceptance criteria and measurable success indicators.

---

## 14. Current project stage

Tusk is currently in discovery and definition.

The immediate objective is to establish:

1. the current business process;
2. representative source files;
3. the two end-to-end processing workflows;
4. the conceptual data model;
5. the required validations and approvals;
6. the audit and versioning model;
7. a narrow deterministic proof of concept.

Technology and architecture decisions should be made only when supported by confirmed requirements and representative data.

---

## 15. Project success direction

Tusk should be considered successful when it can process approved representative files in a repeatable way, identify and route exceptions, preserve complete lineage, support human approval, and allow authorized users to understand how final results were produced.

Specific numerical targets should be defined only after the current process and operating conditions are measured.
