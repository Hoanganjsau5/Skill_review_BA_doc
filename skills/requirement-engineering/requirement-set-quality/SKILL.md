---
asset_type: skill
skill_id: re.requirement-set-quality
name: Requirement Set Quality Evaluation
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to:
  - srs
  - brd
  - prd
  - vision-scope
  - use-case-spec
  - user-story-backlog
  - acceptance-criteria-spec
  - system-requirement-spec
  - interface-requirement-spec
  - regulatory-requirement-extract
depends_on: []
sources:
  - source_id: SRC-0001
    version: "2018 (Second edition)"
    sections: ["Clause 5.2.6"]
  - source_id: SRC-0002
    version: "NASA/SP-2016-6105 Rev2"
    sections: ["Appendix C"]
  - source_id: SRC-0003
    version: "NASA/SP-2016-6105 Rev2 (Section 4.2)"
    sections: ["Section 4.2"]
  - source_id: SRC-0004
    version: "Version 4 (INCOSE-TP-2010-006-04)"
    sections: ["Characteristics of a Set of Requirements"]
  - source_id: SRC-0005
    version: "2017 (First edition)"
    sections: ["Clause 6.4.3"]
  - source_id: SRC-0006
    version: "2023 (Second edition)"
    sections: ["System Requirements Definition Process"]
last_verified_at: "2026-11-11"
verified_by: null
needs_reverification: false
supersedes: null
---

# Skill: `re.requirement-set-quality` (Requirement Set Quality Evaluation)

## 1. Purpose & Responsibility Boundary

### 1.1 Purpose
`re.requirement-set-quality` evaluates the **internal collective quality of a set of requirements** ($R = \{r_1, r_2, \dots, r_n\}$) within a single artifact or across a partitioned requirement collection. While an individual requirement $r_i$ may be syntactically clear, singular, and verifiable in isolation (`re.requirement-quality`), the **collection of requirements** may still fail as a specification due to omitted scope areas, missing companion/lifecycle counterparts, mutual contradictions between items, exact or semantic duplication, broken inter-requirement prerequisites, or chaotic classification and terminology drift.

This Skill operationalizes the **Characteristics of a Set of Requirements** (ISO/IEC/IEEE 29148:2018 Clause 5.2.6, ISO/IEC/IEEE 12207:2017 Clause 6.4.3, INCOSE GtWR v4 Set Characteristics) into 6 core criteria (`RSQ-01` .. `RSQ-06`) and 10 operational evaluation rules (`RSQ-R001` .. `RSQ-R010`).

### 1.2 Primary Ownership vs. Neighboring Skills (Strict Non-Overlap)

| Concern / Issue Type | Primary Owner | Why / Boundary Rule |
|---|---|---|
| Ambiguity, compound obligations, missing actor/action/target, or unverifiable wording inside **one** requirement ($r_i$) | `re.requirement-quality` | Single-statement defects (`RQ-01`..`RQ-09`). `re.requirement-set-quality` NEVER re-flags single-statement wording defects. |
| **Scope Coverage**, missing companion requirements within declared scope, **Internal Set Consistency** (contradictions between $r_i$ and $r_j$), **Duplicate Requirements**, inter-requirement dependency gaps, set classification/terminology coherence | **`re.requirement-set-quality` (THIS SKILL)** | Properties that emerge only when evaluating two or more requirements together ($r_i \times r_j$) or comparing the requirement set $R$ against its declared scope boundary. |
| Whether requirements align with **Stakeholder Needs**, **Business Objectives**, authoritative policies, or represent gold-plating (**Need Coverage** & semantic intent alignment) | `re.requirement-validation` | Compares requirements ($R$) against authoritative stakeholder needs/objectives ($N, O, P$). |
| Missing/broken/asymmetric **Traceability Links** (`NEED` $\leftrightarrow$ `REQ` $\leftrightarrow$ `UC/US` $\leftrightarrow$ `DESIGN` $\leftrightarrow$ `TEST`) (**Link Coverage** & relationship integrity) | `re.requirement-traceability` | Evaluates explicit trace relationships across artifact layers. Internal unplaced/isolated requirements within the set structure belong to `RSQ-05`/`RSQ-06`, whereas missing cross-layer trace links belong to `re.requirement-traceability`. |
| Deep multi-dimensional trade-off and feasibility conflicts across architecture, budget, hardware, and competing NFRs | `fr.requirement-conflict-analysis` (Planned) | `RSQ-03` flags direct logical, behavioral, data, or threshold contradictions within the requirement set; deep architectural/resource feasibility trade-offs delegate to `fr.requirement-conflict-analysis`. |

---

## 2. Core Evaluation Criteria (`RSQ-01` .. `RSQ-06`)

All criteria are defined in [`criteria.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-set-quality/criteria.yaml):

1. **`RSQ-01` — Scope Coverage:** Every feature area, actor role, subsystem boundary, and external interface explicitly declared as in-scope for the artifact/release is represented by requirements in the set.
2. **`RSQ-02` — Set Completeness & Companion Coverage:** Within covered scope areas, the requirement set leaves no unexplained functional, state-transition, lifecycle (e.g., create/update/cancel/expire), or exception/boundary counterpart gaps, nor unresolved set-level placeholders.
3. **`RSQ-03` — Internal Consistency & Freedom from Contradictions:** Requirements within the set do not contradict one another in logic, state transitions, business rules, timing/numeric thresholds, permissions, or shared domain terminology/units.
4. **`RSQ-04` — Uniqueness & Freedom from Duplication:** Each requirement in the set is unique; the set is free from verbatim duplicates, paraphrased semantic duplicates, and undocumented partial overlaps across sections.
5. **`RSQ-05` — Inter-Requirement Dependency & Interface Coherence:** Prerequisite capabilities, producer-consumer data flows, shared states, and explicit cross-references between requirements within the set are mutually satisfied and free from circular or dangling intra-set dependencies.
6. **`RSQ-06` — Set Organization, Classification & Granularity Coherence:** Requirements are logically grouped, accurately classified by type (e.g., functional vs. quality/NFR vs. constraint vs. interface), and maintained at a coherent level of abstraction without unplaced or misclassified items.

---

## 3. Operational Evaluation Rules (`RSQ-R001` .. `RSQ-R010`)

Defined in [`rules.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-set-quality/rules.yaml):

| Rule ID | Mapped Criterion | Rule Type | Normative Level | Summary |
|---|---|---|---|---|
| `RSQ-R001` | `RSQ-01` | `comparison` | `normative-standard` | Declared Scope Feature / Actor / Interface Omission Detection |
| `RSQ-R002` | `RSQ-02` | `analysis` | `normative-standard` | Missing Companion Lifecycle / State-Transition / Exception Counterpart Detection |
| `RSQ-R003` | `RSQ-02` | `analysis` | `engineering-best-practice` | Unresolved Set-Level Placeholder & Deferred Section Detection |
| `RSQ-R004` | `RSQ-03` | `comparison` | `normative-standard` | Direct Behavioral, Condition-Outcome & Permission Contradiction Detection |
| `RSQ-R005` | `RSQ-03` | `comparison` | `normative-standard` | Incompatible Numeric Threshold, Timing, Unit & Data Constraint Detection |
| `RSQ-R006` | `RSQ-03` | `analysis` | `normative-standard` | Intra-Set Terminology & Entity Definition Drift Detection |
| `RSQ-R007` | `RSQ-04` | `comparison` | `normative-standard` | Exact & Semantic Duplicate Requirement Detection |
| `RSQ-R008` | `RSQ-04` | `comparison` | `engineering-best-practice` | Partial Overlap & Divergent Restatement Detection |
| `RSQ-R009` | `RSQ-05` | `analysis` | `normative-standard` | Unsatisfied Intra-Set Prerequisite, Producer-Consumer & Dangling Reference Detection |
| `RSQ-R010` | `RSQ-06` | `analysis` | `engineering-best-practice` | Requirement Misclassification, Abstraction Mixing & Structural Orphan Detection |

---

## 4. Input Contract

### 4.1 Required Inputs
- **`requirement_set` (`array<object>`, min 2 items for pairwise rules):** A collection of requirements extracted from one or more sections/artifacts, each with at least:
  - `req_id` (or stable document locator / index)
  - `text` (statement or structured fields)
  - `location` (`artifact_id`, `section`, `line_range` or `item_id`)
  - Optional attributes: `category` / `type`, `priority`, `actor`, `module`, `dependencies`.

### 4.2 Optional Contextual Inputs (Unlock Deeper Criteria)
- **`declared_scope`:** Scope section, feature list, context diagram, actor catalog, or release boundary definition (Required to evaluate `RSQ-01`; if absent, `RSQ-01` is marked `not_assessable`).
- **`domain_glossary` / `data_dictionary`:** Canonical term definitions and measurement units (enhances `RSQ-03` / `RSQ-R006`).
- **`partition_metadata`:** Indicates whether the provided `requirement_set` is the **full requirement set** (`completeness_mode: "full"`) or a **partial slice/module extract** (`completeness_mode: "partial"`).
  - *Crucial Safeguard:* When `completeness_mode: "partial"`, missing scope items (`RSQ-01`), missing companion requirements (`RSQ-02`), or external module prerequisites (`RSQ-05`) that might reside in unprovided sections MUST NOT be reported as confirmed defects — they must be classified as `observation` (`not_assessable` / `insufficient_evidence`) requesting the remaining sections.
- **`upstream_individual_quality_findings` (Optional Handoff from `re.requirement-quality`):** Prior findings on individual requirements. If a requirement $r_i$ was flagged as severely ambiguous (`RQ-03`) or incomplete (`RQ-04`), pairwise consistency/duplication checks involving $r_i$ adjust confidence accordingly rather than fabricating set-level conflicts.

---

## 5. Evaluation Procedure (Step-by-Step)

1. **Step 1 — Context & Completeness Mode Gate:**
   - Determine whether `requirement_set` is a `full` specification or a `partial` slice, and whether `declared_scope` is provided.
   - If `< 2` requirements are provided and `declared_scope` is absent, halt set-level pairwise evaluation and emit an `observation` (`not_assessable`).
2. **Step 2 — Normalize Set Representation:**
   - Map each requirement $r_i \in R$ to a language-independent semantic tuple: `(req_id, section/type, actor, trigger/precondition, action/capability, target_object, constraint/threshold, postcondition/state, referenced_ids)`.
3. **Step 3 — Scope Coverage Assessment (`RSQ-01` / `RSQ-R001`):**
   - If `declared_scope` is available, build the checklist of in-scope features, actors, and external interfaces. Verify each has $\ge 1$ covering requirement in $R$ (excluding items explicitly marked Out-of-Scope / Future Phase).
4. **Step 4 — Set Completeness & Companion Analysis (`RSQ-02` / `RSQ-R002`, `RSQ-R003`):**
   - Check stateful entities and workflows in $R$ for missing lifecycle counterparts (e.g., state entered with no exit transition; lock/reserve capability with no unlock/release/timeout capability; happy-path trigger with no failure/rejection rule where data/security integrity is at stake) and set-level placeholders.
5. **Step 5 — Pairwise & Cluster Consistency Analysis (`RSQ-03` / `RSQ-R004`, `RSQ-R005`, `RSQ-R006`):**
   - Group requirements by shared `target_object`, `actor`, `trigger/state`, and `metric`.
   - Compare pairs/clusters $(r_i, r_j)$ for conflicting outcomes under overlapping conditions (`RSQ-R004`), incompatible numeric/temporal bounds or units (`RSQ-R005`), and synonymous/homonymous term drift (`RSQ-R006`).
6. **Step 6 — Uniqueness & Overlap Analysis (`RSQ-04` / `RSQ-R007`, `RSQ-R008`):**
   - Detect exact/semantic duplicates (`RSQ-R007`) and partial overlaps where one requirement restates part of another with subtle divergence (`RSQ-R008`). Distinguish intentional summary/detail hierarchy (when explicitly cross-referenced) from accidental duplication.
7. **Step 7 — Intra-Set Dependency & Interface Coherence (`RSQ-05` / `RSQ-R009`):**
   - Verify that every internal cross-reference (`REQ-X`), consumed state/event, or prerequisite capability required by $r_i$ exists in $R$ and is free from circular prerequisite deadlocks.
8. **Step 8 — Set Organization & Classification Review (`RSQ-06` / `RSQ-R010`):**
   - Check whether functional requirements, quality attributes (NFRs), and constraints are placed in appropriate sections/categories, at a coherent abstraction level, with no unplaced/isolated fragments.

---

## 6. Output Contract

Compatible with [`finding.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/common/finding.schema.json) and [`review-result.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/runtime/review-result.schema.json):

- **When executed by `artifact-reviewer` (single artifact containing a requirement set):**
  - Findings use `basis.type: "criterion"`, `basis.ref_id: "RSQ-01" .. "RSQ-06"`, `basis.skill_id: "re.requirement-set-quality"`, `basis.skill_version: "0.1.0"`.
- **When executed by `cross-artifact-analyzer` (comparing scope section/artifact vs. requirement set or comparing multiple requirement modules):**
  - Findings use `basis.type: "analysis-rule"` or `"comparison-rule"`, `basis.ref_id: "RSQ-R001" .. "RSQ-R010"`, with `evidence` containing at least 2 items for `"comparison-rule"`.
- **Multi-Item Evidence Requirement:**
  - Every contradiction (`RSQ-03`) or duplication (`RSQ-04`) finding MUST cite the specific identifiers and verbatim excerpts of **all** involved requirements ($r_i$ and $r_j$) in `evidence` and `affected_artifacts`.
- **Assessment State Categories (`criterion_assessment_states`):**
  - Each criterion `RSQ-01` .. `RSQ-06` is reported in the summary as `pass`, `issue_found`, `not_assessable`, or `not_applicable`.

---

## 7. Multi-Artifact & Multi-Language Design

- **Artifact-Independent:** Applies equally to traditional `shall` SRS tables, Agile User Story backlogs (Epics + User Stories), Use Case catalogs, PRD feature tables, and system/interface requirement specifications.
- **Language-Independent Without Lexical Dogma:** Set-level properties (scope coverage, logical contradiction, semantic duplication, prerequisite satisfaction, classification coherence) operate on normalized semantic propositions rather than surface grammar. Therefore, `re.requirement-set-quality` does **not** require a surface Language Pack directory (`language-packs/`), and evaluates English, Vietnamese, or mixed-language requirement sets uniformly.

---

## 8. Non-Goals & Limitations

- **Does NOT evaluate single-statement wording quality** (delegated to `re.requirement-quality`).
- **Does NOT validate whether the declared scope itself satisfies stakeholder needs or business strategy** (delegated to `re.requirement-validation`).
- **Does NOT audit cross-artifact traceability matrices (`NEED` $\leftrightarrow$ `REQ` $\leftrightarrow$ `TEST`)** (delegated to `re.requirement-traceability`).
- **Does NOT manage baselines, versions, or change requests.**
