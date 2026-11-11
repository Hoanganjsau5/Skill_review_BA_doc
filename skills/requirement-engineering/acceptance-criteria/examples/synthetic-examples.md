# Synthetic Examples — `re.acceptance-criteria`

Human-readable walkthroughs paired with the machine-readable suite in
[`golden-test-cases.yaml`](golden-test-cases.yaml). All artifacts are self-written
synthetic material (repository rule: no real project documents without permission).
Each example states the sample excerpt, the expected criterion statuses, and why —
including the suppressions that make the suite a calibration instrument, not a keyword trap.

## EX-01 — Unquantified + vague outcome (`ACA-01`, `ACA-08`, `ACA-R001`, `ACA-R008`) — anchors ACA-GTC-01

> AC-101.1 (owner FR-101, declared format: bullet-list):
> "Then the search results load quickly and show relevant hotels."

- **Expected:** `ACA-01` Issue, `ACA-08` Issue, `ACA-02` Not Applicable (declared non-GWT format), rest pass/NA.
- **Why:** `quickly` is a quantity-sensitive bound with no threshold anywhere in the package; `relevant` admits divergent accept/reject readings (first-10 vs filters-applied). Both findings must carry the two competing interpretations and a testable rewrite, per the vendor rule.

## EX-02 — Bundled Vietnamese behaviors + declared-but-uncovered rejection path (`ACA-03`, `ACA-05`) — anchors ACA-GTC-02

> FR-210: "…từ chối booking có ngày nhận phòng quá 12 tháng."
> AC-210.1: "Người dùng tạo booking thành công **và** hệ thống gửi email xác nhận **và** lưu booking vào cơ sở dữ liệu."

- **Expected:** `ACA-03` Issue (split: creation vs email), `ACA-05` Issue (no AC accepts the declared >12-month rejection).
- **Why independent-failure test:** the email can fail while creation passes — two concerns. Contrast with the allowed facet pattern in EX-08 (status + record + feedback of ONE transaction). The >12-month rejection is taken from the FR text itself — no invented failure modes.

## EX-03 — GWT slot errors (`ACA-02`, `ACA-R002`) — anchors ACA-GTC-03

> Given **the user taps Pay** and the gateway does not respond within 30s / When the retry is triggered / Then the user sees the order as processing
> (second scenario: no Then at all)

- **Expected:** `ACA-02` Issue ×2 (action parked in Given; scenario without expected result).
- **Why:** keyword slots are the test-mapping contract; a Then-less scenario defines no acceptance decision. Bounded 30s precondition keeps `ACA-01` clean — structural and semantic errors are separate statuses.

## EX-04 — Bidirectional anchor gaps + id collision (`ACA-04`, `ACA-07`) — anchors ACA-GTC-04

> Owner inventory FR-401/402/403 (full scope package); ACs: two different criteria share id `AC-401.1`; `AC-404.1` references absent `FR-499`; `FR-402` has zero ACs.

- **Expected:** `ACA-04` Issue (both directions), `ACA-07` Issue (duplicate id), `ACA-01`/`ACA-08` Compliant.
- **Key calibration:** the broken-anchor AC's wording is quantified and clear — it must NOT be reported as ambiguous. Ownership/coverage is the finding's home.

## EX-05 — Quantified-but-wrong-owner: ownership, never ambiguity (`ACA-06` owns it) — anchors ACA-GTC-05

> FR-501 declares hotel SEARCH. AC-501.2 (anchored to FR-501): "Booking payment completes within 5 seconds under normal network conditions."

- **Expected:** `ACA-06` Issue (payment obligation absent from owner item); `ACA-01`/`ACA-08` Compliant (the 5-second bound is decidable); anchor exists so `ACA-04` Compliant.
- **Why:** acceptance criteria inherit, they do not legislate. Flagging this as "ambiguous timing" would be the exact false positive the boundary rule forbids.

## EX-06 — Partial package = Not Assessable, zero invented defects (`ACA-04/05/06/09/10`) — anchors ACA-GTC-06

> One AC ("…method per project test plan"), no owner inventory, no scope declaration, test plan not in package.

- **Expected:** coverage/error-path/creep/comparison/demonstration all **Not Assessable** + clarification requests; wording criteria still judge the single AC; **zero confirmed findings**.
- **Why:** mirrors the sibling safeguard — missing context is requested, never assumed defective.

## EX-07 — Design lock-in + threshold contradiction (`ACA-06`, `ACA-09`) — anchors ACA-GTC-07

> AC-601.1: "Points are written to the **MySQL table loyalty_balances in the same DB transaction**…" (owner item says only "award points… expire per policy").
> AC-601.2 vs AC-601.3: same condition, **24** vs **48** months.

- **Expected:** `ACA-06` Issue (technology as acceptance condition — downgrade path if an approved design constraint doc is supplied); `ACA-09` Issue citing both excerpts verbatim.
- **Why:** condition overlap is proven from text before declaring contradiction; the duplicate-drift hazard is recorded in the same finding, not double-counted.

## EX-08 — Golden compliant suite (`ACA-01..10` all Compliant) — anchors ACA-GTC-08

> US-700 declares two numeric windows (24h refund) and a gateway-failure mode. ACs: within-window (status + refund record + toast as ONE decision), out-of-window rejection copy, fault-injected retryable state with ticket id; unique ids, explicit per-AC methods.

- **Expected:** every status Compliant, zero findings.
- **Why this is the calibration positive:** facet `And` content passes `ACA-R003`, declared failure modes are all covered (`ACA-R005`), bounds refine the owner item exactly (`ACA-R006`), methods match outcome kinds (`ACA-R010`).

## EX-09 — Vietnamese anti-false-positive + format NA (`ACA-02` NA, `ACA-08` suppression) — anchors ACA-GTC-09

> TC-810-01 (declared table format, columns Điều kiện/Hành động/Kết quả/Cách kiểm chứng): "…danh sách <= 20 khách sạn cùng thành phố hiển thị **nhanh chóng, tối đa 2 giây** trên mạng 4G."

- **Expected:** `ACA-08` Compliant — signal `nhanh chóng` suppressed because the bound follows immediately (vi language-pack's own rule); `ACA-02` Not Applicable justified by declared format.
- **Why:** proves the suite reports the *interpretation gap*, not the *word*.

## EX-10 — Strict boundary: bad requirement prose, clean AC suite → delegate (`SKILL.md` §3) — anchors ACA-GTC-10

> US-900 statement: "handle suggestions smartly and support users easily" (vague). Its two ACs: fully decidable, anchored, method-stated home-screen renders.

- **Expected here:** all `ACA-*` Compliant/NA, **zero findings**; delegated observations to `re.requirement-quality` (statement wording) and `re.requirement-set-quality` (undefined product scope).
- **Why:** ownership discipline — the AC-suite lens must not borrow a sibling's defect to manufacture a finding.

---

### Note on representation

Same semantics are exercised across formats (Gherkin EX-03/08, bullet EX-01/02/04/05/07, table EX-09) to demonstrate `Representation Neutrality`: form variation never by itself changes a status.

### Schema-gap observation (v0.2.0 proposal)

`review-result.schema.json` lacks a `criterion_evaluations[]` array, so the four statuses per case currently ride in summary text/rationale; `criterion.schema.json` `additionalProperties: false` forces the extended assessability metadata into `synthesis_note`. Proposals tracked in the examples README; not yet schema changes (shared files are out of this Skill's write scope).
