# Synthetic Examples — `re.requirement-validation`

All examples below are synthetic, domain-agnostic illustrations designed to clarify how `re.requirement-validation` evaluates **alignment between requirements and stakeholder needs, business objectives, authoritative policies, and operational concepts** without overlapping `re.requirement-quality`, `re.requirement-set-quality`, or `re.requirement-traceability`.

---

## Example 1: Partial Need Coverage (`RVAL-01` / `RVAL-R002`)

**Input Context:**
- **Stakeholder Need `SN-04` (Warehouse Operations Director):** "Warehouse supervisors need real-time visibility into cold-chain temperature excursions **and** automated SMS/push alerts within 60 seconds whenever a freezer unit exceeds $-15^\circ\text{C}$ so perishable inventory can be rescued."
- **Specified Requirement `REQ-MON-01`:** "The Monitoring Dashboard shall display the current temperature of each freezer unit refreshed every 30 seconds and highlight readings above $-15^\circ\text{C}$ in red."
- *(No requirement in the full SRS specifies automated SMS/push alerts when a threshold excursion occurs).*

**Expected Assessment:**
- **Criterion:** `RVAL-01` (`issue_found`), **Rule:** `RVAL-R002`, **Severity:** `high`.
- **Reasoning:** Even if a traceability matrix links `SN-04` $\leftrightarrow$ `REQ-MON-01` (so `re.requirement-traceability` sees a link), `REQ-MON-01` only satisfies passive dashboard viewing and omits the automated active alert required to rescue perishable inventory when a supervisor is not watching the screen.

---

## Example 2: Stakeholder Intent Distortion in Vietnamese (`RVAL-02` / `RVAL-R003`)

**Input Context (Language: `vi`):**
- **Nhu cầu Stakeholder `NEED-02` (Khách hàng doanh nghiệp):** "Khách hàng cần tự tải xuống Hóa đơn GTGT điện tử ngay lập tức trên cổng thông tin tự phục vụ (Self-service Portal) sau khi thanh toán thành công."
- **Yêu cầu phần mềm `REQ-INV-05`:** "Sau khi thanh toán thành công, hệ thống phải cho phép khách hàng gửi biểu mẫu yêu cầu cấp hóa đơn để Nhân viên Kế toán kiểm tra và gửi qua email trong vòng 3 ngày làm việc."

**Expected Assessment:**
- **Criterion:** `RVAL-02` (`issue_found`), **Rule:** `RVAL-R003`, **Severity:** `high`.
- **Reasoning:** `REQ-INV-05` is well-written, verifiable, and consistent in itself, but it replaces immediate self-service download with a 3-business-day manual back-office ticket workflow, contradicting the stakeholder's core intent.

---

## Example 3: Business Objective & KPI Conflict (`RVAL-03` / `RVAL-R005`)

**Input Context:**
- **Business Objective `BO-01`:** "Achieve $\ge 90\%$ straight-through automated approval for micro-loans under \$500 with end-to-end decision time under 2 minutes."
- **Requirement `REQ-LOAN-08`:** "Every loan application regardless of requested amount shall be routed to the Senior Credit Officer queue for manual document review prior to approval."

**Expected Assessment:**
- **Criterion:** `RVAL-03` (`issue_found`), **Rule:** `RVAL-R005`, **Severity:** `critical`.
- **Reasoning:** Mandating $100\%$ manual review for all loan amounts reduces straight-through automated approval to $0\%$, directly defeating `BO-01`.

---

## Example 4: Boundary Between Validation (`re.requirement-validation`) and Traceability (`re.requirement-traceability`)

**Input Context:**
- **Stakeholder Need `SN-01`:** "Allow patients to reschedule appointments up to 12 hours before the scheduled slot."
- **Requirement `REQ-APT-02`:** "The Patient Portal shall allow a patient to reschedule a confirmed appointment to another available slot provided the request is submitted at least 12 hours before the scheduled start time."
- **Traceability Attribute on `REQ-APT-02`:** `source_need_id: null` (missing backward link).

**Expected Assessment by `re.requirement-validation`:**
- **`RVAL-01` & `RVAL-02`:** `Compliant` (No validation defect).
- **Reasoning:** Semantically, `REQ-APT-02` completely and accurately fulfills `SN-01`. The missing `source_need_id` attribute is a structural link omission owned exclusively by **`re.requirement-traceability` (`RTR-01`)**.
