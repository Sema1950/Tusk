
# Tusk — Universal Bordereau Mapping Concept

**Status:** Provisional  
**Purpose:** Define the proposed universal bordereau mapping approach before implementing a specific mapping or processing engine.

## 1. Goal

Tusk should accept bordereau files from different brokers and transform them into the insurance company's standard template.

Different brokers provide largely equivalent underlying information but use different:

* column names;
* column order;
* date, percentage, and currency formats;
* Excel workbook structures;
* representations of empty and special values.

The system should normalize these differences into one controlled standard format.

This document focuses on policy bordereau. The same general approach may later be evaluated for claims, but policy and claims remain independent processing streams. No shared claims implementation or cross-file reconciliation is assumed.

---

## 2. Current process

Today, an analyst creates a separate Excel script for each supported broker format.

Each script typically combines:

* mapping broker columns to standard-template columns;
* value transformations;
* broker-specific handling rules;
* generation of the final Excel output.

For policy bordereau, these scripts already exist and operate semi-automatically.

Problems with the current approach include:

* a new broker usually requires a new script;
* a change in broker format requires a script change;
* mapping rules are hidden inside individual scripts;
* logic may be duplicated across scripts;
* version and change control are difficult to centralize;
* it is difficult to determine exactly which rules produced a historical result.

Existing Excel scripts are important evidence of the current process, but they are not treated as an automatic source of truth.

---

## 3. Target approach

The proposed direction is to separate the two concerns currently fused inside individual Excel scripts:

1. one reusable deterministic processing engine;
2. a separate mapping description for each broker format.

A new ordinary broker format should normally require a new mapping configuration rather than a new complete processing script.

This remains a provisional architectural direction until it is proven through a working thin slice.

---

## 4. Universal deterministic engine

The proof of concept is provisionally expected to use one reusable deterministic Python engine.

Its responsibilities may include:

1. accepting the source Excel file;
2. receiving an explicitly selected mapping;
3. reading the file according to mapping parameters;
4. mapping source fields to standard-template fields;
5. applying permitted transformations;
6. running defined validations;
7. producing the output file;
8. recording the versions used, processing results, and errors.

Provisional proof-of-concept technologies are:

* Python;
* `pandas`;
* `openpyxl`;
* JSON for mapping configuration.

These technologies are not final decisions. They must be confirmed or revised based on the practical proof of concept.

Core principle:

> The same source file, mapping version, engine version, configuration, and confirmed rules should produce the same result.

AI does not participate in deterministic execution.

---

## 5. Mapping as data

Rules for a specific broker format should be stored separately from program code.

A mapping configuration may be organized by:

* broker;
* processing stream;
* broker format version;
* target-template version.

It may provisionally contain:

* broker identifier;
* stream identifier;
* broker format version;
* target-template version;
* source worksheet name;
* header-row number;
* source column;
* target column;
* data type;
* permitted transformations;
* empty-value handling rules;
* mapping status;
* mapping version.

Illustrative example:

```json
{
  "broker_id": "broker_a",
  "stream": "policy_bordereau",
  "source_sheet": "Bordereau",
  "header_row": 2,
  "template_version": "1.0",
  "columns": [
    {
      "source_column": "Policy Inception",
      "target_column": "Effective Date",
      "data_type": "date",
      "transformations": ["trim", "parse_date"]
    }
  ]
}
````

This example is conceptual only.

The exact JSON structure is not approved and must be derived from the first real thin slice. No physical mapping schema should be created before the real requirements are understood.

---

## 6. Worksheet and header position

During Stage 1, the engine should not attempt to automatically infer:

* the correct worksheet;
* the header row;
* the broker;
* the broker format version.

These parameters should be explicitly provided in the mapping or selected by a human.

Illustrative example:

```json
{
  "source_sheet": "Sheet1",
  "header_row": 2
}
```

Automatic broker recognition, worksheet detection, header detection, and format-version detection are separate future capabilities. They are not part of the first proof of concept.

---

## 7. Broker and mapping selection

The engine must know which mapping configuration to apply.

During Stage 1, the mapping should be selected explicitly by a human.

Minimum selection context may include:

* broker;
* stream;
* broker format version or mapping identifier.

Automatic broker recognition and automatic mapping selection are deferred.

They may be considered later after representative formats and reliable indicators have been accumulated and confirmed.

---

## 8. Transformation library

A mapping must not contain arbitrary executable code.

It may reference only pre-implemented, tested, and permitted transformation operations.

During Stage 1, the transformation library should be minimal and include only operations demonstrated as necessary by the selected real bordereau.

Possible initial operations may include:

* `trim`;
* `parse_date`;
* `parse_percentage`;
* `normalize_currency`;
* `replace_value`;
* `default_if_empty`.

These operations are examples, not an approved mandatory list.

The starting library must not assume support for:

* combining multiple columns;
* splitting one column;
* complex conditional transformations;
* other structural transformations not demonstrated by the representative file.

A new operation should be added only when representative data demonstrates the need.

When a new operation is required, it should be implemented as a reusable controlled function in the shared engine rather than as hidden broker-specific logic or a new complete broker script.

---

## 9. Sources used to determine correctness

The existing Excel script is not the sole reference for correctness.

For the first broker, the following sources should be used:

* the source broker bordereau;
* the standard insurance-company template;
* the existing Excel script;
* the output produced by the existing script;
* confirmed clarification from an analyst or business owner where required.

### Standard template

The standard template defines the required target structure, including:

* required columns;
* column order;
* expected output structure.

The template may not define every business transformation or rule.

### Existing Excel script

The existing Excel script is used as:

* evidence of current logic;
* a source for discovering current transformations;
* a comparison baseline.

It must not automatically be assumed correct because it may contain an outdated rule or an error.

### Confirmed business clarification

Confirmed business clarification is required when correctness cannot be established from the template and existing script alone.

Unconfirmed assumptions must not be silently converted into mapping rules.

---

## 10. First thin slice

Stage 1 should reproduce one existing policy-bordereau process for one broker.

Four artefacts are required:

1. the source bordereau;
2. the standard insurance-company template;
3. the existing Excel script for that broker format;
4. the output produced by that script from the same representative source file.

If a required artefact cannot be obtained, the Stage 1 approach must be reviewed rather than silently assuming an equivalent substitute.

After the required artefacts are available:

1. document the actual source-to-target column correspondences;
2. identify the actual transformations;
3. distinguish simple transformations from special rules;
4. identify unresolved or questionable rules;
5. define the minimum mapping configuration required;
6. define the minimum transformation operations required;
7. create the minimal deterministic engine;
8. produce a new output;
9. compare it with the standard template and existing script output;
10. investigate every material discrepancy.

---

## 11. Stage 1 success criteria

The proof of concept is successful if the new engine:

* produces a file in the required standard-template structure;
* correctly transfers and transforms confirmed values;
* stores mapping separately from engine code;
* contains no hidden broker-specific logic inside the core engine;
* produces a reproducible result;
* surfaces errors and unsupported cases;
* allows every material discrepancy with the existing script output to be explained.

Matching the existing script alone is not sufficient.

Every material discrepancy must be classified as one of the following:

* new-engine error;
* old-script error;
* formatting-only difference;
* unconfirmed business rule;
* open question.

Unexplained discrepancies must not be silently accepted.

---

## 12. Result verification

Comparison should include, where applicable:

* row count;
* column set;
* column order;
* values;
* dates;
* percentages;
* currency values;
* empty values;
* special codes;
* output workbook structure.

Whether formulas, workbook formatting, styles, or other Excel-specific characteristics are part of the required output is an open question. This should be determined after the standard template and existing output are reviewed.

Verification of deterministic logic should be automatable and repeatable.

---

## 13. Human review and approval

A new or changed mapping must not be used operationally without human review and permission.

The approval process itself is not yet defined.

Open questions include:

* who may approve a mapping;
* whether the author and approver must be different people;
* where approval is recorded;
* which approval details must be preserved;
* how a mapping is withdrawn;
* how an old mapping version is superseded;
* what happens to files processed using a previous version.

Until the approval process is defined, the appropriate wording is:

> A mapping that has passed the required human review and is permitted for use.

The concept must not imply that a complete approval workflow already exists.

---

## 14. AI mapping assistant

AI is not required for known files that already have an available permitted mapping.

For a new or changed broker format, AI may later propose an initial mapping.

AI may potentially:

* analyze unfamiliar headers;
* compare them with target-template fields;
* retrieve similar previously confirmed cases;
* propose possible correspondences;
* explain the basis of a proposal.

AI must not:

* approve a mapping independently;
* automatically apply a new mapping;
* alter deterministic rules;
* alter policy or financial values;
* produce the final result outside the deterministic engine.

A human must review and correct the proposal before the mapping is permitted for use.

The deterministic engine must continue operating if AI is unavailable, disabled, or replaced.

---

## 15. Accumulation of confirmed cases

In the future, confirmed mapping cases may be stored as examples for new AI proposals.

Provisional options may include:

* embeddings;
* a vector database;
* retrieval-augmented generation;
* a ready-made LLM accessed through an API.

The exact stored context is not yet defined.

Potentially useful context may include:

* source header;
* target field;
* file context;
* value type;
* previously confirmed transformations.

These are research possibilities, not an approved data structure.

Chroma is only a provisional option and not an accepted technology decision.

Model fine-tuning is deferred. It should be considered only if accumulation of confirmed examples and retrieval-based assistance prove insufficient.

---

## 16. Development sequence

### Stage 1 — One policy-bordereau broker

* define the first mapping configuration;
* build the minimal deterministic engine;
* compare the new result with the required template and current output;
* confirm or revise the basic approach.

### Stage 2 — Remaining policy-bordereau brokers

* extract actual logic from existing solutions;
* create separate mapping configurations;
* extend only the shared operation library where evidence requires it;
* verify each broker format.

### Stage 3 — AI mapping assistant

* test AI proposals against known confirmed cases;
* determine which context is useful;
* define the human-review process;
* evaluate whether retrieval of historical examples provides sufficient value.

### Stage 4 — Claims

* evaluate the confirmed approach using representative claims files;
* create claims-specific mappings and requirements;
* test AI assistance where claims mappings do not exist;
* preserve the independence of claims and policy streams.

No cross-file reconciliation between policy and claims is included unless it is separately approved later.

---

## 17. Core principles

### Deterministic core

All permitted transformations, validations, and output generation are performed through controlled deterministic code.

### Mapping separated from code

Broker-specific correspondences and parameters are stored separately from the reusable engine.

### Minimal operation library

New operations are added only when representative data demonstrates a confirmed need.

### AI proposes only

AI is not part of the mandatory deterministic processing path.

### Human accountability

Humans remain responsible for reviewing and permitting new mappings, rules, and material exceptions.

### Traceability

For each result, it should be possible to identify:

* the source file;
* the selected mapping;
* the mapping version;
* the engine version;
* the relevant configuration;
* the transformations performed;
* the validation results;
* the output file.

### Versioning

Mapping changes must not silently overwrite previous logic.

### Incremental development

One minimal end-to-end process is confirmed first.

More complex transformations, automatic recognition, and AI capabilities are added only when a real need and demonstrated value exist.

---

## 18. Expected result

Instead of many isolated Excel scripts, Tusk should gradually provide:

* one reusable deterministic processing engine;
* separate versioned mapping configurations;
* a minimal library of reusable controlled transformations;
* reproducible result verification;
* a controlled human review and approval process;
* an AI assistant for proposing new mappings;
* traceable history of source files, mappings, rules, versions, decisions, and outputs.

```

