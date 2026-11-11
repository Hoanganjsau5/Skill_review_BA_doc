---
asset_type: skill
skill_id: re.srs-review
name: SRS Structural Review
domain: requirement-engineering
version: 0.1.0
status: draft
applies_to:
  - srs
  - system-requirement-spec
depends_on: []
sources:
  - source_id: SRC-0010
    version: "IEEE Std 830-1998 (superseded; recalled at outline level only — proposed registration)"
    sections: ["Recommended SRS outline — 1 Introduction / 2 Overall Description / 3 Specific Requirements + Appendices"]
  - source_id: SRC-0011
    version: "3rd edition (2010) — proposed registration, memory-based"
    sections: ["SRS content elements", "Practical SRS review guidance"]
  - source_id: SRC-0001
    version: "2018 (Second edition)"
    sections: ["Clause 5.2.5", "Clause 5.2.6"]
  - source_id: SRC-0002
    version: "NASA/SP-2016-6105 Rev2"
    sections: ["Appendix C"]
  - source_id: SRC-0003
    version: "NASA/SP-2016-6105 Rev2 (Section 4.2)"
    sections: ["Section 4.2"]
  - source_id: SRC-0005
    version: "2017 (First edition)"
    sections: ["Clause 6.4.3"]
last_verified_at: "2026-11-11"
verified_by: null
needs_reverification: false
supersedes: null
---

# Skill: `re.srs-review` (SRS Structural Review)

## 1. Purpose & Responsibility Boundary

### 1.1 Purpose
`re.srs-review` evaluates the **SRS as a document**: whether its whole-document STRUCTURE and completeness hold — required sections present and non-empty, document-control front matter and revision history, TOC/heading/internal-reference integrity, a structural home for every mandated requirement class (external interfaces, NFRs, features, data), feature-to-section allocation and declared ID-scheme uniformity, a resolvable reference/footnote/appendix apparatus, freedom from whole-section placeholders, and section-level abstraction discipline.

This is the owner explicitly assigned by `re.requirement-quality`'s delegation table (`skills/requirement-engineering/requirement-quality/SKILL.md` §3: "Overall SRS structure, missing document sections") and by `SKILL_REGISTRY.yaml` (`re.srs-review` — "Planned artifact-specific structural composite").

> **Clarification of the delegation-table wording:** where `re.requirement-quality` mentions "set-level completeness" alongside SRS structure, **requirement-SET completeness stays owned by `re.requirement-set-quality`** (`RSQ-01`/`RSQ-02` — features, actors, lifecycle companions inside a requirement collection). `re.srs-review` owns **document-section** completeness only.

The outline baseline used by this Skill is the project's adopted SRS template; when none is supplied, it falls back to the recognized standard outline — the chapter taxonomy of **IEEE Std 830-1998** (`SRC-0010`, *proposed* registration; superseded by ISO/IEC/IEEE 29148:2018 `SRC-0001`, recalled here at chapter/section-name level only, with no sub-clause text quoted).

### 1.2 Primary Ownership vs. Neighboring Skills (Strict Non-Overlap)

| Concern / Issue Type | Primary Owner | Why / Boundary Rule |
|---|---|---|
| Wording, ambiguity, completeness, singularity, verifiability, abstraction **inside one requirement statement** ($r_i$) | `re.requirement-quality` | `RQ-01`..`RQ-09` operate per statement. A clean document skeleton can still contain bad statements — `re.srs-review` never re-flags them. |
| Requirement-**set** properties: scope coverage by requirements, companion/lifecycle gaps, contradictions $r_i \times r_j$, duplication, intra-set references, classification mixing | `re.requirement-set-quality` | `RSQ-01`..`RSQ-06` judge the collection of requirements, not the document. `re.srs-review` judges sections/TOC/references — structure that exists even before requirement semantics. |
| Alignment of requirements with stakeholder needs, objectives, policies; gold-plating | `re.requirement-validation` | `RVAL-01`..`RVAL-06` compare content against upstream sources; no structural section authority. |
| Cross-layer trace links (`NEED ↔ REQ ↔ DESIGN ↔ TEST`), RTM integrity, orphan trace items, **requirement-ID collisions as trace endpoints** | `re.requirement-traceability` | `RTR-01`..`RTR-06`. `re.srs-review` checks the document's own declared ID **scheme** usage and intra-document references only. |
| **Document skeleton: required sections present & non-empty; front matter & revision history; TOC/heading/internal-reference integrity; interface/NFR/feature/data structural homes; feature-list ↔ section allocation; referenced-documents/footnotes/appendices resolution; whole-section placeholders; section-level design leakage** | **`re.srs-review` (THIS SKILL)** | Properties of the SRS **as a document**, assessable from its structure and reference apparatus. |
| Quality of a referenced external document (an ICD, the ERD itself, a policy doc's content) | That document's own review under the matching skill | `re.srs-review` only checks that the reference **resolves** (exists / is catalogued). |
| Correctness of diagrams (ERD/UML content) | `md.erd`, `md.uml` (Planned) | This skill checks a data-description section/reference **exists**, not diagram semantics. |
| Use Case flow depth; Acceptance Criteria suites | `re.use-case-analysis`, `re.acceptance-criteria` (Planned) | Delegation table §3. |

---

## 2. Core Evaluation Criteria (`SRV-01` .. `SRV-08`)

All criteria are defined in [`criteria.yaml`](criteria.yaml):

1. **`SRV-01` — Required Section Presence & Non-Emptiness:** every mandated top-level/second-level section of the adopted outline (Introduction incl. Purpose & Scope; Overall Description incl. product perspective, functions, user characteristics, constraints, assumptions/dependencies; Specific Requirements) exists with substantive content.
2. **`SRV-02` — Document-Control Front Matter & Revision History:** document identifier, version designation, and revision history present and internally agreeing with the declared version.
3. **`SRV-03` — TOC, Heading & Internal Cross-Reference Integrity:** TOC matches actual headings, numbering sequential, every internal "see Section x.y" resolves to a matching element.
4. **`SRV-04` — Interface, NFR, Feature & Data Section Coverage:** each mandated requirement class (external interfaces — user/hardware/software/communications; non-functional; system features; data description) has a structural home or an explicit tailoring declaration.
5. **`SRV-05` — Feature Allocation & Identifier-Scheme Consistency:** declared feature overview ↔ feature sections map bidirectionally; the document's own declared requirement-ID scheme (e.g., `FR-nn`) is used, well-formed, and uniform across all sections.
6. **`SRV-06` — Referenced Documents, Footnotes & Appendix Resolution:** every normatively used References-list entry resolves in the review corpus (two-artifact evidence); every body-invoked appendix exists.
7. **`SRV-07` — Placeholder & Unresolved Section Freedom:** no whole-section `TBD`/template-scaffolding bodies without a registered deferral; no announced-but-empty figure/table slots.
8. **`SRV-08` — Section-Level Abstraction Discipline:** requirement-role sections do not contain normative design/implementation regions (whole-subsection schema/architecture leakage).

---

## 3. Operational Evaluation Rules (`SRV-R001` .. `SRV-R011`)

Defined in [`rules.yaml`](rules.yaml):

| Rule ID | Mapped Criterion | Rule Type | Normative Level | Summary |
|---|---|---|---|---|
| `SRV-R001` | `SRV-01` | `analysis` | `normative-standard` | Section-Inventory Skeleton Diff vs. Adopted Outline |
| `SRV-R002` | `SRV-02` | `analysis` | `engineering-best-practice` | Front-Matter Document-Control Scan (version/revision history) |
| `SRV-R003` | `SRV-03` | `comparison` | `engineering-best-practice` | TOC ↔ Heading Two-List Reconciliation |
| `SRV-R004` | `SRV-03` | `analysis` | `engineering-best-practice` | Intra-Document Reference Resolution |
| `SRV-R005` | `SRV-04` | `analysis` | `normative-standard` | Requirement-Class Section-Coverage Audit (interfaces/NFR/features/data) |
| `SRV-R006` | `SRV-05` | `comparison` | `engineering-best-practice` | Feature-List ↔ Section Allocation Bijection Check |
| `SRV-R007` | `SRV-05` | `analysis` | `engineering-best-practice` | Declared ID-Scheme Conformity Scan (document-wide) |
| `SRV-R008` | `SRV-06` | `comparison` | `normative-standard` | **Two-artifact** Reference-List ↔ Corpus-Inventory Resolution |
| `SRV-R009` | `SRV-06` | `comparison` | `engineering-best-practice` | Appendix Bidirectional Reference Check |
| `SRV-R010` | `SRV-07` | `engineering-best-practice` | `engineering-best-practice` | Section-Level Placeholder / Template-Scaffolding Scan |
| `SRV-R011` | `SRV-08` | `analysis` | `engineering-best-practice` | Section-Role vs. Content-Type (Design-Leak) Check |

> **Two-artifact evidence contract (`SRV-R008`):** a confirmed finding of the class *"referenced document missing from corpus"* MUST cite (1) the SRS-side reference entry (excerpt + locator) **and** (2) the review-corpus inventory evidence of non-resolution (excerpt / search scope). If no corpus inventory was supplied, the check is `Not Assessable` — the document may simply not have been uploaded; calling it "missing" without the second artifact is a contract violation.

---

## 4. Skill Boundary and Delegation

When an Agent executing `re.srs-review` encounters evidence outside document structure, it records a scoped observation and recommends delegation:

| Topic Observed | In `re.srs-review`? | Delegate / Recommend (`SKILL_REGISTRY.yaml`) | Current Registry Status |
|---|---|---|---|
| SRS document skeleton, sections, TOC, front matter, reference apparatus, whole-section placeholders, section-level design leakage | **Yes (Primary Scope)** | `re.srs-review` (this Skill) | `draft` (`0.1.0`) |
| Ambiguous / compound / untestable wording in an individual requirement | No | `re.requirement-quality` (`RQ-01`..`RQ-09`) | `draft` (`0.1.0`) |
| Duplicate or contradictory requirements; declared-scope coverage by the requirement set; deferred clusters inside populated sections | No | `re.requirement-set-quality` (`RSQ-01`..`RSQ-06`) | `draft` (`0.1.0`) |
| Requirements not matching stakeholder needs/objectives; gold-plating | No | `re.requirement-validation` (`RVAL-01`..`RVAL-06`) | `draft` (`0.1.0`) |
| RTM / cross-layer trace links, ID collisions as trace endpoints | No | `re.requirement-traceability` (`RTR-01`..`RTR-06`) | `draft` (`0.1.0`) |
| Detailed Use Case flows | No | `re.use-case-analysis` | `planned` |
| Acceptance Criteria suites | No | `re.acceptance-criteria` | `planned` |
| Content correctness of referenced ERD/UML artifacts | No | `md.erd`, `md.uml` | `planned` |

> **Rule:** never declare a hard dependency (`depends_on`) on a `planned` Skill. Delegation is a recommendation inside the Finding or Review Result. This Skill declares `depends_on: []` — it can run before or after any sibling skill.

---

## 5. Input Contract

### 5.1 Required Inputs
- **`srs_document`:** the SRS (or system requirement specification) under review, with its section/heading structure preserved.
- **`document_completeness_mode` (`full` | `partial`):** whether the supplied material is the **whole document** or a slice. **Crucial safeguard:** in `partial` mode, every whole-document absence claim (`SRV-01`, `SRV-04`, `SRV-05`, `SRV-07` beyond the slice) is `Not Assessable` — never a confirmed Issue.

### 5.2 Contextual Inputs (Unlock / Gate Deeper Checks)
- **`adopted_template_or_declared_outline` (Optional):** the project's SRS template. Absent → the recognized standard outline is assumed and recorded in review metadata as an assumption.
- **`review_corpus_inventory` (Required for `SRV-R008`):** the list of documents available in the review package (titles/versions). Absent → referenced-document resolution is `Not Assessable`.
- **`tailoring_declaration` (Optional but decisive):** explicit scope-out statements ("not applicable — rationale") for optional sections/interface classes; converts absence into `Compliant` (false-positive prevention).
- **`open_issues_register` (Optional):** registered deferrals legitimizing visible placeholders.
- **`declared_id_scheme` (Optional):** the document's own conventions statement (e.g., "FR-nn functional, NFR-nn non-functional"). Without any declaration, scheme-conformity scanning is skipped with a minor observation (the skill never invents a scheme).

---

## 6. Assessability Model (Summary)

Detailed per-criterion tables live in `criteria.yaml` → `synthesis_note`. The governing gates:

1. **Whole-document criteria** (`SRV-01`, `SRV-04`, `SRV-05`, `SRV-07`): require `document_completeness_mode: full`. A single pasted section → `Not Assessable` for these.
2. **Front-matter criteria** (`SRV-02`): assessable whenever the front matter itself is supplied, even without the requirement chapters.
3. **Navigation criteria** (`SRV-03`): TOC reconciliation needs both TOC and body headings; with only headings, the numbering-sequence and internal-reference subsets remain assessable.
4. **Corpus criteria** (`SRV-06`): appendix/footnote-internal resolution is single-document; referenced-**document** resolution requires the corpus inventory (two-artifact rule `SRV-R008`).
5. **Abstraction criteria** (`SRV-08`): assessable wherever a region's declared role and its content are both visible in the supplied material.
6. `Not Applicable` is reserved for genuine template/tailoring non-applicability — never a shortcut for missing context (which is `Not Assessable`).

---

## 7. Review Procedure

1. **Step 1 — Mode & Baseline Gate:** establish `document_completeness_mode`; establish the outline baseline (template, else recognized standard outline — record as assumption); note whether TOC/front matter/corpus inventory are present.
2. **Step 2 — Skeleton Extraction:** parse the heading tree with locators; extract TOC entries, front-matter block, references list, footnote definitions, appendix inventory, declared conventions (ID scheme, tailoring statements).
3. **Step 3 — Section Presence & Coverage (`SRV-01`, `SRV-04` / `SRV-R001`, `SRV-R005`):** diff skeleton against baseline; audit requirement-class homes, honoring tailoring declarations.
4. **Step 4 — Document Control & Navigation (`SRV-02`, `SRV-03` / `SRV-R002`, `SRV-R003`, `SRV-R004`):** front matter and revision-history currency; TOC ↔ heading reconciliation; internal-reference resolution (existence + subject match).
5. **Step 5 — Allocation & Scheme (`SRV-05` / `SRV-R006`, `SRV-R007`):** feature overview ↔ feature sections bijection; declared ID scheme conformity across sections.
6. **Step 6 — Reference Apparatus (`SRV-06` / `SRV-R008`, `SRV-R009`):** resolve normatively used reference entries against the corpus inventory (two-artifact evidence); appendix bidirectional check.
7. **Step 7 — Placeholder & Abstraction Hygiene (`SRV-07`, `SRV-08` / `SRV-R010`, `SRV-R011`):** whole-section placeholder scan (with deferral cross-check); section-role vs. content-type design-leak scan.
8. **Step 8 — Status Mapping, Findings & Delegation:** map each `(Section-context, Criterion)` outcome to `Compliant` / `Issue` / `Not Assessable` / `Not Applicable`; emit Findings per §8; record `limitations` / `clarification_requests` for missing context; attach delegation notes (§4) instead of out-of-scope judgments.

---

## 8. Output Contract

Compatible with `schemas/common/finding.schema.json` and `schemas/runtime/review-result.schema.json` (same conventions as sibling `re.*` skills):

- **Executed by `artifact-reviewer` (single SRS):** findings use `basis.type: "criterion"`, `basis.criterion_ref.item_id: "SRV-01" .. "SRV-08"`, owner `re.srs-review@0.1.0`.
- **Executed by `cross-artifact-analyzer` (SRS ↔ review corpus, or TOC-block ↔ heading-tree comparison):** findings use `basis.type` per the active schema convention with `basis.ref_id: "SRV-R001" .. "SRV-R011"`; **comparison-rule findings MUST carry ≥ 2 evidence items** (per §3 contract; `SRV-R008` two-artifact rule).
- **`finding.category`** aligns with active Profile finding categories: primarily `completeness` and `structure`; `consistency` for TOC/reference divergences (`SRV-03`, `SRV-05` scheme drift); `clarity` is NOT used here (wording → `re.requirement-quality`).
- **Evidence discipline:** exact excerpts + locators (section, line_range/page, element_id) preserved verbatim from the source document; never modify the reviewed artifact.
- **`review-result.limitations[]`** records: partial-document mode, absent corpus inventory, absent template (assumed baseline), absent declared ID scheme; **`clarification_requests[]`** requests the missing inventory/template/deferral register when material.

---

## 9. Knowledge & Principles

1. **Structure before semantics:** every structural check here is answerable from the document's organization and reference apparatus without judging any individual statement's meaning — that ordering is what keeps the `re.*` skills non-overlapping.
2. **Absence is only confirmable over a proven search scope:** in `partial` mode, absence of a section/feature/appendix elsewhere is `Not Assessable` (`SRC-0010` outline provides the checklist, not the corpus).
3. **Tailoring turns absence into compliance:** an optional section or interface class declared out of scope with rationale in a tailoring/assumptions statement is `Compliant`, not an Issue (see `examples/golden-test-cases.yaml#SRV-GTC-05`).
4. **Two-artifact rule for "missing referenced document":** never conclude "missing" from one side; require reference-entry evidence + corpus-inventory non-resolution (`SRV-R008`). Unuploaded ≠ nonexistent.
5. **Recall discipline on the superseded standard:** `SRC-0010` (IEEE Std 830-1998) is used strictly at chapter/section-name outline level, honestly flagged as superseded by `SRC-0001`; `SRC-0011` (Wiegers & Gilbert 3rd ed.) is memory-based and labeled so in every `origin_note`. No invented clause numbers, no verbatim standard text.
6. **The document's own conventions win:** ID schemes, section lists, and abstraction boundaries are enforced against what the document/template itself declares — the skill never imposes an invented universal template.

---

## 10. Authoritative References

| source_id | Title | Version/Edition | authority_level | Verification / Access Note |
|---|---|---|---|---|
| `SRC-0010` | IEEE Std 830-1998 — Recommended Practice for Software Requirements Specifications | 1998 | `official-standard` | **PROPOSED registration.** Superseded by ISO/IEC/IEEE 29148:2018 (`SRC-0001`). Content recalled at outline level only (Ch 1/2/3 + appendices); no sub-clause text quoted. |
| `SRC-0011` | Wiegers & Gilbert, Software Requirements | 3rd edition, 2010 | `industry-best-practice` | **PROPOSED registration.** Memory-based recall; no verbatim quotation; treat locators as conceptual. |
| `SRC-0001` | ISO/IEC/IEEE 29148 — Requirements engineering | 2018 (Second edition) | `official-standard` | Registered; used at conceptual locators already phrased in the registry (Clauses 5.2.5/5.2.6). |
| `SRC-0002` | NASA Systems Engineering Handbook — Appendix C | NASA/SP-2016-6105 Rev2 (2016) | `industry-best-practice` | Registered; TBD-elimination guidance at section granularity. |
| `SRC-0003` | NASA Systems Engineering Handbook — Section 4.2 | NASA/SP-2016-6105 Rev2 (2016) | `industry-best-practice` | Registered; abstraction level & valid-constraint guidance. |
| `SRC-0005` | ISO/IEC/IEEE 12207:2017 — Software life cycle processes | 2017 (First edition) | `official-standard` | Registered; Clause 6.4.3 specification-output expectation at process level. |

See Research Note: [`knowledge/research-notes/RN-0005-srs-review.md`](../../../knowledge/research-notes/RN-0005-srs-review.md).

---

## 11. Evaluation Criteria, Rules, Checklist, and Examples

- **Core Criteria (`SRV-01` .. `SRV-08`):** [`criteria.yaml`](criteria.yaml)
- **Detection & Evaluation Rules (`SRV-R001` .. `SRV-R011`):** [`rules.yaml`](rules.yaml)
- **Reviewer Checklist (Vietnamese):** [`checklist.md`](checklist.md)
- **Synthetic Examples & Golden Test Cases:** [`examples/README.md`](examples/README.md), [`examples/synthetic-examples.md`](examples/synthetic-examples.md), [`examples/golden-test-cases.yaml`](examples/golden-test-cases.yaml)

---

## 12. Expected Output
- `review-result` JSON containing:
  - `findings[]` with `basis` referencing `re.srs-review@0.1.0#SRV-01..SRV-08` (criterion) or `SRV-R001..SRV-R011` (rule), categories `completeness` / `structure` / `consistency`, exact multi-item `evidence[]` for comparison rules, and `suggested_correction` phrased as structural remedies (add section, fix TOC, register deferral, move design region to SDD, catalog reference).
  - `clarification_requests[]` / `limitations[]` for partial documents, missing corpus inventory, missing template, or undeclared ID schemes.
  - `delegation_notes[]` toward `re.requirement-quality`, `re.requirement-set-quality`, `re.requirement-validation`, `re.requirement-traceability` when statement-, set-, semantic-, or link-level evidence appears.

---

## 13. Limitations & Documented Gaps

1. **Proposed sources not yet registered:** `SRC-0010` and `SRC-0011` are **proposed** registry entries (paste-ready blocks delivered with this skill's hand-off report). Until `knowledge/source-registry.yaml` is updated by the maintainer, findings citing them carry `validation.status: unvalidated` and this limitation note. IEEE Std 830-1998 is superseded by ISO/IEC/IEEE 29148:2018 (`SRC-0001`) and is recalled at outline level only.
2. **Runtime execution limitation:** the Skill_Review system is at Foundation stage (`0.1.0`) without an automated runtime adapter; this Skill remains `draft` and all criteria/rules are `validation.status: unvalidated`.
3. **Schema conventions inherited:** extended criterion metadata lives inside `synthesis_note` and rule metadata inside `method` (shared `additionalProperties: false` schemas are untouched — same documented gap as `re.requirement-quality` §13.3).
4. **Rendered-layout checks out of scope:** page-number correctness, fonts, and layout styling of TOC/figures are not evaluated (structure only); Word/PDF pagination artifacts may need the `doc-parser` tool — if parsing loses the TOC or heading levels, report the missing tool/adapter in `limitations`, do not guess.
5. **Set/document ambiguity guard:** when the review package contains requirement *data* without document *structure* (e.g., a JSON requirement array), this Skill is not the right tool — route the orchestrator to `re.requirement-set-quality` and record `Not Applicable` at skill level.
