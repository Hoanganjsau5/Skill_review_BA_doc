---
asset_type: skill
skill_id: re.use-case-analysis
name: "Use Case Analysis"
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to: [use-case, use-case-spec]
depends_on: []
sources:
  - { source_id: SRC-0001, version: "2018 (Second edition)", sections: ["Clause 5.2.5", "Clause 6.5"] }
  - { source_id: SRC-0002, version: "NASA/SP-2016-6105 Rev2", sections: ["Appendix C"] }
  - { source_id: SRC-0003, version: "NASA/SP-2016-6105 Rev2 (Section 4.2)", sections: ["Section 4.2"] }
  - { source_id: SRC-0007, version: "Addison-Wesley, 2001 (proposed registration; knowledge from memory/secondary sources)", sections: ["Topic: use case essentials", "Topic: styles/abstraction levels", "Topic: extensions and failure scenarios"] }
last_verified_at: "2026-11-11"
verified_by: "Skill System Architect"
needs_reverification: false
supersedes: null
---

# Skill: Use Case Analysis (`re.use-case-analysis`)

## 1. Purpose
This skill evaluates the quality of **use case specifications as behavioral requirement units**: element completeness, flow readability and step discipline, extension/exception coverage, abstraction-level consistency, intra-package reference integrity, outcome testability, and disclosure of assumptions. Three architectural principles govern it:

1. **Structure serves reviewability, not ceremony.** Numbering, atomization and extension anchoring are required because downstream steps (validation, acceptance criteria, traceability) must be able to address one behavior at a time — not because templates must be filled.
2. **Semantic evaluation over keyword matching.** Detecting "design leakage" or an "undecidable outcome" requires intent-vs-mechanism reasoning per step; naive term blacklists produce false positives against legitimate domain vocabulary and valid business constraints.
3. **Strict ownership boundaries.** Sentence-level wording quality belongs to `re.requirement-quality`; set duplication/scope organization to `re.requirement-set-quality`; matrix-level bidirectional traceability to `re.requirement-traceability`. This skill judges the use case as a unit.

## 2. Scope

### 2.1 In-scope criteria
| Criterion | Name | Evaluation objective |
|---|---|---|
| `UCA-01` | Goal identity & ID discipline | Unique ID and actor-goal name per use case |
| `UCA-02` | Actors & system boundary | Primary/secondary actors enumerated; boundary legible |
| `UCA-03` | Trigger & preconditions | Start condition and entry state declared |
| `UCA-04` | Postconditions & success guarantee | Guaranteed outcomes per actor, incl. failure minimums |
| `UCA-05` | Main flow step discipline | Numbered, atomic, actor↔system steps; explicit loops |
| `UCA-06` | Extension & exception coverage | Anchored branches incl. rejection and no-response paths |
| `UCA-07` | Abstraction-level consistency | No premature design in basic flow; one style level |
| `UCA-08` | Cross-reference integrity | Cited BR/FR IDs resolve inside the supplied package |
| `UCA-09` | Outcome testability | Terminal states decidable without invented metrics |
| `UCA-10` | Explicit assumptions | Uncertainty flagged, never embedded as fact |

> **Anti-Dogma Principle:** qualitative wording ("gửi xác nhận phù hợp" / "sends an appropriate confirmation") is NOT an automatic defect when anchored to a business rule or named artifact; a screen named once as a locator is NOT premature design; a compact flow with a declared summary-level style is assessed against its declared level. Demand decidability and anchoring, not numeric thresholds or field-by-field template completion.

### 2.2 Out of scope (explicit exclusions)
- Ambiguity, vagueness, compound wording of **individual requirement/precondition sentences** → `re.requirement-quality` (RQ-03, RQ-04, RQ-07).
- Duplicate/overlapping use cases **across the set**, scope coverage of the module, set organization → `re.requirement-set-quality` (RSQ).
- RTM completeness, orphan/backward/forward/symmetry trace analysis → `re.requirement-traceability` (RTR-01..RTR-06).
- Whether the goal matches stakeholder needs; gold-plating → `re.requirement-validation` (RVAL).
- Deriving acceptance criteria/test cases from the flows → `re.acceptance-criteria` (planned).
- Diagram syntax (UML use-case diagram correctness) → `modeling-diagrams` domain profiles.

## 3. Skill Boundary and Delegation
| Topic Observed | In this skill? | Delegate to | Current Registry Status |
|---|---|---|---|
| One flow step's wording is ambiguous/compound | No | `re.requirement-quality` (RQ-03/RQ-04) | draft |
| Two UCs in the set clearly duplicate each other; module scope drift | No | `re.requirement-set-quality` | draft |
| Full bidirectional trace matrix gaps; orphans | No | `re.requirement-traceability` | draft |
| UC outcome vs stakeholder need mismatch | No | `re.requirement-validation` | draft |
| Missing extension for payment no-response; UC element gaps; design leakage | **Yes** | — | — |

> Never declare a hard dependency (`depends_on`) on a `planned` Skill; delegation is recorded as recommendation. `depends_on: []` here is intentional even though delegation exists.

## 4. Prerequisites & Multi-Artifact Handling

### 4.1 Supported representations
- Structured use-case spec tables (fields: ID, actors, trigger, pre/post, main flow, extensions) in Word/Markdown/Excel exports.
- Narrative (expanded-cockburn or numbered-steps prose) use cases.
- Use-case index/summary lists (assessed only for UCA-01/UCA-06 level declaration).
- Tool reports: if an adapter cannot parse the representation, report the gap in `review-result.limitations`; **never fabricate parsed fields**.

### 4.2 Handling principles
- **Separation of Parsing and Evaluation** — as above; missing adapter ⇒ limitation, not Issue.
- **Granularity & Boundary Integrity** — evaluate the use-case units as the author segmented them; do not invent splits or merge UCs to be "helpful".
- **Preservation of Original Text** — every Evidence carries the exact excerpt plus ArtifactLocation (artifact_path, element_id such as `UC-003/step 5`, section, line_range).
- **Two-sided rules** (`UCA-R005`, `UCA-R006`) additionally require the comparison corpus (ID index / convention source) in the package; without it the related criterion is Not Assessable, never a confirmed Issue.

## 5. Multi-Language Architecture
Core criteria are language-independent. Language signals (`en`, `vi` packs concept reused from `re.requirement-quality` §5): step-style checks ("System thực hiện…", "the system shall…") are heuristics only; actor attribution is judged semantically regardless of language. A use-case spec mixing Vietnamese narrative with English identifiers (`mã giảm giá`, `BR-07`) is normal and never a finding. Unknown language ⇒ limitation note + language-independent structural checks only.

## 6. Criterion Context Requirements & Assessability Model
| Criterion | Minimum info | Optional context | Assessable from record alone? | When Not Assessable | When Not Applicable |
|---|---|---|---|---|---|
| UCA-01 | ID + name fields | ID convention doc | Yes | header absent from fragment | — |
| UCA-02 | Flow with step subjects | module scope list | Yes | unattributed single paragraph | — |
| UCA-03 | Header/flow start | related UCs | Yes | entry state not inferable from supplied fragment | declared outline |
| UCA-04 | Final steps or Postconditions | BRs | Yes | flow truncated | — |
| UCA-05 | Main flow text | extensions | Yes | main flow not supplied | declared summary level |
| UCA-06 | Main flow + extensions section | BRs | Yes | neither supplied | abstract UC declared flow-less |
| UCA-07 | Main flow text | glossary | Yes | terms ambiguous without glossary | — |
| UCA-08 | Citations + ID index | RTM extract | **No — needs index** | index absent/partial | UC cites no IDs by project practice |
| UCA-09 | Outcome statements | anchors | Yes | outcomes deferred to unsupplied doc | — |
| UCA-10 | Flow + assumptions section | meeting notes | Partly | cannot tell assumption vs fact | — |

## 7. Criterion Status and Finding Mapping
### 7.1 Statuses
`Compliant` / `Issue` / `Not Assessable` / `Not Applicable` — same semantics as `re.requirement-quality` §7.1; Not Applicable is never granted merely because evaluation is hard.

### 7.2 Mapping
| Situation | Finding type | Severity/confidence |
|---|---|---|
| Issue with full context (e.g. unresolved BR id + index) | `confirmed-issue` | major / high |
| Issue depending on inferred intent (e.g. design leakage) | `potential-issue` | medium confidence, severity per criterion hint |
| Structural nit / deferral note (e.g. extension numbering) | `improvement-suggestion` | minor |
| Material Not Assessable blocking execution understanding (e.g. no flow at all for an implementation sprint) | consolidated `needs-clarification` Finding (one per artifact) | — |
| Compliant / Not Applicable | no Finding | — |

### 7.3 Output contract
Findings carry `basis: { type: criterion, criterion_ref: { owner_type: skill, owner_id: re.use-case-analysis, owner_version: 0.1.0, item_id: UCA-xx } }`, category ∈ {completeness, consistency, structure, testability}, rule IDs in rationale, and — for comparison rules — ≥2 evidence items quoting both sides. Unresolved external docs go to `clarification_requests[]`; parsing/representation gaps to `limitations[]`.

## 8. Knowledge & Principles
1. **Essentials over template literalism** (SRC-0007 topics): an element may live inside flow prose and still count as present.
2. **Extensions are the requirement's immune system** (SRC-0007 topic): coverage is judged per risk class (input, decision, external call), with third-party no-response treated as foreseeable.
3. **Valid constraint vs premature design** (SRC-0003 §4.2, reused from `re.requirement-quality` principle set): business-perspective concreteness is fine; internal mechanism narration is not.
4. **Qualitative-but-anchored outcomes pass verifiability** (SRC-0001 Clause 5.2.5 conceptual, SRC-0002 heuristics): no invented metrics.
5. **No project-decision authority** (`skills/_template` rule): naming formats enforced only against a supplied convention or the corpus's dominant pattern (then improvement-suggestion only).
6. **Never invent actors, UCs, or missing content** — local-pack guard carried into findings discipline: suggestions are labeled, evidence is quoted.

## 9. Authoritative References
| source_id | Title | Version | authority_level | Verification / Access Note |
|---|---|---|---|---|
| SRC-0001 | ISO/IEC/IEEE 29148:2018 | 2018 | official-standard | Conceptual level only, as worded in source-registry (Clauses 5.2.5, 6.5; no verbatim claims). |
| SRC-0002 | NASA SE Handbook App. C | SP-2016-6105 Rev2 | industry-best-practice | Public; heuristics applied to flow steps. |
| SRC-0003 | NASA SE Handbook §4.2 | SP-2016-6105 Rev2 | industry-best-practice | Public; abstraction/valid-constraint guidance. |
| SRC-0007 | A. Cockburn, *Writing Effective Use Cases* | Addison-Wesley 2001 — **proposed, not yet in source-registry** | industry-best-practice | Knowledge from memory/secondary sources; full text not held; cited at topic level ("essentials", "styles levels", "extensions") — **no page or clause numbers claimed**. See RN-0003 §5. |

See Research Note: [`../../../knowledge/research-notes/RN-0003-use-case-analysis.md`](../../../knowledge/research-notes/RN-0003-use-case-analysis.md).

## 10. Review Procedure
1. **Inspect context & declare representation level** — parse fields/flows; note limitations for unparsable packages; detect each artifact's declared style level (summary vs user-goal).
2. **Segment use-case units** — preserve author segmentation; enumerate UCs for UCA-01/UCA-06 inventory.
3. **Identify language(s)** per record (en/vi/mixed) — structural checks proceed regardless.
4. **Run element inventory (UCA-R001)** → UCA-01..04, 06 gates; apply §6 Not Assessable / Not Applicable gates before any Issue.
5. **Evaluate flows** — UCA-R002 (steps), UCA-R003 (extensions), UCA-R004 (abstraction), then UCA-09 testability of terminal outcomes and UCA-10 disclosure.
6. **Two-sided integrity** — UCA-R005/R006 only when index/convention supplied; ≥2 evidence items per finding.
7. **Anti-false-positive pass** — re-read each candidate Issue asking: is the flagged item domain vocabulary/valid constraint/author-declared level? Is the wording complaint actually RQ territory? Reclassify or delegate accordingly.
8. **Map statuses → findings/clarifications** (§7), list delegations, and emit `review-result`.

## 11. Evaluation Assets
- Criteria definitions: [`criteria.yaml`](criteria.yaml) — UCA-01..UCA-10.
- Operational rules: [`rules.yaml`](rules.yaml) — UCA-R001..UCA-R006.
- Review checklist (Vietnamese): [`checklist.md`](checklist.md).
- Examples & Golden Tests: [`examples/`](examples/README.md).

## 12. Expected Output
A standard `review-result` (schemas/runtime/review-result.schema.json) with per-criterion statuses recorded via findings/rationales, `clarification_requests[]` for unsupplied comparison corpora, `early_feasibility_signals` untouched (feasibility belongs elsewhere), and `limitations[]` for representation/language gaps. No `criterion_evaluations[]` array exists in the current schema — statuses are expressed through the finding mapping in §7.

## 13. Limitations & Documented Schema Gaps
- SRC-0007 is **proposed** and unregistered; registry edit and An's ruling are pending (see delivery report). Until registered, SKILL frontmatter cites it ahead of the shared registry — deliberate draft-status disclosure.
- 29148 use-case-specific clauses are intentionally NOT cited (paywalled; not verified at clause level) — only the already-registered conceptual anchors.
- `criterion.schema.json` / `analysis-rule.schema.json` are `additionalProperties: false`; extended metadata is kept inside `synthesis_note` / `method` block strings, matching `re.requirement-traceability` practice.
- Validation status of every criterion/rule is `unvalidated` until Golden Tests are executed by the runtime (ADR-0004); the runtime is not yet present in this repo generation.
