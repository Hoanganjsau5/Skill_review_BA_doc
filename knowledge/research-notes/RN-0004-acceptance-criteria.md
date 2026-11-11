---
note_id: RN-0004
topic: "Acceptance Criteria suite quality — đặc trưng verifiable/atomic/phủ hai chiều cho bộ AC"
target_skills: [re.acceptance-criteria]
sources: [SRC-0001, SRC-0002, SRC-0003, SRC-0004, SRC-0008, SRC-0009]
author: Skill System Architect
created_at: 2026-11-11
status: complete
---

# Research Note: Acceptance Criteria (`re.acceptance-criteria`)

## 1. Câu hỏi nghiên cứu

1. Một **bộ Acceptance Criteria (AC)** đạt chất lượng cần những đặc trưng gì, khi AC về bản chất là requirement nhìn từ phía nghiệm thu (kế thừa đặc tính Verifiable/Unambiguous/Singular của 29148 nhưng áp trên phạm vi AC-section)?
2. Check nào là **set-level** (phủ hai chiều AC↔owner item, đường lỗi/biên, trùng/mâu thuẫn giữa các AC) và ranh giới nào phải **delegate** sang `re.requirement-quality`, `re.requirement-set-quality`, `re.requirement-traceability` để không chồng ownership?
3. Cấu trúc Given/When/Then (BDD/Gherkin) và INVEST quy định những gì — ở mức **khái niệm** — cho well-formedness và testability của AC, và làm sao tránh báo dương tính khi dự án không dùng format GWT hoặc đã bound định ngữ ngay sau đó?

## 2. Trích xuất từ nguồn

| # | source_id | Locator | Nội dung trích xuất (tóm tắt, paraphrase — không trích nguyên văn) | authority_level |
|---|-----------|---------|--------------------------------------------------------------------|-----------------|
| E1 | SRC-0001 | Clause 5.2.5 (characteristics of an individual requirement) | Đặc tính cá nhân requirement gồm Verifiable, Unambiguous, Singular (theo dẫn chiếu khái niệm đã ghi trong source-registry); AC là requirement nên kế thừa ba đặc tính này ở phạm vi AC text. | official-standard |
| E2 | SRC-0001 | Clause 5.2.6 (characteristics of a set of requirements) | Set phải Complete/Consistent — áp cho bộ AC: mọi owner trong scope có AC, các AC không mâu điều kiện-kết quả. | official-standard |
| E3 | SRC-0001 | Clause 6.4 (requirements validation) / 6.5 (traceability) | Validation đối chiếu nhu cầu stakeholder; traceability dựa trên identifier duy nhất — chống lưng khái niệm cho ACA-04 (neo owner) và ACA-07 (id integrity). | official-standard |
| E4 | SRC-0002 | Appendix C (How to Write a Good Requirement) | Heuristics: tránh compound/multi-obligation một câu; mọi requirement phải gắn cách kiểm chứng; cảnh báo định ngữ mơ hồ. Dùng cho ACA-03/R003, ACA-01, ACA-08, ACA-10. | industry-best-practice |
| E5 | SRC-0003 | Section 4.2 (Technical Requirements Definition) | Phân biệt **ràng buộc hợp lệ** vs **thiết kế sớm** (premature design); chọn verification method theo loại characteristic. Nền cho ACA-06/R006 (design lock-in) và ACA-10 (method fit). | industry-best-practice |
| E6 | SRC-0004 | Set characteristics (paraphrase) | Complete, Consistent, Able to be Validated như thuộc tính cấp set — củng cố ACA-04/ACA-09 không sao chép câu chữ có bản quyền. | industry-best-practice |
| E7 | SRC-0008 (đề xuất) | INVEST acronym (2003, agilemodeling.com) — paraphrase từ bộ nhớ/nguồn thứ cấp | Chữ T (Testable): story/AC phải xác định được cách kiểm chứng; Small/Negotiable gợi ý atomicity và AC không đóng băng thiết kế. CHƯA trích nguyên văn định nghĩa từng chữ. | industry-best-practice |
| E8 | SRC-0009 (đề xuất) | "Introducing BDD" (Dan North, 2006) + Gherkin reference (cucumber.io docs) — paraphrase khái niệm | Ý tưởng tách precondition/action/outcome thành các phần của một scenario kiểm chứng được; từ khóa Given/When/Then/And với ngữ nghĩa khe nội dung. Không khẳng định câu/định nghĩa nguyên văn. | industry-best-practice |

**Tài liệu nội bộ (không phải source đăng ký — chỉ provenance cho `origin_note`):**

| # | Nguồn | Nội dung dùng | Ghi chú biến đổi |
|---|-------|---------------|------------------|
| M1 | `agents/.agents/skills/business-requirement-analysis/SKILL.md` | Bảng chất lượng: Atomicity ("một chức năng hoặc ràng buộc duy nhất"), Testability ("Có thể xác định tiêu chí nghiệm thu và viết Test Case"), Completeness pre/post-conditions; quy định "không bịa requirement, phải label PROPOSED". | Bỏ phần tương tác/orchestration; giữ kiểm tra khai báo. |
| M2 | `agents/.agents/skills/ba-documentation/SKILL.md` | AC là mục bắt buộc của tài liệu; Consistency BR↔FR↔UC↔Test Cases; giữ ID đã duyệt. | Nuôi ACA-07 và ranh giới ACA-09. |
| M3 | `vendor/skills/yihannangua_prd-review-skill/prd-review/references/business-rule-checklist.md` | Pattern GWT khuyến nghị (Given precondition / When actor-action / Then expected behavior / And state+feedback); hàng failure/exception/retry/rollback; "Observable acceptance criteria or test oracle". | Thành ACA-R002 slot typing, ACA-R005 declared-failure-mode, ACA-R010 evidence-fit; facet-And được phân tích để KHÔNG vi phạm ACA-03. |
| M4 | `vendor/skills/.../requirement-quality-checklist.md` | Phép thử mơ hồ "two reasonable readers"; vague verbs/undefined thresholds/unspecified actor-scope-permission; mỗi finding mơ hồ phải nêu 2 cách đọc + wording đề xuất. | Thành gate bắt buộc của ACA-R008. |
| M5 | `vendor/skills/TsCarpe_claude-sdlc-skills` (trellis-handoff, PRD template) | AC cấp business phải tương ứng parent rules/PRD ("对应 … parent prd 验收标准"); AC chương nghiệm thu kỹ thuật phải "可测". | Củng cố ACA-06 (AC không tự lập pháp) và ACA-01. |
| M6 | `requirement-quality/language-packs/vi.yaml` (sibling skill, read-only) | Signal định ngữ vi (nhanh, kịp thời, dễ, hợp lý) + anti-FP rule "bound ngay sau đó thì không báo". | ACA-R008 tiêu thụ signal, không tái sở hữu language pack. |

## 3. Tổng hợp & Nguyên tắc thiết kế cho `re.acceptance-criteria`

1. **AC là requirement phía nghiệm thu → kế thừa đặc tính cá nhân của 29148 (E1), nhưng chỉ trong AC-section.** Ngoài section đó là phần đất của `re.requirement-quality` (RQ-03/05/07). Đây là lý do ACA-01/03/08 mang official-standard mà vẫn đặt `delegated_to_other_skills` rất hẹp.
2. **Property cấp set áp trên bộ AC (E2/E6):** hai chiều phủ AC↔owner (ACA-04), trùng/mâu thuẫn (ACA-09), đường lỗi (ACA-05). Set-level check của AC suite granularity ≠ RSQ-01/02 (toàn bộ requirement set theo declared project scope) ≠ RTR (cấu trúc link đa tầng RTM) — ba tầng ownership tách biệt, thực hiện bằng bidirectional set-diff cùng kiểu flow-map của skill anh em nhưng chỉ trên cạnh AC→owner.
3. **Detection Signal ≠ Defect (nguyên tắc anti-dogma kế thừa RN-0001):** từ mơ hồ, connector "và/and", "thiếu số" chỉ là trigger; chỉ Issue khi qua gate tương ứng — competing-interpretation (R008), independent-failure (R003), quantity-sensitivity (R001), condition-overlap (R009). Pattern facet-And của M3 phải được xử là atomic (một quyết định accept/reject với nhiều bằng chứng).
4. **Format-relative, không format-absolute:** GWT well-formedness (E8/M3) chỉ áp khi dự án dùng GWT; declared table/prose → Not Applicable có justification (GTC-09). Cùng thông tin ba khe (precondition/action/outcome) ở cột bảng đạt ý định tương tự.
5. **AC không tự lập pháp (E5/M1/M5):** AC chỉ nghiệm thu owner item; thêm nghĩa vụ/kênh/cơ chế = creep hoặc premature design (ACA-06), với exemptions cho setup-data/environment/measurement-method và downgrade path khi design-doc được cung cấp.
6. **Context Dependency Gate:** thiếu owner inventory/scope/test plan ngoài package → Not Assessable + clarification (GTC-06), tuyệt đối không suy diễn "thiếu AC" hay "thiếu cách kiểm chứng" thành defect.
7. **Criterion Status ≠ Finding:** bốn status chuẩn repository; `qa.*` (planned) không bao giờ vào `depends_on`; delegation ghi recommendation.

## 4. Ứng viên criteria/rules

| Đề xuất ID | Statement (rút gọn) | Dựa trên | Ghi chú |
|------------|---------------------|----------|---------|
| ACA-01 | Outcome quyết định pass/fail không cần đoán; bound khi quantity-sensitive | E1, E4, E8 | official-standard; anti-dogma behavioral |
| ACA-02 | Khe Given/When/Then đúng khi dùng GWT | E8, M3 | NA theo declared format |
| ACA-03 | Một quyết định nghiệm thu mỗi AC (independent-failure test) | E1, E4, E7, M1 | facet-And được phép |
| ACA-04 | AC↔owner bidirectional trong declared scope | E2, E3, E6, E7, M5 | safeguard partial-package |
| ACA-05 | AC cho failure/boundary mode ĐÃ khai báo trong owner text | E4, M3, M1 | cấm bịa mode |
| ACA-06 | Không creep, không design lock-in | E5, E7, M1, M5 | exemptions + PROPOSED label |
| ACA-07 | Id AC duy nhất, theo quy ước khai báo/suy ra | E3, M2 | expert-recommendation + origin_note |
| ACA-08 | Một cách đọc accept/reject; gate 2 cách đọc | E1, E4, E6, M4, M6 | official-standard |
| ACA-09 | Không trùng/mâu thuẫn AC↔AC, AC↔owner functional text | E2, E6, M4 | cite ≥2 verbatim |
| ACA-10 | Phương thức chứng minh nêu rõ (per-AC hoặc mapping) | E4, E5, E7, M3 | method-evidence fit |
| ACA-R001..R010 | Method vận hành 1:1 theo ACA-01..10 + gates FP | như trên | rule YAML `method` block |

## 5. Điểm chưa chắc chắn / Giới hạn xác minh

- **SRC-0008 (Bill Wake, "INVEST in a Good Story", 2003) và SRC-0009 (Dan North, "Introducing BDD", 2006; Gherkin reference cucumber.io) CHƯA được đăng ký** trong `knowledge/source-registry.yaml` — block đăng ký đề xuất gửi kèm báo cáo cho An; bản chất truy cập: **kiến thức từ bộ nhớ/nguồn thứ cấp**, chỉ dùng ở mức khái niệm (acronym, cấu trúc scenario, ngữ nghĩa từ khóa); KHÔNG trích nguyên văn định nghĩa, KHÔNG bịa số trang/URL chi tiết. URL article cụ thể và phiên bản chính xác của Gherkin docs cần An xác nhận khi đăng ký.
- **29148/INCOSE paywalled/copyright:** mọi locator là conceptual/structural (đúng kỷ luật access_note hiện hành của registry); các cụm "Clause 5.2.5/5.2.6/6.4/6.5" lấy theo dẫn chiếu đã ghi sẵn trong source-registry, không tự thêm clause số mới.
- **Mở rộng khái niệm:** "AC kế thừa đặc tính requirement" là synthesis của nhóm tài liệu này (ngôn từ tiêu chí do đó là origin_note-synthesized, không phải mệnh đề ISO).
- **Điều khoản GWT của các dự án nội bộ:** team TripMate chưa khai báo convention AC-numbering chính thức trong tài liệu đã đọc — ACA-07 dừng ở mức "declared-or-inferable", chờ project config (`projects/_template/config/review-config.yaml`) cung cấp convention thực.
- Chưa có runtime để chạy golden suite → mọi `validation.status = unvalidated`; các case là spec hành vi cho bước validate sau.
