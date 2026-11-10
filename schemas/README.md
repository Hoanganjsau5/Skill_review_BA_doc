# Schemas (Data Contracts)

Dialect: **JSON Schema 2020-12**. `$id` dùng base `https://schemas.agentic-review-system.example/` (chỉ là định danh). `$ref` giữa các file dùng đường dẫn tương đối. Version mỗi schema ở `x-version` (SemVer).

## 1. Tổ chức

| Nhóm | Mục đích | Files |
|---|---|---|
| `common/` | Kiểu dùng chung | `common-defs.schema.json` (SemVer, VersionRef, AssetItemRef, Evidence, ExternalEvidence, Assumption, CapturedValue, ProducerRef, Severity, Confidence, Scope…) |
| `definitions/` | Metadata của asset tái sử dụng | `skill-manifest`, `criterion`, `analysis-rule`, `specialist-profile`, `capability`, `source-entry` |
| `runtime/` | Dữ liệu trao đổi khi review | `project-context`, `task`, `agent-assignment`, `review-result`, `finding`, `risk`, `feasibility-assessment`, `delivery-readiness`, `critic-validation`, `conflict-record`, `final-report`, `review-run-manifest` |

## 2. Producer / Consumer

| Contract | Producer | Consumer |
|---|---|---|
| task | Orchestrator | Orchestrator |
| agent-assignment | Orchestrator | Core Agent |
| review-result | Core Agent (trừ synthesizer) | Orchestrator |
| finding | artifact-reviewer, cross-artifact-analyzer | solution-assessor, critic, synthesizer |
| risk, feasibility-assessment | solution-assessor (`feasibility-risk`) | critic, solution-assessor (`delivery-readiness`), synthesizer |
| delivery-readiness | solution-assessor (`delivery-readiness`) | critic, synthesizer |
| critic-validation | critic | Orchestrator |
| conflict-record | Orchestrator | synthesizer, manifest |
| final-report | report-synthesizer | User |
| review-run-manifest | Orchestrator | User, audit |

## 3. Quy tắc chính được mã hóa trong schema
- `agent-assignment.profile` là trường đơn (Profile Execution Isolation).
- `finding.basis`: `oneOf` criterion / analysis-rule / comparison-rule / expert-judgment; `expert-judgment` không được `confirmed-issue` và `requires_critic: true`; `comparison-rule` cần ≥ 2 evidence.
- `risk`: likelihood/impact = `not-assessed` hoặc có `method_ref`.
- `feasibility-assessment`: `conditionally-feasible` cần `conditions`; `insufficient-evidence` cần `unresolved_questions`.
- `delivery-readiness`: `dor_ref: null` ⇒ `insufficient-evidence`.
- `CapturedValue`: `unavailable`/`not-applicable` bắt buộc `reason`.
- `SemVerRange` cấm `*`, `latest`.

## 4. Quy tắc không biểu diễn được bằng JSON Schema (kiểm tra bởi validator/Critic)
- Evidence của `comparison-rule` đến từ ≥ 2 artifact **khác nhau**.
- `criterion_ref`/`rule_ref` tồn tại ở version tham chiếu.
- Skill dependency: V1–V6 (`skills/README.md`).
- Tính duy nhất của ID trong một run.

## 5. Versioning
MAJOR: phá vỡ tương thích · MINOR: thêm trường tùy chọn · PATCH: sửa mô tả. Run manifest ghi version schema đã dùng.
