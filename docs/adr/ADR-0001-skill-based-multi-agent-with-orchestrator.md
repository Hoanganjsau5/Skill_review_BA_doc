# ADR-0001: Skill-based Multi-Agent System với Central Orchestrator

- Status: Accepted
- Date: 2026-11-10

## Context
Cần một hệ thống đánh giá tài liệu kỹ thuật và tính khả thi giải pháp, tái sử dụng được cho nhiều dự án. Một prompt lớn duy nhất khó bảo trì, khó truy vết, và trộn lẫn tri thức chuyên môn với điều phối.

## Decision
Áp dụng kiến trúc **Skill-based Multi-Agent + Central Orchestrator**:
- Orchestrator điều phối, không chứa tri thức chuyên môn.
- Tri thức chuyên môn tách thành Skill tái sử dụng, độc lập dự án.
- Agent là executor, được cấp Skill động theo Assignment.
- Knowledge Base, Tools, Schemas, Project Context là các thành phần tách biệt.

## Consequences
- (+) Tái sử dụng Skill giữa dự án và giữa Agent; thay đổi tri thức không đụng tới điều phối.
- (+) Có thể truy vết kết quả về Skill/criterion/source.
- (−) Nhiều thành phần cần quản lý version và contract.
- (−) Chưa có Skill validated thì hệ thống chưa hoạt động thực tế.

## Alternatives considered
- Single giant prompt: bị loại (không mở rộng, không truy vết).
- Một Agent cho mỗi loại tài liệu: bị loại (Agent proliferation, trùng lặp logic) — xem ADR-0002.
