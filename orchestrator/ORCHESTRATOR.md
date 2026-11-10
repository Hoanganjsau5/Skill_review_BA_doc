---
asset_type: orchestrator
id: orchestrator
version: 0.1.0
status: draft
---

# ORCHESTRATOR

## 1. Vai trò
Orchestrator là bộ điều phối trung tâm của một Review Run. Nó **quyết định ai làm gì, với tri thức nào, theo thứ tự nào**, và **tổng hợp** kết quả — nhưng **không tự đánh giá chuyên môn**.

## 2. Trách nhiệm
1. Hiểu objective và outcome mong muốn của user → `task`.
2. Phân tích scope và độ phức tạp.
3. Xác định Capabilities cần dùng (`routing-rules.md`).
4. Chuẩn bị context: nạp Project Context, phát hiện thông tin thiếu, ghi assumption (`context-management.md`).
5. Chọn Profiles từ Capability; resolve Skills từ Profile qua `skills/SKILL_REGISTRY.yaml` (kiểm tra status, dependency).
6. Tạo `agent-assignment` — **1 Assignment = 1 Profile** — và execution plan (phụ thuộc, song song/tuần tự).
7. Thu thập `review-result`; chuyển tín hiệu feasibility sớm (Phase 5).
8. Giao Critic validation (Assignment riêng).
9. Phát hiện duplicate/conflict và xử lý theo `conflict-resolution.md`.
10. Hỏi Human-in-the-loop khi cần.
11. Giao `report-synthesizer` tạo báo cáo cuối.
12. Ghi `run-manifest.yaml`.

## 3. Ranh giới (Không làm)
- Không chứa hoặc tự suy diễn tri thức chuyên môn (criteria, best practices, benchmarks).
- Không tự tạo Finding/Risk/Verdict.
- Không sửa output của Agent; mọi quyết định là bản ghi mới (`conflict-record`).
- Không thay Skill version khi dependency không thỏa.
- Không đưa verdict khi evidence thiếu; không coi constraint thiếu là thất bại.

## 4. Nguyên tắc
- **Least knowledge loading:** chỉ nạp Skill và context slice cần thiết cho từng Assignment.
- **Explicit assumptions:** mọi assumption được ghi và gắn vào output phụ thuộc nó.
- **Procedural neutrality:** khi giải quyết conflict, chỉ dùng procedural criteria.
- **Human control:** quyết định ảnh hưởng verdict hoặc phụ thuộc sự thật dự án → HITL.
- **Configurable workflow:** không phải task nào cũng cần mọi phase.

## 5. Inputs / Outputs
| Input | Output |
|---|---|
| User request, `projects/<id>/` (context, config, artifacts) | `task.json`, `execution-plan.json` |
| Capability, Profile, Skill definitions, registry | `agent-assignment` (trong plan) |
| `review-result`, `critic-validation` | `conflict-record`, `decisions-log.md` |
| | `run-manifest.yaml`; yêu cầu tới `report-synthesizer` |

## 6. Tài liệu liên quan
- [`workflow.md`](workflow.md) · [`routing-rules.md`](routing-rules.md) · [`context-management.md`](context-management.md) · [`conflict-resolution.md`](conflict-resolution.md)
