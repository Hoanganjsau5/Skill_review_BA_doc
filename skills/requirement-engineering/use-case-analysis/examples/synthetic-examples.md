# Synthetic Examples — `re.use-case-analysis`

Generic, project-independent walkthroughs behind the Golden Test Cases. All names/IDs are invented for illustration.

## Ex. 1 — Implicit precondition & unprotected external call (UCA-GTC-01)
A `Create Booking` spec declares a trigger and postconditions but leaves Preconditions blank while step 3 presumes the traveler is signed in with a filled cart. Step 5 (payment gateway call) has no extension. **Verdict:** UCA-03 Issue (minor) — declared-vs-impressed entry state gap; UCA-06 Issue (major) — external-call risk class missing both rejection and no-response paths. FR/BR index absent ⇒ UCA-08 Not Assessable, not "all references broken".

## Ex. 2 — Vietnamese prose flow, no numbering (UCA-GTC-02)
`Đặt tour ghép` supplies only a paragraph: keep-seat + prompt-details + pay in one breath, "làm đi làm lại cho đến khi xong", bank never declared as actor. **Verdict:** UCA-02/UCA-05/UCA-06 Issues; UCA-03/04/09 Not Assessable because the fragment simply has no header fields to judge (absent ≠ unsupplied distinction enforced). Single-step wording vagueness intentionally left to `re.requirement-quality`.

## Ex. 3 — Design leakage vs legitimate concreteness (UCA-GTC-03, cf. GTC-06)
BAD: steps bind `t_payment_session`, describe "the green rounded Pay button", fix "PayOO v2 JSON payload" while meeting notes say provider undecided → UCA-07 + UCA-10. GOOD: "System assembles the confirmation per BR-12 … within the business SLA window; Traveler sees it on My Trips page" → zero findings: one-time screen locator ≠ design narration; SLA window = valid business constraint; qualitative text anchored to a defined BR.

## Ex. 4 — Two-sided reference integrity (UCA-GTC-04)
`Cancel Booking` cites BR-99 three times; complete index export shows BR-01..BR-34. **Verdict:** UCA-08 Issue (major) with TWO evidence items (UC excerpt + index range). Because BR-99 was the only anchor making refund outcomes decidable, UCA-09 and UCA-04 follow as dependent minor Issues. FR-21 cited and present → explicitly no finding (guard against blanket citation faults).

## Ex. 5 — Index-only package (UCA-GTC-05)
The reviewer receives one spreadsheet row (`UC-050 | Manage Wallet`) with no bodies. **Verdict:** every criterion Not Assessable; `limitations[]` records the missing adapter/package gap; zero findings. The skill must not "helpfully" invent element-missing defects from a summary row.

## Ex. 6 — Boundary discipline matrix (UCA-GTC-07)
Observed → Owner:
| Observation | Owner skill | Why not UCA |
|---|---|---|
| Step says "xử lý thanh toán linh hoạt và phù hợp" (vague wording) | re.requirement-quality (RQ-03/04) | sentence-level clarity |
| UC-A1 duplicates UC-004 in the set; module scope drift | re.requirement-set-quality | set organization |
| RTM row missing although UC defines flows fine | re.requirement-traceability | matrix, not citation resolution |
| Outcome cannot be tested | re.requirement-quality (RQ-07) for a single requirement; UCA-09 for flow outcomes | unit of evaluation |
| ID `UC-A1` deviates from 8/9 corpus pattern, no convention doc | UCA-R006 → improvement-suggestion only | project-decision is forbidden as skill authority |
