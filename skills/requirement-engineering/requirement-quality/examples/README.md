# Examples & Golden Test Cases (`re.requirement-quality`)

## 1. Overview
This directory contains **original synthetic examples** (`EX-01` .. `EX-15`) and **structured Golden Test Cases** (`GTC-01` .. `GTC-15`) for validating the `re.requirement-quality` Skill across diverse domains (healthcare telemetry, warehouse automation, e-invoicing, cloud IAM, B2B billing, transit ticketing, IoT gateways, banking ledger), requirement formats, and languages (`en`, `vi`, mixed `vi+en`, and unsupported language fallback).

> **Copyright & Originality Note:** All requirement statements in this directory are original synthetic examples created for `Skill_Review`. None are copied from ISO/IEC/IEEE 29148, NASA, or INCOSE publications.

## 2. Files in this Directory

| File | Purpose |
|---|---|
| [`synthetic-examples.md`](synthetic-examples.md) | Human-readable walkthrough of the 15 required scenarios (`EX-01` .. `EX-15`), showing input, context, criterion status evaluation, and false-positive avoidance. |
| [`golden-test-cases.yaml`](golden-test-cases.yaml) | Machine-readable Golden Test Suite (`GTC-01` .. `GTC-15`) with expected statuses for `RQ-01` .. `RQ-09`, expected `Finding` payloads (`schemas/runtime/finding.schema.json`), and behavioral assertions. |

## 3. Scenario Coverage Matrix (Section 13 Requirements)

| Scenario # | Required Coverage Topic | Example ID | Golden Test ID | Language | Artifact / Representation |
|---|---|---|---|---|---|
| 1 | Clear and testable functional requirement | `EX-01` | `GTC-01` | `en` | `srs` (prose statement) |
| 2 | Ambiguous requirement (referential & boolean combinator ambiguity) | `EX-02` | `GTC-02` | `en` | `functional-requirement-list` |
| 3 | Requirement with vague qualitative expressions (unbounded vs bounded contrast) | `EX-03` | `GTC-03` | `en` | `nfr-list` |
| 4 | Requirement with multiple independent obligations (`Singular`) | `EX-04` | `GTC-04` | `en` | `brd` |
| 5 | Requirement containing a valid implementation constraint (anti-false-positive on `Appropriate`) | `EX-05` | `GTC-05` | `en` | `interface-spec` (Constraint) |
| 6 | Requirement that does not need a numerical measurement (behavioral/state verification) | `EX-06` | `GTC-06` | `en` | `system-requirement-spec` |
| 7 | User Story format | `EX-07` | `GTC-07` | `en` | `user-story` (`backlog-item`) |
| 8 | EARS-style requirement (Event-driven / Unwanted behavior) | `EX-08` | `GTC-08` | `en` | `ears` |
| 9 | Requirement with missing business context (`Not Assessable` gate on `RQ-01`, `RQ-06`, `RQ-08`, `RQ-09`) | `EX-09` | `GTC-09` | `en` | `requirement-table` |
| 10 | Requirement with missing verification information | `EX-10` | `GTC-10` | `en` | `prd` |
| 11 | Vietnamese requirement (vague terms, escape clause, open-ended `v.v.`) | `EX-11` | `GTC-11` | `vi` | `srs` |
| 12 | English requirement ( bounded qualitative term — false-positive prevention) | `EX-12` | `GTC-12` | `en` | `api-spec` |
| 13 | Mixed-language requirement (`vi` + `en` technical terms + undefined bilingual slang) | `EX-13` | `GTC-13` | `vi+en` | `srs` |
| 14 | Constraint or business rule (contradicting authoritative parent source on `RQ-08` & constraint on `RQ-06`) | `EX-14` | `GTC-14` | `vi` | `business-rule-doc` |
| 15 | Edge case where a criterion is genuinely `Not Applicable` (container header & top-level axiomatic rule) | `EX-15` | `GTC-15` | `en` | `requirement-table` |

---

## 4. Behavioral Validation Procedure (When Runtime Adapter is Available)

Because the repository is currently at Foundation stage (`0.1.0`) without an executable LLM Runtime Adapter, behavioral validation cannot be executed automatically yet. Once the Runtime Adapter is implemented, execute behavioral validation as follows:

1. For each test case `GTC-01` .. `GTC-15` in `golden-test-cases.yaml`:
   - Assemble an `agent-assignment` (`schemas/runtime/agent-assignment.schema.json`) with `core_agent: artifact-reviewer@0.1.0`, `profile: requirements-review@0.1.0`, and `skills: [re.requirement-quality@0.1.0]`.
   - Pass the test case's `input_requirement` and `supplied_context` as the assignment's artifact and context slice.
2. Validate the returned `review-result` JSON against `schemas/runtime/review-result.schema.json`.
3. Compare each `(Requirement, Criterion)` status and emitted `Finding` against `expected_criterion_statuses` and `expected_findings`:
   - Verify **zero false positives** on `GTC-01`, `GTC-05`, `GTC-06`, `GTC-08`, `GTC-12`.
   - Verify **`Not Assessable` enforcement** (no invented `Compliant` or `Issue`) on `GTC-09` and `GTC-10`.
   - Verify **`Not Applicable` precision** on `GTC-15`.
4. Only after all 15 Golden Test Cases pass behavioral verification may `re.requirement-quality` be promoted from `draft` to `validated`.

---

## 5. Documented Shared Schema Gap & Separate v0.2.0 Proposal

Per **Inspection Rules 3 & 4**, shared schemas in `schemas/` were **not** modified during this task. Instead, the following optional, non-breaking additions are proposed for human approval in `schemas/` v0.2.0:

1. **`schemas/definitions/criterion.schema.json` (v0.2.0 proposal):**
   - Add optional fields to `$defs.Criterion`: `name`, `evaluation_objective`, `pass_conditions`, `issue_conditions`, `required_context`, `optional_context`, `standalone_assessable_when`, `not_assessable_conditions`, `not_applicable_conditions`, `evidence_expectations`, `scope_boundaries` (currently stored inside `synthesis_note`).
2. **`schemas/definitions/analysis-rule.schema.json` (v0.2.0 proposal):**
   - Add optional fields to `$defs.Rule`: `criterion_id`, `normative_level` (`mandatory | recommended | heuristic`), `detection_approach` (`deterministic-pattern | structural-validation | context-reasoning | expert-judgment`), `applicable_languages`, `false_positive_considerations`, `exceptions` (currently stored inside `method`).
3. **`schemas/runtime/review-result.schema.json` (v0.2.0 proposal):**
   - Add optional `item_evaluations[]` array where each item records `{ element_id, criterion_ref, status: "compliant" | "issue" | "not-assessable" | "not-applicable", rationale, limitation_note, finding_ids }` so `Compliant`, `Not Assessable`, and `Not Applicable` evaluations are preserved in machine-readable JSON alongside `findings[]`.
