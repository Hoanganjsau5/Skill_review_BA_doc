# ADR-0005: Ranh giới Knowledge Base và Skill Library

- Status: Accepted
- Date: 2026-11-10

## Context
Cần tránh (a) Skill chỉ là bản sao tài liệu nguồn, (b) tiêu chí đánh giá không rõ nguồn gốc, (c) trộn tri thức chung với dữ liệu dự án.

## Decision
| | Knowledge Base | Skill Library |
|---|---|---|
| Bản chất | Nguồn gốc (registry, tóm tắt chuẩn, references, research notes) | Tri thức chuẩn hóa: procedure, criteria, rules, checklist |
| Dùng khi | Xây dựng/cập nhật Skill; Critic kiểm chứng nguồn | Thực hiện review |
| Runtime | Không nạp mặc định | Chỉ nạp Skill được chọn |
| Dữ liệu dự án | Không | Không |

- Mỗi criterion/rule có `source_refs` (`source_id` + locator) trỏ tới `knowledge/source-registry.yaml` và `synthesis_note` diễn giải — không sao chép nguyên văn dài.
- Pipeline 7 bước: register source → research note → synthesize → procedure → criteria/rules → validate bằng examples → version + `last_verified_at`.
- `project-decision` không được xuất hiện trong Skill.

## Consequences
- (+) Chuỗi truy vết Finding → Criterion/Rule → Source.
- (−) Xây dựng Skill tốn công nghiên cứu (chủ đích).
