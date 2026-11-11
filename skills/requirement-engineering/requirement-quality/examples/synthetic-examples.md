# Synthetic Examples (`re.requirement-quality`)

All 15 examples below are **original synthetic examples** designed to illustrate and test `re.requirement-quality` (`RQ-01` .. `RQ-09`).

---

## EX-01 — Clear and Testable Functional Requirement (English, SRS)
- **Artifact Type:** `srs` · **Requirement Type:** Functional · **Level:** Software · **Language:** `en`
- **Requirement (`REQ-INV-101`):**
  > "When a buyer submits a purchase order with a total amount exceeding the buyer's configured credit limit, the Order Service shall reject the purchase order and return error code `ERR_CREDIT_LIMIT_EXCEEDED`."
- **Supplied Context:**
  - Parent requirement `BR-12`: Prevent credit exposure beyond approved buyer credit limits.
  - Project conventions: ID pattern `^REQ-[A-Z]+-[0-9]{3}$`, prose `shall` template, glossary defines `buyer`, `purchase order`, `credit limit`.
  - Technical constraints: Synchronous REST order service; standard deterministic state/error check.
- **Evaluation Summary:**
  - `RQ-01` .. `RQ-09`: **All `Compliant`**. No Finding generated.

---

## EX-02 — Ambiguous Requirement: Referential & Combinator Ambiguity (English, Functional List)
- **Artifact Type:** `functional-requirement-list` · **Requirement Type:** Functional · **Language:** `en`
- **Requirement (`REQ-WMS-014`):**
  > "When the Warehouse Controller sends a dispatch manifest to the Carrier Gateway, it shall archive it and/or notify the supervisor or the shift lead and the dock clerk."
- **Supplied Context:** No additional disambiguating context.
- **Evaluation Summary:**
  - `RQ-03` (`Unambiguous`): **`Issue`** (`confirmed-issue`, `major`).
    - First `it` could refer to `Warehouse Controller` or `Carrier Gateway`; second `it` could refer to the `dispatch manifest` or the state (`RQ-R004`).
    - `and/or` is an ambiguous combinator (`RQ-R005`).
    - `notify the supervisor or the shift lead and the dock clerk` has two boolean groupings: `(supervisor OR shift lead) AND dock clerk` vs `supervisor OR (shift lead AND dock clerk)` (`RQ-R005`).
  - `RQ-05` (`Singular`): **`Issue`** (`potential-issue`, `minor`) — archiving and multi-role notification are bundled via `and/or`.

---

## EX-03 — Requirement with Vague Qualitative Expressions (English, NFR List)
- **Artifact Type:** `nfr-list` · **Requirement Type:** Non-functional (Performance & Usability) · **Language:** `en`
- **Requirement (`NFR-PORTAL-008`):**
  > "The analytics dashboard shall be user-friendly and shall render large reports quickly as appropriate, etc."
- **Supplied Context:** No glossary definitions for `large reports` or `quickly`; no linked acceptance criteria.
- **Evaluation Summary:**
  - `RQ-03` (`Unambiguous`): **`Issue`** (`confirmed-issue`, `major`) — `user-friendly`, `large reports`, `quickly` (`RQ-R003`) and escape clause `as appropriate` (`RQ-R006`) have no clear single interpretation.
  - `RQ-04` (`Complete`): **`Issue`** (`confirmed-issue`, `major`) — open-ended tail `etc.` (`RQ-R008`) and undefined condition `as appropriate` leave the requirement incomplete.
  - `RQ-05` (`Singular`): **`Issue`** (`confirmed-issue`, `minor`) — combines usability (`user-friendly`) and report rendering latency (`render large reports quickly`) in one item (`RQ-R009`).
  - `RQ-07` (`Verifiable`): **`Issue`** (`confirmed-issue`, `major`) — subjective term `user-friendly` and unbounded `quickly` cannot be objectively verified (`RQ-R012`).

---

## EX-04 — Requirement with Multiple Independent Obligations (English, BRD)
- **Artifact Type:** `brd` · **Requirement Type:** Functional · **Language:** `en`
- **Requirement (`REQ-HR-022`):**
  > "The Payroll Module shall calculate monthly net salary per employee by the 25th of each month, shall export tax withholding files to the national tax portal, and shall allow employees to update their emergency contact phone numbers in the self-service profile."
- **Evaluation Summary:**
  - `RQ-05` (`Singular`): **`Issue`** (`confirmed-issue`, `major`, rule `RQ-R009`) — bundles three completely independent capabilities (salary calculation, external tax export, and employee self-service emergency contact editing) that have different actors, triggers, and verification cycles.

---

## EX-05 — Valid Implementation Constraint vs. Premature Design (English, Interface Spec)
- **Artifact Type:** `interface-spec` · **Requirement Type:** Constraint · **Level:** System Interface · **Language:** `en`
- **Requirement (`CON-SEC-003`):**
  > "All external partner webhook payloads transmitted over the public internet shall be signed using HMAC-SHA256 with a 256-bit shared secret in the `X-Signature-256` HTTP header."
- **Supplied Context:**
  - `architecture-decisions.md` (`PADR-004`): Mandates HMAC-SHA256 for partner webhook interoperability.
- **Evaluation Summary:**
  - `RQ-02` (`Appropriate`): **`Compliant`** (`RQ-R002`). Although `HMAC-SHA256` and `X-Signature-256` specify concrete technical mechanisms, the item is a system-interface security constraint backed by `PADR-004`. Must **not** be flagged as premature design.
  - `RQ-03`, `RQ-04`, `RQ-05`, `RQ-07`: **`Compliant`**.

---

## EX-06 — Requirement That Does Not Need a Numerical Measurement (English, System Spec)
- **Artifact Type:** `system-requirement-spec` · **Requirement Type:** Functional (State Transition) · **Language:** `en`
- **Requirement (`REQ-DOOR-019`):**
  > "While the autoclave chamber pressure is above atmospheric baseline, the Safety Interlock Controller shall prevent the chamber door latch from transitioning to the `UNLOCKED` state."
- **Supplied Context:** `atmospheric baseline` and `UNLOCKED` state are defined in the system state dictionary.
- **Evaluation Summary:**
  - `RQ-07` (`Verifiable`): **`Compliant`** (`RQ-R012`). Compliance is objectively verifiable via state-transition testing/demonstration (attempting to unlock while pressure > baseline and verifying latch state remains locked). No additional latency or percentage number is required.

---

## EX-07 — User Story Format (English, Backlog Item — Incomplete Acceptance/Bounds)
- **Artifact Type:** `user-story` · **Requirement Type:** Functional · **Language:** `en`
- **Requirement (`US-BILL-041`):**
  > "As a billing administrator, I want to export overdue invoices so that I can follow up with customers."
- **Supplied Context:**
  - Project convention: User Stories follow `As a <role>, I want <goal>, so that <benefit>`, and must have linked Acceptance Criteria specifying export format and overdue filter rule before entering Sprint Ready.
  - Supplied Acceptance Criteria: *None provided (`missing`)*.
- **Evaluation Summary:**
  - `RQ-01` (`Necessary`): **`Compliant`** (benefit/rationale is stated in the `so that` clause and aligns with billing scope).
  - `RQ-04` (`Complete`) & `RQ-07` (`Verifiable`): **`Issue`** (`needs-clarification`, `major`, rules `RQ-R007`, `RQ-R012`, `RQ-R015`) — the story statement follows the User Story skeleton (`RQ-09` statement structure), but without Acceptance Criteria defining what constitutes "overdue" and what export format/fields are produced, the requirement is incomplete and not objectively verifiable.

---

## EX-08 — EARS-Style Requirement (English, EARS Specification)
- **Artifact Type:** `ears` · **Requirement Type:** Functional (Unwanted Behavior pattern) · **Language:** `en`
- **Requirement (`EARS-TEL-012`):**
  > "IF the telemetry uplink connection is lost for more than 10 consecutive seconds, THEN the Edge Collector shall buffer incoming sensor frames in non-volatile local storage up to 500 MB."
- **Supplied Context:**
  - Project convention: EARS `IF <unwanted condition>, THEN the <system> shall <response>` syntax.
  - Hardware context: Edge device has 4 GB non-volatile flash reserved for telemetry buffering.
  - Parent requirement `SYS-TEL-02`: Zero telemetry loss during transient network outages up to 15 minutes.
- **Evaluation Summary:**
  - `RQ-01` .. `RQ-09`: **All `Compliant`**.

---

## EX-09 — Requirement with Missing Business & Constraint Context (English, Requirement Table)
- **Artifact Type:** `requirement-table` · **Requirement Type:** Functional · **Language:** `en`
- **Requirement (`REQ-EXPORT-005`):**
  > "When an auditor requests a ledger snapshot for a fiscal quarter, the Reporting Service shall generate a digitally signed PDF report containing all posted journal entries for that quarter."
- **Supplied Context:**
  - Only the single table row (`REQ-EXPORT-005`) is provided.
  - `business_objectives`, `parent_requirement`, `technical_constraints`, `infrastructure`, `authoritative_source`, and `project_conventions` are all `missing`.
- **Evaluation Summary (Testing Context Gates):**
  - `RQ-03` (`Unambiguous`), `RQ-04` (`Complete`), `RQ-05` (`Singular`), `RQ-07` (`Verifiable`): **`Compliant`** (assessable from the statement alone).
  - `RQ-01` (`Necessary`): **`Not Assessable`** (no business need/parent/rationale supplied).
  - `RQ-02` (`Appropriate`): **`Compliant`** (artifact is a software requirement table and behavior is at service boundary).
  - `RQ-06` (`Feasible`): **`Not Assessable`** (no infrastructure/constraint context supplied).
  - `RQ-08` (`Correct`): **`Not Assessable`** (no authoritative source/parent requirement supplied).
  - `RQ-09` (`Conforming`): **`Not Assessable`** (no project formatting/ID conventions supplied).
  - **Findings emitted:** **Zero** (missing context is noted in `review-result.limitations`; no fabricated `Compliant` or `Issue` verdicts on `RQ-01`, `RQ-06`, `RQ-08`, `RQ-09`).

---

## EX-10 — Requirement Delegating Verification to Missing External Artifact (English, PRD)
- **Artifact Type:** `prd` · **Requirement Type:** Non-functional (Performance) · **Language:** `en`
- **Requirement (`NFR-SEARCH-002`):**
  > "The Product Catalog Search API shall meet the latency targets and concurrency tiers specified in Performance Benchmark Matrix `PERF-MAT-2026-v2`."
- **Supplied Context:**
  - Document `PERF-MAT-2026-v2` is referenced by ID but was **not** included in the review scope artifacts.
- **Evaluation Summary:**
  - `RQ-04` (`Complete`) & `RQ-07` (`Verifiable`): **`Not Assessable`** (rules `RQ-R008`, `RQ-R012`). Emit a `needs-clarification` Finding / `clarification_request` asking for `PERF-MAT-2026-v2` rather than declaring the requirement defective or compliant.

---

## EX-11 — Vietnamese Requirement with Linguistic Issues (Vietnamese, SRS)
- **Artifact Type:** `srs` · **Requirement Type:** Functional · **Language:** `vi`
- **Requirement (`REQ-NOTIFY-007`):**
  > "Hệ thống cần xử lý yêu cầu hoàn tiền nhanh chóng và gửi thông báo phù hợp cho khách hàng và/hoặc nhân viên hỗ trợ khi cần thiết, v.v."
- **Supplied Context:** Không có định nghĩa ngưỡng thời gian hay danh sách trường trong glossary.
- **Evaluation Summary (using `language-packs/vi.yaml`):**
  - `RQ-03` (`Unambiguous`): **`Issue`** (`confirmed-issue`, `major`) — từ định tính không ngưỡng `"nhanh chóng"`, `"phù hợp"` (`RQ-R003`), từ nối mơ hồ `"và/hoặc"` (`RQ-R005`), escape clause `"khi cần thiết"` (`RQ-R006`).
  - `RQ-04` (`Complete`): **`Issue`** (`confirmed-issue`, `major`) — kết thúc mở `"v.v."` (`RQ-R008`) và chưa xác định điều kiện `"khi cần thiết"`.
  - `RQ-05` (`Singular`): **`Issue`** (`potential-issue`, `minor`) — gộp xử lý hoàn tiền và gửi thông báo qua `"và"` / `"và/hoặc"`.
  - `RQ-07` (`Verifiable`): **`Issue`** (`confirmed-issue`, `major`) — không thể kiểm chứng khách quan `"nhanh chóng"` và `"phù hợp"`.

---

## EX-12 — English Requirement with Bounded Qualitative Term (Anti-False-Positive, API Spec)
- **Artifact Type:** `api-spec` · **Requirement Type:** Non-functional · **Language:** `en`
- **Requirement (`API-RATE-004`):**
  > "When a client exceeds 100 requests/second per API key, the API Gateway shall quickly reject excess requests within 15 ms (p99) by returning HTTP status `429 Too Many Requests`."
- **Supplied Context:** Standard REST API Gateway specification.
- **Evaluation Summary (Anti-False-Positive Test):**
  - Even though `quickly` is a signal word in `language-packs/en.yaml` (`vague_qualitative_terms`) and `/` appears in `requests/second` (`ambiguous_combinators`), contextual evaluation (`RQ-R003`, `RQ-R005`) sees that `quickly` is immediately bounded by `within 15 ms (p99)` and `requests/second` is a unit of measure.
  - `RQ-03`, `RQ-04`, `RQ-05`, `RQ-07`: **`Compliant`**. **Zero Findings generated.**

---

## EX-13 — Mixed-Language Requirement: Valid Technical Terms vs. Ambiguous Slang (Vietnamese + English, SRS)
- **Artifact Type:** `srs` · **Requirement Type:** Functional · **Language:** `vi` + `en` (mixed)
- **Requirement A (`REQ-AUTH-010` — Valid Mixed-Language):**
  > "Khi nhận được request đăng nhập hợp lệ, Authentication Service phải phát hành một `JWT access token` có thời hạn (`exp`) đúng 900 giây theo chuẩn `RFC 7519`."
  - **Result:** **`Compliant`** (`RQ-R016`). Technical terms (`request`, `Authentication Service`, `JWT access token`, `exp`, `RFC 7519`) are unambiguous industry-standard identifiers.
- **Requirement B (`REQ-AUTH-011` — Ambiguous Mixed-Language):**
  > "Khi hệ thống bị lag hoặc user thực hiện flow bất thường, hệ thống phải tự động handle một cách smooth."
  - **Result:** **`Issue`** on `RQ-03`, `RQ-04`, `RQ-07` (`confirmed-issue`, `major`, rules `RQ-R003`, `RQ-R007`, `RQ-R012`, `RQ-R016`) — `"bị lag"`, `"flow bất thường"`, `"handle"`, `"một cách smooth"` are undefined colloquial mixed-language expressions with no deterministic condition or outcome.

---

## EX-14 — Business Rule / Constraint Contradicting Authoritative Source & Project Constraint (Vietnamese, Business Rule Doc)
- **Artifact Type:** `business-rule-doc` · **Requirement Type:** Business Rule · **Language:** `vi`
- **Requirement (`BR-TAX-009`):**
  > "Đối với hóa đơn bán lẻ có tổng giá trị thanh toán từ 20.000.000 VNĐ trở lên, Hệ thống Thanh toán phải cho phép khách hàng hoàn tất giao dịch bằng tiền mặt tại quầy mà không cần xác thực định danh."
- **Supplied Context:**
  - Authoritative parent regulation (`REG-PAY-01` in project context): Giao dịch từ 20.000.000 VNĐ trở lên bắt buộc thanh toán qua chuyển khoản ngân hàng đã định danh, không chấp nhận tiền mặt.
  - Technical/operational constraint (`CON-POS-02`): Quầy thu ngân không được phép nhận tiền mặt cho hóa đơn $\ge$ 20.000.000 VNĐ.
- **Evaluation Summary:**
  - `RQ-03`, `RQ-04`, `RQ-05`, `RQ-07`: **`Compliant`** (câu viết rất rõ ràng, đầy đủ, đơn nhất và kiểm thử được!).
  - `RQ-08` (`Correct`): **`Issue`** (`confirmed-issue`, `critical`, rule `RQ-R013`) — mâu thuẫn trực tiếp với quy định nguồn `REG-PAY-01`.
  - `RQ-06` (`Feasible`): **`Issue`** (`confirmed-issue`, `major`, rule `RQ-R011`) — vi phạm ràng buộc vận hành `CON-POS-02`.

---

## EX-15 — Edge Case Where Criteria Are Genuinely `Not Applicable` (English, Requirement Table)
- **Artifact Type:** `requirement-table` · **Language:** `en`
- **Case 15A — Non-Normative Section Container Row (`SEC-HDR-04`):**
  - **Item (`SEC-HDR-04`, `row_type: section-header`):** `"4.2 Inventory Reservation and Stock Allocation Rules"`
  - **Evaluation:** Because the table row is explicitly tagged as a non-normative section container header (`row_type: section-header`) grouping child requirements, `RQ-01` .. `RQ-08` are genuinely **`Not Applicable`**.
- **Case 15B — Top-Level Axiomatic Business Policy (`POL-CORE-001`):**
  - **Item (`POL-CORE-001`, `is_primary_authoritative_source: true`):** `"The base accounting currency of the general ledger shall be USD (ISO 4217)."`
  - **Supplied Context:** Declared as the top-level axiomatic business policy in the charter with no higher parent source; project explicitly sets `formatting_conventions: not-applicable` for charter axioms.
  - **Evaluation:** `RQ-08` (`Correct` against a parent source) and `RQ-09` (`Conforming` to formatting templates) are **`Not Applicable`**; `RQ-02`, `RQ-03`, `RQ-04`, `RQ-05`, `RQ-07` are **`Compliant`**.
