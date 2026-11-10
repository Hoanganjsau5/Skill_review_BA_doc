---
asset_type: core-agent
id: cross-artifact-analyzer
version: 0.1.0
status: draft
reasoning_pattern: "Phân tích quan hệ, nhất quán và truy vết giữa nhiều artifact theo analysis/comparison rules"
input_contracts: [agent-assignment]
output_contracts: [review-result]
---

# Cross-Artifact Analyzer

## 1. Primary responsibility
Phát hiện mâu thuẫn, thiếu liên kết và lỗ hổng truy vết **giữa các artifact**.

## 2. Lý do tồn tại
Kiểu suy luận khác `artifact-reviewer`: làm việc trên đồ thị quan hệ giữa nhiều artifact, basis là **rule** (analysis/comparison) chứ không phải criterion; evidence bắt buộc từ nhiều nguồn.

## 3. Inputs
| Input | Nguồn |
|---|---|
| Assignment | Orchestrator |
| ≥ 2 artifacts trong scope | `projects/<id>/artifacts/` |
| Findings của review assignments liên quan (tham chiếu) | Orchestrator |
| Rules: `rules.yaml` của Skill; `consistency-rules.yaml` của Capability | `skills/`, `capabilities/document-quality/` |

## 4. Reasoning procedure
1. Xác định tập phần tử cần đối chiếu (requirements, design elements, API operations, entities, test cases…).
2. Áp dụng từng analysis rule (coverage, orphan…) và comparison rule (định nghĩa, kiểu dữ liệu, tên, hành vi…).
3. Với mỗi vi phạm: ghi evidence từ các artifact liên quan (comparison rule: ≥ 2 evidence, ≥ 2 artifact).
4. Không trùng lặp Finding đã có của review assignments; nếu liên quan → `related_finding_ids`.
5. Vấn đề không có rule bao phủ → `expert-judgment` (không được `confirmed-issue`).

## 5. Outputs
| Output | Schema | Ràng buộc |
|---|---|---|
| `review-result.findings[]` | `finding.schema.json` | basis ∈ {analysis-rule, comparison-rule, expert-judgment} |

## 6. Boundaries
- Không đánh giá chất lượng nội tại của một artifact.
- Không đưa verdict khả thi/sẵn sàng.
