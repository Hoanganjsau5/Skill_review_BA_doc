# Review Checklist — Skill: `re.requirement-traceability`

Use this checklist when executing `re.requirement-traceability` (`v0.1.0`) to evaluate structural traceability relationships across requirements and related lifecycle artifacts.

## 0. Pre-Assessment Trace Model & Artifact Gate
- [ ] **Identify Trace Representation:** Is traceability recorded in a standalone RTM (`rtm`), inline requirement attributes (`source_id`, `parent_id`, `uc_id`, `design_id`, `test_id`), or embedded cross-reference tables?
  - *If zero trace representations or multi-layer artifacts are provided:* Mark `RTR-01` .. `RTR-06` as `not_assessable`.
- [ ] **Identify Lifecycle Phase & Expected Trace Layers (`declared_trace_model`):**
  - Do NOT flag missing Design or Test links (`RTR-02`) if Design/Test artifacts are outside the current lifecycle phase (`not_applicable`).
  - If an RTM references external IDs in an artifact file that was not uploaded in the review package, mark target existence (`RTR-04`) and topical relevance (`RTR-05`) for that unprovided file as `not_assessable` (Observation).
- [ ] **Enforce Skill Boundaries:**
  - Do NOT evaluate single-statement wording ambiguity or testability (`re.requirement-quality`).
  - Do NOT evaluate horizontal precondition dependencies among peer requirements in the same set (`re.requirement-set-quality` `RSQ-05`).
  - Do NOT evaluate deep semantic stakeholder intent alignment when trace links are present and topically relevant (`re.requirement-validation` `RVAL-02`).

## 1. Backward Traceability Coverage (`RTR-01` / `RTR-R001`)
- [ ] Does every active requirement have $\ge 1$ explicit backward trace link to an upstream origin (Business Objective, Stakeholder Need, Parent Requirement, or Regulatory Clause)?

## 2. Forward Traceability Coverage (`RTR-02` / `RTR-R002`, `RTR-R003`)
- [ ] Does every active requirement have $\ge 1$ explicit forward trace link to each downstream layer required by the current lifecycle phase (Child Requirements, Use Cases/User Stories/Acceptance Criteria, Design Elements, Test Cases)?
- [ ] Where hierarchical requirement levels exist (e.g., System Requirements $\to$ Software Requirements, Epics $\to$ User Stories), are parent-child decomposition links complete?

## 3. Bidirectional Traceability Symmetry (`RTR-03` / `RTR-R004`)
- [ ] Where links are recorded in both forward and backward directions across tables or artifacts, does $(u \to d)$ always match $(d \to u)$ symmetrically?

## 4. Reference & Identifier Integrity (`RTR-04` / `RTR-R005`, `RTR-R006`, `RTR-R007`)
- [ ] Does every referenced source and target ID resolve to an existing item in the target artifact inventory (no broken/dangling IDs)?
- [ ] Are all referenced upstream and downstream items in an active state (not `Deprecated`, `Deleted`, `Withdrawn`, or `Rejected`)?
- [ ] Are all traceable item IDs globally unique within their namespace (no duplicate ID collisions)?

## 5. Relationship Relevance & Evidence Support (`RTR-05` / `RTR-R008`, `RTR-R009`)
- [ ] Do the linked source and target items actually address the same capability, entity, or constraint (no bogus copy-paste ID pairings)?
- [ ] Does the linked verification/test item match the requirement's declared verification method (`Inspection`, `Analysis`, `Demonstration`, `Test`)?

## 6. Orphan & Unallocated Element Freedom (`RTR-06` / `RTR-R010`)
- [ ] Are all requirements defined in the specification included in the RTM / trace graph (no cross-layer orphan requirements)?
- [ ] Does every active Use Case, Design Component, and Test Case in scope trace back to at least one requirement (no unallocated downstream artifacts)?
