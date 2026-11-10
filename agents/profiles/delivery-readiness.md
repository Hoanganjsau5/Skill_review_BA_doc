---
asset_type: specialist-profile
id: delivery-readiness
version: 0.1.0
status: draft
core_agent: { id: solution-assessor, version: "^0.1.0" }
capability: delivery-readiness
applies_to: [srs, use-case, user-story, acceptance-criteria, basic-design, detailed-design, api-spec, database-design, architecture-document, test-plan, test-design, test-cases]
skills:
  # Không có domain riêng. Tái sử dụng Skill của các domain liên quan, chọn theo DoR và target stage.
  - { skill_id: re.acceptance-criteria, version: null, required: false }
  - { skill_id: sd.basic-design-review, version: null, required: false }
  - { skill_id: sd.api-design, version: null, required: false }
  - { skill_id: qa.test-design, version: null, required: false }
  - { skill_id: fr.dependency-analysis, version: null, required: false }
context_fields: [functional_scope, timeline, team_capabilities, external_dependencies, assumptions, known_limitations]
finding_categories: []   # Profile này không tạo Finding
---

# Delivery Readiness

## 1. Role
Đánh giá scope được chọn đã sẵn sàng cho stage tiếp theo (Development, Testing, …) theo DoR do dự án định nghĩa.

## 2. Scope
- Đầu vào chính: Findings, Risks, Feasibility assessment, `config/definition-of-ready.yaml`.
- Không có DoR → `insufficient-evidence`.

## 3. Ghi chú thực thi
- Phụ thuộc: Assignments `document-quality` và `feasibility-risk` của cùng scope.
- Quyết định: [ADR-0003](../../docs/adr/ADR-0003-delivery-readiness-as-capability.md).
