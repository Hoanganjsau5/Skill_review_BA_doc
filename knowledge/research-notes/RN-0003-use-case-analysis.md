---
note_id: RN-0003
topic: "Use Case Analysis — Element Completeness, Flow Discipline & Abstraction Level (Cockburn essentials + 29148/NASA conceptual anchors)"
target_skills: [re.use-case-analysis]
sources: [SRC-0001, SRC-0002, SRC-0003, SRC-0007]
author: Skill System Architect
created_at: 2026-11-11
status: complete
---

# Research Note: Use Case Analysis (`re.use-case-analysis`)

## 1. Câu hỏi nghiên cứu
1. Một use case "đủ" nghĩa là gì khi tách bạch với chất lượng từng câu requirement (vốn do `re.requirement-quality` quản)? Bộ phần tử tối thiểu (essentials) nào phải có, và phần tử nằm trong prose có được tính là "có" không?
2. Làm sao đánh giá kỷ luật luồng (đánh số, tính nguyên tử, luân phiên actor↔system, vòng lặp tường minh, nhánh exception bao gồm từ chối và không phản hồi) mà không sa vào dogma mẫu hình?
3. Ranh giới nào giữa "ngôn ngữ cụ thể hợp lệ của domain" và "thiết kế sớm" trong basic flow; ai sở hữu lỗi trùng lặp use case trong set?

## 2. Trích xuất từ nguồn
| # | source_id | Locator | Nội dung trích xuất (tóm tắt, paraphrase) | authority_level |
|---|---|---|---|---|
| 1 | `SRC-0007` | Topic: use case essentials (secondary-source recollection, KHÔNG trích trang) | Các yếu tố cốt lõi của một use case hiệu quả: tên/định danh mục tiêu người dùng, actor chính/phụ, hệ thống ranh giới, điều kiện khởi động (trigger), preconditions, luồng thành công chính dạng bước, extensions cho từng bước, postconditions kèm success guarantee và tối thiểu guarantee cho nhánh lỗi; viết theo mức trừu tượng nhất quán (styles levels). | `industry-best-practice` |
| 2 | `SRC-0001` | Clause 5.2.5 (mức khái niệm, như chú thích sẵn có trong registry) | Đặc tính cá nhân yêu cầu (Complete, Singular, Verifiable…) áp dụng tương tự cho từng bước luồng và phát biểu kết quả; KHÔNG trích điều khoản riêng về use case của 29148 vì chưa xác minh được nguyên văn. | `official-standard` |
| 3 | `SRC-0001` | Clause 6.5 (mức khái niệm) | Tính đúng đắn của quan hệ truy vết được khai báo; dùng cho chuẩn "ID được trích dẫn phải resolve" ở mức tham chiếu nội bộ package, phần ma trận thuộc `re.requirement-traceability`. | `official-standard` |
| 4 | `SRC-0002` | Appendix C | Heuristic yêu cầu ghép/đa nghĩa vụ — tái sử dụng cho test "một bước nhiều nghĩa vụ"; cảnh báo đòi chỉ số định lượng khi kiểm chứng hành vi/trạng thái là đủ. | `industry-best-practice` |
| 5 | `SRC-0003` | Section 4.2 | Phân biệt ràng buộc hợp lệ (valid constraint) với thiết kế sớm (premature design); mức trừu tượng — nền cho UCA-07. | `industry-best-practice` |
| 6 | (local) | `agents/.agents/skills/use-case-analysis/SKILL.md` | Rubric nội bộ: Actor/Goal/Boundary, pre/post, main/alternative/exception, đối chiếu FR/BR, "no missing steps", cấm tự tạo actor/UC không căn cứ, gắn nhãn PROPOSED. Đã strip phần tương tác/generation, chỉ giữ phần đánh giá. | nguồn thô của team (không đăng ký SRC) |

## 3. Tổng hợp & Nguyên tắc thiết kế cho `re.use-case-analysis`
1. **Unit of evaluation = use case as a whole.** Cấu trúc phần tử, neo extension, mức trừu tượng và tính quyết định được của kết quả là thuộc tính của *flow*, không trùng với 9 đặc tính câu-đơn-lẻ của `re.requirement-quality`; mỗi khi một phàn nàn thực chất là câu chữ, ủy quyền và đóng finding.
2. **Essentials-in-prose counts.** Một phần tử (trigger, precondition) viết trong văn luồng được tính là có, miễn suy ra được không mơ hồ — chống dogma trường-bắt-buộc (nguồn #1 kết hợp guard của local pack).
3. **Extension coverage per risk class.** Input người dùng, quyết định theo BR, gọi hệ thống ngoài là các lớp rủi ro bắt buộc có nhánh hoặc lý do tường minh; with hệ thống ngoài, từ chối và không phản hồi là hai đường riêng.
4. **Intent-vs-mechanism semantic test** cho UCA-R004 thay vì blacklist từ khóa: danh từ cụ thể được phán là vocabulary hay internals theo glossary; locator màn-hình một lần không phải design leak.
5. **Two-sided integrity with graceful degradation:** UCA-R005/R006 chỉ kết luận Issue khi có cả hai vế evidence; thiếu index/convention → Not Assessable hoặc improvement-suggestion. Naming convention là project-decision — skill không có quyền chuẩn hóa, chỉ đối chiếu.
6. **Disclosure over invention:** giả định/chưa chốt phải được gắn cờ (UCA-10); reviewer không tự "hoàn thiện" use case bằng nội dung bịa.

## 4. Ứng viên criteria/rules
| Đề xuất ID | Statement (rút gọn) | Dựa trên (#) | Ghi chú |
|---|---|---|---|
| `UCA-01`..`UCA-04` | Định danh+mục tiêu; actor/boundary; trigger/preconditions; postconditions/guarantee | #1, #2, local #6 | `criteria.yaml` |
| `UCA-05`..`UCA-07` | Kỷ luật bước luồng; phủ extension; nhất quán mức trừu tượng | #1, #4, #5 | `criteria.yaml` |
| `UCA-08`..`UCA-10` | Integrity tham chiếu ID; testability kết quả; cờ giả định | #3, #2, local #6 | `criteria.yaml` |
| `UCA-R001`..`UCA-R006` | Inventory phần tử; step discipline; extension risk-class; design-leak; so sánh resolve ID; so sánh convention | #1..#5 | `rules.yaml`; R005/R006 loại comparison, yêu cầu ≥2 evidence items |

## 5. Điểm chưa chắc chắn / cần xác minh
- **SRC-0007 chưa được đăng ký** trong `knowledge/source-registry.yaml` (proposed; entry bàn giao trong report). Toàn bộ hiểu biết về Cockburn ở đây đến từ trí nhớ/tài liệu thứ cấp — **không giữ toàn văn**; mọi locator chỉ ở mức topic ("seven essentials", "styles/abstraction levels"), không trích số trang, không dẫn câu nguyên văn. Cần xác minh khi có bản sách/chapter hợp pháp.
- Danh sách "essentials" và cách chia extension theo bước là paraphrase có thể chưa sát từng chữ bản gốc; số lượng và tên mục essentials có thể khác ấn bản/nguồn thứ cấp.
- ISO/IEC/IEEE 29148:2018 CÓ các điều khoản mô tả use case/actor ở vùng Clause 6.4 (usage guide), nhưng vì text paywalled và chưa kiểm chứng mức clause, skill CỐ Ý không dẫn locator use-case-specific — chỉ dùng 5.2.5/6.5 conceptual đã đăng ký. Bổ sung sau khi xác minh.
- Ranh giới UCA-08 vs `re.requirement-traceability` (RTR-04/RTR-05 broken-link rules) cần An chốt: hiện phân định "citation resolution nội bộ package" (UCA) vs "ma trận hai chiều/orphans" (RTR); nếu An muốn dồn hết broken-ID cho RTR, UCA-08 hạ thành improvement-suggestion channel.
- `authority_level` của UCA-10 là expert-recommendation (không có chuẩn ngoài cho việc "phải cờ giả định"); origin_note đã khai. Nếu team muốn chuẩn hóa thành internal-convention thì cần origin_note dẫn quyết định họp — hiện chưa có.
- Local pack nhắc "Include/Extend relationships" (phía UML-diagram): đã ĐẨY RA ngoài scope SKILL.md §2.2 (modeling-diagrams) để tránh đánh giá syntax quan hệ như requirement; cần An xác nhận không đưa vào UCA.
