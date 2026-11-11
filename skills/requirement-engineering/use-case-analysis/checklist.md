# Review Checklist — Skill: `re.use-case-analysis`

Sử dụng kèm phiên bản skill được khai báo trong `SKILL.md` (hiện: 0.1.0). Mỗi câu hỏi chỉ được trả lời Issue sau khi đã qua cổng ngữ cảnh ở mục 0 và các gate Not Assessable / Not Applicable của criterion tương ứng.

## 0. Cổng tiền-đánh giá (Pre-Assessment Gate)
- [ ] Xác định representation của use-case: bảng đặc tả có trường riêng, văn prose đánh số bước, hay danh sách tóm tắt? Không parse được → ghi `limitations[]`, KHÔNG bịa trường đã có.
- [ ] Tài liệu có khai báo level (summary/outline vs user-goal chi tiết)? Nếu khai báo outline → áp gate Not Applicable theo mức khai báo, không đòi đủ mọi trường.
- [ ] Package đánh giá có kèm index ID (SRS/BR extract) hoặc quy ước định danh không? Không có → UCA-08 = Not Assessable, UCA-R006 chỉ ra improvement-suggestion theo pattern corpus.
- [ ] **Enforce Skill Boundaries:** KHÔNG đánh giá câu chữ mơ hồ/hợp nhất của từng requirement đơn lẻ (→ `re.requirement-quality`), trùng lặp/scope toàn set (→ `re.requirement-set-quality`), ma trận trace hai chiều/orphan (→ `re.requirement-traceability`). Ghi nhận ủy quyền, mở Finding ở skill đó.]

## 1. Định danh & mục tiêu (UCA-01 / UCA-R001, UCA-R006)
- [ ] Mỗi use case có ID ổn định, không trùng trong phạm vi review?
- [ ] Tên diễn đạt một mục tiêu nghiệp vụ của primary actor (không phải tên màn hình/tính năng)?
- [ ] (Nếu có quy ước ID được cung cấp) Định dạng/series có theo quy ước?

## 2. Actor & hệ thống ranh giới (UCA-02 / UCA-R001)
- [ ] Primary actor được nêu và khớp với mục tiêu?
- [ ] Secondary actor (kể cả hệ thống ngoài) được liệt kê hoặc suy ra được từ chủ ngữ các bước?
- [ ] Có bước nào hành động được thực hiện bởi bên vô danh ("hệ thống kiểm tra với ngân hàng" mà bank chưa từng là actor)?

## 3. Trigger & điều kiện tiền (UCA-03 / UCA-R001)
- [ ] Có khai báo điều kiện khởi động (người dùng mở màn hình, sự kiện, lịch)?
- [ ] Trạng thái đầu (đã đăng nhập, đã có giỏ hàng...) được khai báo ở Preconditions hay bị ẩn trong bước 1?

## 4. Hậu điều kiện & bảo đảm thành công (UCA-04 / UCA-R001)
- [ ] Kết thúc luồng chính nêu rõ hệ thống bảo đảm điều gì, cho TỪNG actor liên quan?
- [ ] Các nhánh lỗi có tối thiểu "minimal guarantee" (không đặt chỗ, không trừ tiền)?

## 5. Kỷ luật bước luồng chính (UCA-05 / UCA-R002)
- [ ] Các bước được đánh số để extension neo được (3a, 5b...)?
- [ ] Mỗi bước một nghĩa vụ, chủ thể rõ (actor ↔ system luân phiên)?
- [ ] Vòng lặp/ lặp lại nêu rõ vật được lặp và điều kiện dừng?

## 6. Nhánh alternate/exception (UCA-06 / UCA-R001, UCA-R003)
- [ ] Mỗi bước loại rủi ro (input người dùng, quyết định theo BR, gọi hệ thống ngoài) có extension hoặc lý do không-có-gì?
- [ ] Trường hợp hệ thống ngoài từ chối VÀ không phản hồi/timeout đều có đường xử lý?
- [ ] Extension có neo bước rẽ và nêu quay lại luồng / kết thúc với hậu trạng thái?

## 7. Mức trừu tượng (UCA-07 / UCA-R004)
- [ ] Basic flow mô tả WHAT/RESPONSE, không kể HOW nội bộ (widget, bảng DB, payload)?
- [ ] Granularity nhất quán — không nhảy giữa mức summary và mức keystroke trong cùng luồng?
- [ ] Thuật ngữ cụ thể là domain vocabulary hay design leak (đối chiếu glossary)?

## 8. Tham chiếu chéo (UCA-08 / UCA-R005)
- [ ] Mọi BR-xx/FR-xx trích trong use case resolve được trong index được cung cấp? (Finding cần ≥2 evidence item: trích use case + trích index.)
- [ ] Tham chiếu khớp chủ đề với nội dung BR/FR được dẫn?

## 9. Khả năng kiểm chứng kết quả (UCA-09 / UCA-R005)
- [ ] Mỗi trạng thái kết thúc (success + extension terminal) quyết định được đúng/sai mà không bịa threshold số?
- [ ] Ngôn ngữ định tính ("xác nhận phù hợp") có neo BR/artifact tên rõ?

## 10. Giả định & câu hỏi mở (UCA-10 / UCA-R001)
- [ ] Nội dung chưa chốt (hành vi bên thứ ba, chính sách chờ duyệt) được gắn cờ TBD/PROPOSED thay vì viết như sự thật?
- [ ] Có mâu thuẫn giữa bước "chốt rồi" và tài liệu khác nói chủ đề còn mở?
