# Tools

Tools cung cấp **năng lực vận hành**, không đưa phán quyết chuyên môn. Giai đoạn hiện tại **chỉ mô tả interface**, chưa có implementation. Khi hiện thực, có thể dùng năng lực sẵn có của nền tảng hoặc script nhỏ; mỗi tool phải có `tool_id` và version để ghi vào run manifest.

| tool_id | Nhóm | Mục đích | Input | Output | Trạng thái |
|---|---|---|---|---|---|
| `doc-parser` | Parsing | Đọc Markdown/PDF/Word → text có cấu trúc + locator (section/page/line) | file path | sections[] với locator, content_hash | planned |
| `diagram-extractor` | Parsing | Trích xuất phần tử từ diagram (PlantUML/Mermaid/ảnh) | file path | elements[], relations[] hoặc `unavailable` | planned |
| `spec-parser` | Parsing | Đọc OpenAPI/SQL DDL → cấu trúc | file path | operations[]/entities[] | planned |
| `content-hasher` | File | Tính `sha256:` cho artifact/config | file path | ContentHash | planned |
| `schema-validator` | Validation | Validate JSON/YAML theo `schemas/` | data + schema id | valid / errors[] | planned |
| `registry-validator` | Validation | Kiểm tra Skill dependency V1–V6, phát hiện circular dependency (DFS) | `SKILL_REGISTRY.yaml` + manifests | errors[], warnings[], effective_status map | planned |
| `reference-lookup` | Retrieval | Tra cứu nguồn trong `knowledge/source-registry.yaml` và ghi chú liên quan | source_id / query | entries[] | planned |
| `project-retrieval` | Retrieval | Truy xuất đoạn artifact theo scope cho context slicing | project_id + scope | excerpts[] với locator | planned |

## Quy tắc
1. Tool không bịa dữ liệu: không trích xuất được → trả `unavailable` kèm lý do.
2. Mọi output có locator để làm evidence.
3. Tool không chứa tri thức chuyên môn (criteria thuộc Skill).
4. Tìm kiếm nguồn bên ngoài (web) chỉ phục vụ **xây dựng Skill**/Knowledge Base, hoặc khi user yêu cầu evidence cụ thể; kết quả phải đăng ký vào source registry trước khi được dùng làm căn cứ.
