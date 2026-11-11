# Checklist — Acceptance Criteria (`re.acceptance-criteria`)

Checklist dẫn xuất từ `criteria.yaml` / `rules.yaml` (Skill version `0.1.0`, trạng thái `draft`). **Chỉ tham chiếu ID**, không định nghĩa tiêu chí mới tại đây.

## 0. Gate trước khi đánh giá (bắt buộc ghi nhận)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 0.1 | §10 B1 | Định dạng AC của dự án đã được khai báo hay suy ra nhất quán chưa (Gherkin / bảng / gạch đầu dòng / văn xuôi)? | Tên định dạng + tài liệu quy ước (hoặc mẫu nhất quán quan sát được). |
| 0.2 | §10 B1 | Phạm vi review (release/module) và `completeness_mode` (full/partial) đã rõ chưa? | Khai báo phạm vi; nếu thiếu → giới hạn đánh giá ACA-04/ACA-05. |
| 0.3 | §4.2 | Ranh giới từng AC xác định được chắc chắn không (một gạch đầu dòng ≠ một AC)? | Danh sách AC đã chuẩn hóa + các đoạn nghi ngờ ranh giới. |
| 0.4 | §4.2 | Bộ owner item (FR/UC/story) kèm id và text có nằm trong package không? | Liệt kê owner id; chỗ thiếu → Not Assessable, cấm suy diễn. |

## 1. ACA-01 — Verifiable & Observable Outcome (`ACA-R001`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 1.1 | `ACA-01` | Mỗi AC có nêu kết quả quan sát được để quyết định pass/fail mà không phải đoán không? | Trích nguyên văn AC + một câu chỉ ra khoảng hở diễn giải (hoặc ngưỡng đạt). |
| 1.2 | `ACA-R001` | Với outcome nhạy cảm số lượng (thời gian, số lần, kích thước, tỉ lệ), ngưỡng/cận đã được nêu hoặc dẫn chiếu định nghĩa rõ chưa? | Ngưỡng tìm thấy hoặc câu "không có ngưỡng" kèm vị trí. |
| 1.3 | `ACA-R001` | Anti-dogma: AC định tính nhưng hành vi kiểm chứng được (thông báo hiển thị, trạng thái bản ghi) đã được THẢ, không ép thêm số? | Ghi chú suppress nếu có tín hiệu từ vựng mà không có khe hở diễn giải. |

## 2. ACA-02 — Given/When/Then Well-formedness (`ACA-R002`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 2.1 | `ACA-02` | Dự án dùng định dạng GWT không? Nếu không và không có khóa GWT → Not Applicable có kèm justification. | Khai báo định dạng của dự án. |
| 2.2 | `ACA-R002` | Given chỉ chứa tiền trạng thái/dữ kiện; When chứa đúng hành động của actor; Then chứa kết quả hệ thống quan sát được? | Trích clause đặt sai khe (nếu có). |
| 2.3 | `ACA-R002` | And-clause chỉ mở rộng cùng một kết quả (trạng thái dữ liệu + phản hồi người dùng) — KHÔNG báo lỗi atomicity cho pattern này. | Ghi chú khi suppress. |

## 3. ACA-03 — Atomicity (`ACA-R003`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 3.1 | `ACA-R003` | Test "failure độc lập": hai vế nối bằng và/and/or có thể một pass một fail không? Nếu có và thuộc hai mối quan tâm khác nhau → Issue. | Ngắt các vế trong trích dẫn + đề xuất tách. |
| 3.2 | `ACA-R003` | "và/hoặc" để ngỏ phương án được chấp nhận → chuyển/ghép phát hiện sang `ACA-08`. | Hai cách đọc cạnh tranh của vế nối. |

## 4. ACA-04 — Bidirectional AC–Owner Coverage (`ACA-R004`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 4.1 | `ACA-R004` | Chiều 1: mọi owner item trong phạm vi khai báo có ≥1 AC không? | Danh sách owner id zero-AC (chỉ khi completeness_mode=full). |
| 4.2 | `ACA-R004` | Chiều 2: mọi AC có neo (anchor) resolve được tới owner item không? | AC id + anchor hỏng/vago; owner id tham chiếu. |
| 4.3 | `ACA-04` | Partial package: khoảng trống so với section chưa cung cấp → Not Assessable + clarification, KHÔNG kết luận "thiếu AC". | Mục lục package + yêu cầu bổ sung ngữ cảnh. |
| 4.4 | Boundary | Câu hỏi phủ rộng scope của requirement set → delegate `re.requirement-set-quality` (RSQ-01/RSQ-02); cấu trúc ma trận trace → `re.requirement-traceability`. | delegated_observations ghi rõ skill đích. |

## 5. ACA-05 — Negative/Edge/Error-Path Presence (`ACA-R005`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 5.1 | `ACA-R005` | Failure/boundary mode nào được nêu TRONG owner item text (validation rule, limit, lời gọi ngoài, quyền)? | Trích owner item từng mode. |
| 5.2 | `ACA-R005` | Mỗi mode đáng kể có AC quyết định acceptance không? Chỉ tìm trong package — cấm bịa mode "hợp lý". | Cặp (mode → AC id) hoặc gap đã trích dẫn. |
| 5.3 | `ACA-05` | Owner item thuần hiển thị tĩnh, không đổi trạng thái/lời gọi ngoài → Not Applicable theo từng item. | Justification per item. |

## 6. ACA-06 — No Creep, No Design Lock-in (`ACA-R006`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 6.1 | `ACA-R006` | Diff nghĩa vụ AC vs owner item: AC có thêm kênh/bản ghi/integration/ngưỡng mới không? | Hai trích dẫn nguyên văn (AC + owner). |
| 6.2 | `ACA-R006` | AC nêu cơ chế implementation (table, endpoint, công nghệ) như ĐIỀU KIỆN nghiệm thu → Issue; nếu constraint đã được duyệt ở design doc → hạ mức, ghi chú. | Cơ chế bị nêu + nguồn constraint (nếu có). |
| 6.3 | `ACA-R006` | Anti-FP: AC định lượng để LÀM CHẶT owner item mơ hồ → clarification request đề xuất wording, không phải creep defect. | Hai bản thể hiện của ngưỡng. |

## 7. ACA-07 — AC Identity & Numbering (`ACA-R007`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 7.1 | `ACA-R007` | Id AC có duy nhất trong suite/trong owner item không? | Cặp id trùng nguyên văn. |
| 7.2 | `ACA-R007` | Quy ước đánh số (TC-01 per story, AC-<story>.<n>…) có nhất quán/khai báo; numbering reset có prefix để tham chiếu cross-story hết mơ hồ không? | Mẫu quan sát được hoặc quy ước khai báo. |
| 7.3 | `ACA-R007` | Nhiều kiểu xung đột mà không khai báo → needs-clarification, không phải defect. | Các kiểu mâu thuẫn. |

## 8. ACA-08 — Unambiguous Acceptance Wording (`ACA-R008`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 8.1 | `ACA-R008` | Quét tín hiệu: định tính mơ hồ (vi: nhanh, nhanh chóng, kịp thời, dễ, dễ dàng, hợp lý; en: fast, easy, appropriate, user-friendly), escape clause ('khi cần thiết', 'as needed'), danh sách mở ('v.v.', 'etc.'), actor/object/thời điểm/quyền/hành vi xung đột chưa chỉ định. | Từ tín hiệu + vị trí. |
| 8.2 | `ACA-R008` | Gate bắt buộc: xây được HAI cách đọc accept/reject khác nhau không? Không xây được → suppress (không báo lỗi chỉ vì có từ). | Hai cách đọc + vì sao khác biệt quan trọng. |
| 8.3 | `ACA-R008` | Mỗi Issue kèm wording đề xuất testable; định nghĩa nằm ngoài package → Not Assessable + clarification. | Bản sửa ứng viên / yêu cầu ngữ cảnh. |

## 9. ACA-09 — AC Duplication & Contradiction (`ACA-R009`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 9.1 | `ACA-R009` | Cluster AC theo owner+behavior; hai AC cùng ĐIỀU KIỆN cho kết quả mâu thuẫn (24h vs 48h)? | ≥2 trích dẫn nguyên văn với id + điều kiện chồng lấn. |
| 9.2 | `ACA-R009` | AC có mâu thuẫn với functional description của chính owner item không? | Cặp AC vs owner excerpt. |
| 9.3 | `ACA-R009` | Anti-FP: điều kiện khác nhau thì kết quả khác nhau KHÔNG phải contradiction; phân cấp umbrella/story-level có cross-reference là duplication-có-chủ-đích. | Ghi chú suppress. |

## 10. ACA-10 — Stated Demonstration (`ACA-R010`)

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 10.1 | `ACA-R010` | Mỗi AC có phương thức chứng minh (per-AC hoặc suite-level mapping trong package)? | Trích method/column hoặc dòng mapping phủ AC. |
| 10.2 | `ACA-R010` | Loại bằng chứng của method có khớp loại outcome không (timing→đo tự động; layout→demo ảnh; state→kiểm dữ liệu)? | Cặp (AC outcome, method) khi nghi lệch. |
| 10.3 | `ACA-R010` | 'Verify as appropriate' / placeholder → Issue; method ở test plan ngoài package → Not Assessable + yêu cầu plan. | Placeholder nguyên văn / tên plan thiếu. |

## 11. đóng gói kết quả

| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|-----|------------------|------------------|
| 11.1 | §7 | Mỗi finding mang basis đúng (`criterion`/`analysis-rule`/`comparison-rule`), owner `re.acceptance-criteria@0.1.0`, item id ACA-*? | JSON basis. |
| 11.2 | §3 | Quan sát ngoài ranh giới đã delegate (requirement-quality / requirement-set-quality / requirement-traceability / requirement-validation / qa.*)? | delegated_observations. |
| 11.3 | §6 | Not Applicable nào cũng có justification theo `not_applicable_conditions`, không dùng để né đánh giá khó? | Lý do NA từng criterion. |
