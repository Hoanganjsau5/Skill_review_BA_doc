---
asset_type: specialist-profile
id: database-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [database-design, data-model]
skills:
  - { skill_id: sd.database-design, version: null, required: true }
  - { skill_id: sd.data-modeling, version: null, required: false }
  - { skill_id: md.erd, version: null, required: false }
context_fields: [project_overview, functional_scope, technical_constraints, mandatory_technologies]
finding_categories: [completeness, clarity, consistency, structure, data-integrity, naming]
---

# Database Review

## 1. Role
Đánh giá chất lượng tài liệu thiết kế cơ sở dữ liệu và data model.

## 2. Scope
- In scope: schema, entity, quan hệ, ràng buộc, quy ước đặt tên được mô tả trong tài liệu.
- Out of scope: nhất quán với API Spec (→ `traceability`/`integration-review`); hiệu năng thực tế (→ `feasibility-risk`, cần evidence).

## 3. Ghi chú thực thi
- ERD nằm trong Database Design có thể đồng thời được `diagram-review` đánh giá ở Assignment riêng.
