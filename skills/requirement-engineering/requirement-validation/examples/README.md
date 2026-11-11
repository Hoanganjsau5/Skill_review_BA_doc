# Examples & Golden Test Cases — `re.requirement-validation`

This directory contains generic, project-independent synthetic examples and structured Golden Test Cases (`RVAL-GTC-01` .. `RVAL-GTC-10`) used for static and behavioral validation of `re.requirement-validation`.

## Files
- [`synthetic-examples.md`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-validation/examples/synthetic-examples.md): Human-readable walkthroughs of stakeholder need coverage gaps, intent distortion, business objective conflicts, policy violations, gold-plating, ConOps mismatches, and boundary distinctions.
- [`golden-test-cases.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-validation/examples/golden-test-cases.yaml): 10 machine-readable Golden Test Cases covering:
  - `RVAL-GTC-01`: Unaddressed & partially addressed Stakeholder Needs (`RVAL-01` / `RVAL-R001`, `RVAL-R002`).
  - `RVAL-GTC-02`: Stakeholder Intent Distortion & Priority Inversion in Vietnamese (`RVAL-02` / `RVAL-R003`, `RVAL-R004`).
  - `RVAL-GTC-03`: Business Objective & KPI Misalignment (`RVAL-03` / `RVAL-R005`, `RVAL-R006`).
  - `RVAL-GTC-04`: Authoritative Business Rule & Regulatory Policy Violation (`RVAL-04` / `RVAL-R007`).
  - `RVAL-GTC-05`: Unjustified Requirement / Gold-Plating Detection (`RVAL-05` / `RVAL-R008`).
  - `RVAL-GTC-06`: Missing Upstream Baseline Safeguard (`Not Assessable` across `RVAL-01` .. `RVAL-06` when only an SRS is provided without upstream needs/objectives/policies).
  - `RVAL-GTC-07`: False-Positive Prevention — Essential security/audit enabling requirements are NOT flagged as gold-plating (`Compliant` on `RVAL-05`).
  - `RVAL-GTC-08`: Operational Concept (ConOps) Environmental Mismatch (`RVAL-06` / `RVAL-R009`) — Requiring continuous online sync in an offline field-inspection ConOps.
  - `RVAL-GTC-09`: Stakeholder Acceptance Criteria Deficit (`RVAL-06` / `RVAL-R010`).
  - `RVAL-GTC-10`: Strict Ownership Boundary — Structural trace link omission (`re.requirement-traceability`) vs Semantic Need Coverage (`re.requirement-validation`).
