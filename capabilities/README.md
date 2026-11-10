# Capabilities

**Capability** = năng lực đánh giá tổng hợp. Capability ghép Profiles, định nghĩa phases, aggregation rules và verdict rules. Capability **không chứa tri thức chuyên môn**: tri thức nằm trong `skills/`.

| Capability | Layer | Câu hỏi | Profiles | Output |
|---|---|---|---|---|
| [document-quality](document-quality/CAPABILITY.md) | Layer 1 | Tài liệu có đúng, đủ, rõ, nhất quán, truy vết được, kiểm thử được không? | 6 `*-review`, `traceability`, `integration-review` | finding[] |
| [feasibility-risk](feasibility-risk/CAPABILITY.md) | Layer 2 | Giải pháp có khả thi dưới ràng buộc thực tế không? | `feasibility-risk` | risk[], feasibility-assessment |
| [delivery-readiness](delivery-readiness/CAPABILITY.md) | Cross-layer | Scope có sẵn sàng cho stage tiếp theo theo DoR của dự án không? | `delivery-readiness` | delivery-readiness |

## Ranh giới với Skill
| Skill | Capability |
|---|---|
| *Cách* đánh giá một khía cạnh chuyên môn (procedure, criteria, rules) | *Ghép* các đánh giá và *quy tắc* ra kết luận tổng hợp |
| Ví dụ: phương pháp phân tích xung đột yêu cầu | Ví dụ: khi nào verdict là `insufficient-evidence` |

Rule trong Capability chỉ được là **logic tổng hợp** hoặc **nhất quán domain-agnostic**, có `authority_level: internal-convention`.

## Thêm Capability mới
1. Copy [`CAPABILITY_TEMPLATE.md`](CAPABILITY_TEMPLATE.md).
2. Thêm task type mapping trong `orchestrator/routing-rules.md`.
3. Định nghĩa output schema nếu cần (cập nhật `schemas/`).
