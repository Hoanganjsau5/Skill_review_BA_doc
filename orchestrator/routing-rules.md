# Routing Rules

Version: 0.1.0

File này là **nơi duy nhất** định nghĩa ánh xạ **Task type → Capability**. Ánh xạ Capability → Profile nằm trong `capabilities/*/CAPABILITY.md`; Profile → Skill nằm trong `agents/profiles/*.md`.

## 1. Task type → Capabilities

| Task type | Mô tả | Capabilities |
|---|---|---|
| `document-review` | Đánh giá chất lượng tài liệu | `document-quality` |
| `feasibility-assessment` | Đánh giá khả thi giải pháp | `feasibility-risk` (+ `document-quality` ở mức cần thiết để có input) |
| `readiness-check` | Kiểm tra sẵn sàng cho stage tiếp theo | `document-quality`, `feasibility-risk`, `delivery-readiness` |
| `full-assessment` | Đánh giá toàn diện | `document-quality`, `feasibility-risk`, `delivery-readiness` |

Khi task không khớp rõ ràng một task type → Orchestrator đề xuất task type và hỏi user xác nhận.

## 2. Artifact type → Profile eligibility

Orchestrator chỉ tạo Assignment cho Profile khi scope có artifact thuộc `applies_to` của Profile (khai báo trong Profile). Bảng dưới đây chỉ là **tóm tắt tham khảo**; nguồn chân lý là Profile file.

| Artifact type | Profile(s) |
|---|---|
| `srs`, `use-case`, `user-story`, `acceptance-criteria` | requirements-review |
| `basic-design`, `detailed-design`, `api-spec` | design-review |
| `architecture-document` | architecture-review |
| `database-design`, `data-model` | database-review |
| `uml`, `bpmn`, `sequence-diagram`, `dfd`, `c4-diagram`, `erd` | diagram-review |
| `test-plan`, `test-design`, `test-cases` | qa-review |
| ≥ 2 loại artifact có quan hệ trace | traceability |
| `api-spec`/`architecture-document` của ≥ 2 service | integration-review |

## 3. Quy tắc bổ sung
- Không tạo Assignment khi Profile không có Skill nào dùng được → ghi `coverage_gap`.
- Một artifact có thể thuộc nhiều Profile (ví dụ ERD trong Database Design → `database-review` và `diagram-review`); mỗi Profile một Assignment.
