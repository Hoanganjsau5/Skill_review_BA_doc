# Examples & Golden Test Cases — `re.acceptance-criteria`

This directory contains generic, project-independent synthetic examples and structured Golden Test Cases (`ACA-GTC-01` .. `ACA-GTC-10`) used for static and behavioral validation of `re.acceptance-criteria` (pipeline step 6). All artifacts are self-written; no real project documents are used.

## Files

- [`synthetic-examples.md`](synthetic-examples.md): Human-readable walkthroughs (EX-01 .. EX-10) of unquantified/vague ACs, GWT slot errors, bundled Vietnamese behaviors, bidirectional anchor gaps, design lock-in + threshold contradiction, the golden compliant suite, and the boundary-suppression cases.
- [`golden-test-cases.yaml`](golden-test-cases.yaml): 10 machine-readable Golden Test Cases covering:
  - `ACA-GTC-01`: Unquantified outcome + vague qualifier (`ACA-01`, `ACA-08`; `ACA-02` Not Applicable by declared bullet-list format).
  - `ACA-GTC-02`: Vietnamese suite — `và`-bundled independent behaviors (`ACA-03`) and a declared >12-month rejection mode with no negative-path AC (`ACA-05`).
  - `ACA-GTC-03`: Malformed Given/When/Then — action inside Given, scenario without Then (`ACA-02` / `ACA-R002`).
  - `ACA-GTC-04`: Bidirectional gaps — FR with zero ACs + broken-anchor AC (`ACA-04` / `ACA-R004`) and duplicate AC id (`ACA-07` / `ACA-R007`).
  - `ACA-GTC-05`: **False-positive prevention** — a quantified, decidable AC attached to the wrong owner item is an ownership/creep finding (`ACA-06`), never an ambiguity finding (`ACA-08` stays Compliant).
  - `ACA-GTC-06`: **Not Assessable safeguard** — no owner inventory/scope and an external test plan absent → `ACA-04/05/06/09/10` Not Assessable, zero confirmed findings, clarification requests instead.
  - `ACA-GTC-07`: Design lock-in in an AC (`ACA-06`) + same-condition 24-vs-48-month contradiction (`ACA-09` / `ACA-R009`, both excerpts verbatim required).
  - `ACA-GTC-08`: Golden all-Compliant GWT suite including the facet-And allowance (`ACA-R003`) — the calibration positive.
  - `ACA-GTC-09`: Vietnamese declared-table format — `ACA-02` Not Applicable justified by format declaration; `nhanh chóng` signal **suppressed** by the immediate `<= 2 giây` bound (anti-FP gate mirrors the `re.requirement-quality` vi language-pack rule).
  - `ACA-GTC-10`: **Strict ownership boundary** — vague story *statement* wording with a clean AC suite: zero findings here; delegations to `re.requirement-quality` (statement wording) and `re.requirement-set-quality` (product-scope question) recorded as recommendations.

## Naming convention (per `skills/_template/examples/README.md`)

Future standalone per-item files follow `<criterion_or_rule_id>-pass-<n>.md` / `-fail-<n>.md` (e.g., `ACA-01-fail-1.md`). At 0.1.0 the walkthroughs live consolidated in `synthetic-examples.md` with EX- anchors mapping 1:1 to the GTC cases, mirroring the sibling requirement-engineering skills.

## Validation status

All `validation.status` values in `criteria.yaml` / `rules.yaml` remain `unvalidated`: the Foundation stage has no runtime adapter to execute these cases yet. The golden suite is the behavioral specification for that future execution.

## v0.2.0 proposal notes (schema gaps, shared with siblings)

1. Add `criterion_evaluations[]` to `review-result.schema.json` so the four statuses per criterion are first-class output, not summary prose.
2. Relax `criterion.schema.json` / `analysis-rule.schema.json` (`additionalProperties: false` today) to promote the `synthesis_note` pseudo-keys (assessability gates, scope boundaries) to real fields — currently carried as YAML-shaped text inside the note.

Do not apply either change from this Skill folder — schemas are shared files.
