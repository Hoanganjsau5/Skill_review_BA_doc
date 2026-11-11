# SRC-0004: INCOSE Guide to Writing Requirements v4 (Summary Note)

- **Source ID:** `SRC-0004`
- **Title:** INCOSE Guide to Writing Requirements (GtWR)
- **Version:** `Version 4 (INCOSE-TP-2010-006-04)` (July 2023)
- **Authority Level:** `industry-best-practice` (Industry Guidance — NOT a mandatory ISO clause)
- **Access & Verification Status:** Secondary-source and official INCOSE Version 4 summary sheet verification only. Full copyrighted text is not stored in this repository.

## Key Engineering Guidance Extracted
1. **Individual Requirement Characteristics vs. Set Characteristics:**
   - GtWR v4 reinforces the separation between characteristics of an *individual requirement statement* (Necessary, Appropriate, Unambiguous, Complete, Singular, Feasible, Verifiable, Correct, Conforming) and characteristics of a *set of requirements*.
2. **Context-Sensitive Linguistic Heuristics:**
   - Pronouns with unclear antecedents ("it", "they", "this", "that") create referential ambiguity when multiple nouns precede them.
   - Escape clauses ("if possible", "when appropriate", "where practical", "as required") weaken testability and completeness unless bounded by explicit conditions.
   - Unbounded performance/temporal terms ("real-time", "instantaneously", "immediately", "fast") require contextual bounds or measurable ranges for performance requirements, whereas functional ordering ("immediately transition to state Locked") may denote event sequencing rather than latency.
3. **Conforming vs. Universal Style Dogma:**
   - Conformity evaluates adherence to the *project's* chosen requirement patterns, glossary, and attribute schema (whether traditional `shall` statements, EARS patterns, User Stories, or tabular specifications), not a single mandatory English phrasing.
4. **Characteristics of a Set of Requirements (`re.requirement-set-quality`):**
   - GtWR v4 defines specific characteristics for a *set* of requirements: **Complete** (covers all scope dimensions, operational modes, and interfaces without gaps), **Consistent** (free of contradictions, overlapping/duplicate statements, and inconsistent terminology/units across items), **Comprehensible** (logically organized, classified, and structured so dependencies and hierarchy are clear), and **Able to be Validated** (supports validation against stakeholder needs).
