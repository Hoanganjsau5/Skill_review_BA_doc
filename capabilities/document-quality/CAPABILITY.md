---
asset_type: capability
id: document-quality
version: 0.1.0
status: draft
assessment_layer: document-quality
profiles: [requirements-review, design-review, architecture-review, database-review, diagram-review, qa-review, traceability, integration-review]
phases: [4, 5, 8, 9]
output_contracts: [finding]
project_config_inputs: [review-config]
---

# Document Quality Assessment

## 1. Primary question
Tài liệu có đúng, đầy đủ, rõ ràng, nhất quán, đúng cấu trúc, truy vết được, kiểm thử được và phù hợp tiêu chuẩn/quy ước áp dụng không?

## 2. Scope
- In scope: chất lượng tài liệu và thiết kế được mô tả trong tài liệu.
- Out of scope: tính khả thi của giải pháp (→ `feasibility-risk`).

## 3. Composition
| Profile | Phase | Phụ thuộc |
|---|---|---|
| requirements-review, design-review, architecture-review, database-review, diagram-review, qa-review | 4 | — (song song) |
| traceability | 4 | Các `*-review` của artifacts liên quan |
| integration-review | 4 | `design-review`, `architecture-review` liên quan |

Chỉ tạo Assignment cho Profile có artifact trong scope (`orchestrator/routing-rules.md`).

## 4. Inputs / Outputs
- Inputs: artifacts, Skills của Profiles, `consistency-rules.yaml`.
- Outputs: `finding[]` (gồm Document Findings, Requirement/Design Gaps, Inconsistencies, Traceability Issues, Improvement Suggestions — phân biệt bằng `category` và `classification`), `early_feasibility_signals[]`.

## 5. Aggregation rules (internal-convention)
- **AGG-DQ-001:** Không gộp Finding gốc; duplicate → consolidated group (conflict-resolution §5).
- **AGG-DQ-002:** Tóm tắt theo artifact → category → severity.
- **AGG-DQ-003:** Finding `expert-judgment` được báo cáo tách riêng thành "Tín hiệu bổ sung tiêu chí".
- **AGG-DQ-004:** Mọi coverage gap (Skill không dùng được) phải được nêu trong phần Document Quality của report, kèm Profile bị ảnh hưởng.

## 6. Verdict rules
Capability này **không đưa verdict tổng thể** về chất lượng tài liệu ở phiên bản 0.1.0. Có thể bổ sung "document quality gate" khi dự án định nghĩa tiêu chí (tương lai).

## 7. Domain-agnostic consistency rules
Xem [`consistency-rules.yaml`](consistency-rules.yaml).

## 8. Limitations
- Chất lượng đánh giá phụ thuộc Skill có sẵn; hiện chưa có Skill validated.
