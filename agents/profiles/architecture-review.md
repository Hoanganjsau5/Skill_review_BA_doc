---
asset_type: specialist-profile
id: architecture-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [architecture-document]
skills:
  - { skill_id: sa.microservices, version: null, required: false }
  - { skill_id: sa.ddd, version: null, required: false }
  - { skill_id: sa.bff, version: null, required: false }
  - { skill_id: sa.api-gateway, version: null, required: false }
  - { skill_id: sa.distributed-systems, version: null, required: false }
  - { skill_id: md.c4-model, version: null, required: false }
context_fields: [project_overview, technical_constraints, mandatory_technologies, infrastructure, architecture_decisions]
finding_categories: [completeness, clarity, consistency, structure, decision-rationale, quality-attribute-coverage]
---

# Architecture Review

## 1. Role
Đánh giá chất lượng tài liệu kiến trúc phần mềm.

## 2. Scope
- In scope: tài liệu kiến trúc có đủ, rõ, nhất quán, có rationale cho quyết định, có mô tả các view cần thiết.
- Out of scope: kiến trúc có **phù hợp/khả thi** với constraints hay không (→ `feasibility-risk`).

## 3. Ghi chú thực thi
- Orchestrator chọn tập con Skill theo phong cách kiến trúc mà tài liệu mô tả (ví dụ chỉ nạp `sa.bff` khi có BFF). Vì vậy không Skill nào `required: true`; nếu không Skill nào áp dụng được → coverage gap.
