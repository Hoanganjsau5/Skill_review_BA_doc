# ADR-0006: Finding Reference Model

- Status: Accepted
- Date: 2026-11-10

## Context
Không phải mọi Finding đều xuất phát từ một evaluation criterion. Finding của `cross-artifact-analyzer` xuất phát từ phân tích/so sánh giữa artifacts. Ép mọi Finding gắn criterion dẫn đến tham chiếu sai hoặc bỏ sót vấn đề thật khi thư viện Skill còn mỏng.

## Decision
Finding có trường `basis` bắt buộc, đúng một loại:

| basis.type | Tham chiếu | Producer |
|---|---|---|
| `criterion` | `criterion_ref` (skill@version#criterion_id) | artifact-reviewer |
| `analysis-rule` | `analysis_rule_ref` (owner@version#rule_id) | cross-artifact-analyzer |
| `comparison-rule` | `comparison_rule_ref` (owner@version#rule_id) | cross-artifact-analyzer |
| `expert-judgment` | — | artifact-reviewer, cross-artifact-analyzer |

- `owner` = Skill (rule domain-specific, trong `rules.yaml`) hoặc Capability (rule domain-agnostic, trong `capabilities/document-quality/consistency-rules.yaml`).
- Mọi Finding: `evidence` ≥ 1, `rationale` bắt buộc, `producer` (assignment, core agent, profile).
- `comparison-rule`: ≥ 2 evidence từ ≥ 2 artifact khác nhau.
- `expert-judgment`: không được `confirmed-issue`; bắt buộc qua Critic; được tổng hợp làm tín hiệu bổ sung criterion/rule cho Skill.

## Consequences
- (+) Phản ánh đúng bản chất từng loại phân tích; không ép tham chiếu giả.
- (−) Schema Finding phức tạp hơn (dùng `oneOf`).
