# ADR-0007: Conflict Resolution Protocol

- Status: Accepted
- Date: 2026-11-10

## Context
Nhiều Agent có thể đưa kết luận khác nhau. Cần xử lý minh bạch mà không thêm Agent, không để Orchestrator tự phán đoán chuyên môn, và không ghi đè kết quả.

## Decision
- Thực hiện bởi **Orchestrator** theo thủ tục (`orchestrator/conflict-resolution.md`). Phán đoán chuyên môn → Critic (Assignment riêng) hoặc con người.
- Phân loại: CF-DUP, CF-SCOPE, CF-ASSUMP, CF-CONTRA, CF-RATING, CF-VERDICT, CF-CRITIC.
- Đối chiếu scope/artifact hash/assumptions trước, rồi evidence theo procedural criteria; không xếp hạng theo Agent.
- Re-validation có giới hạn (mặc định 1 lượt/conflict).
- Output gốc bất biến; quyết định ghi trong `conflict-record` (schema riêng) kèm rationale và `decided_by`.
- HITL bắt buộc khi: evidence chưa đủ sau re-validation; phụ thuộc sự thật/quyết định dự án; ảnh hưởng verdict hoặc severity cao nhất; Critic reject output ảnh hưởng verdict.
- Rating chưa giải quyết: hiển thị cả hai, tạm dùng mức cao hơn, gắn cờ (internal-convention).

## Consequences
- (+) Minh bạch, truy vết được, không thêm Agent.
- (−) Có thể tăng số câu hỏi HITL; verdict có thể bị hạ về `insufficient-evidence` khi chưa có phản hồi.

## Ghi chú: Logical vs Physical
Các thành phần trong protocol (Orchestrator, Critic) là thành phần logic; xem `docs/ARCHITECTURE.md` §7.
