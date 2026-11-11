# Language Packs (`re.requirement-quality`)

## 1. Purpose and Architectural Role
Language Packs decouple **natural-language linguistic signals** from the **language-independent Core Criteria** (`../criteria.yaml`) and **Core Evaluation Rules** (`../rules.yaml`).

- **Core Criteria (`RQ-01` .. `RQ-09`):** Define semantic quality characteristics that hold in every human language.
- **Language Packs (`<lang>.yaml`):** Supply language-specific cue patterns, grammatical considerations, examples, and false-positive warnings used by heuristic rules (`RQ-R003`, `RQ-R004`, `RQ-R005`, `RQ-R006`, `RQ-R008`, `RQ-R009`, `RQ-R015`, `RQ-R016`).

> **Critical Rule:** Every pattern or expression in a Language Pack is a **heuristic detection signal (`normative_level: Heuristic`)**, NEVER an automatic defect. The Agent must evaluate the surrounding context, parenthetical bounds, linked acceptance criteria, and project glossary before reporting an `Issue`.

---

## 2. Implemented Language Packs

| Language Code (BCP 47 / ISO 639-1) | Language Name | File | Status |
|---|---|---|---|
| `en` | English | [`en.yaml`](en.yaml) | `draft` (`0.1.0`) |
| `vi` | Vietnamese (Tiếng Việt) | [`vi.yaml`](vi.yaml) | `draft` (`0.1.0`) |

---

## 3. Language Pack Structure Contract

Every `<lang>.yaml` file must contain the following top-level keys:
- `language_pack_id`: `"re.requirement-quality.lang.<lang>"`
- `language_code`: ISO 639-1 code (e.g., `"en"`, `"vi"`, `"ja"`)
- `language_name`: Human-readable name
- `version`: SemVer (`"0.1.0"`)
- `applies_to_skill`: `{ skill_id: "re.requirement-quality", version_range: "^0.1.0" }`
- `usage_policy`: Explicit statement that signals require contextual verification
- `signal_categories`:
  - `vague_qualitative_terms` (maps to `RQ-03`, `RQ-07` via `RQ-R003`, `RQ-R012`)
  - `imprecise_quantifiers` (maps to `RQ-03`, `RQ-04`, `RQ-07` via `RQ-R003`)
  - `open_ended_clauses_and_placeholders` (maps to `RQ-04` via `RQ-R008`)
  - `ambiguous_combinators` (maps to `RQ-03`, `RQ-05` via `RQ-R005`, `RQ-R009`)
  - `escape_clauses` (maps to `RQ-03`, `RQ-04`, `RQ-07` via `RQ-R006`)
  - `pronoun_and_reference_patterns` (maps to `RQ-03` via `RQ-R004`)
  - `compound_obligation_markers` (maps to `RQ-05` via `RQ-R009`)
- `grammatical_considerations`: Language-specific grammar rules (e.g., passive voice without actor, scope of negation/conjunction, classifier/omitted-subject patterns)
- `representation_patterns`: Standard skeletons for User Story, EARS, and modal verbs in that language (used only when the representation or project convention is declared)
- `false_positive_warnings`: Explicit scenarios where a signal word is completely valid
- `examples`: Acceptable (`compliant`) vs. problematic (`issue`) synthetic statements in that language

---

## 4. How to Add a New Language Pack (e.g., Japanese `ja`)

1. Create `language-packs/ja.yaml` following the structure contract in Section 3.
2. Do **not** modify `../criteria.yaml` or `../rules.yaml`.
3. Add synthetic test cases for the new language in `../examples/golden-test-cases.yaml`.
4. Register the addition in `../CHANGELOG.md` and bump the Skill `MINOR` version (`0.1.0` $\rightarrow$ `0.2.0`).
