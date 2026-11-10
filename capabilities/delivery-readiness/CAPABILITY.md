---
asset_type: capability
id: delivery-readiness
version: 0.1.0
status: draft
assessment_layer: cross-layer
profiles: [delivery-readiness]
phases: [7, 8, 9]
output_contracts: [delivery-readiness]
project_config_inputs: [review-config, definition-of-ready]
---

# Delivery Readiness Assessment

Quyết định: [ADR-0003](../../docs/adr/ADR-0003-delivery-readiness-as-capability.md) — Cross-domain Capability, không có Core Agent riêng.

## 1. Primary question
Scope được chọn đã đủ chuẩn bị để chuyển sang stage tiếp theo (Development, Testing, …) chưa?

## 2. Scope
- In scope: đối chiếu kết quả Document Quality + Feasibility & Risk với **DoR do dự án định nghĩa** cho `target_stage`.
- Out of scope: định nghĩa DoR (thuộc dự án); hệ thống **không áp đặt DoR phổ quát**.

## 3. Composition
| Profile | Phase | Phụ thuộc |
|---|---|---|
| delivery-readiness | 7 | `document-quality` + `feasibility-risk` của cùng scope |

## 4. Inputs / Outputs
- Inputs: Findings, Risks, Feasibility assessment, `config/definition-of-ready.yaml`, `review-config.target_stage`.
- Output: `delivery-readiness`.

## 5. Aggregation rules (internal-convention)
- **AGG-DR-001:** Mỗi DoR criterion có trạng thái `met | unmet | unknown`, kèm evidence hoặc tham chiếu Finding/Risk.
- **AGG-DR-002:** `blocking_issues` chỉ gồm vấn đề vi phạm DoR criterion `mandatory` hoặc được DoR định nghĩa là blocking.

## 6. Verdict rules (internal-convention)
Áp dụng theo thứ tự:
- **VR-DR-001:** Không có DoR cho `target_stage` → `insufficient-evidence`.
- **VR-DR-002:** Có DoR criterion `mandatory` ở trạng thái `unmet` → `not-ready`.
- **VR-DR-003:** Có DoR criterion `mandatory` ở trạng thái `unknown` → `insufficient-evidence`.
- **VR-DR-004:** Mọi criterion `mandatory` đều `met`, nhưng còn criterion không bắt buộc `unmet`/`unknown` hoặc còn điều kiện → `ready-with-conditions` (liệt kê `outstanding_prerequisites`).
- **VR-DR-005:** Mọi criterion đều `met`, không có điều kiện → `ready`.

## 7. Verdict coherence rules
- **VC-DR-001:** Feasibility overall `not-feasible` cho cùng scope mà Readiness là `ready`/`ready-with-conditions` → CF-VERDICT (trừ khi có lý do được ghi nhận).
- **VC-DR-002:** Readiness `ready` trong khi còn `confirmed-issue` `critical` chưa giải quyết trong scope → CF-VERDICT.

## 8. Limitations
- Chất lượng đánh giá phụ thuộc chất lượng DoR do dự án cung cấp.
