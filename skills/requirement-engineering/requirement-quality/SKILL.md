---
asset_type: skill
skill_id: re.requirement-quality
name: Requirement Quality
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to:
  - srs
  - brd
  - prd
  - user-story
  - ears
  - use-case
  - functional-requirement-list
  - nfr-list
  - system-requirement-spec
  - api-spec
  - interface-spec
  - business-rule-doc
  - backlog-item
  - requirement-table
depends_on: []
sources:
  - source_id: SRC-0001
    version: "2018 (Second edition)"
    sections: ["Clause 5.2.5"]
  - source_id: SRC-0002
    version: "NASA/SP-2016-6105 Rev2"
    sections: ["Appendix C"]
  - source_id: SRC-0003
    version: "NASA/SP-2016-6105 Rev2 (Section 4.2)"
    sections: ["Section 4.2"]
  - source_id: SRC-0004
    version: "Version 4 (INCOSE-TP-2010-006-04)"
    sections: ["Characteristics of Individual Requirement Statements", "Writing Rules Summary"]
last_verified_at: "2026-11-11"
verified_by: "Skill System Architect"
needs_reverification: false
supersedes: null
---

# Requirement Quality (`re.requirement-quality`)

## 1. Purpose
Evaluate the quality of **individual software and systems engineering requirements** extracted from diverse engineering artifacts across multiple natural languages.

This Skill is designed around three architectural principles:
1. **Language-independent Core:** The nine core evaluation criteria (`RQ-01` .. `RQ-09`), status model, context requirements, and finding mapping do not depend on any specific natural language.
2. **Artifact-independent Evaluation:** Requirements may originate from SRS, BRD, PRD, User Stories, EARS statements, Use Cases, API/interface specifications, business rule catalogs, or backlog tables.
3. **Extensibility:** Natural-language heuristics (`language-packs/*.yaml`), requirement representation formats, and project-specific conventions are decoupled from the core criteria so new languages (e.g., `ja`) or conventions can be added without modifying `criteria.yaml`.

---

## 2. Scope

### 2.1 In Scope — Nine Core Characteristics (ISO/IEC/IEEE 29148:2018 Clause 5.2.5)
| Criterion ID | Name | Evaluation Objective |
|---|---|---|
| `RQ-01` | **Necessary** | Determine whether the requirement is justified by an identifiable business, stakeholder, parent, or regulatory need. |
| `RQ-02` | **Appropriate** | Determine whether the requirement expresses the appropriate level of detail and abstraction for its entity/artifact level without premature implementation bias. |
| `RQ-03` | **Unambiguous** | Determine whether the requirement admits only one reasonably clear interpretation in its context. |
| `RQ-04` | **Complete** | Determine whether sufficient information (actor/subject, action/behavior, conditions, bounds, or valid references) is present to understand the requirement at its level. |
| `RQ-05` | **Singular** | Determine whether the requirement expresses one independent obligation, capability, or constraint rather than bundling unrelated obligations. |
| `RQ-06` | **Feasible** | Determine whether the requirement appears achievable within the supplied technical, operational, environment, and resource constraints. |
| `RQ-07` | **Verifiable** | Determine whether compliance with the requirement can be objectively verified (via test, demonstration, analysis, or inspection). |
| `RQ-08` | **Correct** | Determine whether the requirement accurately represents its authoritative source, parent requirement, or stated stakeholder need. |
| `RQ-09` | **Conforming** | Determine whether the requirement follows applicable project, organizational, and documentation conventions (templates, IDs, glossary, mandatory attributes). |

> **Anti-Dogma Principle:** These nine characteristics are **semantic quality attributes**, not mandatory writing templates. A requirement does **not** automatically fail because it lacks a numeric metric, uses User Story or tabular syntax, or omits the modal verb `shall`.

### 2.2 Out of Scope (Explicit Exclusions)
This Skill evaluates **individual requirements** one by one. It is **NOT** responsible for full evaluation of:
- Overall SRS or document structure completeness.
- Requirement-set consistency, conflict analysis across a document, or set-level coverage.
- Duplicate requirements across an entire system.
- Bidirectional traceability across requirements, design, APIs, and test cases.
- Full Use Case flow quality or alternative/exception flow completeness.
- Authoring or full review of standalone Acceptance Criteria suites.
- Test Case design and test procedure authoring.
- System-wide architectural feasibility or detailed technical solution assessment.
- Overall project Delivery Readiness.

---

## 3. Skill Boundary and Delegation

When an Agent executing `re.requirement-quality` encounters evidence of an issue outside individual requirement quality, it must **not** attempt a full out-of-scope assessment. Instead, it records a scoped observation or limitation and recommends delegation to the appropriate Skill or Capability in `SKILL_REGISTRY.yaml`:

| Topic Observed | In `re.requirement-quality`? | Delegate / Recommend (`SKILL_REGISTRY.yaml`) | Current Registry Status |
|---|---|---|---|
| Quality of an individual requirement statement (`RQ-01`..`RQ-09`) | **Yes (Primary Scope)** | `re.requirement-quality` (this Skill) | `draft` (`0.1.0`) |
| Overall SRS structure, missing document sections, set-level completeness | No | `re.srs-review` | `planned` |
| Detailed Use Case flows, preconditions, postconditions, extensions | No | `re.use-case-analysis` | `planned` |
| Detailed review of Acceptance Criteria suites | No | `re.acceptance-criteria` | `planned` |
| Cross-artifact or bidirectional requirement traceability | No | `re.requirement-traceability` (Profile: `traceability`) | `planned` |
| Conflicts or contradictions between multiple requirements in a set | No | `fr.requirement-conflict-analysis` (Capability: `feasibility-risk`) | `planned` |
| System/architectural technical feasibility under project constraints | No | `fr.technical-feasibility` (Capability: `feasibility-risk`) | `planned` |
| Test case design and test coverage derivation | No | `qa.test-design`, `qa.test-coverage` (Profile: `qa-review`) | `planned` |
| Stage gate / Definition of Ready evaluation | No | Capability `delivery-readiness` | `draft` (`0.1.0`) |

> **Rule:** Never declare a hard dependency (`depends_on`) on a `planned` Skill. Delegation is recorded as a recommendation in the Finding or Review Result.

---

## 4. Prerequisites & Multi-Artifact Handling

### 4.1 Supported Artifacts and Representations
- **Artifact types (`applies_to`):** `srs`, `brd`, `prd`, `user-story`, `ears`, `use-case`, `functional-requirement-list`, `nfr-list`, `system-requirement-spec`, `api-spec`, `interface-spec`, `business-rule-doc`, `backlog-item`, `requirement-table`.
- **Requirement representations:**
  - Traditional natural-language statements (prose sentences or numbered paragraphs).
  - Structured tables / spreadsheets (columns for ID, statement, priority, rationale, verification method, etc.).
  - Requirement lists / hierarchies.
  - User Story format (`As a <role>, I want <goal>, so that <benefit>` — or equivalent in another language).
  - EARS patterns (Ubiquitous, Event-driven `WHEN`, State-driven `WHILE`, Unwanted behavior `IF ... THEN`, Optional `WHERE`).
  - Given/When/Then behavioral specifications when used as requirement statements.
  - Interface/API requirement clauses and business rule statements.
- **Requirement types:** Functional, Non-functional (performance, reliability, usability, maintainability, portability), Constraints, Interface requirements, Business rules, Data requirements, Security requirements.

### 4.2 Artifact & Boundary Principles
1. **Separation of Parsing and Evaluation:** Document parsing/extraction is performed by operational Tools (`doc-parser`, `spec-parser`, `project-retrieval` in `tools/README.md`). If a document format cannot be parsed by available runtime tools, report the missing Tool/adapter in `review-result.limitations` and do not fabricate extracted text.
2. **Granularity & Boundary Integrity:** Do not assume one heading, one paragraph, one table row, or one User Story automatically equals one requirement. If requirement boundaries are unclear (e.g., an unsegmented multi-paragraph prose block), report the boundary ambiguity (`RQ-05` / `RQ-09`) rather than silently inventing requirement splits.
3. **Preservation of Original Text:** Always preserve the exact original requirement excerpt and its `ArtifactLocation` (`artifact_path`, `section`, `line_range` or `page`, `element_id`) in `Evidence`. Never modify the source document.

---

## 5. Multi-Language Architecture

### 5.1 Architectural Separation
- **Core Criteria (`criteria.yaml`) & Core Rules (`rules.yaml`):** 100% independent of natural language. They define semantic conditions, structural checks, and context gates.
- **Language Packs (`language-packs/<lang>.yaml`):** Provide language-specific linguistic signals (vague qualitative terms, open-ended clauses, ambiguous combinators, unanchored pronouns, escape clauses, modal/obligation markers, and false-positive warnings).
  - Implemented packs: English ([`language-packs/en.yaml`](language-packs/en.yaml)) and Vietnamese ([`language-packs/vi.yaml`](language-packs/vi.yaml)).
  - Adding a new language (e.g., `ja`) requires only adding `language-packs/ja.yaml` following [`language-packs/README.md`](language-packs/README.md).
- **Project Conventions (`project-context` / `review-config`):** Configured per project (e.g., mandatory modal verbs, ID patterns, approved glossary, template structure). Evaluated under `RQ-09` (`Conforming`), never hardcoded as universal language rules.

### 5.2 Language Identification & Fallback Rules
1. Evaluate language per **individual requirement** (never assume an entire document uses a single language).
2. Use explicit language metadata when supplied; otherwise apply reliable language detection.
3. **Mixed-language requirements** (e.g., Vietnamese statement embedding English technical terms or API identifiers): load both relevant Language Packs (`vi` + `en`) and do not flag domain-standard English technical identifiers inside Vietnamese requirements unless project conventions forbid them.
4. **Unknown or unsupported language:** Record a limitation in `review-result.limitations`, skip language-pack heuristic signals, and execute only language-independent structural and context-based checks that remain valid.

---

## 6. Criterion Context Requirements & Assessability Model

A core requirement of this Skill is **never inferring missing context**. Every criterion defines what context it needs:

| Criterion | Minimum Information Required | Optional Supporting Context | Assessable from Statement Alone? | When to Return `Not Assessable` | When `Not Applicable` is Justified |
|---|---|---|---|---|---|
| `RQ-01` **Necessary** | Requirement statement + identifiable need (business objective, stakeholder need, parent requirement, regulatory mandate, or explicit rationale). | Traceability links, product vision, scope boundaries. | **No** (except when the statement itself explicitly declares redundancy/obsolescence, e.g., "Deprecated — no longer needed"). | No source justification, parent requirement, rationale, or business/stakeholder need is provided. | Rarely; e.g., pure informational headings or non-normative explanatory notes explicitly marked as non-requirements. |
| `RQ-02` **Appropriate** | Requirement statement + declared requirement/artifact level (e.g., business, stakeholder, system, software, interface) or target entity boundary. | Architecture decisions (`architecture-decisions.md`), known constraints, target audience. | **Partially** — only if the artifact type/level is known and the statement clearly specifies low-level code/UI implementation mechanics inappropriate for that level. | Artifact/requirement level is unknown, OR the statement specifies a technical choice and it is unknown whether that choice is a mandated upper-level constraint or premature design. | Non-normative context notes; or when evaluating a pure implementation-level specification where low-level detail is the intended level. |
| `RQ-03` **Unambiguous** | Original requirement statement. | Domain glossary, surrounding section definitions, Language Pack for the requirement's language. | **Yes** for syntactic/referential/vague-term ambiguity; **Needs glossary** if specialized domain terms could be Either well-defined jargon or undefined terms. | Statement is corrupted/unreadable, or uses domain-specific symbols/acronyms whose meaning depends entirely on an unavailable external glossary. | Never for a normative requirement statement. |
| `RQ-04` **Complete** | Original requirement statement + requirement type. | Referenced tables/diagrams/interfaces, condition catalogs, NFR context. | **Yes** when mandatory structural slots for its type are missing (e.g., missing actor/subject, missing action/outcome, dangling reference "see Section TBD", "to be defined"). | The requirement delegates details to an external artifact/section ("as specified in ICD-04") that was not provided in the review scope. | Never for a normative requirement statement. |
| `RQ-05` **Singular** | Original requirement statement. | Requirement representation format (e.g., EARS, User Story, table). | **Yes** — independent obligations, decoupled capabilities, or unrelated constraints bundled together can be identified directly from the statement structure. | Statement is truncated or unparseable. | Composite container headers that explicitly serve only as a grouping title for child atomic requirements. |
| `RQ-06` **Feasible** | Requirement statement + relevant project/technical/environmental/resource constraints (`project-context.yaml`). | Benchmarks, infrastructure specs, team capabilities, timeline, budget, external service limits. | **No** (except when the statement is logically self-contradictory or violates fundamental mathematical/physical laws, e.g., "100.0% availability with zero redundancy over public internet"). | Technical, environmental, or project constraints needed to judge achievability are `missing` in Project Context and the statement is not self-contradictory. | Pure business-rule definitions or glossary/policy definitions that impose no technical/operational realization constraint beyond deterministic logic. |
| `RQ-07` **Verifiable** | Original requirement statement + requirement type. | Acceptance criteria, verification method metadata, measurement environment, glossary. | **Yes** when the statement specifies observable deterministic behavior/state transition or clearly unverifiable subjective goals ("shall be intuitive and pleasing"). | Verification depends on an external acceptance test specification or referenced threshold table that exists in the project but was not supplied in the review scope. | Pure organizational policy statements that are not system/software requirements (if included in artifact). |
| `RQ-08` **Correct** | Requirement statement + authoritative source (parent requirement, stakeholder input record, regulation, or business rule source). | Domain expert confirmation, business objectives, ADR. | **No** (except when the statement contains an internal mathematical/logical error that cannot be true under any source). | Authoritative source, parent requirement, or stakeholder intent is not supplied. | Top-level axiomatic business policy when no higher-level source exists and the statement is the authoritative source itself. |
| `RQ-09` **Conforming** | Requirement statement + applicable project/organizational conventions (template, ID format, mandatory attributes, glossary rules). | Artifact type convention, style guide. | **No** (unless the artifact itself declares its own template/convention in its header/preamble and the requirement violates it). | No project conventions, template rules, or style guides are supplied in Project Context / config or artifact preamble. | Ad-hoc exploratory notes where the project explicitly states no formatting/template convention applies (`status: not-applicable`). |

---

## 7. Criterion Status and Finding Mapping

### 7.1 Four Criterion Statuses (per `(Requirement, Criterion)` pair)
- `Compliant`: Positive evidence confirms the requirement satisfies the criterion (and required context is present).
- `Issue`: Specific evidence shows a violation or weakness against the criterion.
- `Not Assessable`: Essential context or referenced artifact required by Section 6 is missing; the Agent **must not** guess `Compliant` or `Issue`.
- `Not Applicable`: The criterion genuinely does not apply to this item (see Section 6 table). Must never be used merely because evaluation is hard.

### 7.2 Mapping Criterion Status to `finding.schema.json`
Not every `(Requirement, Criterion)` evaluation produces a Finding:

| Criterion Status | Generates Finding? | `finding.classification` | `severity` & `confidence` Guidance (`SYSTEM_CONFIG.md`) |
|---|---|---|---|
| `Compliant` | **No** | — | — |
| `Issue` (clear, direct violation with complete context) | **Yes** | `confirmed-issue` | `critical` / `major` / `minor` based on downstream impact; `confidence: high` |
| `Issue` (contextual risk or heuristic signal that remains ambiguous in context) | **Yes** | `potential-issue` | `major` / `minor`; `confidence: medium` or `low` |
| `Issue` (minor stylistic/structural refinement when meaning is still clear) | **Yes** | `improvement-suggestion` | `minor` or `info`; `confidence: high` or `medium` |
| `Not Assessable` (missing context is non-critical or already tracked at project level) | **No** (record in `limitations` / `clarification_requests`) | — | — |
| `Not Assessable` (missing context materially blocks understanding or verification of a key requirement) | **Optional (1 consolidated Finding or `clarification_request`)** | `needs-clarification` | `major` or `minor`; `confidence: high` (that info is missing) |
| `Not Applicable` | **No** | — | — |

### 7.3 Mapping to Existing Input/Output Contracts (`schemas/`)
- **Input mapping:**
  - Artifact text and locations come from `agent-assignment.scope.artifacts` (`ArtifactLocation`, with `element_id` holding the Requirement ID).
  - Project constraints, business objectives, functional scope, mandatory technologies, and assumptions come from `project-context.yaml` (`project-context.schema.json`).
  - Project conventions (templates, ID rules, glossary) come from `project-context` / `review-config.yaml` or artifact preamble.
- **Output mapping (`review-result.schema.json` & `finding.schema.json`):**
  - Each Finding uses `basis`:
    ```json
    {
      "type": "criterion",
      "criterion_ref": {
        "owner_type": "skill",
        "owner_id": "re.requirement-quality",
        "owner_version": "0.1.0",
        "item_id": "RQ-03"
      }
    }
    ```
  - `finding.category` maps to the active Profile's `finding_categories` (e.g., `clarity` for `RQ-03`, `completeness` for `RQ-04`, `verifiability`/`testability` for `RQ-07`, `structure` for `RQ-05`/`RQ-09`, `consistency` for `RQ-01`/`RQ-02`/`RQ-08`).
  - `finding.evidence[]` preserves `location.artifact_path`, `location.element_id` (Requirement ID), `location.section`/`line_range`, and exact `excerpt`.
  - `finding.rationale` records the rule ID applied (`RQ-Rxxx`), the criterion status (`Issue` or `Not Assessable`), and contextual reasoning.
  - Missing context across requirements is recorded in `review-result.clarification_requests[]` and `review-result.limitations[]`.

---

## 8. Knowledge & Principles

1. **Semantic Evaluation over Keyword Matching (`SRC-0001`, `SRC-0002`, `SRC-0004`):** Linguistic signals from a Language Pack (e.g., English *"fast"*, *"appropriate"*, Vietnamese *"nhanh chóng"*, *"phù hợp"*) are **heuristic triggers**, never automatic defects. If the same requirement or linked glossary defines the bound (e.g., *"fast recovery (RTO <= 30 seconds)"*), the requirement is `Compliant` on `RQ-03` and `RQ-07`.
2. **Qualitative / Behavioral Verifiability (`SRC-0001`, `SRC-0002`):** Not every requirement requires a numerical metric. Deterministic state transitions, role-based access rules, and structural format rules are objectively verifiable by test or inspection without numbers.
3. **Valid Constraints vs. Premature Design (`SRC-0001`, `SRC-0003`):** Specifying a concrete protocol, database, or encryption algorithm in a requirement is an `RQ-02` (`Appropriate`) issue **only** if it is an unjustified implementation choice at a higher abstraction level. When mandated by an external interface, regulation, or architectural decision (`architecture-decisions.md`), it is a valid constraint.
4. **Representation Neutrality (`SRC-0001`, `SRC-0004`):** A User Story, an EARS statement, a tabular specification row, or a traditional `shall` statement can each be `Compliant` or `Issue` across `RQ-01`..`RQ-09`. Do not penalize a requirement for not using `shall` unless the project's own convention (`RQ-09`) mandates `shall`.

---

## 9. Authoritative References

| source_id | Title | Version/Edition | authority_level | Verification / Access Note |
|---|---|---|---|---|
| `SRC-0001` | ISO/IEC/IEEE 29148 — Systems and software engineering — Life cycle processes — Requirements engineering | 2018 (Second edition) | `official-standard` | Secondary-source & official abstract verification (Clause 5.2.5); full text paywalled. |
| `SRC-0002` | NASA Systems Engineering Handbook — Appendix C: How to Write a Good Requirement | NASA/SP-2016-6105 Rev2 (2016) | `industry-best-practice` | Public US Government handbook; used as supporting guidance/heuristics. |
| `SRC-0003` | NASA Systems Engineering Handbook — Section 4.2: Technical Requirements Definition | NASA/SP-2016-6105 Rev2 (2016) | `industry-best-practice` | Public US Government handbook; used for rationale, abstraction level, and constraints. |
| `SRC-0004` | INCOSE Guide to Writing Requirements (GtWR) | Version 4 (INCOSE-TP-2010-006-04, 2023) | `industry-best-practice` | Verified via official INCOSE v4 summary sheet & secondary literature; full text copyrighted. |

See Research Note: [`knowledge/research-notes/RN-0001-individual-requirement-quality.md`](../../../knowledge/research-notes/RN-0001-individual-requirement-quality.md).

---

## 10. Review Procedure

When assigned to evaluate requirements in an artifact, the Agent must execute the following 7 steps:

1. **Step 1 — Inspect Context & Conventions:**
   - Load the provided `context_slice` (`project-context.yaml`, `architecture-decisions.md`, `assumptions-and-limitations.md`, glossary, project requirement conventions).
   - Identify which context dimensions are `provided`, `assumed`, `missing`, or `not-applicable`.
2. **Step 2 — Segment & Normalize Requirement Records:**
   - Extract or read individual requirement records from the artifact (`requirement_id`, `original_text`, `artifact_type`, `requirement_type`, `requirement_level`, `location`, `attributes`).
   - If requirement boundaries are ambiguous, record a boundary finding/limitation (`RQ-05`/`RQ-09`) rather than guessing boundaries.
3. **Step 3 — Identify Language per Requirement:**
   - Determine the natural language(s) of each requirement (`en`, `vi`, mixed, or other).
   - Load matching Language Packs from `language-packs/`. If a language is unsupported, record a limitation in `review-result.limitations` and restrict evaluation to language-independent rules.
4. **Step 4 — Evaluate Criteria `RQ-01` .. `RQ-09` with Context Gates:**
   - For each requirement and each criterion `RQ-01` .. `RQ-09`:
     - Check whether minimum required context (Section 6) is available.
     - If essential context is missing and no self-contained violation exists $\rightarrow$ set status to `Not Assessable`.
     - If the criterion genuinely does not apply $\rightarrow$ set status to `Not Applicable`.
     - Otherwise, apply the evaluation rules in [`rules.yaml`](rules.yaml) and Language Pack signals to determine `Compliant` or `Issue`.
5. **Step 5 — Contextual Verification of Heuristic Signals (Anti-False-Positive Gate):**
   - For every heuristic signal triggered (e.g., vague word, conjunction `and`/`và`, passive voice, missing numeric metric, technical constraint term):
     - Check surrounding clauses, linked acceptance criteria, glossary definitions, and requirement type exceptions.
     - Discard the signal (`Compliant`) if the meaning is unambiguous and verifiable in context.
6. **Step 6 — Map to Findings & Clarification Requests:**
   - Convert `Issue` statuses (and material `Not Assessable` blockers) into `Finding` objects conforming to `schemas/runtime/finding.schema.json` using the mapping in Section 7.2.
   - Populate `clarification_requests[]` and `limitations[]` in `review-result.json`.
7. **Step 7 — Delegate Out-of-Scope Observations:**
   - If set-level conflicts, missing cross-document trace links, or architectural feasibility concerns are observed, record `early_feasibility_signals` or delegation notes (Section 3) without overstepping this Skill's boundary.

---

## 11. Evaluation Criteria, Rules, Checklist, and Examples

- **Core Criteria (`RQ-01` .. `RQ-09`):** [`criteria.yaml`](criteria.yaml)
- **Detection & Evaluation Rules (`RQ-R001` .. `RQ-R018`):** [`rules.yaml`](rules.yaml)
- **Language Packs:** [`language-packs/README.md`](language-packs/README.md), [`language-packs/en.yaml`](language-packs/en.yaml), [`language-packs/vi.yaml`](language-packs/vi.yaml)
- **Reviewer Checklist:** [`checklist.md`](checklist.md)
- **Synthetic Examples & Golden Test Cases:** [`examples/README.md`](examples/README.md), [`examples/synthetic-examples.md`](examples/synthetic-examples.md), [`examples/golden-test-cases.yaml`](examples/golden-test-cases.yaml)

---

## 12. Expected Output
- `review-result` JSON object (`schemas/runtime/review-result.schema.json`) containing:
  - `findings[]` with `basis.type = "criterion"` referencing `re.requirement-quality@0.1.0#RQ-01..RQ-09`, `category` aligned with the executing Profile (`completeness`, `clarity`, `consistency`, `structure`, `testability`, `verifiability`), exact `evidence[]`, `rationale` (including rule ID and criterion status), and `suggested_correction`.
  - `clarification_requests[]` for missing context (`Not Assessable`) that materially affects requirement understanding.
  - `early_feasibility_signals[]` when an `RQ-06` observation indicates a potential project-level feasibility issue.
  - `limitations[]` for unsupported languages, unparseable formats, or unassessable criteria due to missing project context.

---

## 13. Limitations & Documented Schema Gaps

1. **Verification Limitation on Copyrighted Standards:** `SRC-0001` (ISO/IEC/IEEE 29148:2018) and `SRC-0004` (INCOSE GtWR v4) are commercial/copyrighted standards verified via official abstracts/summaries and practitioner references; full texts are not stored in the repository.
2. **Runtime Execution Limitation:** The Skill_Review system is currently at Foundation stage (`0.1.0`) without an automated LLM Runtime Adapter or behavioral test runner. Therefore, this Skill's status remains `draft` and its criteria/rules remain `validation.status: unvalidated` until behavioral execution is implemented.
3. **Documented Shared Schema Gaps (Unmodified per Inspection Rule 3 & 4):**
   - `schemas/definitions/criterion.schema.json` and `schemas/definitions/analysis-rule.schema.json` set `additionalProperties: false` with a compact field set. To preserve 100% schema compatibility without modifying shared schemas, extended criterion metadata (`required_context`, `optional_context`, `not_assessable_conditions`, `not_applicable_conditions`) and rule metadata (`criterion_id`, `normative_level`, `detection_approach`, `false_positive_considerations`, `exceptions`) are structured inside `synthesis_note` and `method` respectively.
   - `schemas/runtime/review-result.schema.json` does not yet include a dedicated `criterion_evaluations[]` array for recording per-requirement `(requirement_id, criterion_id, status: Compliant | Issue | Not Assessable | Not Applicable)` tuples when no Finding is emitted.
   - See [`examples/README.md`](examples/README.md) for the non-breaking v0.2.0 schema extension proposal.
