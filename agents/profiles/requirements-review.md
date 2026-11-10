---
asset_type: specialist-profile
id: requirements-review
version: 0.1.0
status: draft
core_agent: { id: artifact-reviewer, version: "^0.1.0" }
capability: document-quality
applies_to: [srs, use-case, user-story, acceptance-criteria]
skills:
  - { skill_id: re.srs-review, version: null, required: true }
  - { skill_id: re.requirement-quality, version: null, required: true }
  - { skill_id: re.use-case-analysis, version: null, required: false }
  - { skill_id: re.acceptance-criteria, version: null, required: false }
context_fields: [project_overview, business_objectives, functional_scope]
finding_categories: [completeness, clarity, consistency, structure, testability, verifiability]
---

# Requirements Review

## 1. Role
Đánh giá chất lượng tài liệu yêu cầu (SRS, Use Case, User Story, Acceptance Criteria).

## 2. Scope
- In scope: chất lượng nội tại của từng tài liệu yêu cầu.
- Out of scope: truy vết sang design/test (→ `traceability`); tính khả thi của yêu cầu (→ `feasibility-risk`).

## 3. Ghi chú thực thi
- SRS lớn có thể chia Assignment theo chương.
- Không phụ thuộc Assignment khác.
