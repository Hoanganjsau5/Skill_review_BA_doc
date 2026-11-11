# Examples & Golden Test Cases — `re.requirement-set-quality`

This directory contains generic, project-independent synthetic examples and structured Golden Test Cases (`RSQ-GTC-01` .. `RSQ-GTC-10`) used for static and behavioral validation of `re.requirement-set-quality`.

## Files
- [`synthetic-examples.md`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-set-quality/examples/synthetic-examples.md): Human-readable walkthroughs of set-level defects, pass cases, missing-context cases, and boundary distinctions across English and Vietnamese requirement sets.
- [`golden-test-cases.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-set-quality/examples/golden-test-cases.yaml): 10 machine-readable Golden Test Cases covering:
  - `RSQ-GTC-01`: Scope Coverage gap (`RSQ-01` / `RSQ-R001`) — In-scope actor/module omitted from full requirement set.
  - `RSQ-GTC-02`: Missing companion lifecycle transition (`RSQ-02` / `RSQ-R002`) — Account lock state introduced with no unlock/expiry requirement (Vietnamese SRS).
  - `RSQ-GTC-03`: Internal behavioral & numeric threshold contradiction (`RSQ-03` / `RSQ-R004`, `RSQ-R005`) — Conflicting cancellation windows and fee rules across sections.
  - `RSQ-GTC-04`: Paraphrased semantic duplication & partial overlap (`RSQ-04` / `RSQ-R007`, `RSQ-R008`) — Duplicate audit logging requirements across User Stories.
  - `RSQ-GTC-05`: Circular precondition deadlock & broken internal reference (`RSQ-05` / `RSQ-R009`).
  - `RSQ-GTC-06`: Missing context / partial slice safeguard (`RSQ-01`, `RSQ-02` -> `not_assessable`) — Prevents false positives when reviewing a partial module extract.
  - `RSQ-GTC-07`: False-positive prevention — General rule with explicit exception cross-reference and tier-specific limits (`PASS` on `RSQ-03`).
  - `RSQ-GTC-08`: Well-formed, consistent, complete requirement set (`PASS` across `RSQ-01` .. `RSQ-06`).
  - `RSQ-GTC-09`: Set organization & misclassification defect (`RSQ-06` / `RSQ-R010`) — Global encryption/availability NFRs buried inside a UI feature list.
  - `RSQ-GTC-10`: Strict ownership boundary check — Single-statement ambiguity (`re.requirement-quality`), stakeholder intent mismatch (`re.requirement-validation`), and missing test trace link (`re.requirement-traceability`) excluded from `re.requirement-set-quality`.
