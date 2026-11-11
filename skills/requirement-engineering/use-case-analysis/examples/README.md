# Examples & Golden Test Cases — `re.use-case-analysis`

Generic, project-independent synthetic examples and structured Golden Test Cases (`UCA-GTC-01` .. `UCA-GTC-07`) used for static and behavioral validation of `re.use-case-analysis` once the review runtime exists (all `validation.status: unvalidated` until then).

## Files
- [`synthetic-examples.md`](synthetic-examples.md): human-readable walkthroughs of implicit preconditions, unprotected external calls, design leakage vs. legitimate concreteness, two-sided reference resolution, index-only packages, and the boundary-ownership matrix.
- [`golden-test-cases.yaml`](golden-test-cases.yaml): 7 machine-readable Golden Test Cases covering:
  - `UCA-GTC-01`: Missing precondition declaration + payment step without rejection/no-response extensions; UCA-08 Not Assessable without index.
  - `UCA-GTC-02`: Vietnamese narrative use case — unnumbered multi-obligation prose, anonymous actor actions, open loop; unsupplied header fields gate UCA-03/04/09 to Not Assessable.
  - `UCA-GTC-03`: Premature design narration + granularity swing (UCA-07) and uncertainty asserted as fact against package notes (UCA-10).
  - `UCA-GTC-04`: Broken cross-reference — BR-99 cited, absent from complete index; every finding carries two evidence sides (UCA-08/UCA-R005, dependent UCA-04/UCA-09).
  - `UCA-GTC-05`: Missing-context safeguard — index-row-only package yields Not Assessable across UCA-01..UCA-10 with zero findings.
  - `UCA-GTC-06`: False-positive prevention — BR-anchored qualitative outcome, one-time screen locator, valid SLA constraint all pass with zero findings.
  - `UCA-GTC-07`: Strict ownership boundary — vague step wording belongs to `re.requirement-quality`; set duplication to `re.requirement-set-quality`; naming deviation without a supplied convention doc yields improvement-suggestion only (UCA-R006).
