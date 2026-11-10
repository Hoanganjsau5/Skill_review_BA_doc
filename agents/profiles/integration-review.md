---
asset_type: specialist-profile
id: integration-review
version: 0.1.0
status: draft
core_agent: { id: cross-artifact-analyzer, version: "^0.1.0" }
capability: document-quality
applies_to: [api-spec, architecture-document, detailed-design]
skills:
  - { skill_id: sd.api-design, version: null, required: true }
  - { skill_id: sa.microservices, version: null, required: false }
  - { skill_id: sa.bff, version: null, required: false }
  - { skill_id: sa.api-gateway, version: null, required: false }
  - { skill_id: sa.distributed-systems, version: null, required: false }
context_fields: [technical_constraints, external_dependencies, architecture_decisions]
finding_categories: [contract-mismatch, inconsistency, missing-integration-spec, responsibility-overlap]
---

# Integration Review

## 1. Role
Kiểm tra nhất quán giao tiếp và hợp đồng giữa các service/thành phần (Cross-Service Integration).

## 2. Scope
- In scope: contract giữa producer/consumer, BFF ↔ backend, Gateway routing, trách nhiệm chồng lấn.
- Out of scope: chất lượng nội tại của từng API Spec (→ `design-review`).

## 3. Ghi chú thực thi
- Chỉ tạo khi scope có tài liệu của ≥ 2 service/thành phần giao tiếp nhau.
- Phụ thuộc: Assignments `design-review`/`architecture-review` liên quan.
