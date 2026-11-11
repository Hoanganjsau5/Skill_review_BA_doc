# Examples — `re.srs-review`

Thư mục chứa bộ Golden Test Cases và các ví dụ tổng hợp cho skill rà soát **cấu trúc tài liệu SRS**.

## Files

| File | Nội dung |
|---|---|
| `golden-test-cases.yaml` | 10 test cases chuẩn hóa (`SRV-GTC-01`..`SRV-GTC-10`) — input context, expected criterion statuses, expected findings, explanation. |
| `synthetic-examples.md` | 7 walkthrough dạng văn bản mô tả từng pattern phát hiện chính và ranh giới ủy quyền. |

## Test Case Index

| ID | Lang | Scenario (một dòng) |
|---|---|---|
| `SRV-GTC-01` | en | Thiếu section bắt buộc của Overall Description (Constraints, Assumptions & Dependencies) + không có home cho software/communications interfaces (`SRV-01`, `SRV-04`); SRV-02/03 Not Assessable do bản convert mất front matter/TOC. |
| `SRV-GTC-02` | vi | Section bị đánh số lại nhưng TOC không cập nhật; "Xem Mục 3.4" trong FR-21 rơi vào section sai chủ đề (`SRV-03` / `SRV-R003`, `SRV-R004`). |
| `SRV-GTC-03` | en | **Two-artifact rule**: `[R1] ICD-PAY-02 v1.3` được dùng normative nhưng corpus inventory không chứa nó; "Appendix D" được viện dẫn dù phụ lục dừng ở C (`SRV-06` / `SRV-R008`, `SRV-R009`). |
| `SRV-GTC-04` | en | **Not Assessable gate**: chỉ dán một section lẻ (`partial`) → mọi kết luận "thiếu toàn tài liệu" là Not Assessable, zero findings bịa đặt; `SRV-08` vẫn assessable. |
| `SRV-GTC-05` | vi | **Chống false-positive tailoring**: Hardware/Communications interfaces vắng nhưng được khai báo out-of-scope kèm lý do tại §1.6 → `Compliant`, không Issue. |
| `SRV-GTC-06` | en | **Boundary → `re.requirement-quality`**: tài liệu cấu trúc hoàn hảo nhưng câu FR-12 mơ hồ ("quickly/relevant"), FR-13 compound → mọi SRV Compliant, delegation note sang RQ-03/RQ-05. |
| `SRV-GTC-07` | vi | **Boundary → `re.requirement-set-quality`**: FR-07 (tự động hoàn tiền 24h) mâu thuẫn FR-22 (phải duyệt thủ công) → delegation note sang RSQ-03; cấu trúc tài liệu sạch, mọi SRV Compliant. |
| `SRV-GTC-08` | vi | Section placeholder cấp tài liệu ("3.8 [TBD — sẽ bổ sung sau]", scaffolding template sót lại) + ID `NF-301` phá vỡ scheme `FR-nn` tự khai ở §1.4 (`SRV-07`, `SRV-05`). |
| `SRV-GTC-09` | vi | Design leak cấp region: chương khai báo "chỉ chứa yêu cầu" nhưng chứa `3.9 Thiết kế CSDL` (DDL) và `3.10 Kiến trúc microservices` thay thế phần WHAT của feature (`SRV-08`). |
| `SRV-GTC-10` | en | **Golden compliant baseline**: SRS v2.0 đầy đủ front matter/revision history, TOC đồng bộ, references resolve (kể cả chuẩn công khai định danh bằng title+edition), scheme uniform, không placeholder, thiết kế nằm ở SDD — toàn bộ `Compliant`. |

## Ghi chú sử dụng

- Trạng thái chuẩn: `[Compliant, Issue, Not Assessable, Not Applicable]` (khớp `status_enum` trong `golden-test-cases.yaml`).
- `Not Assessable` ≠ `Not Applicable`: NA vì thiếu context (partial mode, thiếu corpus inventory) phải kèm `limitations`/`clarification_requests`; N/A chỉ dùng khi template/tailing khai báo không áp dụng.
- Findings của các rule `comparison` (`SRV-R003`, `SRV-R006`, `SRV-R008`, `SRV-R009`) bắt buộc ≥ 2 evidence items; `SRV-R008` là hợp đồng two-artifact (SRS side + corpus side).
- `validation.status` toàn bộ là `unvalidated` ở `0.1.0` — bộ GTC là tư liệu chờ xác minh hành vi khi runtime sẵn sàng.
