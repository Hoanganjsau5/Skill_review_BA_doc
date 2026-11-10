# ADR-0002: Core Agents, Specialist Profiles và Profile Execution Isolation

- Status: Accepted
- Date: 2026-11-10

## Context
Danh sách vai trò ban đầu có ≥ 11 Agent theo loại tài liệu. Phần lớn có cùng hành vi ("đọc artifact, đối chiếu tiêu chí, xuất Finding"), chỉ khác tri thức. Đồng thời cần quy trách nhiệm kết quả theo từng vai trò chuyên môn.

## Decision
1. Ba lớp tách biệt:
   - **Core Agent** — theo kiểu suy luận và trách nhiệm thực thi (5): `artifact-reviewer`, `cross-artifact-analyzer`, `solution-assessor`, `critic`, `report-synthesizer`.
   - **Specialist Profile** — cấu hình vai trò, phạm vi, Skills (10, ban đầu ở trạng thái `draft`).
   - **Skill** — tri thức.
2. Chỉ tạo Core Agent mới khi có ít nhất một: (a) kiểu suy luận khác, (b) input/output contract khác, (c) yêu cầu độc lập trách nhiệm. Phải có ADR.
3. **Profile Execution Isolation:**
   - 1 Assignment = đúng 1 Profile; có `assignment_id`, scope, context slice, output riêng.
   - Được chia 1 Profile thành nhiều Assignment; **không** gộp nhiều Profile vào 1 Assignment.
   - Song song khi không phụ thuộc.
   - Critic luôn ở Assignment tách biệt với producer.
   - Isolation ở mức execution context, không phải process (ADR-0007 / ARCHITECTURE §7).
4. Batching trong tương lai phải giữ quy trách nhiệm theo Profile và cần ADR mới.

## Consequences
- (+) Không Agent proliferation; mở rộng vai trò = thêm Profile.
- (+) Mỗi Finding/Risk/Verdict truy được về assignment và profile.
- (−) Số lần gọi model nhiều hơn so với gộp Profile.
