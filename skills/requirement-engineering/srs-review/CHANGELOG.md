# Changelog — `re.srs-review`

## [0.1.0] - 2026-11-11

**Trạng thái (Status):** `draft` — chờ xác minh hành vi (behavioral validation) khi hệ thống có runtime.

### Added
- Skill `re.srs-review` (domain `requirement-engineering`): toàn bộ thư mục `skills/requirement-engineering/srs-review/` — SKILL.md, criteria.yaml, rules.yaml, checklist.md (bảng tiếng Việt), examples/.
- 8 tiêu chí cấu trúc tài liệu SRS: `SRV-01`..`SRV-08` (presence & non-emptiness của các section bắt buộc; front matter & revision history; TOC/heading/internal-reference integrity; structural homes cho external interfaces/NFR/features/data; feature allocation & declared ID-scheme consistency; referenced documents/footnotes/appendices resolution; whole-section placeholder freedom; section-level abstraction discipline). Grounded at conceptual/outline level in SRC-0010 (IEEE Std 830-1998 — recalled at outline level only), SRC-0011 (Wiegers & Gilbert 3rd ed., memory-based), và các locator đã ghi trong registry: SRC-0001 (Clause 5.2.5/5.2.6), SRC-0002 (Appendix C), SRC-0003 (Section 4.2), SRC-0005 (Clause 6.4.3).
- 11 quy tắc thực thi: `SRV-R001`..`SRV-R011` (analysis + comparison). Trong đó `SRV-R008` định nghĩa **hợp đồng two-artifact**: kết luận "tài liệu được tham chiếu không tồn tại trong corpus" bắt buộc kèm (1) excerpt entry tham chiếu phía SRS và (2) bằng chứng corpus inventory không chứa nó; thiếu corpus inventory → `Not Assessable`, không suy diễn "missing".
- Checklist rà soát `checklist.md` (tiếng Việt): cổng ngữ cảnh `partial/full`, template/outline baseline, corpus inventory, chống false-positive do tailoring.
- Bộ Golden Test Cases: 10 ca `SRV-GTC-01`..`SRV-GTC-10` trong `examples/golden-test-cases.yaml` (3 song ngữ vi/en), gồm: gate Not Assessable khi chỉ dán một section lẻ (GTC-04), chống false-positive tailoring (GTC-05), hai ca ranh giới ủy quyền — wording → `re.requirement-quality` (GTC-06), mâu thuẫn trong tập requirement → `re.requirement-set-quality` (GTC-07), hai-artifact missing reference (GTC-03), baseline Compliant toàn phần (GTC-10).
- `examples/synthetic-examples.md` (6 walkthrough tổng hợp), `examples/README.md`, và Research Note `knowledge/research-notes/RN-0005-srs-review.md`.

### Sources verified
- Đã đọc và đối chiếu registry hiện có: `SRC-0001`, `SRC-0002`, `SRC-0003`, `SRC-0005` (dùng đúng locator đã ghi — conceptual). `SRC-0010` (IEEE Std 830-1998) và `SRC-0011` (Wiegers & Gilbert, Software Requirements, 3rd ed., 2010) là **đề xuất đăng ký mới (PROPOSED — chưa có trong `knowledge/source-registry.yaml`)**; paste-ready blocks giao kèm báo cáo. Recall giới hạn ở mức outline (830) / memory-based (Wiegers) — không trích câu, không bịa số sub-clause.

### Boundary statement
- `re.srs-review` đánh giá **SRS như một tài liệu** (structure & whole-document completeness). KHÔNG đánh giá: wording từng requirement (→ `re.requirement-quality` RQ-01..09), tính nhất quán/trùng lặp của tập requirement (→ `re.requirement-set-quality` RSQ-01..06), sự thỏa mãn nhu cầu stakeholder (→ `re.requirement-validation`), liên kết trace đa lớp và ID-collision làm endpoint (→ `re.requirement-traceability`). TBD trong một câu → RQ-04; deferred cluster trong section đã có nội dung → RSQ-02/RSQ-R003.
- `depends_on: []` — skill không thuộc tính theo skill nào; ủy quyền chỉ là delegation note.

### Known limitations (0.1.0)
- `validation.status: unvalidated` cho toàn bộ criteria/rules (hệ thống ở Foundation stage, chưa có runtime adapter).
- SRC-0010/0011 chưa được đăng ký chính thức trong source-registry.
- Trang mục lục của bản convert (docx→text/pdf) có thể mất TOC hoặc heading levels → gate Not Assessable cho SRV-03 nếu thiếu một trong hai phía.

## [Unreleased]
- Chờ: xác minh hành vi GTC khi có runtime; đăng ký SRC-0010/0011 vào `knowledge/source-registry.yaml`; cân nhắc adapter `doc-parser` cho TOC/page artifacts.
