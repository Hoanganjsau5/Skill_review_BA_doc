# Synthetic Examples — `re.requirement-set-quality`

All examples below are synthetic, domain-agnostic illustrations designed to clarify how `re.requirement-set-quality` evaluates a **collection of requirements** without overlapping `re.requirement-quality`, `re.requirement-validation`, or `re.requirement-traceability`.

---

## Example 1: Scope Coverage Omission (`RSQ-01` / `RSQ-R001`)

**Input Context (`completeness_mode: "full"`):**
- **Declared Scope (Section 1.2):** "Release 1.0 covers three core modules: (1) Inventory Catalog Management, (2) Purchase Order Creation, and (3) Supplier Return & RMA Processing."
- **Full Requirement Set (`REQ-001` .. `REQ-018`):** Contains 10 requirements for Inventory Catalog Management and 8 requirements for Purchase Order Creation, and **0 requirements** for Supplier Return & RMA Processing.

**Expected Assessment:**
- **Criterion:** `RSQ-01` (`issue_found`), **Rule:** `RSQ-R001`, **Severity:** `high`.
- **Reasoning:** Each individual requirement in `REQ-001..018` is well-written (`re.requirement-quality` passes), but the **set** omits an entire module explicitly declared in-scope in Section 1.2.

---

## Example 2: Missing Companion Lifecycle Transition in Vietnamese SRS (`RSQ-02` / `RSQ-R002`)

**Input Context (`completeness_mode: "full"`, Language: `vi`):**
- `REQ-AUTH-01`: "Khi người dùng nhập sai mật khẩu 5 lần liên tiếp, hệ thống phải chuyển trạng thái tài khoản sang `LOCKED` và từ chối mọi yêu cầu đăng nhập."
- `REQ-AUTH-02`: "Khi tài khoản ở trạng thái `ACTIVE`, người dùng có thể đổi mật khẩu sau khi xác thực OTP."
- *(No other requirements in the Authentication set mention `LOCKED` or unlocking/expiration).*

**Expected Assessment:**
- **Criterion:** `RSQ-02` (`issue_found`), **Rule:** `RSQ-R002`, **Severity:** `high`.
- **Reasoning:** `REQ-AUTH-01` is completely clear and verifiable on its own (`RQ-03`, `RQ-07` pass), but at the **set level**, the `LOCKED` state is a dead-end trap because no requirement in the set specifies how a `LOCKED` account is unlocked (auto-expiry after $N$ minutes, self-service reset, or administrator unlock).

---

## Example 3: Pairwise Threshold & Behavioral Contradiction (`RSQ-03` / `RSQ-R004`, `RSQ-R005`)

**Input Context (`completeness_mode: "full"`):**
- `REQ-ORD-04` (Section 3.1 Order Lifecycle): "The customer shall be permitted to cancel a confirmed order free of charge up to **24 hours** after order placement, provided the order status is `CONFIRMED`."
- `REQ-BILL-09` (Section 4.2 Billing & Refunds): "Any cancellation of an order in `CONFIRMED` status submitted more than **2 hours** after order placement shall incur a 15% restocking fee."

**Expected Assessment:**
- **Criterion:** `RSQ-03` (`issue_found`), **Rule:** `RSQ-R004` / `RSQ-R005`, **Severity:** `critical`.
- **Reasoning:** For any `CONFIRMED` order cancelled between 2 hours and 24 hours after placement, `REQ-ORD-04` mandates $0\%$ fee while `REQ-BILL-09` mandates a $15\%$ fee. Both requirements are individually unambiguous, so `re.requirement-quality` passes both; only set-level comparison (`re.requirement-set-quality`) catches the contradiction.

---

## Example 4: False-Positive Prevention on Partial Requirement Slice (`RSQ-01`, `RSQ-02` -> `not_assessable`)

**Input Context (`completeness_mode: "partial"`):**
- Only Section 3.2 ("Checkout Payment Authorization" — `REQ-PAY-01` .. `REQ-PAY-03`) is provided for review. Section 1.2 Scope mentions "Guest Checkout, Loyalty Points, and Monthly Invoicing".

**Expected Assessment:**
- **Criteria `RSQ-01` & `RSQ-02`:** `not_assessable` (Observation only, NOT a defect finding).
- **Reasoning:** Because `completeness_mode` is `"partial"`, the absence of Loyalty Points and Monthly Invoicing requirements in the 3-requirement snippet is expected and must not be reported as a scope gap.
