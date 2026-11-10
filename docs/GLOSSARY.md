# GLOSSARY

| Thuật ngữ | Định nghĩa |
|---|---|
| **Orchestrator** | Thành phần điều phối trung tâm. Hiểu task, lập execution plan, routing, quản lý phụ thuộc, phát hiện/giải quyết conflict theo thủ tục, tổng hợp. Không chứa tri thức chuyên môn. |
| **Capability** | Năng lực đánh giá tổng hợp (Document Quality, Feasibility & Risk, Delivery Readiness). Định nghĩa Profiles cần dùng, phases, aggregation rules, verdict rules. Không chứa tri thức chuyên môn. |
| **Core Agent** | Instruction template định nghĩa theo kiểu suy luận và trách nhiệm thực thi. Không phải process. |
| **Specialist Profile** | Cấu hình vai trò: phạm vi chuyên môn, artifact áp dụng, Core Agent thực thi, Skills cần nạp. |
| **Assignment** | Một đơn vị thực thi: đúng 1 Core Agent + 1 Profile + Skills + scope + context slice riêng, cho ra đúng 1 `review-result`. |
| **Skill** | Module tri thức chuyên môn đã chuẩn hóa: procedure, criteria, rules, checklist, examples. Độc lập dự án, có version và status. |
| **Criterion** | Tiêu chí đánh giá có thể kiểm tra trên một artifact; có `criterion_id` vĩnh viễn và `source_refs`. |
| **Analysis rule** | Quy tắc phân tích cấu trúc/quan hệ trên tập artifact (coverage, orphan…). |
| **Comparison rule** | Quy tắc so sánh thuộc tính/khẳng định giữa ≥ 2 artifact. |
| **Effective status** | Status thấp nhất của một Skill và toàn bộ dependency (bắc cầu). |
| **Knowledge Base** | Kho nguồn gốc: source registry, tóm tắt chuẩn, references, research notes. Dùng để xây dựng Skill, không nạp mặc định khi review. |
| **Source** | Một tài liệu nguồn được đăng ký với `source_id`, version/edition, authority level. |
| **Project Context** | Thông tin đặc thù dự án (mục tiêu, scope, ràng buộc, team, hạ tầng, quyết định…), mỗi trường có status `provided/missing/assumed/not-applicable`. |
| **Context slice** | Phần Project Context được cấp cho một Assignment cụ thể. |
| **Finding** | Vấn đề phát hiện trong tài liệu/thiết kế, có basis và evidence. |
| **Risk** | Sự kiện bất định có thể ảnh hưởng tiêu cực đến kết quả dự án. |
| **Feasibility Assessment** | Phán quyết khả thi của một scope, kèm evidence, assumptions, conditions, confidence. |
| **Delivery Readiness Assessment** | Phán quyết mức sẵn sàng của một scope cho stage tiếp theo, dựa trên DoR do dự án định nghĩa. |
| **DoR (Definition of Ready)** | Bộ tiêu chí sẵn sàng do từng dự án định nghĩa; hệ thống không áp đặt DoR phổ quát. |
| **Critic validation** | Kết quả kiểm chứng độc lập của Critic đối với một output: `validated / challenged / rejected`. |
| **Conflict record** | Bản ghi phát hiện, phân tích và quyết định về một conflict; không sửa output gốc. |
| **Coverage gap** | Phần đánh giá không thực hiện được do Skill bị loại (planned, dependency lỗi…). |
| **Review Run** | Một lần thực thi review, lưu tại `projects/<id>/reviews/<run-id>/`. |
| **Run manifest** | Bản ghi phiên bản/hash/cấu hình của mọi thứ dùng trong một run. |
| **CapturedValue** | Giá trị kèm `capture_status: captured / unavailable / not-applicable` và lý do. |
| **HITL** | Human-in-the-loop: điểm cần con người làm rõ hoặc quyết định. |
| **Runtime Adapter** | (Tương lai) lớp ánh xạ kiến trúc logic sang một nền tảng thực thi cụ thể. |
