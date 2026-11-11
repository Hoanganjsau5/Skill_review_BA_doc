# Changelog — `re.requirement-validation`

## [0.1.0] - 2026-11-11
- **Status:** `draft`
- **Added:**
  - Initial design and implementation of `re.requirement-validation` within the `requirement-engineering` domain.
  - Defined 6 core evaluation criteria (`RVAL-01` .. `RVAL-06`) grounded in ISO/IEC/IEEE 29148:2018 Clause 6.4, ISO/IEC/IEEE 12207:2017 Clauses 6.4.2 & 6.4.11, ISO/IEC/IEEE 15288:2023, NASA SP-2016-6105 Rev2 Section 4.2, and INCOSE GtWR v4.
  - Defined 10 operational evaluation rules (`RVAL-R001` .. `RVAL-R010`) supporting both `cross-artifact-analyzer` and `artifact-reviewer`.
  - Added `checklist.md`, `examples/synthetic-examples.md`, and 10 Golden Test Cases (`RVAL-GTC-01` .. `RVAL-GTC-10`) in `examples/golden-test-cases.yaml`.
  - Established strict ownership boundaries separating semantic validation (`re.requirement-validation`) from structural traceability (`re.requirement-traceability`), internal set quality (`re.requirement-set-quality`), and individual requirement quality (`re.requirement-quality`).
