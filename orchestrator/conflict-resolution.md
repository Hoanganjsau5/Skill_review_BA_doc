# Conflict Resolution Protocol

Version: 0.1.0 · Quyết định: [ADR-0007](../docs/adr/ADR-0007-conflict-resolution-protocol.md) · Contract: `schemas/runtime/conflict-record.schema.json`

Thực hiện bởi Orchestrator. Orchestrator chỉ áp dụng **procedural criteria**; phán đoán chuyên môn được giao cho `critic` (Assignment riêng) hoặc con người.

## 1. Phân loại

| Mã | Loại | Dấu hiệu | Conflict thật? |
|---|---|---|---|
| `CF-DUP` | Duplicate | Cùng artifact/location/entity, cùng nhận định | Không — gom nhóm |
| `CF-SCOPE` | Scope/version mismatch | Kết luận khác nhau trên artifact hash/scope/section khác nhau | Giả conflict |
| `CF-ASSUMP` | Assumption conflict | Dùng giả định khác nhau về cùng context | Có |
| `CF-CONTRA` | Contradictory findings | Cùng đối tượng, nhận định trái ngược | Có |
| `CF-RATING` | Severity/classification disagreement | Cùng vấn đề, khác severity/classification | Có |
| `CF-VERDICT` | Verdict incoherence | Vi phạm verdict coherence rules của Capability | Có |
| `CF-CRITIC` | Critic challenge/reject | Critic trả `challenged`/`rejected` | Có |

## 2. Quy trình

1. **Detect & classify** → tạo `conflict-record` (`status: open`).
2. **So scope:** artifact `content_hash`, section, scope, assumptions. Khác → `CF-SCOPE`, giữ cả hai, chú thích, `status: resolved-as-scope-difference`.
3. **Đối chiếu evidence** theo procedural criteria (§3).
4. Evidence đủ phân định → ghi quyết định (`accepted_refs`, `rejected_refs`, `rationale`, `decided_by: orchestrator-procedural`).
5. Chưa đủ và còn lượt re-validation → tạo Assignment mới (critic, hoặc producer profile) với câu hỏi hẹp + evidence của cả hai phía → quay lại bước 3.
6. Hết lượt hoặc thuộc trigger HITL (§6) → `status: escalated` → hỏi con người → ghi quyết định (`decided_by: human:<id>`) hoặc `status: unresolved`.

## 3. Procedural criteria (không xếp hạng theo Agent)
1. Evidence trích dẫn trực tiếp với location cụ thể > suy luận gián tiếp.
2. Basis có `authority_level` cao hơn; Skill effective status `validated` > `draft` > `expert-judgment`.
3. Evidence phải bao phủ đúng đối tượng tranh chấp.
4. Assumption đã xác nhận > assumption tự đặt.

Không phân định được → "evidence chưa đủ". **Không chọn ngẫu nhiên.**

## 4. Không ghi đè
- Output gốc bất biến.
- Hiển thị trong report dựa trên trạng thái: `accepted`, `rejected`, `superseded_by`, `unresolved`.
- `CF-RATING` chưa giải quyết: hiển thị cả hai mức; mức hiệu lực tạm = mức cao hơn, gắn cờ `unresolved` (`unresolved_rating_policy`, configurable).

## 5. Duplicate
Tạo nhóm hợp nhất (`consolidated_group`) tham chiếu mọi Finding gốc; report hiển thị một mục kèm danh sách nguồn. Không xóa Finding gốc.

## 6. Trigger bắt buộc HITL
1. Evidence chưa đủ sau khi hết lượt re-validation.
2. Conflict phụ thuộc sự thật/quyết định của dự án (đặc biệt `CF-ASSUMP` về constraint, budget, kiến trúc).
3. Conflict ảnh hưởng Feasibility/Readiness verdict, hoặc liên quan Finding `critical`.
4. Critic `rejected` output ảnh hưởng verdict.

Chưa có phản hồi:
- Conflict giữ `unresolved`.
- Verdict bị ảnh hưởng được hạ thành `insufficient-evidence` hoặc `conditionally-feasible` / `ready-with-conditions` kèm điều kiện tường minh.
- Đưa vào mục *Unresolved Questions* của report.

## 7. Cấu hình
| Key | Default |
|---|---|
| `max_revalidation_rounds_per_conflict` | 1 |
| `unresolved_rating_policy` | `show-both-use-higher-flagged` |
