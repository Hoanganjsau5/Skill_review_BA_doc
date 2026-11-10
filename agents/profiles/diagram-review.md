---
asset_type: specialist-profile
id: diagram-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [uml, c4-diagram, erd, bpmn, sequence-diagram, dfd]
skills:
  - { skill_id: md.uml, version: null, required: false }
  - { skill_id: md.c4-model, version: null, required: false }
  - { skill_id: md.erd, version: null, required: false }
  - { skill_id: md.bpmn, version: null, required: false }
  - { skill_id: md.sequence-diagram, version: null, required: false }
  - { skill_id: md.data-flow-diagram, version: null, required: false }
context_fields: [project_overview]
finding_categories: [notation-correctness, completeness, clarity, consistency, level-of-abstraction]
---

# Diagram Review

## 1. Role
Đánh giá tính đúng ký pháp, đầy đủ và rõ ràng của các mô hình và sơ đồ kỹ thuật.

## 2. Scope
- In scope: từng diagram theo ký pháp tương ứng.
- Out of scope: nhất quán giữa diagram và tài liệu văn bản (→ `traceability`).

## 3. Ghi chú thực thi
- Orchestrator chỉ nạp Skill tương ứng loại diagram trong scope.
- Diagram dạng ảnh cần Tool trích xuất; nếu không trích xuất được → `limitations` và `needs-clarification`.
