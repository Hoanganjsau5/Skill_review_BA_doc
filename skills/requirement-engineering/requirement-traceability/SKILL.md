---
asset_type: skill
skill_id: re.requirement-traceability
name: Requirement Traceability Evaluation
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to:
  - rtm
  - srs
  - brd
  - prd
  - vision-scope
  - use-case-spec
  - user-story-backlog
  - acceptance-criteria-spec
  - system-requirement-spec
  - architecture-design-doc
  - test-plan-or-suite
depends_on: []
sources:
  - source_id: SRC-0001
    version: "2018 (Second edition)"
    sections: ["Clause 6.5"]
  - source_id: SRC-0002
    version: "NASA/SP-2016-6105 Rev2"
    sections: ["Appendix C"]
  - source_id: SRC-0003
    version: "NASA/SP-2016-6105 Rev2 (Section 4.2)"
    sections: ["Section 4.2"]
  - source_id: SRC-0004
    version: "Version 4 (INCOSE-TP-2010-006-04)"
    sections: ["Traceability & Attributes"]
  - source_id: SRC-0005
    version: "2017 (First edition)"
    sections: ["Clause 6.4.3"]
  - source_id: SRC-0006
    version: "2023 (Second edition)"
    sections: ["System Requirements Definition & Traceability"]
last_verified_at: "2026-11-11"
verified_by: null
needs_reverification: false
supersedes: null
---

# Skill: `re.requirement-traceability` (Requirement Traceability Evaluation)

## 1. Purpose & Responsibility Boundary

### 1.1 Purpose
`re.requirement-traceability` evaluates **explicit traceability relationships and link integrity across requirements and related lifecycle artifacts** (ISO/IEC/IEEE 29148:2018 Clause 6.5, ISO/IEC/IEEE 12207:2017 Clause 6.4.3, ISO/IEC/IEEE 15288:2023, NASA SP-2016-6105 Rev2 Section 4.2, INCOSE GtWR v4).

Traceability may be represented as a standalone Requirements Traceability Matrix (`rtm`), inline requirement attributes (`source_id`, `parent_req_id`, `covered_by_test_ids`), section cross-reference tables, or embedded links across upstream and downstream artifacts:
- **Upstream (Origins):** Business Objectives (`BO`), Stakeholder Needs (`SN` / `NEED`), Parent/System Requirements (`SYS-REQ`), Regulatory Clauses (`REG`).
- **Midstream (Decomposition & Functional Modeling):** Software/Product Requirements (`REQ`), Child Requirements, Use Cases (`UC`), User Stories (`US`), Acceptance Criteria (`AC`).
- **Downstream (Realization & Verification):** Architecture/Design Components & APIs (`ARCH` / `CMP` / `API`), Test Cases & Verification Procedures (`TC` / `VER`).

### 1.2 Primary Ownership vs. Neighboring Skills (Strict Non-Overlap)

| Concern / Issue Type | Primary Owner | Why / Boundary Rule |
|---|---|---|
| Whether a single requirement has a unique ID attribute conforming to template syntax (`RQ-09`) or is testable (`RQ-07`) | `re.requirement-quality` | Single-statement quality. `re.requirement-traceability` evaluates **relationships/links between items**, not single-statement prose. |
| Whether peer requirements within the same requirement set have satisfied precondition dependencies (`REQ-A` $\to$ `REQ-B`) or cover declared document scope | `re.requirement-set-quality` | Intra-set horizontal dependencies (`RSQ-05`) and Scope Coverage (`RSQ-01`). Vertical cross-layer trace links (`NEED` $\leftrightarrow$ `REQ` $\leftrightarrow$ `UC` $\leftrightarrow$ `DESIGN` $\leftrightarrow$ `TEST`) belong to `re.requirement-traceability`. |
| Whether the semantic content of requirements adequately solves Stakeholder Needs (`RVAL-01`), preserves stakeholder intent (`RVAL-02`), or constitutes unrequested gold-plating (`RVAL-05`) | `re.requirement-validation` | Semantic validation against upstream needs/objectives. If `REQ-05` has a valid trace link to `NEED-01` (`RTR` passes), `re.requirement-validation` still evaluates whether `REQ-05` distorts `NEED-01`'s meaning. Conversely, if `REQ-05` semantically satisfies `NEED-01` but has no recorded trace link in the RTM, **`re.requirement-traceability` (`RTR-01`)** flags the missing link. |
| **Link Coverage** (Backward `RTR-01` & Forward `RTR-02`), **Bidirectional Symmetry (`RTR-03`)**, **Broken/Deprecated Target IDs (`RTR-04`)**, **Bogus/Irrelevant Trace Links (`RTR-05`)**, **Orphan Requirements & Unallocated Downstream Items (`RTR-06`)** | **`re.requirement-traceability` (THIS SKILL)** | Structural and relational integrity of the traceability graph across lifecycle layers. |

---

## 2. Core Evaluation Criteria (`RTR-01` .. `RTR-06`)

All criteria are defined in [`criteria.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-traceability/criteria.yaml):

1. **`RTR-01` — Backward Traceability Coverage:** Every requirement in scope is explicitly linked backward to its authoritative origin (business objective, stakeholder need, parent requirement, or regulatory mandate).
2. **`RTR-02` — Forward Traceability Coverage:** Every requirement in scope is explicitly linked forward to its required downstream artifacts for the current lifecycle stage (child requirements, Use Cases/User Stories/Acceptance Criteria, design/architecture elements, and/or Test Cases).
3. **`RTR-03` — Bidirectional Traceability Symmetry:** Forward trace links (`Upstream` $\to$ `Downstream`) and backward trace links (`Downstream` $\to$ `Upstream`) are mutually consistent and symmetric across tables and artifacts.
4. **`RTR-04` — Reference & Identifier Integrity:** Every source and target identifier referenced in a trace link resolves to an existing, active (non-deprecated/non-deleted) artifact item, with no duplicate ID collisions across the trace namespace.
5. **`RTR-05` — Relationship Relevance & Evidence Support:** Trace links represent genuine derivation, allocation, or verification relationships between topical peers rather than bogus, mismatched, or placeholder ID pairings.
6. **`RTR-06` — Orphan & Unallocated Element Freedom:** Within the declared traceability model, there are no unexplained orphan requirements (isolated from both origin and downstream layers) and no unallocated downstream design/test items claiming to implement or test unspecified requirements.

---

## 3. Operational Evaluation Rules (`RTR-R001` .. `RTR-R010`)

Defined in [`rules.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-traceability/rules.yaml):

| Rule ID | Mapped Criterion | Rule Type | Normative Level | Summary |
|---|---|---|---|---|
| `RTR-R001` | `RTR-01` | `analysis` | `normative-standard` | Missing Backward Origin Link Detection |
| `RTR-R002` | `RTR-02` | `analysis` | `normative-standard` | Missing Forward Downstream / Verification Link Detection |
| `RTR-R003` | `RTR-02` | `comparison` | `normative-standard` | Parent-to-Child Decomposition Link Gap Detection |
| `RTR-R004` | `RTR-03` | `comparison` | `normative-standard` | Asymmetric Forward vs. Backward Link Mismatch Detection |
| `RTR-R005` | `RTR-04` | `comparison` | `normative-standard` | Broken / Non-Existent Target Identifier Detection |
| `RTR-R006` | `RTR-04` | `comparison` | `normative-standard` | Deprecated / Deleted / Withdrawn Target Link Detection |
| `RTR-R007` | `RTR-04` | `analysis` | `engineering-best-practice` | Trace Identifier Collision & Locator Ambiguity Detection |
| `RTR-R008` | `RTR-05` | `comparison` | `normative-standard` | Bogus / Topically Irrelevant Trace Link Detection |
| `RTR-R009` | `RTR-05` | `comparison` | `engineering-best-practice` | Verification Method & Test Link Incompatibility Detection |
| `RTR-R010` | `RTR-06` | `comparison` | `normative-standard` | Cross-Layer Orphan Requirement & Unallocated Downstream Artifact Detection |

---

## 4. Input Contract

### 4.1 Required Inputs
- **`traceability_representation` (At least one of):**
  - Standalone Requirements Traceability Matrix (`rtm`)
  - Inline trace attributes on requirements (`source_refs`, `parent_id`, `use_case_ids`, `design_refs`, `test_case_ids`)
  - Cross-reference tables inside SRS/BRD/PRD/Test Plan
- **`artifact_inventories` (One or more artifact item lists in scope):**
  - Upstream items (`business_objectives`, `stakeholder_needs`, `parent_requirements`)
  - Target `requirements`
  - Downstream items (`child_requirements`, `use_cases`, `user_stories`, `acceptance_criteria`, `design_elements`, `test_cases`)
- **`declared_trace_model` (Optional, inferred from provided artifacts if omitted):**
  - Specifies which trace layers are expected at the current project lifecycle phase (e.g., `["NEED->REQ", "REQ->UC"]` during early analysis vs. `["NEED->REQ", "REQ->DESIGN", "REQ->TEST"]` during full system specification).

### 4.2 Lifecycle-Stage & Missing-Artifact Safeguard
- **Do NOT penalize missing downstream artifacts that are outside the current lifecycle phase or review package:**
  - If the review package is at the early BRD $\to$ SRS stage and no Design Document or Test Suite is in scope (nor expected in `declared_trace_model`), forward links to Design/Test (`RTR-02`) are marked `not_applicable` or `not_assessable` rather than flagged as missing defects.
  - If an RTM references external IDs (`TC-101`) from a Test Suite that was not uploaded in the review package, `RTR-02` (link presence in RTM) can be assessed, while `RTR-04` (whether `TC-101` exists inside the Test Suite file) and `RTR-05` (whether `TC-101`'s content matches `REQ-01`) are marked `not_assessable` with an `observation` requesting the Test Suite artifact.

---

## 5. Evaluation Procedure (Step-by-Step)

1. **Step 1 — Discover Trace Model & Available Artifact Inventories:**
   - Identify which artifact layers and trace tables/attributes are present in the review package and which trace directions are expected for the lifecycle stage.
   - If zero trace tables, inline trace attributes, or multi-layer artifacts are provided, mark `RTR-01`..`RTR-06` as `not_assessable`.
2. **Step 2 — Audit Identifier Uniqueness & Resolution (`RTR-04` / `RTR-R005`, `RTR-R006`, `RTR-R007`):**
   - Build the symbol table of all item IDs and status tags across provided artifacts.
   - Flag duplicate ID collisions (`RTR-R007`), links pointing to non-existent IDs (`RTR-R005`), and links pointing to items marked `Deprecated` / `Deleted` / `Rejected` / `Out-of-Scope` (`RTR-R006`).
3. **Step 3 — Audit Backward Traceability Coverage (`RTR-01` / `RTR-R001`):**
   - For each active requirement in scope, verify it has $\ge 1$ backward trace link to an upstream origin (Objective, Stakeholder Need, Parent Requirement, or Regulation).
4. **Step 4 — Audit Forward Traceability Coverage (`RTR-02` / `RTR-R002`, `RTR-R003`):**
   - For each active requirement in scope, verify it has $\ge 1$ forward trace link to each downstream layer required by `declared_trace_model` (Child Requirements, Use Cases/Stories/AC, Design Elements, Test Cases).
5. **Step 5 — Audit Bidirectional Symmetry (`RTR-03` / `RTR-R004`):**
   - Where both forward links (e.g., in upstream artifact or RTM table A) and backward links (e.g., in downstream artifact or RTM table B) are recorded, verify that $(u \to d) \iff (d \to u)$.
6. **Step 6 — Audit Relationship Relevance & Verification Compatibility (`RTR-05` / `RTR-R008`, `RTR-R009`):**
   - When the text of both linked items $(u, d)$ is available, verify that $u$ and $d$ actually pertain to the same capability/constraint (`RTR-R008`) and that verification links match the declared verification method (`RTR-R009`).
7. **Step 7 — Detect Cross-Layer Orphans & Unallocated Downstream Items (`RTR-06` / `RTR-R010`):**
   - Identify requirements completely isolated from the trace graph and downstream Design/Test items that have no backward trace link to any requirement.

---

## 6. Output Contract

Compatible with [`finding.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/common/finding.schema.json) and [`review-result.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/runtime/review-result.schema.json):

- **When executed by `cross-artifact-analyzer` (comparing RTM, BRD, SRS, Design, and Test artifacts):**
  - Emits Findings with `basis.type: "comparison-rule"` or `"analysis-rule"`, `basis.ref_id: "RTR-R001" .. "RTR-R010"`, `basis.skill_id: "re.requirement-traceability"`, `basis.skill_version: "0.1.0"`.
- **When executed by `artifact-reviewer` (auditing a standalone RTM or an SRS with embedded trace tables):**
  - Emits Findings with `basis.type: "criterion"`, `basis.ref_id: "RTR-01" .. "RTR-06"`.

---

## 7. Multi-Artifact & Multi-Language Design

- **Artifact-Independent:** Supports dedicated RTM spreadsheets/tables, inline YAML/Markdown attributes, BRD-to-SRS matrices, Epic-to-User-Story-to-Acceptance-Criteria backlogs, and SRS-to-Test-Case tables.
- **Language-Independent:** Traceability graph analysis (ID resolution, symmetry, backward/forward link presence) is 100% language-agnostic, and topical relevance checks (`RTR-05`) operate on semantic concepts across English, Vietnamese, or bilingual artifacts without surface Language Packs (`language-packs/`).

---

## 8. Non-Goals & Limitations

- **Does NOT judge whether the requirement's prose is unambiguous or singular** (owned by `re.requirement-quality`).
- **Does NOT judge deep semantic stakeholder intent alignment or business KPI strategy** when trace links are structurally valid and topically related (owned by `re.requirement-validation`).
- **Does NOT manage live ALM/Jira link synchronization, baselines, or change approval workflows.**
