# SYSTEM_CONFIG

Cấu hình và chính sách toàn cục của hệ thống. Các giá trị đánh dấu **[configurable]** có thể được ghi đè ở cấp dự án qua `projects/<id>/config/review-config.yaml` (trừ khi ghi chú khác).

---

## 1. System identity

| Key | Value |
|---|---|
| `system_name` | Agentic Review System |
| `system_version` | `0.1.0` |
| `lifecycle_stage` | foundation (chưa có Skill validated) |
| `schema_dialect` | JSON Schema 2020-12 |
| `schema_base_uri` | `https://schemas.agentic-review-system.example/` (định danh, không phải endpoint) |
| `communication_language` | Tiếng Việt; giữ thuật ngữ kỹ thuật tiếng Anh |
| `file_formats` | Markdown (tài liệu), YAML (config/metadata), JSON Schema (contracts), JSON (runtime output) |

## 2. Evidence & Knowledge Quality Policy (bắt buộc, không ghi đè)

1. **Không bịa** professional standards, benchmarks, technology capabilities, project facts.
2. Claim định lượng hoặc nhạy cảm thời gian (performance, scalability, cost, technology maturity) phải dựa trên: benchmark do người dùng cung cấp, tài liệu chính thức của vendor, kết quả test tái lập được, technical specification đã xác minh, hoặc nguồn nghiên cứu đáng tin cậy. **Không dựa duy nhất vào trí nhớ của model.**
3. Khi không đủ evidence → trả về `Insufficient Evidence` thay vì đoán.
4. Phân biệt `authority_level`:

| authority_level | Ý nghĩa | Được dùng trong |
|---|---|---|
| `official-standard` | Chuẩn chính thức (ISO/IEC/IEEE, đặc tả chính thức…) | Skill |
| `industry-best-practice` | Thực hành được công nhận rộng rãi, có nguồn | Skill |
| `expert-recommendation` | Khuyến nghị của chuyên gia/tác giả có uy tín, có nguồn | Skill |
| `internal-convention` | Quy ước nội bộ của hệ thống/tổ chức, có nguồn gốc ghi nhận | Skill, Capability, SYSTEM_CONFIG |
| `project-decision` | Quyết định của một dự án cụ thể | **Chỉ** Project Context |

## 3. Severity scale — `internal-convention` [configurable]

> Đây là quy ước nội bộ của hệ thống, **không phải chuẩn quốc tế**.

| Level | Ý nghĩa |
|---|---|
| `critical` | Ngăn cản việc sử dụng tài liệu/giải pháp cho mục đích dự kiến, hoặc có khả năng gây sai lệch nghiêm trọng ở giai đoạn sau nếu không xử lý |
| `major` | Ảnh hưởng đáng kể đến tính đúng/đủ/nhất quán; cần xử lý trước khi chuyển giai đoạn |
| `minor` | Ảnh hưởng hạn chế; nên xử lý |
| `info` | Ghi nhận hoặc gợi ý cải thiện, không phải lỗi |

## 4. Confidence scale — `internal-convention` [configurable]

| Level | Ý nghĩa |
|---|---|
| `high` | Evidence trực tiếp, đầy đủ; basis có authority rõ; không phụ thuộc assumption chưa xác nhận |
| `medium` | Evidence có nhưng gián tiếp/không đầy đủ, hoặc phụ thuộc assumption hợp lý chưa xác nhận |
| `low` | Evidence yếu hoặc phụ thuộc nhiều assumption; cần xác minh thêm |

## 5. Verdict sets (cố định)

- **Finding classification:** `confirmed-issue`, `potential-issue`, `needs-clarification`, `improvement-suggestion`.
- **Feasibility verdict:** `feasible`, `conditionally-feasible`, `not-feasible`, `insufficient-evidence`.
- **Delivery Readiness verdict:** `ready`, `ready-with-conditions`, `not-ready`, `insufficient-evidence`.
- **Risk likelihood/impact:** chỉ được gán giá trị khi dự án định nghĩa `risk-assessment-method.yaml`; nếu không → `not-assessed`.

## 6. Finding basis policy

| basis.type | Producer hợp lệ | Ràng buộc |
|---|---|---|
| `criterion` | artifact-reviewer | — |
| `analysis-rule` | cross-artifact-analyzer | — |
| `comparison-rule` | cross-artifact-analyzer | ≥ 2 evidence từ ≥ 2 artifact khác nhau |
| `expert-judgment` | artifact-reviewer, cross-artifact-analyzer | Không được là `confirmed-issue`; bắt buộc qua Critic |

Mọi Finding bắt buộc có `evidence` (≥ 1) và `rationale`.

## 7. Skill lifecycle & usage [configurable: `allow_draft_skills`]

| Status | Dùng trong review |
|---|---|
| `planned` | Không |
| `draft`, `under-review` | Chỉ khi `allow_draft_skills: true`; report gắn cờ |
| `validated` | Có (mặc định) |
| `deprecated` | Có, kèm cảnh báo |
| `retired` | Không |

Áp dụng theo **effective status** = status thấp nhất trong chuỗi dependency (thứ tự `draft` < `under-review` < `validated`).

## 8. Versioning policy

- Mọi asset (System, Orchestrator, Core Agent, Profile, Capability, Skill, Schema) dùng **SemVer** `MAJOR.MINOR.PATCH`.
- Skill: MAJOR = đổi/bỏ criteria/rules; MINOR = thêm criteria/rules; PATCH = sửa lời văn, không đổi ngữ nghĩa.
- Schema: MAJOR = thay đổi phá vỡ tương thích; MINOR = thêm trường tùy chọn; PATCH = sửa mô tả.
- ID của criterion/rule là vĩnh viễn; không tái sử dụng sau khi retired.

## 9. Skill dependency policy

- `depends_on` chỉ giữa Skill ↔ Skill; dùng SemVer range (`^`, `~`, khoảng tường minh, pin cứng). **Cấm** `*`, `latest`.
- Range mặc định khuyến nghị: `^`.
- Circular dependency: **cấm**.
- Độ sâu dependency khuyến nghị: **≤ 2** (`internal-convention`); vượt → cảnh báo, không chặn.
- Dependency không thỏa → Skill bị loại khỏi assignment, ghi `coverage_gap`; Orchestrator **không tự thay version**.
- Chi tiết: [`skills/README.md`](skills/README.md).

## 10. Orchestration defaults [configurable]

| Key | Default | Ghi chú |
|---|---|---|
| `profile_execution` | `one-profile-per-assignment` | Không configurable — xem ADR-0002 |
| `parallel_execution` | `true` | Với các assignment không phụ thuộc nhau |
| `max_revalidation_rounds_per_conflict` | `1` | internal-convention |
| `unresolved_rating_policy` | `show-both-use-higher-flagged` | internal-convention |
| `max_skill_dependency_depth_warning` | `2` | internal-convention |
| `allow_draft_skills` | `false` | |
| `hitl_required_for_verdict_conflicts` | `true` | Không nên tắt |

## 11. Reproducibility statement (bắt buộc trong mọi report)

> Review run này được ghi nhận đầy đủ trong `run-manifest.yaml` để truy vết và có thể chạy lại với cùng cấu hình đã khai báo. Do tính không tất định của LLM và các yếu tố runtime không thể thu thập (ví dụ system prompt ẩn của nền tảng, cập nhật model phía nhà cung cấp), kết quả chạy lại **có thể khác** kết quả này.

## 12. Out of scope (giai đoạn hiện tại)

DevOps, advanced Security, Legal Compliance và các domain không liên quan. Kiến trúc cho phép mở rộng bằng cách thêm Skill domain / Profile / Capability mới mà không thay đổi Core.
