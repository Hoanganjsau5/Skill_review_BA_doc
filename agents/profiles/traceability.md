---
asset_type: specialist-profile
id: traceability
version: 0.1.0
status: draft
core_agent: { id: cross-artifact-analyzer, version: "^0.1.0" }
capability: document-quality
applies_to: [srs, use-case, user-story, acceptance-criteria, basic-design, detailed-design, api-spec, database-design, data-model, test-plan, test-design, test-cases]
skills:
  - { skill_id: re.requirement-traceability, version: null, required: true }
  - { skill_id: qa.test-coverage, version: null, required: false }
context_fields: [functional_scope]
finding_categories: [traceability-gap, orphan-element, inconsistency, coverage-gap]
---

# Traceability

## 1. Role
Kiểm tra truy vết và nhất quán dọc chuỗi Requirement → Design → API/Data → Test.

## 2. Scope
- In scope: liên kết và nhất quán giữa ≥ 2 artifact thuộc các tầng khác nhau.
- Out of scope: chất lượng nội tại từng tài liệu.

## 3. Ghi chú thực thi
- Chỉ tạo khi scope có ≥ 2 loại artifact liên quan.
- Phụ thuộc: các Assignment `*-review` của artifacts liên quan (dùng Findings làm tham chiếu, tránh trùng lặp).
- Dùng thêm domain-agnostic rules trong `capabilities/document-quality/consistency-rules.yaml`.
