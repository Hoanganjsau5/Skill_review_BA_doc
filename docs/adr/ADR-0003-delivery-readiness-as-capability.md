# ADR-0003: Delivery Readiness là Cross-domain Capability

- Status: Accepted
- Date: 2026-11-10

## Context
Delivery Readiness cần tổng hợp tri thức từ Requirement Engineering, Software Design, Architecture, QA và kết quả Feasibility. Nó không phải một knowledge domain riêng, và chưa có bằng chứng nó cần quy trình suy luận khác với việc "phán đoán dưới ràng buộc và evidence".

## Decision
- Delivery Readiness là **Capability** (`capabilities/delivery-readiness/`), thực thi bởi Core Agent `solution-assessor` với Profile `delivery-readiness`.
- Không tạo Skill domain riêng; Profile tái sử dụng Skill của các domain liên quan.
- Tiêu chí DoR do từng dự án định nghĩa (`projects/<id>/config/definition-of-ready.yaml`). Hệ thống không cung cấp DoR "chuẩn".
- Không có DoR → verdict là `insufficient-evidence`.

## Điều kiện xem xét tách thành Core Agent riêng (cần ADR mới)
1. Quy trình suy luận khác rõ rệt (ví dụ theo dõi readiness qua nhiều run).
2. Input/output contract không còn phù hợp `solution-assessor`.
3. Cần độc lập trách nhiệm giữa đánh giá feasibility và readiness.

## Consequences
- (+) Không thêm Agent; tái sử dụng tri thức.
- (−) `solution-assessor` có hai Profile với output khác nhau; phân biệt bằng Profile và schema.
