# Context Management

Version: 0.1.0

## 1. Nguồn context
- `projects/<id>/context/project-context.yaml` — 14 trường, mỗi trường có `status`.
- `projects/<id>/context/architecture-decisions.md` — ADR của dự án.
- `projects/<id>/context/assumptions-and-limitations.md`.
- Thông tin user cung cấp trong request (ghi lại vào context hoặc assumptions).

## 2. Đánh giá thông tin thiếu

Với mỗi trường `missing`, Orchestrator phân loại mức ảnh hưởng **đối với task hiện tại**:

| Impact | Ý nghĩa | Hành động |
|---|---|---|
| `blocking` | Không thể đưa ra kết luận có ý nghĩa cho một phần scope | Hỏi user; nếu không có trả lời → phần liên quan trả về `insufficient-evidence` |
| `material` | Ảnh hưởng đáng kể đến kết luận | Hỏi user **hoặc** đề xuất assumption tường minh để user xác nhận |
| `minor` | Ảnh hưởng nhỏ | Ghi assumption, tiếp tục |
| `none` | Không liên quan task | Bỏ qua |

Ví dụ: thiếu `budget` là `none` với `document-review`, nhưng có thể là `material` với `feasibility-assessment`.

**Nguyên tắc:** constraint bị thiếu **không bao giờ** tự động được coi là dự án thất bại.

## 3. Assumption
- Mỗi assumption có: `assumption_id`, `statement`, `source` (`user-confirmed | agent-proposed | project-context`), `status` (`proposed | confirmed | rejected`), `impact`.
- Output phụ thuộc assumption phải tham chiếu `assumption_id`.
- Assumption `proposed` chưa xác nhận → confidence của output phụ thuộc không được là `high`.

## 4. Context slicing
Mỗi Assignment chỉ nhận:
- Artifacts/sections trong scope.
- Các trường context liên quan đến Profile (ví dụ `feasibility-risk` cần budget, timeline, team, infrastructure; `requirements-review` thường chỉ cần overview, functional scope).
- Assumptions liên quan.
- Với Assignment phụ thuộc: output (Findings/Risks) của Assignment trước, không phải toàn bộ context của chúng.

Danh sách trường context cấp cho Assignment được ghi trong `agent-assignment.context_slice` để truy vết.

## 5. Clarification request
Agent có thể trả về `clarification_requests[]` trong `review-result`. Orchestrator gom, khử trùng lặp, và quyết định hỏi user hay ghi assumption theo bảng §2.
