---
note_id: RN-0005
topic: "Rà soát cấu trúc tài liệu SRS (document-level structure & completeness) cho skill re.srs-review"
target_skills:
  - re.srs-review
sources: [SRC-0001, SRC-0002, SRC-0003, SRC-0005, SRC-0010, SRC-0011]
author: "Skill Author (re.srs-review delegation)"
created_at: "2026-11-11"
status: complete
---

# RN-0005 — SRS Structural Review

## 1. Câu hỏi nghiên cứu

- Một tài liệu SRS "đầy đủ về mặt cấu trúc" nghĩa là gì, ở cấp ĐỘ TOÀN VĂN — tức thứ mà `re.requirement-quality` (cấp câu đơn lẻ) và `re.requirement-set-quality` (cấp tập requirement) không sở hữu?
- Danh mục kiểm tra cấu trúc nào có thể trích nguồn một cách TRUNG THỰC từ chuẩn đã/sắp đăng ký, trong khi bản thân văn bản chuẩn (paywalled) không có trong repo?
- Khi nào một kết luận "thiếu" là hợp lệ và khi nào phải dừng ở Not Assessable (chế độ tài liệu một phần, thiếu corpus inventory)?

Phạm vi dẫn chiếu ranh giới: dòng ủy quyền trong `re.requirement-quality/SKILL.md` §3 gán cho `re.srs-review` — "Overall SRS structure, missing document sections"; cụm "set-level completeness" của dòng đó được làm rõ thuộc `re.requirement-set-quality` (RSQ-01/02), skill này chỉ sở hữu document-section completeness.

## 2. Trích xuất từ nguồn

| # | source_id | Locator | Nội dung trích xuất (trung thực về mức recall) | authority_level |
|---|---|---|---|---|
| 1 | SRC-0010 (PROPOSED — chưa đăng ký) | Recommended SRS outline, recalled at chapter/section-name level ONLY | Cấu trúc khuyến nghị gồm 1 Introduction (Purpose, Scope, Definitions, References, Overview), 2 Overall Description (Product Perspective, Product Functions, User Characteristics, Constraints, Assumptions & Dependencies), 3 Specific Requirements (External Interfaces — user/hardware/software/communications; Performance Requirements; System Features; Data), kèm Appendices. **Không trích câu; không số sub-clause; chuẩn đã bị SUPERSEDED bởi ISO/IEC/IEEE 29148:2018 (SRC-0001).** | official-standard |
| 2 | SRC-0011 (PROPOSED — chưa đăng ký) | SRS content elements & practical review guidance (memory-based recall) | SRS thực hành cần: title page/document identification, revision history; tổ chức requirements theo feature (function list §2 ↔ feature sections §3); quy ước định danh nhất quán (FR-nn/NFR-nn); reference tài liệu ngoài thay vì copy nội dung — nhưng tài liệu được reference phải truy xuất được; SRS mô tả WHAT không thiết kế; design thuộc SDD. Không trích nguyên văn. | industry-best-practice |
| 3 | SRC-0001 | Clause 5.2.5 (Complete) — conceptual, as already phrased in source-registry | Tính đầy đủ của yêu cầu bao gồm tham chiếu hợp lệ/valid references → nền cho apparatus kiểm tra SRV-06 ở mức khái niệm, không tạo locator mới. | official-standard |
| 4 | SRC-0001 | Clause 5.2.6 (bounded, comprehensible set) — conceptual, as phrased in registry | Tập yêu cầu cần bounded/comprehensible → hỗ trợ khái niệm "structural home cho từng lớp yêu cầu" (SRV-04) và organization nhất quán (SRV-05) ở mức khái niệm. | official-standard |
| 5 | SRC-0002 | Appendix C (Completeness & TBD elimination) | Đưa ra hướng dẫn loại bỏ TBD — skill này dùng cho placeholder CẤP SECTION (SRV-07); cụm locator đã được RSQ-02 dùng trong registry, giữ nguyên cách diễn đạt. | industry-best-practice |
| 6 | SRC-0003 | Section 4.2 (level of abstraction; valid constraints vs premature design solutions) | Ranh giới abstraction và quy tắc "constraint hợp lệ ≠ thiết kế sớm" → nhân bản ở cấp REGION cho SRV-08/SRV-R011; giao thức bị hệ thống ngoài áp buộc vẫn là constraint hợp lệ. | industry-best-practice |
| 7 | SRC-0005 | Clause 6.4.3 (Software Requirements Definition) — process level, as phrased in registry | Quá trình định nghĩa yêu cầu phải tạo specification được document → hậu thuẫn quy trình "yêu cầu được document hóa trong một specification có cấu trúc" (SRV-01) ở mức process, không phải clause cấu trúc. | official-standard |
| 8 | Team material: `agents/.agents/skills/ba-documentation/SKILL.md` | Scope + Document Quality Checklist | Team liệt kê họ viết những tài liệu gì (BRD, SRS, FR/NFR, Business Rules, Glossary, Assumption/Decision Log, AC…), và kiểm tra chất lượng tài liệu theo Completeness/Consistency/Clarity/Traceability/Versioning ("ghi rõ phiên bản, ngày cập nhật, người thực hiện" → hậu thuẫn SRV-02). **Không chứa outline đánh số kiểu IEEE nào** — template nội bộ lỏng. | internal convention evidence (material, không phải source đã đăng ký) |
| 9 | Team material: `agents/.agents/skills/business-requirement-analysis/SKILL.md` | Requirement Quality Criteria table | Tiêu chí cấp-từng-requirement (Atomicity/Clarity/Completeness/Consistency/Feasibility/Testability/Traceability) — xác nhận team ĐÃ có checklist per-statement, nhưng không có mục kiểm tra whole-document → khoảng trống SRV là có thật. | internal convention evidence |
| 10 | Team material: `vendor/skills/yihannangua_prd-review-skill` | module/cross-module checklists | Kiểu bằng chứng "source section names, line numbers, headings" cho tham chiếu nội bộ → ảnh hưởng cách đặt evidence_expectations của SRV-R003/R004. Supporting material, không đăng ký làm nguồn chuẩn. | reference-style practice |

## 3. Tổng hợp

**Bốn nhóm defect chỉ tồn tại ở cấp tài liệu** (không suy ra được từ từng câu hay từng cặp requirement):

1. **Skeleton**: section bắt buộc vắng mặt hoặc chỉ là heading rỗng (SRV-01); lớp yêu cầu (interface classes, NFR, features, data) không có "nhà" cấu trúc và không được tailoring (SRV-04). Đây là lý do các lớp nghĩa vụ biến mất khỏi dự án trước cả khi có câu nào xấu.
2. **Điều khiển & điều hướng**: front matter/revision history (SRV-02) quyết định bản nào là chuẩn; TOC/heading/internal references (SRV-03) quyết định người đọc có đến đúng chỗ không — reference treo trong tài liệu contract là mơ hồ pháp lý, không phải lỗi trình bày.
3. **Apparatus tham chiếu**: References/footnotes phải resolve trong review corpus — nguyên văn "nội dung được ủy quyền phải truy xuất được" (SRC-0011 + SRC-0001 5.2.5 ở mức concept); appendix viện dẫn phải tồn tại (SRV-06). Phát hiện "missing document" bắt buộc bằng chứng hai phía vì **chưa tải lên ≠ không tồn tại**.
4. **Kỷ luật nội dung-vs-vai-trò**: placeholder nguyên section (SRV-07, phân biệt với TBD-inline của RQ-04 và deferred-cluster của RSQ-02); design leak nguyên region trong chương "requirements only" (SRV-08, phân biệt với premature detail một câu của RQ-02 và mixing phân loại của RSQ-06).

**Đường ranh giới ba tầng** (statement → SRV-§/document → set): mỗi defect được giao cho đơn-vị-đánh-giá chứa nó; `re.srs-review` không bao giờ re-flag hàng xóm, và ngược lại. **Cổng assessability**: mọi kết luận vắng-mặt toàn-tài-liệu cần `document_completeness_mode: full`; resolution tài liệu-ngoài cần corpus inventory; scheme không khai báo thì không bịa scheme — chỉ ghi nhận observation.

Baseline outline: ưu tiên template dự án; khi thiếu, fallback outline chuẩn phổ biến (chương-level recall của SRC-0010) và GHI RÕ là giả định trong review metadata.

## 4. Ứng viên criteria/rules → đã chốt trong `re.srs-review@0.1.0`

| Ứng viên | Thành phẩm | Ghi chú nguồn |
|---|---|---|
| Section presence & non-emptiness | `SRV-01` / `SRV-R001` | SRC-0010 outline (chapter-level) + SRC-0011 + SRC-0005 (process-level) |
| Front matter & revision history | `SRV-02` / `SRV-R002` | SRC-0011 + ba-documentation Versioning; ibp vì không phải clause chuẩn |
| TOC/heading/internal-reference integrity | `SRV-03` / `SRV-R003` (comparison), `SRV-R004` | SRC-0011 maintainability; kiểu evidence từ prd-review vendor |
| Interface/NFR/feature/data homes | `SRV-04` / `SRV-R005` | SRC-0010 Ch3 taxonomy (outline-level) + SRC-0001 5.2.6 concept |
| Feature allocation & ID scheme uniformity | `SRV-05` / `SRV-R006` (comparison), `SRV-R007` | SRC-0010 2.2↔3.x convention + SRC-0011; scheme của CHÍNH tài liệu |
| References/appendix resolution (two-artifact) | `SRV-06` / `SRV-R008` (comparison), `SRV-R009` | SRC-0010 References practice + SRC-0001 5.2.5 concept + SRC-0011 |
| Whole-section placeholders | `SRV-07` / `SRV-R010` | SRC-0002 Appendix C; ranh giới RQ-04/RSQ-R003 viết tường minh |
| Section-level abstraction discipline | `SRV-08` / `SRV-R011` | SRC-0003 4.2 + SRC-0011; sibling region-level của RQ-02 |
| Không chốt: kiểm tra layout/trang in, tính đúng nội dung tài liệu được reference, baseline quản lý thay đổi | → out of scope (doc-parser / skill tài liệu khác / domain non-goal) | RN-0002 lifecycle non-goals |

## 5. Điểm chưa chắc chắn / cần xác minh

1. **SRC-0010 & SRC-0011 chưa tồn tại trong `knowledge/source-registry.yaml`** (block paste-ready giao trong hand-off report; An quyết định đăng ký). IEEE 830-1998 đã bị thu hồi/superseeded — cần An xác nhận có muốn neo baseline outline vào một chuẩn superseded hay chuyển hẳn sang 29148 (SRC-0001) khi mua được bản full-text.
2. **Mức recall**: mọi locator SRC-0010 ở bài này là chương/tên-mục recall, không đối chiếu bản gốc; SRC-0011 là memory-based, không open-book. Nếu khi full-text sẵn sàng mà sub-structure khác recall, criteria bị ảnh hưởng: SRV-01 (danh sách mandatory), SRV-04 (interface class taxonomy).
3. **Team chưa có template SRS đánh số chính thức** (material §2.8 cho thấy scope liệt kê loose) — fallback "recognized standard outline + assumption note" cần xác nhận với team; nếu team ban hành template riêng, baseline đổi và một phần severity map có thể đổi.
4. **Chưa có behavioral validation**: 10 GTC là thiết kế tĩnh, chưa chạy runtime (hệ thống Foundation `0.1.0`, `validation.status: unvalidated` toàn bộ).
5. **Quy ước locator cho reference nội bộ tiếng Việt** ("Mục", "PHỤ LỤC", "Hình/Bảng") — danh sách pattern trong SRV-R004/R010 dựa trên tiếng Việt thông dụng, cần đối chiếu corpus thật của team khi có.
6. **`local_path` cho SRC-0010/0011** để trống/null trong block đề xuất (file tóm tắt chưa tạo) — chính sách storage summary-only của registry hiện hành cần An duyệt cách ghi này.
