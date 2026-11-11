---
note_id: RN-0001
topic: "Individual Requirement Quality — Multi-Language & Multi-Artifact Evaluation (ISO/IEC/IEEE 29148, NASA, INCOSE)"
target_skills: [re.requirement-quality]
sources: [SRC-0001, SRC-0002, SRC-0003, SRC-0004]
author: Skill System Architect
created_at: 2026-11-11
status: complete
---

# Research Note: Individual Requirement Quality (`re.requirement-quality`)

## 1. Câu hỏi nghiên cứu
1. Làm thế nào để chuẩn hóa 9 đặc tính chất lượng của một yêu cầu đơn lẻ (ISO/IEC/IEEE 29148:2018 Clause 5.2.5) thành bộ tiêu chí độc lập ngôn ngữ tự nhiên (Language-independent Core) và độc lập loại tài liệu (Artifact-independent)?
2. Khi nào một tiêu chí có thể đánh giá chỉ từ bản thân câu yêu cầu (statement alone), khi nào bắt buộc phải trả về `Not Assessable` do thiếu ngữ cảnh, và khi nào thực sự là `Not Applicable`?
3. Làm thế nào để tách biệt các mẫu từ vựng/ngữ pháp theo ngôn ngữ (English `en`, Vietnamese `vi`, mở rộng sang `ja`...) thành các tín hiệu phát hiện (heuristic signals) mà không biến chúng thành lỗi tự động (false positives)?

## 2. Trích xuất từ nguồn
| # | source_id | Locator | Nội dung trích xuất (tóm tắt) | authority_level |
|---|---|---|---|---|
| 1 | `SRC-0001` | Clause 5.2.5 | 9 đặc tính của một yêu cầu đơn lẻ: Necessary, Appropriate, Unambiguous, Complete, Singular, Feasible, Verifiable, Correct, Conforming. Tách biệt với đặc tính của tập yêu cầu ở Clause 5.2.6. | `official-standard` |
| 2 | `SRC-0002` | Appendix C | Các dấu hiệu ngôn ngữ gây mơ hồ (tính từ định tính, từ nối `and/or`, cụm từ mở `etc.`, đại từ mơ hồ), yêu cầu ghép (compound obligations), và lưu ý không áp đặt số đo định lượng khi kiểm chứng hành vi/trạng thái là đủ. | `industry-best-practice` |
| 3 | `SRC-0003` | Section 4.2 | Vai trò của requirement rationale và parent need trong việc đánh giá `Necessary` và `Correct`; đánh giá mức trừu tượng (`Appropriate`) và phân biệt ràng buộc hợp lệ (valid constraint) với thiết kế sớm (premature design); đánh giá `Feasible` cần thông tin ràng buộc kỹ thuật/tài nguyên. | `industry-best-practice` |
| 4 | `SRC-0004` | GtWR v4 Summary | Tách biệt rõ chất lượng câu yêu cầu đơn lẻ và tập yêu cầu; phân biệt quy tắc cấu trúc/ngữ nghĩa với quy ước mẫu câu của dự án (`Conforming`); cảnh báo false-positive khi bắt từ khóa máy móc. | `industry-best-practice` |

## 3. Tổng hợp & Nguyên tắc thiết kế cho `re.requirement-quality`
1. **Language-independent Core vs. Language Packs:**
   - 9 tiêu chí (`RQ-01` .. `RQ-09`) trong `criteria.yaml` và các quy tắc suy luận trong `rules.yaml` chỉ định nghĩa bản chất ngữ nghĩa và cấu trúc logic, không chứa từ vựng tiếng Anh hay tiếng Việt.
   - Các mẫu từ vựng mơ hồ, lượng từ bất định, đại từ không rõ tiền từ, từ nối ghép và lưu ý ngữ pháp đặc thù của từng ngôn ngữ được tách vào `language-packs/en.yaml` và `language-packs/vi.yaml`.
   - Mọi khớp mẫu từ Language Pack chỉ là **Detection Signal (`Heuristic`)**, bắt buộc qua bước đánh giá ngữ cảnh trước khi kết luận `Issue`.
2. **Phân biệt Criterion Status và Finding:**
   - Mỗi cặp `(Requirement, Criterion)` có một trạng thái đánh giá: `Compliant`, `Issue`, `Not Assessable`, hoặc `Not Applicable`.
   - Chỉ tạo `Finding` khi `Status = Issue` (hoặc `needs-clarification` khi `Not Assessable` do thiếu thông tin trọng yếu ngăn cản việc hiểu/thực thi yêu cầu).
3. **Context Dependency Gate (Chống suy diễn khi thiếu ngữ cảnh):**
   - Các tiêu chí tự thân (`Unambiguous`, `Singular`, và một phần `Complete`, `Verifiable`) thường có thể đánh giá trực tiếp trên câu yêu cầu.
   - Các tiêu chí phụ thuộc ngữ cảnh ngoài (`Necessary`, `Correct`, `Feasible`, `Conforming`, và một phần `Appropriate`) **bắt buộc** trả về `Not Assessable` khi thiếu thông tin nguồn gốc, ràng buộc hoặc quy ước dự án, trừ khi bản thân câu yêu cầu tự mâu thuẫn.

## 4. Ứng viên criteria/rules
| Đề xuất ID | Statement | Dựa trên (# trích xuất) | Ghi chú |
|---|---|---|---|
| `RQ-01` .. `RQ-09` | 9 Core Criteria tương ứng Necessary, Appropriate, Unambiguous, Complete, Singular, Feasible, Verifiable, Correct, Conforming | #1, #2, #3, #4 | Định nghĩa trong `criteria.yaml` |
| `RQ-R001` .. `RQ-R018` | 18 Rules định nghĩa phương pháp phát hiện & đánh giá cho 9 tiêu chí (kết hợp Structural validation, Context-dependent reasoning, Deterministic pattern detection qua Language Pack, Expert judgment) | #1, #2, #3, #4 | Định nghĩa trong `rules.yaml` |

## 5. Điểm chưa chắc chắn / Giới hạn xác minh
- Văn bản đầy đủ của `ISO/IEC/IEEE 29148:2018` và `INCOSE GtWR v4` là tài liệu có bản quyền/thu phí; nghiên cứu này xác minh qua catalog chính thức, tóm tắt chính thức của INCOSE RWG và tài liệu kỹ thuật công khai của NASA (`SRC-0002`, `SRC-0003`). Không trích dẫn nguyên văn câu chữ có bản quyền.
