# Changelog — `re.acceptance-criteria`

## [0.1.0] - 2026-11-11

- Status: `draft` (no runtime adapter exists; all validations `unvalidated`).
- Added: initial design — 10 criteria (`ACA-01`..`ACA-10`) for Acceptance Criteria suite review at AC-suite granularity: verifiable/observable outcomes, Given/When/Then well-formedness, atomicity, bidirectional AC–owner anchoring, negative/edge-path presence, no-creep/no-design-lock-in, AC identity conventions, unambiguous wording, AC duplication/contradiction, stated demonstration. Grounded in SRC-0001 (Clauses 5.2.5/5.2.6/6.4/6.5, conceptual), SRC-0002/SRC-0003 (NASA heuristics), SRC-0004 (set characteristics), and proposed SRC-0008 (Bill Wake, INVEST) / SRC-0009 (Dan North BDD + Gherkin) — the latter two pending registration in `knowledge/source-registry.yaml`, honest memory/secondary basis recorded in RN-0004 §5.
- Added: 10 operational rules (`ACA-R001`..`ACA-R010`) with explicit false-positive gates (facet-And allowance, competing-interpretation requirement, declared-failure-mode-only enumeration, obligation-diff exemptions), supporting both `cross-artifact-analyzer` (set comparisons) and `artifact-reviewer` (per-item wording).
- Added: team/vendor material adaptation — quality rows from `business-requirement-analysis` and ID/section rules from `ba-documentation` (team `agents/.agents/skills/`), and the GWT/data-oracle/failure-path patterns from the cloned vendor research pack `yihannangua_prd-review-skill` (references `business-rule-checklist.md`, `requirement-quality-checklist.md`) converted from interactive authoring prompts into declarative review checks; provenance recorded in `origin_note` fields (these packs are not registered sources).
- Added: `checklist.md` (Vietnamese, template table format), `examples/golden-test-cases.yaml` (10 cases incl. vi, Not Assessable safeguard, false-positive prevention, Not Applicable by declared format, and a strict-boundary delegation case), `examples/synthetic-examples.md` (EX-01..EX-10), `examples/README.md`.
- Added: research note `knowledge/research-notes/RN-0004-acceptance-criteria.md`.
- Boundaries: strict ownership separation from siblings — individual requirement statement wording → `re.requirement-quality`; requirement-set scope/companion gaps → `re.requirement-set-quality`; RTM link structure → `re.requirement-traceability`; needs validation/gold-plating → `re.requirement-validation`; test engineering → `qa.*` (planned). `depends_on` intentionally empty (planned skills are never dependencies).

### Sources verified

- SRC-0001 (2018 Second edition) — conceptual-level reference only; verified by Skill System Architect at 2026-11-11.
- SRC-0002 (NASA/SP-2016-6105 Rev2) — verified by Skill System Architect at 2026-11-11.
- SRC-0003 (NASA/SP-2016-6105 Rev2, Section 4.2) — verified by Skill System Architect at 2026-11-11.
- SRC-0004 (INCOSE-TP-2010-006-04 v4) — paraphrase-level, verified by Skill System Architect at 2026-11-11.
- SRC-0008 / SRC-0009 — **proposed, not yet registered**; memory/secondary basis; uncertainties documented in RN-0004 §5 pending An's registration approval.
