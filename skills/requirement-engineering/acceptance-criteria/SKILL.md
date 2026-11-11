---
asset_type: skill
skill_id: re.acceptance-criteria
name: Acceptance Criteria
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to: [acceptance-criteria, user-story, acceptance-criteria-spec]
depends_on: []
sources:
  - { source_id: SRC-0001, version: "2018 (Second edition)", sections: ["Clause 5.2.5 (individual requirement characteristics — Verifiable/Unambiguous/Singular, conceptual paraphrase)", "Clause 5.2.6 (characteristics of a set of requirements, conceptual paraphrase)", "Clause 6.4 (requirements validation, conceptual)", "Clause 6.5 (traceability/identifier support, conceptual)"] }
  - { source_id: SRC-0002, version: "NASA/SP-2016-6105 Rev2", sections: ["Appendix C (how to write a good requirement — verification alignment, ambiguity and compound-requirement heuristics; paraphrase)"] }
  - { source_id: SRC-0003, version: "NASA/SP-2016-6105 Rev2 (Section 4.2)", sections: ["Section 4.2 (valid constraints vs premature design; verification method selection; paraphrase)"] }
  - { source_id: SRC-0004, version: "Version 4 (INCOSE-TP-2010-006-04)", sections: ["Set-level characteristics (Complete, Consistent, Able to be Validated; paraphrase)"] }
  - { source_id: SRC-0008, version: "2003 (agilemodeling.com article)", sections: ["INVEST acronym (Testable, Negotiable, Small readings; paraphrase — memory/secondary basis, see RN-0004)"] }
  - { source_id: SRC-0009, version: "2006 (Dan North blog article) + Gherkin reference (cucumber.io docs)", sections: ["BDD scenario structure and Gherkin keyword semantics (conceptual — memory/secondary basis, see RN-0004)"] }
last_verified_at: "2026-11-11"
verified_by: "Skill System Architect"
needs_reverification: false
supersedes: null
---

# Skill: Acceptance Criteria (`re.acceptance-criteria`)

## 1. Purpose

This Skill evaluates the quality of an **Acceptance Criteria (AC) suite**: the collection of acceptance criteria attached to functional requirements, use cases, or user stories within a review package. It answers one question per artifact: *does this suite let a reasonable reviewer decide accept/reject for every in-scope item, without guessing, bundling, drifting, or silently changing what is owed?*

Three architectural principles govern the design (shared with the sibling requirement-engineering Skills):

1. **Language-independent Core.** Criteria and rules are stated semantically; surface-language cues (e.g., Vietnamese vague qualifiers `nhanh`, `kịp thời`, `hợp lý`) are detection *signals* only, validated by competing-interpretation gates before any Issue. Ambiguity vocabulary is consumed from `re.requirement-quality`'s language packs, never re-owned here.
2. **Artifact-independent Evaluation.** The suite may be expressed as Gherkin scenarios, story-level bullet lists, a table with precondition/action/expected columns, or a standalone acceptance-criteria spec. Form is normalized before evaluation; representation never causes a finding by itself.
3. **Extensibility.** New AC formats or project conventions attach through rules and (later) language packs, not by rewriting criteria.

## 2. Scope

### 2.1 Evaluation Criteria (summary)

| ID | Name | Evaluation Objective |
|----|------|----------------------|
| `ACA-01` | Verifiable & Observable Outcome | Each AC states a pass/fail-decidable outcome; quantified where quantity matters, observably behavioral otherwise. |
| `ACA-02` | Given/When/Then Well-formedness | When GWT format is used, precondition/action/expected-result occupy their proper keyword slots. |
| `ACA-03` | Atomicity | One acceptance decision per AC; conjuncts are facets of one event, not bundled behaviors. |
| `ACA-04` | Bidirectional AC–Owner Coverage | Every in-scope FR/UC/story has ≥1 AC; every AC anchors to a resolvable owner item. |
| `ACA-05` | Negative/Edge/Error-Path Presence | Declared failure/boundary modes of owner items are decided by at least one AC. |
| `ACA-06` | No Creep, No Design Lock-in | ACs accept the owner item only — no new obligations, scope, or implementation decisions. |
| `ACA-07` | AC Identity & Numbering | Stable, unique, convention-conforming AC identifiers. |
| `ACA-08` | Unambiguous Acceptance Wording | One reasonable acceptance interpretation per AC; bounded qualifiers and closed lists. |
| `ACA-09` | AC Duplication & Contradiction | No contradictory or redundantly divergent ACs (AC↔AC, AC↔owner functional text). |
| `ACA-10` | Stated Demonstration | How each AC is proven at acceptance is identifiable in or by the suite. |

> **Anti-Dogma Principle.** No rule fires an Issue merely because a keyword, connector, or format quirk appears. Numeric thresholds are required only where the outcome is quantity-sensitive; GWT structure is required only when the project uses GWT; atomicity never penalizes the prescribed data+feedback `And` pattern. Every candidate defect must survive its stated false-positive gate first.

### 2.2 Out of Scope

- **Individual requirement statement quality** outside AC sections (ambiguity, singularity, verifiability of the FR/US text itself) → `re.requirement-quality` (`RQ-01`..`RQ-09`).
- **Whole-set properties of the requirement collection** — declared project scope coverage, companion/lifecycle counterpart gaps, set-wide duplication/contradiction and organization → `re.requirement-set-quality` (`RSQ-01`..`RSQ-06`). `ACA-04`/`ACA-09` see only AC-suite granularity.
- **Trace matrix structure** — RTM rows, cross-layer link symmetry, orphans between SRS/design/test layers → `re.requirement-traceability` (`RTR-01`..`RTR-06`).
- **Validating that ACs actually satisfy stakeholder needs**, and gold-plating judgment → `re.requirement-validation`.
- **Test-case design and coverage engineering** (writing tests from ACs) → `qa.test-design`, `qa.test-coverage` (Planned).
- **Authoring** acceptance criteria (this Skill reviews suites; it may propose wording inside findings but does not produce the artifact).

## 3. Skill Boundary and Delegation

| Topic Observed While Reviewing | In this Skill? | Delegate / Recommend (`SKILL_REGISTRY.yaml`) | Current Registry Status |
|---|---|---|---|
| Wording defect of an FR/story statement (outside AC sections) | No | `re.requirement-quality` (`RQ-03`/`RQ-05`/`RQ-07`) | draft (0.1.0) |
| Requirement set missing scope areas or companion requirements | No | `re.requirement-set-quality` (`RSQ-01`/`RSQ-02`) | draft (0.1.0) |
| RTM link structure, bidirectional trace symmetry across layers | No | `re.requirement-traceability` (`RTR-01`..`RTR-03`) | draft (0.1.0) |
| Whether ACs/requirements satisfy stakeholder needs; gold-plating | No | `re.requirement-validation` | draft (0.1.0) |
| Feasibility of an AC threshold (can we even build/measure it?) | Signal only (`early_feasibility_signals`) | `fr.technical-feasibility` | planned |
| Test-case quality derived from the ACs | No | `qa.test-design` / `qa.test-coverage` | planned |
| Quality of the AC suite itself: wording, structure, anchoring, paths, creep | **Yes (this Skill)** | — | — |

**Rules of engagement.** Delegation is recorded as a recommendation (`delegated_observation`), never silently dropped. This Skill **never** declares `depends_on` on a planned Skill; ownership boundaries above are enforced inside each criterion's `scope_boundaries` and in Step 7 of the Review Procedure. When an observation crosses a boundary but is the *same defect seen at AC granularity* (e.g., a duplicated AC restating a duplicated requirement), report at AC granularity and note the sibling criterion id in the rationale.

## 4. Prerequisites and Multi-Artifact Handling

### 4.1 Supported Inputs

- Artifacts: `acceptance-criteria` (AC lists embedded in stories/sections), `acceptance-criteria-spec` (standalone AC document), `user-story` (story + its AC block — AC portion only).
- Representations: Gherkin-style scenarios; bullet lists (`AC-1: …`); tables (columns for precondition/action/expected/method); prose paragraphs with recognizable per-criterion boundaries; backlog exports with anchor fields.
- Companion context: enumerated owner items (FR/UC/US ids + text) or full artifact containing them; declared review scope (release/module); project AC-format and id conventions if any; glossary/measurement conventions.

### 4.2 Handling Principles

1. **Separation of Parsing and Evaluation.** Structure extraction (AC boundary detection, anchor normalization, keyword slotting) is delegated to parsing Tools (`doc-parser`, `spec-parser`) at runtime. If a Tool is unavailable or fails on a section, evaluation proceeds on confidently bounded items and the missing Tool/format is recorded in `limitations[]` — never fabricated.
2. **Granularity and Boundary Integrity.** Do not assume one heading equals one AC or that bullet lists are AC suites; confirm acceptance-decision semantics per item. Where AC boundaries are ambiguous, report a structure observation and evaluate only the unambiguous subset (Not Assessable elsewhere).
3. **Preservation of Original Text.** Every finding cites the exact excerpt with `ArtifactLocation` (artifact_path, section, line_range/page, element_id). Multilingual artifacts keep original wording in evidence.
4. **Package Completeness Safeguard.** With `completeness_mode: partial` (owner items, definitions, or plans absent), unanchored-coverage and negative-path conclusions become `Not Assessable` + clarification requests. A missing AC for an item you were not given is not evidence.

## 5. Multi-Language Architecture

- Core criteria (`ACA-01`..`ACA-10`) are language-independent; they evaluate semantic properties (decidability, one-decision-per-AC, anchor resolvability).
- Surface cues come from `re.requirement-quality`'s language packs (`en.yaml`, `vi.yaml`) consumed read-only through `ACA-R008`; Vietnamese ACs trigger the same gates as English ones. A mixed-language suite is evaluated item-by-item in its own language.
- An unknown/unlisted language: run language-independent checks (anchors, ids, condition-overlap comparison structure) and record the language gap in `limitations[]`.
- Project-specific AC conventions (numbering style, method columns) are validated under `ACA-07`/`ACA-R010` as *declared or inferable* patterns, not hardcoded into criteria.

## 6. Criterion Context Requirements and Assessability Model

| Criterion | Minimum Information Required | Optional Supporting Context | Assessable from Statement Alone? | When to Return Not Assessable | When Not Applicable Is Justified |
|---|---|---|---|---|---|
| ACA-01 | AC text | Glossary, measurement conventions | Yes (self-contained AC) | Outcome bound lives in an external, unprovided definition | Explicit investigation/prototype acceptance declared by team |
| ACA-02 | AC text with visible GWT keywords | Declared AC-format guide | Yes | Unparseable mixed fragments (parser limitation) | Project's declared format is not GWT and no keywords appear |
| ACA-03 | AC text | Owner-item scope | Yes | — | — |
| ACA-04 | AC list + owner-item enumeration + declared scope | Backlog/RTM | No | Scope declaration or owner-item set absent/partial | — |
| ACA-05 | Owner-item text (failure modes visible) + AC set | Exception-flow descriptions, domain patterns | No | Owner items not provided | Owner item has no state change/external call/boundary (static display) |
| ACA-06 | AC text + its owner-item text | Approved design constraints | No | Owner item not provided | — |
| ACA-07 | AC list as presented (ids visible) | Style guide declaring convention | Yes | Conflicting patterns and no declared convention | Single-bullet prose suites under a declared un-numbered format |
| ACA-08 | AC text | Language-pack signals, referenced definitions | Yes (bounded check) | Definition cited but not in package | — |
| ACA-09 | Suspect pair both-in-package | Glossary (terminology drift) | No (comparison rule: ≥2 items) | Only one side provided | — |
| ACA-10 | AC list (+ suite method mapping if present) | QA conventions, in-package test plan section | Yes with per-AC methods | Method lives in an external plan not provided | Declared exploratory acceptance |

**Never infer missing context.** Missing definitions/plans/owner items produce `Not Assessable` + `clarification_requests[]`, never a confirmed defect.

## 7. Criterion Status and Finding Mapping

### 7.1 Statuses

Each criterion returns one of four statuses per evaluated scope-unit: `Compliant`, `Issue`, `Not Assessable`, `Not Applicable`. `Not Applicable` is justified only by the criterion's own `not_applicable_conditions` (e.g., declared non-GWT format for `ACA-02`) and must cite that justification; it **must never** be used merely because evaluation is hard or context is missing — that is `Not Assessable`.

### 7.2 Status → Finding Classification

| Status | finding.classification | Severity / Confidence Guidance |
|---|---|---|
| Issue | `confirmed-issue` when the rule's gate fully fires with in-package evidence; else `potential-issue` | Severity from `default_severity_hint`, up/down with user impact stated in rationale; confidence `high` only with both-sides verbatim evidence (comparison rules). |
| Issue (context-boundary) | `needs-clarification` | When competing interpretations are unresolvable without the unprovided definition/plan/scope. |
| Compliant | (no finding) | — |
| Not Assessable | `needs-clarification` + `limitations[]` entry | Request the specific missing context item. |
| Not Applicable | (no finding) | Record the justification id in `rationale`. |

### 7.3 Schema Mapping

- `Finding.basis = { type: "criterion" | "analysis-rule" | "comparison-rule", criterion_ref: { owner_type: "skill", owner_id: "re.acceptance-criteria", owner_version: "0.1.0", item_id: "ACA-0x" | "ACA-R00x" } }`.
- Comparison-rule findings (`ACA-R004`, `ACA-R006`, `ACA-R009`) carry **≥2 evidence items**, each with verbatim excerpt and location.
- `finding.category` uses profile categories (`verifiability`, `completeness`, `clarity`, `consistency`, `structure`, `scope-creep` as mapped by `requirements-review` profile).
- Ambiguity findings (`ACA-R008`) must include both competing interpretations, why the divergence matters, and a proposed testable wording (vendor requirement).
- Delegated observations cross-boundary (Step 7) are emitted with `basis.owner_id` of this skill plus `delegation_note` naming the target skill id — never by spoofing another skill's basis.

## 8. Knowledge and Principles

1. **An AC is a requirement seen from the acceptance side.** Individual-requirement characteristics (Verifiable, Unambiguous, Singular — `SRC-0001` Clause 5.2.5, conceptual; `SRC-0002` Appendix C heuristics) apply to AC wording; set characteristics (`SRC-0001` Clause 5.2.6, `SRC-0004`) apply to the suite. This is why `ACA-01/03/08` carry official-standard authority but are scoped to AC sections only.
2. **Separation of acceptance concerns (BDD lineage).** Precondition, action, and expected outcome are distinct slots (`SRC-0009`, conceptual; vendor `business-rule-checklist` pattern). Structure rules enforce slotting, never a specific dialect.
3. **Acceptance must reject bad builds, not only confirm good ones.** Happy-path-only suites are incomplete acceptance (`ACA-05`), but failure modes are taken only from declared text — reviewers do not invent plausible ones.
4. **ACs inherit, they do not legislate.** New obligations or design decisions inside ACs are scope change wearing acceptance clothing (`ACA-06`; `SRC-0003` valid-constraint vs premature-design distinction; team rule: invented content must be labeled PROPOSED).
5. **Story-readiness cues.** INVEST (`SRC-0008`, paraphrase) motivates Testable (`ACA-10`, `ACA-01`) and Small/atomic readings (`ACA-03`) without importing the whole acronym as normative.
6. **One defect, one owner.** The same phenomenon observed through requirement text, set scope, or RTM structure belongs to the sibling skills; this skill keeps the AC-suite lens (`ACA-04` bidirectional anchor diff vs `RSQ-02` vs `RTR-01..03`).

## 9. Authoritative References

| source_id | Title | Version | authority_level | Verification / Access Note |
|---|---|---|---|---|
| SRC-0001 | ISO/IEC/IEEE 29148:2018 Requirements engineering | 2018 (Second edition) | official-standard | Paywalled; conceptual/structural reference only — no verbatim claims (see repository access_note). |
| SRC-0002 | NASA SE Handbook — Appendix C | NASA/SP-2016-6105 Rev2 | industry-best-practice | Public US-Gov publication; summarized heuristics. |
| SRC-0003 | NASA SE Handbook — Section 4.2 | NASA/SP-2016-6105 Rev2 | industry-best-practice | Public; constraints vs premature design. |
| SRC-0004 | INCOSE Guide to Writing Requirements v4 | INCOSE-TP-2010-006-04 | industry-best-practice | Copyrighted; conceptual set-characteristics only. |
| SRC-0008 | Bill Wake, "INVEST in a Good Story" | 2003 (agilemodeling.com) | industry-best-practice | **Proposed registration** — memory/secondary basis; acronym and paraphrased readings only, no fabricated quotes/pages (RN-0004 §5). |
| SRC-0009 | Dan North, "Introducing BDD" (2006) + Gherkin reference (cucumber.io docs) | 2006 + docs (version unspecified) | industry-best-practice | **Proposed registration** — conceptual keyword semantics only; no verbatim claims (RN-0004 §5). |

Research groundwork: [`knowledge/research-notes/RN-0004-acceptance-criteria.md`](../../../knowledge/research-notes/RN-0004-acceptance-criteria.md). Team/vendor raw material (`agents/.agents/skills/business-requirement-analysis`, `ba-documentation`; vendor `prd-review` reference checklists) is internal provenance recorded in `origin_note` fields — those packs are not registered sources.

## 10. Review Procedure

1. **Inspect Context and Conventions.** Load declared AC format (GWT/table/prose), id convention, review scope (release/module), `completeness_mode`, glossary/measurement conventions. Record absent context for the safeguard steps.
2. **Segment and Normalize AC Records.** Detect AC boundaries per §4.2 (never assume one-bullet-per-AC blindly); normalize anchors (explicit id refs or structural containment), slot content for GWT items, and build the owner-item inventory from the package. Missing parser capability → `limitations[]`, evaluate bounded subset.
3. **Identify Language per Item.** Assign en/vi/other per AC; consume language-pack signals read-only for Step 5; unknown language → language-independent checks + limitation.
4. **Evaluate Criteria with Context Gates.** Run `ACA-R001` (verifiability), `ACA-R002` (GWT slots, if applicable), `ACA-R003` (atomicity), `ACA-R004` (bidirectional anchors), `ACA-R005` (declared failure modes), `ACA-R006` (obligation diff), `ACA-R007` (ids), `ACA-R008` (ambiguity), `ACA-R009` (pairwise conflict), `ACA-R010` (demonstration). Apply each criterion's `not_assessable_conditions` / `not_applicable_conditions` before status.
5. **Contextual Verification of Heuristic Signals (Anti-False-Positive Gate).** For every signal-triggered candidate (qualifier words, conjunctions, numeric bounds), attempt the competing-interpretation / independent-failure / condition-overlap test; suppress or downgrade per the rule's false_positive_considerations. Quantified-but-misowned ACs route to `ACA-04`/`ACA-06`, never to ambiguity findings.
6. **Map to Findings and Clarification Requests.** Statuses → §7.2; both-sides excerpts for comparison rules; missing context → `clarification_requests[]` naming exactly what unblocks assessment.
7. **Delegate Out-of-Scope Observations.** Non-AC statement defects → `re.requirement-quality`; set-scope gaps → `re.requirement-set-quality`; RTM structure → `re.requirement-traceability`; needs-satisfaction → `re.requirement-validation`; test engineering → `qa.*` (planned — emit as recommendation with registry status). Keep AC-granularity findings owned here.

## 11. Evaluation Criteria, Rules, Checklist, Examples

- Machine-readable criteria: [`criteria.yaml`](criteria.yaml) (`ACA-01`..`ACA-10`).
- Operational rules with false-positive gates: [`rules.yaml`](rules.yaml) (`ACA-R001`..`ACA-R010`).
- Human checklist (Vietnamese): [`checklist.md`](checklist.md).
- Golden suite (10 cases) and walkthroughs: [`examples/golden-test-cases.yaml`](examples/golden-test-cases.yaml), [`examples/synthetic-examples.md`](examples/synthetic-examples.md).

## 12. Expected Output

A `review-result` (schema: `schemas/runtime/review-result.schema.json`) containing: `findings[]` (§7.3 basis), `clarification_requests[]`, `limitations[]` (missing Tools/languages/context), and `delegated_observations[]` (boundary hand-offs with target skill id). Criterion-level statuses `Compliant/Issue/Not Assessable/Not Applicable` are reported per evaluated unit; early feasibility signals (unrealizable thresholds) attach as `early_feasibility_signals[]` for `fr.*` routing, not as findings here.

## 13. Limitations and Documented Schema Gaps

1. **Standards access.** ISO/IEC/IEEE and INCOSE texts are paywalled/copyrighted; all references are conceptual/structural paraphrase, no verbatim claims (per repository `access_note` discipline). `SRC-0008`/`SRC-0009` are **pending registration** with an explicitly honest memory/secondary basis (RN-0004 §5).
2. **Runtime status.** Foundation stage 0.1.0: no LLM/Tool runtime adapter exists, so all `validation.status` remain `unvalidated` and the Skill stays `status: draft`. Golden cases are behavioral specifications awaiting execution.
3. **Schema gaps (documented, same as siblings).** `criterion.schema.json` uses `additionalProperties: false` with compact fields, so extended metadata is carried inside `synthesis_note` as YAML-shaped text; rule extras live inside `method`. `review-result.schema.json` has no dedicated `criterion_evaluations[]` field yet — statuses ride in summary/rationale. See [`examples/README.md`](examples/README.md) for the v0.2.0 schema proposal note.
