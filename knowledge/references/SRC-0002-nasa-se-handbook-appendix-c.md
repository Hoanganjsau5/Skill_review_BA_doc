# SRC-0002: NASA Systems Engineering Handbook — Appendix C (Summary Note)

- **Source ID:** `SRC-0002`
- **Title:** NASA Systems Engineering Handbook, Appendix C: How to Write a Good Requirement
- **Version:** `NASA/SP-2016-6105 Rev2` (2016)
- **Authority Level:** `industry-best-practice` (Industry Guidance — NOT a mandatory ISO clause)
- **Access & Verification Status:** Publicly released US Government engineering handbook; summarized in original wording.

## Key Engineering Guidance Extracted
1. **Editorial and Linguistic Signals (Heuristics, Not Automatic Defects):**
   - Vague adjectives/adverbs (e.g., "minimal", "maximize", "flexible", "easy", "sufficient", "adequate", "user-friendly") often obscure verification criteria unless defined in accompanying context or glossary.
   - Open-ended clauses (e.g., "etc.", "and so on", "as a minimum", "including but not limited to") leave the scope of obligation unbounded.
   - Ambiguous combinators ("and/or") obscure whether satisfaction requires conjunction, disjunction, or both.
2. **Singularity and Compound Obligations:**
   - Bundling multiple independent actions or capabilities into a single statement complicates verification tracking and partial exception handling.
   - However, a single state transition or condition-action pair that requires two tightly coupled attributes to describe one atomic behavior is not necessarily a singularity defect.
3. **Implementation Bias vs. Legitimate Constraints:**
   - Requirements should state *what* is needed rather than *how* to design it, **except** when an interface, regulatory, operational, or architectural constraint is intentionally imposed by a higher-level decision.
4. **Verification Alignment:**
   - Every requirement should permit objective verification (test, demonstration, analysis, or inspection), which does not always require a numeric metric (e.g., deterministic state transitions or format compliance can be verified by test/inspection without numeric thresholds).
