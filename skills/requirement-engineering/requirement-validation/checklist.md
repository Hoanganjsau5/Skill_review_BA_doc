# Review Checklist — Skill: `re.requirement-validation`

Use this checklist when executing `re.requirement-validation` (`v0.1.0`) to evaluate whether specified requirements reflect stakeholder needs, business/system objectives, authoritative policies, and operational concepts.

## 0. Pre-Assessment Baseline & Evidence Gate
- [ ] **Inventory Authoritative Upstream Baselines:** Which of the following are provided in the review package?
  - [ ] `stakeholder_needs` (Required for `RVAL-01`, `RVAL-02`)
  - [ ] `business_objectives` / KPIs (Required for `RVAL-03`)
  - [ ] `authoritative_policies` / Business Rules / Regulations (Required for `RVAL-04`)
  - [ ] Full upstream baseline of Needs + Objectives + Policies (Required for `RVAL-05`)
  - [ ] `operational_scenarios` / ConOps / User Journeys (Required for `RVAL-06`)
- [ ] **Enforce Missing-Baseline Safeguard:** Mark any criterion whose required upstream baseline is missing as `not_assessable`. Never invent stakeholder needs or external policies not present in the provided context.
- [ ] **Enforce Skill Boundaries:**
  - Do NOT report single-statement wording ambiguity (`re.requirement-quality`).
  - Do NOT report internal requirement-to-requirement contradictions when no upstream need/objective/policy is involved (`re.requirement-set-quality`).
  - Do NOT report missing or broken trace link IDs in a trace table when the semantic content itself is aligned (`re.requirement-traceability`).

## 1. Stakeholder & Business Need Coverage (`RVAL-01` / `RVAL-R001`, `RVAL-R002`)
- [ ] Is every in-scope Stakeholder Need addressed by $\ge 1$ requirement in the full requirement set?
- [ ] Where a Stakeholder Need has multiple sub-needs, target personas, or required outcomes, do the mapped requirements cover all essential parts rather than only a superficial fragment?

## 2. Semantic Alignment with Stakeholder Intent (`RVAL-02` / `RVAL-R003`, `RVAL-R004`)
- [ ] Do the derived requirements faithfully preserve the stakeholder's intended actor, workflow mode (e.g., self-service vs manual), channel, and outcome?
- [ ] Are the requirements free from silent narrowing of eligibility or scope without documented approval?
- [ ] Does the priority/criticality of the derived requirements align with the criticality of the stakeholder need?

## 3. Business & System Objective Alignment (`RVAL-03` / `RVAL-R005`, `RVAL-R006`)
- [ ] Do all specified workflows, approval rules, and performance thresholds support (and not undermine) declared Business Objectives and KPI targets?
- [ ] Is every in-scope Business/System Objective operationalized by supporting functional or quality requirements?

## 4. Compliance with Authoritative Business Rules, Policies & Constraints (`RVAL-04` / `RVAL-R007`)
- [ ] Do requirement calculations, access permissions, segregation-of-duties rules, and data retention/privacy rules comply with authoritative business rules and regulatory extracts?

## 5. Freedom from Unjustified Requirements / Gold-Plating (`RVAL-05` / `RVAL-R008`)
- [ ] Does every requirement have an identifiable justification grounded in a stakeholder need, business objective, authoritative policy, or essential technical/security enablement?
- [ ] Are unrequested vanity features or arbitrary scope expansions flagged as gold-plating?

## 6. Operational & Usage Scenario Validity (`RVAL-06` / `RVAL-R009`, `RVAL-R010`)
- [ ] Can target actors execute declared Operational Scenarios (ConOps / user journeys) end-to-end under the specified requirements and operating environment constraints?
- [ ] Do acceptance criteria validate stakeholder-visible business outcomes?
