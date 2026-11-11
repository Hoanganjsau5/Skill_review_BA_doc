---
asset_type: skill
skill_id: re.requirement-validation
name: Requirement Validation & Stakeholder Alignment
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to:
  - srs
  - brd
  - prd
  - vision-scope
  - stakeholder-need-spec
  - business-case
  - use-case-spec
  - user-story-backlog
  - acceptance-criteria-spec
  - system-requirement-spec
  - regulatory-requirement-extract
depends_on: []
sources:
  - source_id: SRC-0001
    version: "2018 (Second edition)"
    sections: ["Clause 5.2", "Clause 6.4"]
  - source_id: SRC-0002
    version: "NASA/SP-2016-6105 Rev2"
    sections: ["Appendix C"]
  - source_id: SRC-0003
    version: "NASA/SP-2016-6105 Rev2 (Section 4.2)"
    sections: ["Section 4.2"]
  - source_id: SRC-0004
    version: "Version 4 (INCOSE-TP-2010-006-04)"
    sections: ["Able to be Validated"]
  - source_id: SRC-0005
    version: "2017 (First edition)"
    sections: ["Clause 6.4.2", "Clause 6.4.11"]
  - source_id: SRC-0006
    version: "2023 (Second edition)"
    sections: ["Stakeholder Needs & Requirements Definition", "Validation Process"]
last_verified_at: "2026-11-11"
verified_by: null
needs_reverification: false
supersedes: null
---

# Skill: `re.requirement-validation` (Requirement Validation & Stakeholder Alignment)

## 1. Purpose & Responsibility Boundary

### 1.1 Purpose
`re.requirement-validation` answers the fundamental validation question of Requirements Engineering (ISO/IEC/IEEE 29148:2018 Clause 6.4, ISO/IEC/IEEE 12207:2017 Clause 6.4.2 & 6.4.11, ISO/IEC/IEEE 15288:2023, NASA SP-2016-6105 Section 4.2): **"Are we specifying the right requirements to satisfy stakeholder needs, business/system objectives, and operational concepts?"**

Even when every individual requirement is syntactically clear and testable (`re.requirement-quality`), the requirement set is internally consistent (`re.requirement-set-quality`), and trace links exist in a table (`re.requirement-traceability`), the specification can still fail validation if:
- Identified stakeholder needs or pain points are omitted or only superficially addressed (`RVAL-01`);
- Requirements distort, narrow, or contradict the stakeholder's actual intent during transformation (`RVAL-02`);
- Requirements fail to contribute to or work against stated business KPIs and system goals (`RVAL-03`);
- Requirements violate authoritative business policies, regulations, or domain constraints (`RVAL-04`);
- Requirements introduce unrequested features with no identifiable stakeholder, business, or architectural justification ("gold-plating") (`RVAL-05`);
- Requirements break real-world user operational workflows or stakeholder acceptance expectations (`RVAL-06`).

### 1.2 Primary Ownership vs. Neighboring Skills (Strict Non-Overlap)

| Concern / Issue Type | Primary Owner | Why / Boundary Rule |
|---|---|---|
| Single-statement wording quality, ambiguity, compound sentences, testability, or whether a single requirement is locally faithful to a directly supplied parent sentence (`RQ-01`, `RQ-08`) | `re.requirement-quality` | Single-statement inspection (`RQ-01`..`RQ-09`). When evaluating holistic Need Coverage across all stakeholder needs, multi-requirement intent preservation, business KPI alignment, policy compliance, and set-wide gold-plating, **`re.requirement-validation`** is the primary owner. |
| Internal contradictions ($r_i$ vs $r_j$), duplicates, or missing companion states **within** the requirement set relative to declared document scope | `re.requirement-set-quality` | Evaluates internal set coherence ($R \times R$) and declared Scope Coverage (`RSQ-01`..`RSQ-06`). |
| **Need Coverage** (every stakeholder need is addressed), **Stakeholder Intent Alignment**, **Business/System Objective Alignment**, **Authoritative Policy Compliance**, **Gold-Plating Detection**, **Operational Concept Validity** | **`re.requirement-validation` (THIS SKILL)** | Evaluates semantic sufficiency and alignment between the requirements ($R$) and authoritative upstream sources ($N$: Stakeholder Needs, $O$: Business/System Objectives, $P$: Policies/Constraints, $C$: Operational Scenarios). |
| Structural existence, symmetry, and ID integrity of trace links (`NEED-01` $\leftrightarrow$ `REQ-05` $\leftrightarrow$ `TC-09`) | `re.requirement-traceability` | `re.requirement-traceability` checks whether explicit trace links exist, resolve, and are symmetric (`RTR-01`..`RTR-06`). `re.requirement-validation` checks whether the **content** of the requirements actually fulfills the stakeholder need — even if a trace link is present, or when no formal trace matrix exists. |

---

## 2. Core Evaluation Criteria (`RVAL-01` .. `RVAL-06`)

All criteria are defined in [`criteria.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-validation/criteria.yaml):

1. **`RVAL-01` — Stakeholder & Business Need Coverage:** Every identified stakeholder need, problem statement, or user group expectation in the authoritative upstream context is adequately addressed by one or more requirements (not omitted or only partially covered).
2. **`RVAL-02` — Semantic Alignment with Stakeholder Intent:** Derived requirements faithfully preserve stakeholder intent without distortion, silent narrowing of outcomes, or reversal of stakeholder priorities.
3. **`RVAL-03` — Business & System Objective Alignment:** Requirements demonstrably support and do not undermine declared business objectives, success metrics (KPIs), and system-level mission goals.
4. **`RVAL-04` — Compliance with Authoritative Business Rules, Policies & Constraints:** Requirements semantically comply with authoritative business rules, domain policies, regulatory mandates, and explicit system constraints.
5. **`RVAL-05` — Freedom from Unjustified Requirements (Gold-Plating Prevention):** Every requirement in the specification has an identifiable justification grounded in a stakeholder need, business objective, authoritative policy, or necessary system/architectural enablement.
6. **`RVAL-06` — Operational & Usage Scenario Validity:** Requirements support coherent, realistic end-to-end operational concepts (ConOps), user workflows, and stakeholder acceptance conditions in the intended environment.

---

## 3. Operational Evaluation Rules (`RVAL-R001` .. `RVAL-R010`)

Defined in [`rules.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-validation/rules.yaml):

| Rule ID | Mapped Criterion | Rule Type | Normative Level | Summary |
|---|---|---|---|---|
| `RVAL-R001` | `RVAL-01` | `comparison` | `normative-standard` | Unaddressed Stakeholder Need Detection |
| `RVAL-R002` | `RVAL-01` | `comparison` | `normative-standard` | Partial / Superficial Need Satisfaction Detection |
| `RVAL-R003` | `RVAL-02` | `comparison` | `normative-standard` | Stakeholder Intent Distortion & Silent Restriction Detection |
| `RVAL-R004` | `RVAL-02` | `comparison` | `engineering-best-practice` | Stakeholder Priority & Value Inversion Detection |
| `RVAL-R005` | `RVAL-03` | `comparison` | `normative-standard` | Business Objective & KPI Target Misalignment Detection |
| `RVAL-R006` | `RVAL-03` | `analysis` | `engineering-best-practice` | Unoperationalized Business Goal Detection |
| `RVAL-R007` | `RVAL-04` | `comparison` | `normative-standard` | Authoritative Business Rule & Regulatory Policy Conflict Detection |
| `RVAL-R008` | `RVAL-05` | `comparison` | `normative-standard` | Unjustified Requirement / Gold-Plating Detection |
| `RVAL-R009` | `RVAL-06` | `comparison` | `normative-standard` | Operational Concept (ConOps) & User Workflow Mismatch Detection |
| `RVAL-R010` | `RVAL-06` | `analysis` | `engineering-best-practice` | Stakeholder Validation / Acceptance Readiness Deficit Detection |

---

## 4. Input Contract

### 4.1 Required Inputs
- **`requirements` (`array<object>`):** The target requirements under validation (from SRS, PRD, BRD, User Story backlog, or Use Case specification).
- **`authoritative_validation_baseline` (At least one of the following upstream/contextual sources):**
  - `stakeholder_needs` (BRD stakeholder needs section, interview/workshop summary, problem statements, user personas/needs catalog)
  - `business_objectives` (Vision & Scope goals, business case KPIs, system mission objectives)
  - `authoritative_policies` (Business rules catalog, regulatory/compliance extract, organizational constraints)
  - `operational_scenarios` (Concept of Operations / ConOps, end-to-end user journeys, business process flows)

### 4.2 Missing-Baseline Safeguard (Strict Evidence Gate)
- **Crucial Rule:** `re.requirement-validation` MUST NEVER hallucinate or assume what stakeholders "probably want" based on generic industry assumptions when authoritative upstream context is absent.
- If a specific baseline category is not provided in the review package:
  - No `stakeholder_needs` provided $\rightarrow$ `RVAL-01` and `RVAL-02` are marked `not_assessable`.
  - No `business_objectives` provided $\rightarrow$ `RVAL-03` is marked `not_assessable`.
  - No `authoritative_policies` provided $\rightarrow$ `RVAL-04` is marked `not_assessable`.
  - No upstream needs/objectives/policies provided at all $\rightarrow$ `RVAL-05` (Gold-Plating) is marked `not_assessable`.
  - No `operational_scenarios` / user workflow context provided $\rightarrow$ `RVAL-06` is marked `not_assessable`.

---

## 5. Evaluation Procedure (Step-by-Step)

1. **Step 1 — Baseline Inventory & Assessability Gate:**
   - Inventory which authoritative validation baselines (`stakeholder_needs`, `business_objectives`, `authoritative_policies`, `operational_scenarios`) and `completeness_mode` (`full` vs `partial`) are present.
   - Immediately set criteria lacking their required baseline to `not_assessable`.
2. **Step 2 — Need Coverage Mapping (`RVAL-01` / `RVAL-R001`, `RVAL-R002`):**
   - For each stakeholder need $n_k \in N$, identify all requirements in $R$ that address $n_k$ (using either explicit trace links or semantic matching).
   - Flag any $n_k$ with zero addressing requirements (`RVAL-R001` — only when `completeness_mode: "full"`), and any $n_k$ where the mapped requirements cover only a subset of the sub-needs/personas/outcomes needed to solve the stakeholder's problem (`RVAL-R002`).
3. **Step 3 — Semantic Intent Verification (`RVAL-02` / `RVAL-R003`, `RVAL-R004`):**
   - Compare each requirement cluster against the stakeholder need it claims to satisfy. Flag semantic distortion, silent narrowing (e.g., stakeholder needs automated self-service; requirement specifies manual ticket submission), or priority inversion.
4. **Step 4 — Business & System Objective Alignment (`RVAL-03` / `RVAL-R005`, `RVAL-R006`):**
   - Compare requirement behaviors and thresholds against declared business/system objectives and KPIs (e.g., objective requires reducing checkout latency below 3s or reducing manual review rate by 80%, while requirements mandate synchronous manual approval on every transaction).
5. **Step 5 — Authoritative Policy & Constraint Compliance (`RVAL-04` / `RVAL-R007`):**
   - Cross-check requirement rules, retention periods, access controls, and calculations against authoritative business rules and regulatory extracts.
6. **Step 6 — Justification & Gold-Plating Check (`RVAL-05` / `RVAL-R008`):**
   - For each requirement in $R$, verify whether it is justified by a stakeholder need, business objective, authoritative policy, or essential technical/operational enablement (e.g., security, audit, error handling). Flag unrequested feature creep ("gold-plating").
7. **Step 7 — Operational Scenario & Acceptance Validity (`RVAL-06` / `RVAL-R009`, `RVAL-R010`):**
   - Walk through declared operational scenarios (ConOps / user journeys) against the requirements to verify that actors can complete end-to-end workflows under realistic operational conditions.

---

## 6. Output Contract

Compatible with [`finding.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/common/finding.schema.json) and [`review-result.schema.json`](file:///c:/Users/Owner/Downloads/Skill_Review/schemas/runtime/review-result.schema.json):

- **When executed by `cross-artifact-analyzer` (comparing BRD/Vision/Policy artifact vs. SRS/PRD/Backlog artifact):**
  - Emits Findings with `basis.type: "comparison-rule"` (or `"analysis-rule"`), `basis.ref_id: "RVAL-R001" .. "RVAL-R010"`, `basis.skill_id: "re.requirement-validation"`, `basis.skill_version: "0.1.0"`, citing at least 2 evidence items (the upstream need/objective/policy quote + the downstream requirement quote or search summary).
- **When executed by `artifact-reviewer` (evaluating an all-in-one BRD/PRD/SRS that contains both Business Needs/Objectives and Functional Requirements in the same document):**
  - Emits Findings with `basis.type: "criterion"`, `basis.ref_id: "RVAL-01" .. "RVAL-06"`.

---

## 7. Multi-Artifact & Multi-Language Design

- **Artifact-Independent:** Supports validation across any combination of Vision/Scope, Business Case, BRD, PRD, SRS, Use Cases, User Stories, Acceptance Criteria, and Regulatory Extracts.
- **Language-Independent:** Evaluates semantic alignment between upstream needs and downstream requirements across English, Vietnamese, or cross-language artifacts (e.g., English Business Case / Policy vs. Vietnamese SRS) without relying on surface lexical patterns. No Language Pack (`language-packs/`) is needed.

---

## 8. Non-Goals & Limitations

- **Does NOT check structural trace matrix formatting or broken ID syntax** (owned by `re.requirement-traceability`).
- **Does NOT check internal requirement-to-requirement contradictions or duplicates when no upstream need/policy is involved** (owned by `re.requirement-set-quality`).
- **Does NOT check single-statement grammar or lexical ambiguity** (owned by `re.requirement-quality`).
- **Does NOT manage stakeholder sign-off workflows or approval gates.**
