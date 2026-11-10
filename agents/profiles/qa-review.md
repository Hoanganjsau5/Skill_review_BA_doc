---
asset_type: specialist-profile
id: qa-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [test-plan, test-design, test-cases]
skills:
  - { skill_id: qa.test-design, version: null, required: true }
  - { skill_id: qa.istqb-principles, version: null, required: false }
  - { skill_id: qa.non-functional-testing, version: null, required: false }
  - { skill_id: qa.defect-management, version: null, required: false }
context_fields: [project_overview, functional_scope, timeline, team_capabilities]
finding_categories: [completeness, clarity, consistency, structure, test-design-quality]
---

# QA Review

## 1. Role
Đánh giá chất lượng tài liệu QA và kiểm thử.

## 2. Scope
- In scope: chất lượng nội tại của test plan, test design, test cases.
- Out of scope: coverage so với requirements (→ `traceability` với `qa.test-coverage`).
