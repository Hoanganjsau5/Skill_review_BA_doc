---
asset_type: specialist-profile
id: design-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [basic-design, detailed-design, api-spec]
skills:
  - { skill_id: sd.basic-design-review, version: null, required: true }
  - { skill_id: sd.api-design, version: null, required: false }
  - { skill_id: sd.error-handling-design, version: null, required: false }
context_fields: [project_overview, functional_scope, technical_constraints, mandatory_technologies, architecture_decisions]
finding_categories: [completeness, clarity, consistency, structure, implementability, contract-definition, error-handling]
---

# Design Review

## 1. Role
Đánh giá chất lượng tài liệu thiết kế (Basic/Detailed Design, API Specification, Error Handling Design).

## 2. Scope
- In scope: chất lượng nội tại của tài liệu thiết kế và đặc tả API.
- Out of scope: database design (→ `database-review`); nhất quán giữa services (→ `integration-review`); khả thi (→ `feasibility-risk`).

## 3. Ghi chú thực thi
- `sd.api-design` chỉ cần khi scope có `api-spec`.
- Không phụ thuộc Assignment khác.
