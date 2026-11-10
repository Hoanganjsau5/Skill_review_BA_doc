---
asset_type: capability
id: feasibility-risk
version: 0.1.0
status: draft
assessment_layer: feasibility
profiles: [feasibility-risk]
phases: [5, 6, 8, 9]
output_contracts: [risk, feasibility-assessment]
project_config_inputs: [review-config, risk-assessment-method]
---

# Feasibility & Solution Assessment

## 1. Primary question
Giải pháp được đề xuất có thể được thực hiện và vận hành dưới ràng buộc thực tế của dự án không?

## 2. Scope — dimensions
| Dimension | Nội dung |
|---|---|
| `requirement-feasibility` | Yêu cầu xung đột, ràng buộc không tương thích, yêu cầu không thực tế, NFR conflicts |
| `technical-feasibility` | Kiến trúc, tương thích công nghệ, performance, scalability, integration complexity, infrastructure |
| `implementation-readiness` | Design đủ chi tiết, quyết định chưa giải quyết, API/data contracts, implementation dependencies, khả năng suy ra test cases |
| `external-dependencies` | Third-party APIs, external services, licenses, data availability, vendor limitations |
| `project-constraints` | Budget, timeline, team size/capabilities, infrastructure, mandatory technologies, operational constraints |

Out of scope: chất lượng tài liệu (→ `document-quality`); readiness theo DoR (→ `delivery-readiness`).

## 3. Composition
| Profile | Phase | Phụ thuộc |
|---|---|---|
| feasibility-risk | 5 (sớm, một phần scope) / 6 (hợp nhất) | Findings + early signals từ `document-quality` |

## 4. Inputs / Outputs
- Inputs: Findings, signals, Project Context slice, `risk-assessment-method.yaml` (tùy chọn), evidence do user cung cấp.
- Outputs: `risk[]`, `feasibility-assessment` (overall + dimension results).

## 5. Aggregation rules (internal-convention)
- **AGG-FR-001:** Risk tham chiếu Finding/assumption/evidence liên quan qua ID.
- **AGG-FR-002:** Không có risk method → likelihood/impact/risk_level = `not-assessed`.
- **AGG-FR-003:** Claim định lượng không có evidence hợp lệ → không được dùng làm căn cứ verdict.

## 6. Verdict rules (internal-convention)
Áp dụng theo thứ tự:
- **VR-FR-001:** Một dimension trong scope có kết luận `not-feasible`, có evidence và đã được Critic `validated` → overall `not-feasible`.
- **VR-FR-002:** Một dimension được đánh dấu *critical cho scope* thiếu evidence → overall `insufficient-evidence`.
- **VR-FR-003:** Mọi dimension khả thi nhưng có điều kiện, hoặc phụ thuộc assumption `material` chưa xác nhận → `conditionally-feasible` (bắt buộc liệt kê `conditions`).
- **VR-FR-004:** `feasible` chỉ khi mọi dimension trong scope `feasible`, không có assumption `material` chưa xác nhận, và verdict đã được Critic `validated`.
- **VR-FR-005:** Verdict luôn kèm scope, evidence, assumptions, conditions, constraints, confidence, unresolved_questions.

## 7. Verdict coherence rules
- **VC-FR-001:** Overall `feasible` nhưng có Risk được đánh giá ở mức cao nhất của risk method mà không có mitigation → CF-VERDICT.
- **VC-FR-002:** Dimension `feasible` nhưng tham chiếu Finding `confirmed-issue`/`critical` chưa được giải quyết trong cùng scope → CF-VERDICT.

## 8. Limitations
- Không thay thế benchmark/POC thực tế; khi cần, verdict là `insufficient-evidence` kèm đề xuất thu thập evidence.
