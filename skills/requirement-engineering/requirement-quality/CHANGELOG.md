# CHANGELOG — `re.requirement-quality`

## [0.1.0] — 2026-11-11

### Added
- Khởi tạo Skill `re.requirement-quality` ở trạng thái `draft`.
- Định nghĩa 9 Core Criteria (`RQ-01` .. `RQ-09`) độc lập ngôn ngữ tự nhiên và độc lập loại tài liệu trong `criteria.yaml`, kèm đầy đủ quy tắc `required_context`, `optional_context`, `standalone_assessable_when`, `not_assessable_conditions` và `not_applicable_conditions`.
- Định nghĩa 16 Detection & Evaluation Rules (`RQ-R001` .. `RQ-R016`) trong `rules.yaml` với sự phân biệt rõ `source_type`, `normative_level` (`Mandatory`, `Recommended`, `Heuristic`), `detection_approach` và `false_positive_considerations`.
- Thiết kế kiến trúc Language Pack mở rộng được (`language-packs/README.md`) và hiện thực 2 gói ngôn ngữ đầu tiên: Tiếng Anh (`language-packs/en.yaml`) và Tiếng Việt (`language-packs/vi.yaml`).
- Xây dựng bộ 15 Synthetic Examples (`examples/synthetic-examples.md`) và 15 Golden Test Cases (`examples/golden-test-cases.yaml`) bao phủ cả phát hiện lỗi thật, chặn suy diễn khi thiếu ngữ cảnh (`Not Assessable`), trường hợp `Not Applicable` hợp lệ, và chống dương tính giả (anti-false-positive).

### Sources verified
- `SRC-0001`: ISO/IEC/IEEE 29148:2018 (Second edition) — Clause 5.2.5 (verified via official catalog abstract and secondary literature at `2026-11-11`; full text paywalled).
- `SRC-0002`: NASA/SP-2016-6105 Rev2 (2016) — Appendix C: How to Write a Good Requirement (verified by Skill System Architect at `2026-11-11`).
- `SRC-0003`: NASA/SP-2016-6105 Rev2 (2016) — Section 4.2: Technical Requirements Definition (verified by Skill System Architect at `2026-11-11`).
- `SRC-0004`: INCOSE Guide to Writing Requirements Version 4 (`INCOSE-TP-2010-006-04`, July 2023) — verified via official INCOSE v4 summary sheet and secondary practitioner literature at `2026-11-11`.
