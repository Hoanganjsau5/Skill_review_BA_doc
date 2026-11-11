# Checklist — `re.srs-review` (SRS Structural Review)

Checklist dẫn xuất từ `criteria.yaml` / `rules.yaml`. **Chỉ tham chiếu ID**, không định nghĩa tiêu chí mới tại đây.
Áp dụng khi rà soát **cấu trúc toàn văn tài liệu SRS** (`v0.1.0`, trạng thái `draft`).

## 0. Cổng ngữ cảnh — bắt buộc trước khi đánh giá (Context Gate)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 0.1 | `SRV-01` | Tài liệu được cung cấp là **toàn văn** (`document_completeness_mode: full`) hay chỉ một chương/mục trích ra (`partial`)? Nếu `partial` → mọi kết luận "thiếu mục" phải chuyển thành `Not Assessable`, không được báo Issue. | Chế độ cung cấp + danh sách chương nhận được |
| 0.2 | `SRV-01` | Dự án có **template/mẫu SRS** được khai báo không? Nếu không, ghi rõ đang giả định outline chuẩn phổ biến (IEEE 830 dạng chương — thu hồi ở mức outline, xem `SRC-0010` access note) làm cơ sở đối chiếu. | Template excerpt hoặc ghi chú "assumed baseline" |
| 0.3 | `SRV-06` | Review corpus có **danh mục tài liệu** (`review_corpus_inventory`) không? Không có → kiểm tra "tài liệu được tham chiếu có tồn tại" là `Not Assessable` (chưa tải lên ≠ không tồn tại). | Danh mục corpus hoặc ghi chú thiếu |
| 0.4 | Boundary | KHÔNG đánh giá: chất lượng diễn đạt từng requirement (`re.requirement-quality`), trùng lặp/mâu thuẫn trong tập requirement (`re.requirement-set-quality`), khớp nhu cầu stakeholder (`re.requirement-validation`), link trace đa lớp (`re.requirement-traceability`). Ghi delegation note nếu phát hiện. | Trích dẫn + ID skill nhận chuyển giao |

## 1. Sự hiện diện & không rỗng của các mục bắt buộc (`SRV-01` / `SRV-R001`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 1.1 | `SRV-01` | Chương Introduction tồn tại và có nội dung thực (Purpose, phát biểu Scope)? | Location + excerpt heading/body |
| 1.2 | `SRV-01` | Overall Description phủ product perspective, product functions, user characteristics, constraints, assumptions & dependencies (không mục nào là heading rỗng)? | Section inventory + body-size note |
| 1.3 | `SRV-01` | Chương Specific Requirements tồn tại và mang nội dung, hay chỉ là placeholder? | Location + excerpt |

## 2. Front matter & lịch sử sửa đổi (`SRV-02` / `SRV-R002`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 2.1 | `SRV-02` | Định danh tài liệu + phiên bản hiện hành có rõ không? | Excerpt trang đầu/version block |
| 2.2 | `SRV-02` | Revision history có bảng (phiên bản, ngày, tác giả, mô tả thay đổi) và **khớp** với version khai báo? | Excerpt bảng revision hoặc xác nhận vắng mặt |
| 2.3 | `SRV-02` | Trường phê duyệt theo template: có mặt (kể cả "pending" hợp lệ) hay hoàn toàn vắng? | Location + excerpt |

## 3. Mục lục, đánh số heading & tham chiếu nội bộ (`SRV-03` / `SRV-R003`, `SRV-R004`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 3.1 | `SRV-03` | Mọi mục lục (TOC) khớp heading thật về số và tên; không entry "ma", không heading bị bỏ khỏi TOC? | **Hai bằng chứng**: excerpt TOC + excerpt heading |
| 3.2 | `SRV-03` | Đánh số đề mục liên tục, không trùng, không nhảy số sau chỉnh sửa? | Danh sách heading đánh số |
| 3.3 | `SRV-03` | Mọi tham chiếu "Xem Mục x.y / see Section x.y / Hình n / Bảng n" nội bộ resolve tới phần tử **tồn tại và đúng chủ đề**? | Excerpt tham chiếu + excerpt đích (hoặc xác nhận không tồn tại) |

## 4. Vùng cấu trúc cho từng lớp yêu cầu (`SRV-04` / `SRV-R005`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 4.1 | `SRV-04` | External interfaces có vùng riêng cho từng lớp áp dụng: user, hardware, software, communications? Lớp không áp dụng phải có khai báo tailoring kèm lý do. | Heading inventory + excerpt tailoring |
| 4.2 | `SRV-04` | Non-functional/performance requirements có mục riêng (hoặc fold được template khai báo)? | Location + excerpt |
| 4.3 | `SRV-04` | System features được tổ chức thành các mục feature trong Specific Requirements? | Section list |
| 4.4 | `SRV-04` | Data description tồn tại (inline, hoặc tham chiếu ERD/data dictionary có tên)? | Excerpt tham chiếu dữ liệu |

## 5. Phân bổ feature & quy ước định danh (`SRV-05` / `SRV-R006`, `SRV-R007`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 5.1 | `SRV-05` | Danh sách chức năng ở Overall Description ↔ các mục feature ở chương 3 ánh xạ hai chiều (mỗi feature khai báo có "nhà"; không có mục lạ không khai báo)? | **Hai bằng chứng**: excerpt function list + excerpt heading |
| 5.2 | `SRV-05` | Có requirement block "trôi nổi" nằm ngoài mọi mục được phân bổ không? | Location block |
| 5.3 | `SRV-05` | Tài liệu có **tự khai** quy ước định danh (FR-nn, NFR-nn…)? Quy ước đó được dùng đúng dạng và nhất quán trên **mọi** mục? | Excerpt khai báo quy ước + excerpt các ID vi phạm (nếu có) |
| 5.4 | `SRV-05` | Chuỗi số ID liên tục trong từng họ prefix (hoặc gap có ghi chú renumber bảo lưu)? | Sequence scan note |

## 6. Tài liệu tham chiếu, footnote & phụ lục (`SRV-06` / `SRV-R008`, `SRV-R009`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 6.1 | `SRV-06` | Mọi entry trong danh mục References được dùng chuẩn-normative đều **resolve được** trong review corpus (hoặc được catalog rõ title+version)? | **BẮT BUỘC HAI BẰNG CHỨNG (two-artifact):** excerpt entry reference (SRS) + bằng chứng corpus inventory không chứa nó. Thiếu corpus → `Not Assessable`. |
| 6.2 | `SRV-06` | Mọi footnote/citation trong body đều có entry tương ứng trong References? | Excerpt footnote + excerpt References list |
| 6.3 | `SRV-06` | Phụ lục được viện dẫn normative trong body có tồn tại trong tài liệu? Phụ lục tồn tại nhưng không ai viện dẫn → observation (info), không phải Issue. | Excerpt viện dẫn + appendix inventory |

## 7. Placeholder & nội dung draft chưa xử lý (`SRV-07` / `SRV-R010`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 7.1 | `SRV-07` | Có mục nào thân chỉ là `TBD` / `TODO` / `sẽ bổ sung sau` / hướng dẫn template còn sót lại không? | Heading + body excerpt placeholder |
| 7.2 | `SRV-07` | Khoản hoãn (defer) có được ghi trong open-issues register kèm owner/target release không? | Excerpt register (nếu có) |
| 7.3 | `SRV-07` | Hình/Bảng được hứa ("xem Hình 2.1") nhưng vùng tương ứng trống? | Excerpt hứa + location vùng trống |
| 7.4 | Boundary | TBD **trong một câu requirement** riêng lẻ → `re.requirement-quality` (RQ-04), không ghi ở đây. | Delegation note |

## 8. Kỷ luật trừu tượng cấp mục (`SRV-08` / `SRV-R011`)
| # | Ref | Câu hỏi kiểm tra | Evidence cần ghi |
|---|---|---|---|
| 8.1 | `SRV-08` | Mục được khai báo "chỉ chứa yêu cầu" có chứa **vùng thiết kế/implementation** normative (schema/DDL, kiến trúc microservices, đặc tả dựng màn hình)? | **Hai bằng chứng**: role declaration (template/preamble) + design region excerpt |
| 8.2 | `SRV-08` | Vùng thiết kế có đang **thay thế** nội dung yêu cầu của feature (WHAT biến mất)? | Feature section inventory |
| 8.3 | Boundary | Chi tiết implementation trong **một câu** requirement → `re.requirement-quality` (RQ-02). Interface protocol bị ràng buộc bởi hệ thống ngoài là constraint hợp lệ, không phải design leak. | Delegation note / rationale constraint |

## 9. Kết xuất (Output)
- [ ] Mỗi criterion `SRV-01`..`SRV-08` có trạng thái: `Compliant` / `Issue` / `Not Assessable` / `Not Applicable` — kèm lý do gate nếu `Not Assessable`.
- [ ] Findings so khớp (`comparison`) có ≥ 2 evidence items; riêng `SRV-R008` đúng hợp đồng two-artifact.
- [ ] Limitations/clarification_requests ghi đủ: chế độ `partial`, thiếu template, thiếu corpus inventory, thiếu khai báo ID scheme.
- [ ] Delegation notes cho evidence ngoài biên (xem mục 0.4).
