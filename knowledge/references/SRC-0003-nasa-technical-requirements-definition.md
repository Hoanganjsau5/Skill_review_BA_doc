# SRC-0003: NASA Systems Engineering Handbook — Section 4.2 Technical Requirements Definition (Summary Note)

- **Source ID:** `SRC-0003`
- **Title:** NASA Systems Engineering Handbook, Section 4.2: Technical Requirements Definition
- **Version:** `NASA/SP-2016-6105 Rev2` (2016)
- **Authority Level:** `industry-best-practice` (Industry Guidance)
- **Access & Verification Status:** Publicly released US Government engineering handbook; summarized in original wording.

## Key Engineering Guidance Extracted
1. **Requirement Rationale and Need Justification (`Necessary`, `Correct`):**
   - Understanding *why* a requirement exists (its rationale, parent need, or operational concept) is essential to verify whether the requirement is necessary and whether it accurately captures the intended need.
   - Without access to the source need or rationale, a reviewer cannot objectively confirm `Necessary` or `Correct`.
2. **Abstraction Level and Flowdown (`Appropriate`):**
   - Requirements exist in a hierarchy (stakeholder/business, system, subsystem, software/component). A statement appropriate for a low-level component specification may be inappropriate (premature design) in a high-level business requirements document.
3. **Feasibility under Constraints (`Feasible`):**
   - Assessing whether an individual requirement is achievable requires knowledge of technical, environmental, resource, and operational constraints. When constraint context is absent, feasibility can only be flagged if the statement is internally self-contradictory or violates fundamental physical/logical laws.
4. **Requirements Validation & Bidirectional Traceability (`re.requirement-validation`, `re.requirement-traceability`):**
   - Section 4.2 emphasizes validating technical requirements against stakeholder expectations, operational concepts (ConOps), and mission objectives, as well as maintaining bidirectional traceability matrices linking parent needs, technical requirements, design allocations, and verification activities to prevent orphan requirements and unverified capabilities.
