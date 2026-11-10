# Workflow

Version: 0.1.0 · Áp dụng bởi Orchestrator.

## 1. Tổng quan 10 phases

| Phase | Tên | Executor | Output chính | Bắt buộc? |
|---|---|---|---|---|
| 1 | Task Understanding | Orchestrator | `task.json` | Luôn |
| 2 | Context Preparation | Orchestrator (+HITL) | context slices, assumptions, clarification requests | Luôn |
| 3 | Skill & Agent Selection | Orchestrator | `execution-plan.json` (assignments) | Luôn |
| 4 | Document Quality Review | artifact-reviewer, cross-artifact-analyzer | `finding[]` | Nếu bật `document-quality` |
| 5 | Preliminary Feasibility Signals | Agent Phase 4 (ghi `early_feasibility_signals`) → Orchestrator | signals | Nếu bật `feasibility-risk` |
| 6 | Consolidated Feasibility Assessment | solution-assessor (`feasibility-risk`) | `risk[]`, `feasibility-assessment` | Nếu bật `feasibility-risk` |
| 7 | Delivery Readiness Assessment | solution-assessor (`delivery-readiness`) | `delivery-readiness` | Nếu bật `delivery-readiness` |
| 8 | Critic Validation | critic | `critic-validation[]` | Luôn khi có output high-impact/uncertain |
| 9 | Conflict Resolution | Orchestrator (+critic/HITL) | `conflict-record[]` | Khi có conflict |
| 10 | Final Reporting | report-synthesizer | `final-report.json/.md` | Luôn |

## 2. Chi tiết

### Phase 1 — Task Understanding
- Xác định objective, assessment types được yêu cầu, target stage (nếu có readiness), artifacts trong scope.
- Nếu objective mơ hồ đến mức ảnh hưởng lựa chọn Capability → hỏi user.

### Phase 2 — Context Preparation
Theo [`context-management.md`](context-management.md): nạp context, phân loại trường thiếu theo mức ảnh hưởng, hỏi hoặc ghi assumption.

### Phase 3 — Skill & Agent Selection
1. Task type → Capabilities (`routing-rules.md`).
2. Capability → Profiles (chỉ Profile có artifact tương ứng trong scope).
3. Profile → Skills; resolve qua registry; tính effective status; kiểm tra dependency (V1–V6, xem `skills/README.md`).
4. Skill không dùng được → ghi `coverage_gap`; Skill bắt buộc bị loại → HITL (tiếp tục/dừng).
5. Tạo Assignments: 1 Profile / Assignment; chia nhỏ theo artifact/section nếu cần.
6. Xác định `depends_on` giữa Assignments; đánh dấu nhóm song song.

### Phase 4 — Document Quality Review
- Các assignment `*-review` chạy **song song**.
- `traceability`, `integration-review` chạy sau khi các review liên quan hoàn tất (nhận Findings làm input tham chiếu).

### Phase 5 — Preliminary Feasibility Signals
- Agent ở Phase 4 ghi `early_feasibility_signals` khi gặp dấu hiệu nghiêm trọng (ví dụ NFR mâu thuẫn rõ ràng).
- Orchestrator có thể khởi động sớm assignment `feasibility-risk` cho phần scope đã đủ input, không chờ toàn bộ Phase 4.

### Phase 6 — Consolidated Feasibility Assessment
- Input: Findings, signals, Project Context slice, risk method (nếu có).
- Output: Risks, Feasibility verdict theo verdict rules của Capability.

### Phase 7 — Delivery Readiness Assessment
- Input: Findings, Risks, Feasibility, DoR của dự án.
- Không có DoR → `insufficient-evidence`.

### Phase 8 — Critic Validation
- Bắt buộc với: Findings `critical`/`major`, Findings `expert-judgment`, mọi verdict, Findings confidence `low` ảnh hưởng verdict.
- Mỗi lô validation là Assignment riêng, không cùng context với producer.

### Phase 9 — Conflict Resolution
Theo [`conflict-resolution.md`](conflict-resolution.md).

### Phase 10 — Final Reporting
Báo cáo gồm các phần tách biệt: Document Quality · Feasibility & Risk · Delivery Readiness · Critical Findings · Unresolved Questions · Recommendations · Conflicts & Coverage Gaps · Reproducibility statement.

## 3. Workflow profiles (gợi ý cấu hình)

| Profile | Phases |
|---|---|
| `document-quality-only` | 1, 2, 3, 4, 8, 9, 10 |
| `feasibility-only` | 1, 2, 3, 6, 8, 9, 10 (có thể kèm 4 ở mức tối thiểu để có input) |
| `readiness-gate` | 1–10 |
| `full-assessment` | 1–10 |

Cấu hình tại `projects/<id>/config/review-config.yaml`.

## 4. HITL points

| Thời điểm | Trigger |
|---|---|
| Phase 1 | Objective/scope mơ hồ ảnh hưởng routing |
| Phase 2 | Thiếu thông tin có ảnh hưởng `blocking` |
| Phase 3 | Skill bắt buộc bị loại (coverage gap nghiêm trọng) |
| Phase 9 | Các trigger trong `conflict-resolution.md` §6 |

Mọi câu hỏi/trả lời ghi vào `decisions-log.md` và `run-manifest.hitl_decisions`.

## 5. Incremental review (tương lai)
Dựa trên `content_hash` của artifact trong run manifest trước: chỉ tạo lại Assignment cho artifact thay đổi và các Assignment phụ thuộc. Chưa triển khai.
