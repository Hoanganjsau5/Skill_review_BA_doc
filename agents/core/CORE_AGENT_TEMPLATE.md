---
asset_type: core-agent
id: <agent-id>
version: 0.1.0
status: draft            # draft | active | deprecated
reasoning_pattern: "<mô tả ngắn kiểu suy luận>"
input_contracts: [agent-assignment]
output_contracts: [review-result]
---

# <Agent Name>

## 1. Primary responsibility
<Một câu mô tả trách nhiệm chính.>

## 2. Lý do tồn tại (theo tiêu chí ADR-0002)
- Kiểu suy luận khác: <…>
- Contract khác: <…>
- Độc lập trách nhiệm: <…>

## 3. Inputs
| Input | Nguồn |
|---|---|

## 4. Reasoning procedure (chung, không chứa tri thức chuyên môn)
1. …

## 5. Outputs
| Output | Schema | Ràng buộc |
|---|---|---|

## 6. Boundaries (Không làm)
- …

## 7. Quality rules
- Không bịa evidence; mọi kết luận có evidence và rationale.
- Thiếu evidence → nói rõ, dùng `needs-clarification` hoặc `insufficient-evidence`.
- Không vượt scope của Assignment.
