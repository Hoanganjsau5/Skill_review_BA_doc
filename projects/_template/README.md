# Project Template

Copy thư mục này thành `projects/<project-id>/` cho mỗi dự án cần review. Tên thư mục bắt đầu bằng `_` để phân biệt template.

| Thư mục | Nội dung | Ghi chú |
|---|---|---|
| `context/` | `project-context.yaml`, `architecture-decisions.md`, `assumptions-and-limitations.md` | Được phép thiếu thông tin; mỗi trường có `status` |
| `config/` | `review-config.yaml`, `definition-of-ready.yaml`, `risk-assessment-method.yaml` | DoR và risk method do **dự án** định nghĩa |
| `artifacts/` | Tài liệu cần review, chia theo loại | Không chỉnh sửa trong quá trình review; hash được ghi vào manifest |
| `reviews/` | Một thư mục cho mỗi Review Run | Output bất biến sau khi run hoàn tất |

## Các bước
1. Điền `context/project-context.yaml` — trường chưa biết để `status: missing`.
2. Đặt tài liệu vào `artifacts/<loại>/`.
3. Cấu hình `config/review-config.yaml`.
4. (Nếu cần readiness) định nghĩa `config/definition-of-ready.yaml` cho stage mục tiêu.
5. (Nếu muốn đánh giá likelihood/impact) định nghĩa `config/risk-assessment-method.yaml`.
6. Yêu cầu Orchestrator thực hiện review.
