# CHANGELOG

Định dạng: mỗi phiên bản hệ thống liệt kê thay đổi cấp hệ thống. Thay đổi của từng Skill được ghi trong `CHANGELOG.md` của Skill đó.

## [0.1.0] — 2026-11-10 — Foundation

### Added
- Kiến trúc logic: Orchestrator, 3 Capabilities, 5 Core Agents, 10 Specialist Profiles (draft), Skill Library (6 domain, chưa có Skill), Knowledge Base, Schemas, Tools (interface), Project template.
- ADR-0001 → ADR-0007.
- Data contracts (JSON Schema 2020-12): common, definitions (6), runtime (12).
- Templates: Core Agent, Profile, Capability, Skill (SKILL.md, criteria, rules, checklist), Research Note, Project.

### Decisions applied (mặc định đề xuất, chờ xác nhận lại nếu cần)
- Profiles tạo dạng `draft`; Skill tham chiếu ở trạng thái `planned`.
- Hệ thống đặt trực tiếp tại thư mục gốc workspace.
- Severity `critical/major/minor/info`, Confidence `high/medium/low` (internal-convention).
- Basis `expert-judgment` được phép với giới hạn.
- Re-validation mặc định 1 lượt/conflict; rating chưa giải quyết → hiển thị cả hai, tạm dùng mức cao hơn, gắn cờ.
- Độ sâu dependency khuyến nghị ≤ 2 (cảnh báo).

### Known limitations
- Không có Skill `validated` → chưa thể review thực tế.
- `consistency-rules.yaml` chưa có rule nào.
- Chưa có Runtime Adapter, chưa có tool implementation.

## Next steps
1. Chọn Skill pilot (đề xuất: `re.requirement-quality`) và chạy pipeline 7 bước (đăng ký source → research note → criteria → validate).
2. Định nghĩa các comparison rule domain-agnostic đầu tiên cho `document-quality`.
3. Chạy một pilot review end-to-end trên một dự án mẫu để kiểm chứng contracts.
4. Thiết kế Runtime Adapter cho nền tảng mục tiêu.
