# Agentic Review System

**Reusable Skill-based Multi-Agent Review System** — framework đánh giá tài liệu kỹ thuật phần mềm (Document Quality) và đánh giá tính khả thi của giải pháp (Feasibility & Delivery Readiness), có thể tái sử dụng cho nhiều dự án.

> **Trạng thái:** `0.1.0` — *Foundation*. Kiến trúc, contracts và templates đã được thiết lập. **Chưa có Skill nào được nghiên cứu/validate**, vì vậy hệ thống **chưa sẵn sàng để thực hiện review thực tế**. Đây là chủ đích để tuân thủ Evidence & Knowledge Quality Policy.

---

## 1. Hệ thống trả lời hai câu hỏi độc lập

| Layer | Câu hỏi | Output |
|---|---|---|
| **Document Quality** | Tài liệu có đúng, đủ, rõ, nhất quán, truy vết được, kiểm thử được không? | Findings |
| **Feasibility & Delivery** | Giải pháp có thực hiện và chuyển giao được dưới ràng buộc thực tế của dự án không? | Risks, Feasibility verdict, Delivery Readiness verdict |

Một tài liệu có thể đạt chất lượng tốt trong khi giải pháp nó mô tả lại không khả thi. Hai chiều được đánh giá **độc lập** và chỉ kết hợp ở tầng báo cáo.

## 2. Mô hình khái niệm

```text
Task ──► Orchestrator ──► Capability ──► Specialist Profile ──► Core Agent (1 Assignment / Profile)
                                               │
                                               └──► Skill@version ──► Criterion / Rule ──► Source (Knowledge Base)
```

| Thành phần | Là gì | Thư mục |
|---|---|---|
| Orchestrator | Điều phối: hiểu task, lập kế hoạch, routing, quản lý phụ thuộc, giải quyết conflict, tổng hợp | [`orchestrator/`](orchestrator/) |
| Capability | Năng lực đánh giá tổng hợp (ghép Profiles + aggregation/verdict rules) — không chứa tri thức chuyên môn | [`capabilities/`](capabilities/) |
| Core Agent | Instruction template theo **kiểu suy luận** (5 agents) | [`agents/core/`](agents/core/) |
| Specialist Profile | Cấu hình vai trò: phạm vi + Core Agent + Skills | [`agents/profiles/`](agents/profiles/) |
| Skill | Tri thức chuyên môn đã chuẩn hóa: procedure, criteria, rules, checklist | [`skills/`](skills/) |
| Knowledge Base | Nguồn gốc tri thức: source registry, references, research notes | [`knowledge/`](knowledge/) |
| Schemas | Data contracts (JSON Schema 2020-12) | [`schemas/`](schemas/) |
| Tools | Năng lực vận hành (parse, validate, retrieve) — hiện chỉ có interface | [`tools/`](tools/) |
| Projects | Context, config, artifacts và review runs của từng dự án | [`projects/`](projects/) |

Chi tiết: [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) · Thuật ngữ: [`docs/GLOSSARY.md`](docs/GLOSSARY.md) · Quyết định kiến trúc: [`docs/adr/`](docs/adr/) · Cấu hình hệ thống: [`SYSTEM_CONFIG.md`](SYSTEM_CONFIG.md)

## 3. Sử dụng cho một dự án mới

1. Copy `projects/_template/` → `projects/<project-id>/`.
2. Điền `context/project-context.yaml` (được phép thiếu — mỗi trường có `status`).
3. Đặt tài liệu cần review vào `artifacts/`.
4. Cấu hình `config/review-config.yaml`; nếu cần đánh giá readiness/risk có định lượng, định nghĩa `config/definition-of-ready.yaml` và `config/risk-assessment-method.yaml`.
5. Yêu cầu Orchestrator thực hiện review. Kết quả được ghi tại `reviews/<run-id>/`.

Core (`orchestrator/`, `agents/`, `capabilities/`, `skills/`, `knowledge/`, `schemas/`) **không thay đổi** giữa các dự án.

## 4. Nguyên tắc cốt lõi

1. Không bịa standards, benchmarks, năng lực công nghệ hay sự thật về dự án.
2. `Insufficient Evidence` là kết quả hợp lệ.
3. Assumption phải tường minh; thiếu thông tin ≠ dự án thất bại.
4. Mỗi Profile chạy trong một Assignment độc lập; output gốc của Agent là bất biến.
5. Mọi Finding có basis (criterion / analysis rule / comparison rule / expert judgment có giới hạn) và evidence.
6. Mọi review run có manifest để truy vết và chạy lại (không cam kết output giống hệt).
7. Quyết định quan trọng thuộc về con người.

## 5. Lộ trình tiếp theo

Xem mục *Next steps* trong [`CHANGELOG.md`](CHANGELOG.md).
