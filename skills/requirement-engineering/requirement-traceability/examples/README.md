# Examples & Golden Test Cases — `re.requirement-traceability`

This directory contains generic, project-independent synthetic examples and structured Golden Test Cases (`RTR-GTC-01` .. `RTR-GTC-10`) used for static and behavioral validation of `re.requirement-traceability`.

## Files
- [`synthetic-examples.md`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-traceability/examples/synthetic-examples.md): Human-readable walkthroughs of backward/forward link gaps, bidirectional asymmetry, broken/deprecated target IDs, bogus copy-paste links, cross-layer orphans, and boundary distinctions.
- [`golden-test-cases.yaml`](file:///c:/Users/Owner/Downloads/Skill_Review/skills/requirement-engineering/requirement-traceability/examples/golden-test-cases.yaml): 10 machine-readable Golden Test Cases covering:
  - `RTR-GTC-01`: Missing backward origin link (`RTR-01`) and missing forward test/decomposition links (`RTR-02`).
  - `RTR-GTC-02`: Bidirectional symmetry mismatch between SRS and Test Suite in Vietnamese (`RTR-03` / `RTR-R004`).
  - `RTR-GTC-03`: Broken non-existent target ID, link to a `Deprecated` Stakeholder Need, and duplicate ID collision (`RTR-04` / `RTR-R005`, `RTR-R006`, `RTR-R007`).
  - `RTR-GTC-04`: Bogus topically irrelevant trace link and incompatible verification method link (`RTR-05` / `RTR-R008`, `RTR-R009`).
  - `RTR-GTC-05`: Cross-layer orphan requirement omitted from RTM and unallocated Test Case lacking parent requirement (`RTR-06` / `RTR-R010`).
  - `RTR-GTC-06`: Missing Trace Context Safeguard (`Not Assessable` across `RTR-01`..`RTR-06` when only raw requirement prose is supplied without trace attributes or RTM).
  - `RTR-GTC-07`: External Unprovided Target Inventory Safeguard (`RTR-01`, `RTR-02` `Compliant`, while `RTR-04`, `RTR-05` `Not Assessable` when RTM references an external Test Suite file not included in the review package).
  - `RTR-GTC-08`: Early-Phase Lifecycle Gate (`RTR-02` forward links to Design/Test marked `Not Applicable` during early BRD-to-SRS trace review).
  - `RTR-GTC-09`: Well-formed, complete, symmetric, evidence-backed bidirectional traceability matrix (`Compliant` across `RTR-01`..`RTR-06`).
  - `RTR-GTC-10`: Strict Ownership Boundary — Semantic stakeholder intent distortion when trace links are structurally valid belongs to `re.requirement-validation`, NOT `re.requirement-traceability`.
