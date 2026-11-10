# Knowledge Base

Kho **nguồn gốc** tri thức. Dùng để xây dựng/cập nhật Skill và để Critic kiểm chứng nguồn. **Không** nạp mặc định khi review. **Không** chứa dữ liệu dự án.

Quyết định: [ADR-0005](../docs/adr/ADR-0005-knowledge-base-vs-skill-library.md)

## 1. Cấu trúc
| Thư mục/File | Nội dung |
|---|---|
| [`source-registry.yaml`](source-registry.yaml) | Sổ đăng ký nguồn (schema: `schemas/definitions/source-entry.schema.json`) |
| [`standards/`](standards/) | Ghi chú/tóm tắt chuẩn chính thức (theo quyền sử dụng) |
| [`references/`](references/) | Tài liệu kỹ thuật, vendor docs, benchmark đã xác minh |
| [`research-notes/`](research-notes/) | Research notes: trích xuất có locator, phục vụ xây Skill |

## 2. Knowledge Quality Policy
1. Mọi nguồn phải được đăng ký trước khi được trích dẫn.
2. Ghi rõ version/edition, ngày xuất bản, `retrieved_at`, `authority_level`.
3. Tôn trọng bản quyền: chuẩn có bản quyền chỉ lưu tóm tắt/ghi chú và locator, không lưu toàn văn khi không được phép.
4. Phân biệt: Official Standards · Industry Best Practices · Expert Recommendations · Internal Conventions. (Project-specific Decisions nằm trong `projects/`.)
5. Claim định lượng/nhạy cảm thời gian phải có nguồn và ngày truy xuất; xem lại định kỳ.
6. Không bịa nguồn, không bịa locator.

## 3. Pipeline 7 bước (tóm tắt)
Register source → Research note → Synthesize → Procedure → Criteria/Rules (source_refs) → Validate với examples → Version + `last_verified_at`. Chi tiết: [`skills/README.md`](../skills/README.md).

## 4. Snapshot cho reproducibility
Khi một run dùng Knowledge Base, run manifest ghi `registry_version` và hash của `source-registry.yaml`.
