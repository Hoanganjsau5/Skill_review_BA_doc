# Synthetic Examples — `re.requirement-traceability`

All examples below are synthetic, domain-agnostic illustrations designed to clarify how `re.requirement-traceability` evaluates **structural traceability relationships across lifecycle layers** without overlapping `re.requirement-quality`, `re.requirement-set-quality`, or `re.requirement-validation`.

---

## Example 1: Bidirectional Asymmetry in Vietnamese SRS & Test Suite (`RTR-03` / `RTR-R004`)

**Input Context (Language: `vi`):**
- **SRS Trace Table:** `REQ-PAY-01` ("Thanh toán qua thẻ nội địa NAPAS") lists Forward Test Links: `["TC-PAY-01", "TC-PAY-02"]`.
- **Test Suite Specification:**
  - `TC-PAY-01` lists Covered Requirement: `["REQ-PAY-01"]`.
  - `TC-PAY-02` lists Covered Requirement: `["REQ-PAY-05"]` (omits `REQ-PAY-01`).

**Expected Assessment:**
- **Criterion:** `RTR-03` (`issue_found`), **Rule:** `RTR-R004`, **Severity:** `medium`.
- **Reasoning:** The forward link `REQ-PAY-01` $\to$ `TC-PAY-02` in the SRS is contradicted by the backward link on `TC-PAY-02` $\to$ `REQ-PAY-05` in the Test Suite.

---

## Example 2: Broken Target ID & Deprecated Origin Link (`RTR-04` / `RTR-R005`, `RTR-R006`)

**Input Context:**
- **Stakeholder Needs Inventory:**
  - `SN-01` (`status: Active`): "Support automated recurring billing."
  - `SN-02` (`status: Deprecated`): "Support legacy fax invoice dispatch."
- **Test Cases Inventory:** `TC-01`, `TC-02`.
- **RTM Row for `REQ-BILL-04` (`status: Active`):**
  - `backward_need_id: "SN-02"` (Deprecated!)
  - `forward_test_id: "TC-99"` (Does not exist in Test Cases Inventory!)

**Expected Assessment:**
- **Criterion:** `RTR-04` (`issue_found`), **Rules:** `RTR-R005` (broken target `TC-99`) and `RTR-R006` (link to deprecated origin `SN-02`), **Severity:** `high`.

---

## Example 3: Bogus Copy-Paste Trace Link (`RTR-05` / `RTR-R008`)

**Input Context:**
- `REQ-SEC-04`: "The Authentication Service shall lock a user account for 30 minutes after 5 consecutive failed TOTP verification attempts."
- `TC-SHIP-12`: "Verify that domestic ground shipping fee is \$0.00 when cart subtotal exceeds \$75.00."
- **RTM Entry:** `REQ-SEC-04` $\to$ `verified_by: ["TC-SHIP-12"]`.

**Expected Assessment:**
- **Criterion:** `RTR-05` (`issue_found`), **Rule:** `RTR-R008`, **Severity:** `high`.
- **Reasoning:** Both `REQ-SEC-04` and `TC-SHIP-12` exist and have valid IDs (`RTR-01`, `RTR-02`, `RTR-04` pass), but `TC-SHIP-12` tests freight shipping discounts and has zero topical relevance to TOTP account lockout (`REQ-SEC-04`).

---

## Example 4: Boundary Between Traceability (`re.requirement-traceability`) and Validation (`re.requirement-validation`)

**Input Context:**
- `SN-10` (`status: Active`): "Allow customers to cancel an unshipped order self-service with a full 100% refund."
- `REQ-ORD-10` (`status: Active`, `source_need_id: "SN-10"`, `verified_by: ["TC-ORD-10"]`): "When a customer cancels an unshipped order self-service, the Order Service shall deduct a 25% cancellation penalty."
- `TC-ORD-10` (`status: Active`, `covers_req_id: "REQ-ORD-10"`): "Verify that cancelling an unshipped order deducts a 25% cancellation penalty."

**Expected Assessment by `re.requirement-traceability`:**
- **`RTR-01` .. `RTR-06`:** `Compliant`.
- **Reasoning:** Every link (`SN-10` $\leftrightarrow$ `REQ-ORD-10` $\leftrightarrow$ `TC-ORD-10`) exists, resolves to an active ID, is bidirectionally symmetric, and addresses the exact same topic (Customer Order Cancellation). The fact that `REQ-ORD-10` charges a $25\%$ penalty instead of the $0\%$ fee requested in `SN-10` is a **semantic intent distortion** owned exclusively by **`re.requirement-validation` (`RVAL-02` / `RVAL-R003`)**.
