---
note_id: RN-0002
topic: "Requirement Engineering Skill Domain — Ownership Matrix, Evaluation Methods & Source Synthesis"
target_skills: [re.requirement-quality, re.requirement-set-quality, re.requirement-validation, re.requirement-traceability]
sources: [SRC-0001, SRC-0002, SRC-0003, SRC-0004, SRC-0005, SRC-0006]
author: Skill System Architect
created_at: 2026-11-11
status: complete
---

# RN-0002: Requirement Engineering Skill Domain — Ownership Matrix, Evaluation Methods & Source Synthesis

- **Note ID:** `RN-0002`
- **Domain:** `requirement-engineering`
- **Target Skills:**
  - `re.requirement-quality` (`v0.1.0`, existing)
  - `re.requirement-set-quality` (`v0.1.0`, newly designed)
  - `re.requirement-validation` (`v0.1.0`, newly designed)
  - `re.requirement-traceability` (`v0.1.0`, newly designed)
- **Authoritative Sources Synthesized:** `SRC-0001` (ISO/IEC/IEEE 29148:2018), `SRC-0002` (NASA Appendix C), `SRC-0003` (NASA Section 4.2), `SRC-0004` (INCOSE GtWR v4), `SRC-0005` (ISO/IEC/IEEE 12207:2017), `SRC-0006` (ISO/IEC/IEEE 15288:2023).
- **Date:** `2026-11-11`

---

## 1. Domain Problem & Non-Overlap Principle

In multi-agent requirement reviews, overlapping skills create duplicate findings, conflicting severities, and unclear remediation ownership. Specifically, "Completeness", "Coverage", "Consistency", and "Alignment" mean fundamentally different things depending on the unit of analysis:

| Analytical Dimension | Primary Owner Skill | Unit of Analysis | Core Question Answered |
|---|---|---|---|
| **Individual Requirement Statement Quality** | `re.requirement-quality` | Single requirement item ($r_i$) | Is this single requirement well-formed, unambiguous, singular, complete in itself, verifiable, appropriate in abstraction, necessary, correct, and conforming? |
| **Internal Quality of the Requirement Set** | `re.requirement-set-quality` | Requirement collection ($R = \{r_1, \dots, r_n\}$) & declared scope | Is the collection of requirements internally consistent, free of duplicates/contradictions, coherent in dependencies/organization, and complete across declared scope areas? |
| **Alignment with Stakeholder Needs & Objectives** | `re.requirement-validation` | Requirements ($R$) $\leftrightarrow$ Stakeholder Needs / Business Objectives / Policies ($N, O, P$) | Are we specifying the *right requirements* that faithfully and completely satisfy stakeholder needs, business objectives, operational concepts, and authoritative rules without gold-plating? |
| **Structural Traceability Across Artifacts** | `re.requirement-traceability` | Trace links ($L \subseteq A_{up} \times R \times A_{down}$) across artifact layers | Do explicit, valid, symmetric, and evidence-backed forward and backward trace links connect requirements to origins and downstream design/acceptance/test artifacts? |

---

## 2. Explicit Disambiguation of Overlapping Concepts

### 2.1 Four Distinct Meanings of "Completeness / Coverage"
1. **Individual Statement Completeness (`RQ-04` in `re.requirement-quality`):** Does a single requirement statement contain all information needed to understand that single obligation at its level (actor, action, object, condition, performance target, no `TBD`/`TBS`)?
2. **Scope Coverage & Set Completeness (`RSQ-01`, `RSQ-02` in `re.requirement-set-quality`):** Does the requirement set cover all features, actors, operational states, and lifecycle/CRUD/exception counterparts declared in the project/document scope boundary?
3. **Need Coverage (`RVAL-01` in `re.requirement-validation`):** Is every identified stakeholder need, pain point, or business objective addressed by the requirement set with sufficient semantic depth to solve the stakeholder's problem?
4. **Link Coverage (`RTR-01`, `RTR-02` in `re.requirement-traceability`):** Do requirements have explicit backward trace links to origins and forward trace links to downstream decomposition/design/verification elements?

### 2.2 Three Distinct Meanings of "Consistency / Conflict"
1. **Intra-Statement Self-Contradiction (`RQ-03` / `RQ-06` in `re.requirement-quality`):** A single requirement contradicts itself internally.
2. **Internal Set Consistency (`RSQ-03` in `re.requirement-set-quality`):** Requirement $r_i$ and requirement $r_j$ within the requirement set specify incompatible behaviors, thresholds, states, or terminology for the same condition.
3. **Authoritative Source / Stakeholder Alignment (`RVAL-02`, `RVAL-04` in `re.requirement-validation`):** Requirement(s) conflict with stakeholder needs, business objectives, or authoritative business/regulatory policies.
*(Note: Cross-constraint feasibility/trade-off conflicts between competing quality attributes and architectural/budget constraints delegate to `fr.requirement-conflict-analysis`.)*

### 2.3 Validation (`re.requirement-validation`) vs. Traceability (`re.requirement-traceability`)
- **Structural Existence vs. Semantic Sufficiency:**
  - If Requirement `REQ-10` has no link to any Stakeholder Need or Test Case, or points to a non-existent ID `NEED-999`, **`re.requirement-traceability`** owns the finding (`RTR-01`, `RTR-02`, `RTR-04`, `RTR-06`).
  - If `REQ-10` is structurally linked to `NEED-01` ("Allow customers to cancel orders with automatic refund within 24h"), or even if no formal trace matrix exists, and `REQ-10` specifies "Only admins can manually cancel orders without refund", **`re.requirement-validation`** owns the semantic misalignment finding (`RVAL-02`).
  - If a trace matrix claims `REQ-10` traces to `TC-55` ("Verify login password length"), where the linked artifact deals with a completely unrelated topic, **`re.requirement-traceability`** flags the bogus/irrelevant trace link (`RTR-05`).
- **Missing Stakeholder Need vs. Missing Backward Link:**
  - Unaddressed Stakeholder Need `NEED-04` (a stakeholder need that has no requirements fulfilling its intent) is owned by **`re.requirement-validation` (`RVAL-01`)**.
  - A requirement `REQ-22` that lacks a backward trace link in the trace matrix/attributes is owned by **`re.requirement-traceability` (`RTR-01` / `RTR-06`)**. If `REQ-22` also has no identifiable stakeholder/business justification in the domain context (gold-plating), **`re.requirement-validation` (`RVAL-05`)** evaluates whether its existence is justified by stakeholder/system objectives.
