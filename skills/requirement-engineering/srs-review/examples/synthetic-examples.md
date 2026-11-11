# Synthetic Examples — `re.srs-review`

Các ví dụ tổng hợp (synthetic) dưới đây mô tả từng pattern phát hiện chính của skill. Mọi ID, tên section và trích dẫn đều là giả lập phục vụ minh họa; ánh xạ sang test cases chuẩn hóa trong `golden-test-cases.yaml`.

---

## Example 1: Skeleton gap — mandatory Overall-Description subsections absent (`SRV-01` / SRV-R001)

**Input Context.** Full-mode SRS, no project template supplied (reviewer records the assumed baseline: recognized standard outline). Heading inventory:

```text
1 Introduction          (1.1 Purpose, 1.2 Document Scope)
2 Overall Description   (2.1 Product Perspective, 2.2 Product Functions, 2.3 User Characteristics)
3 Specific Requirements (3.1 External Interfaces → 3.1.1 User Interfaces only; 3.2 System Features)
```

No Constraints section, no Assumptions & Dependencies section, no tailoring declaration anywhere.

**Expected Assessment.** `SRV-01: Issue (major)` — inventory jumps from 2.3 straight to chapter 3; two mandated Overall-Description subsections have no home, so the entire constraint/assumption class is structurally unable to appear. One finding with section-inventory evidence and the assumed-baseline note. `SRV-04` additionally flags the interface-class hole (only 3.1.1 exists while §2.1 names an external payment gateway). Absence claims are legitimate **only** because `document_completeness_mode: full` proves the search scope.

## Example 2: Renumbered section, stale TOC, dangling "Xem Mục 3.4" (`SRV-03` / SRV-R003, SRV-R004)

**Input Context.** Vietnamese SRS v1.4. TOC: `3.4 Quản lý thanh toán`, `3.5 Thông báo đẩy`. Body headings after rework: `3.4 Thông báo đẩy`, `3.5 Quản lý thanh toán` (TOC not regenerated). FR-21 in 3.2 states: "Quy trình hoàn tiền xem Mục 3.4."

**Expected Assessment.** `SRV-03: Issue (minor)` with two-part evidence (TOC entry excerpt + actual heading excerpt). Worse than cosmetics: FR-21's normative pointer now lands on push notifications, not refunds — SRV-R004's subject-match check escalates this to a contractual ambiguity (still `SRV-03`, one finding, both rules cited). Revision history is current → `SRV-02: Compliant`.

## Example 3: Two-artifact rule — "referenced document missing" needs BOTH sides (`SRV-06` / SRV-R008, SRV-R009)

**Input Context.** References list: `[R1] ICD-PAY-02 v1.3 — Payment Gateway Interface Control Document`, `[R2] ADR-0007`. FR-33 binds its payment behavior "as specified in [R1]". Review-corpus inventory supplied with the package lists only `ADR-0007` and the SRS itself. Separately, §3.4 says "message schema per Appendix D" while the document's appendix inventory ends at Appendix C.

**Expected Assessment.** `SRV-06: Issue (major)`. The finding MUST quote two artifacts: (1) the `[R1]` entry + FR-33's normative use (SRS side), and (2) the corpus inventory showing no ICD-PAY-02 entry (corpus side). Had the corpus inventory NOT been supplied, the correct output is `Not Assessable` + a clarification_request — the document may simply not have been uploaded; unuploaded ≠ nonexistent. The Appendix-D hole resolves on the document alone (SRV-R009), same two-part shape (body invocation + appendix inventory).

## Example 4: Tailoring turns absence into compliance — false-positive prevention (`SRV-04`, `SRV-01` / SRV-R005)

**Input Context.** Vietnamese SRS; §1.6 "Tài liệu cắt bớt (Tailoring)": "Không áp dụng: 3.1.2 Giao diện phần cứng và 3.1.4 Giao diện truyền thông — sản phẩm chỉ là web/mobile…". Sections 3.1.2/3.1.4 genuinely absent. Data description satisfied by reference: "3.4 Dữ liệu: xem ERD-TRIPMATE v2.1" (present in corpus inventory).

**Expected Assessment.** `SRV-04: Compliant`, zero findings. The pass_condition "class without applicable interface explicitly declared not-applicable with rationale" is met; flagging the absent sections would be the canonical tailoring false positive. SRV-06 Compliant too — the ERD pointer resolves in the corpus.

## Example 5: Whole-section placeholder vs. inline TBD — the ownership line (`SRV-07` / SRV-R010; boundary RQ-04)

**Input Context.** Full-mode SRS. §3.8 "Báo cáo & Thống kê" body is exactly `[TBD — sẽ bổ sung sau sprint 5]`; the open-issues register has no entry covering it. Elsewhere, FR-52 reads: "The system shall retain bookings for [TBD] days."

**Expected Assessment.** `SRV-07: Issue (major)` for 3.8 only — a whole unregistered placeholder section. FR-52's inline TBD is **not** this skill's finding: it is a per-statement completeness defect owned by `re.requirement-quality (RQ-04)`; SRV-R010 step 2 explicitly suppresses re-reporting it (route note instead). A second finding would double-count one root cause across the ownership boundary.

## Example 6: Design leakage at REGION scale — and what it is not (`SRV-08` / SRV-R011; boundaries RQ-02, RSQ-06)

**Input Context.** Chapter-3 preamble declares: "Chương này chỉ chứa yêu cầu, không chứa thiết kế — thiết kế thuộc SDD-TRIPMATE." Yet §3.9 "Thiết kế cơ sở dữ liệu" contains normative `CREATE TABLE` DDL, and §3.10 "Kiến trúc kỹ thuật" mandates "Spring Cloud Gateway, gRPC" as the ONLY content of the declared feature "Tích hợp cổng thanh toán". Separately, FR-61 (in an otherwise clean section) says "The system shall use a Redis cache for session storage."

**Expected Assessment.** `SRV-08: Issue` — two normative design REGIONS nested under a requirements-only chapter (two-part evidence: role declaration + design-region excerpt). The §3.10 substitution also means the gateway feature's WHAT is nowhere stated: recorded as an observation per SRV-R011 step 4, NOT as an invented `RSQ-02` set-completeness finding. FR-61's single premature-design statement belongs to `re.requirement-quality (RQ-02)`; if the issue were peer statements at mismatched abstraction *granularity*, that would be `re.requirement-set-quality (RSQ-06)`. Three neighbors, one document — the line is drawn by the unit of evaluation: statement → RQ, section region → SRV, set classification → RSQ.

## Example 7: The partial-document gate — a pasted section proves nothing about the rest (`SRV-01..SRV-07: Not Assessable`)

**Input Context.** Review package contains only "Section 3.5 Booking Confirmation" (FR-41..FR-44) plus the chapter-3 preamble declaring "requirements only". No TOC, no front matter, no references list, no corpus inventory.

**Expected Assessment.** `SRV-01, SRV-02, SRV-03, SRV-04, SRV-05, SRV-06, SRV-07 → Not Assessable` with limitations/clarification_requests naming the missing context (full document, TOC, inventory). Zero invented defects. `SRV-08: Compliant` — the supplied region and its declared role are both visible and agree. This is the anti-hallucination contract: whole-document absence claims need a whole document (see `golden-test-cases.yaml#SRV-GTC-04`).
