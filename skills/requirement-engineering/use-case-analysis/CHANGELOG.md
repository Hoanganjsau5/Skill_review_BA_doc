# Changelog — `re.use-case-analysis`

## [0.1.0] - 2026-11-11
- **Status:** `draft`
- **Added:**
  - Initial design for `re.use-case-analysis` (transitions the entry `planned → draft` in `skills/SKILL_REGISTRY.yaml` — registry edit intentionally NOT performed in this change; see delivery report).
  - Defined 10 core criteria (`UCA-01`..`UCA-10`) covering use-case element completeness, actor/boundary, trigger/preconditions, postconditions/success guarantee, main-flow step discipline, extension/exception coverage, abstraction-level consistency, cross-reference integrity, outcome testability, and explicit assumption disclosure — grounded in SRC-0001/SRC-0002/SRC-0003 conceptual anchors and the proposed SRC-0007 (Cockburn, topic-level only).
  - Defined 6 operational rules (`UCA-R001`..`UCA-R006`) supporting both `artifact-reviewer` (single use-case) and `cross-artifact-analyzer` (comparison rules `UCA-R005`/`UCA-R006` requiring ≥2 evidence items per finding schema).
  - Adapted the team local-pack rubric (`agents/.agents/skills/use-case-analysis/SKILL.md`) into non-interactive assessment criteria; retained its no-fabrication and PROPOSED-labeling guards.
  - Added Vietnamese `checklist.md`, `examples/synthetic-examples.md`, and 7 Golden Test Cases (`UCA-GTC-01`..`UCA-GTC-07`) including a Vietnamese-language case, a Not-Assessable gate case, false-positive-prevention cases, and boundary-delegation cases toward `re.requirement-quality` / `re.requirement-set-quality`.
  - Established strict ownership boundaries: individual wording → `re.requirement-quality`; set duplication/scope → `re.requirement-set-quality`; bidirectional matrices → `re.requirement-traceability` (delegation only; no hard `depends_on`).
  - Research note `knowledge/research-notes/RN-0003-use-case-analysis.md` added, including the honest-access section for the proposed SRC-0007.
