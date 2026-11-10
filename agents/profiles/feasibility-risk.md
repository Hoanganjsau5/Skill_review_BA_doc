---
asset_type: specialist-profile
id: feasibility-risk
version: 0.1.0
status: draft
core_agent: { id: solution-assessor, version: "^0.1.0" }
capability: feasibility-risk
applies_to: [srs, basic-design, detailed-design, api-spec, architecture-document, database-design]
skills:
  - { skill_id: fr.technical-feasibility, version: null, required: true }
  - { skill_id: fr.requirement-conflict-analysis, version: null, required: true }
  - { skill_id: fr.risk-assessment, version: null, required: true }
  - { skill_id: fr.technology-fit, version: null, required: false }
  - { skill_id: fr.dependency-analysis, version: null, required: false }
  - { skill_id: fr.estimation-sanity-check, version: null, required: false }
  - { skill_id: fr.resource-infrastructure-constraints, version: null, required: false }
context_fields: [project_overview, business_objectives, functional_scope, technical_constraints, business_constraints, budget, timeline, team_capabilities, infrastructure, mandatory_technologies, external_dependencies, architecture_decisions, assumptions, known_limitations]
finding_categories: []   # Profile này không tạo Finding
---

# Feasibility & Risk

## 1. Role
Đánh giá tính khả thi của giải pháp và rủi ro dự án dưới ràng buộc thực tế.

## 2. Scope
Dimensions: Requirement Feasibility · Technical Feasibility · Implementation Readiness · External Dependencies · Project Constraints.

## 3. Ghi chú thực thi
- Phụ thuộc: Findings/early signals từ `document-quality` (có thể khởi động sớm cho phần scope đã đủ input — Phase 5).
- Có thể dùng thêm Skill của domain khác (ví dụ `sa.distributed-systems`) khi Orchestrator xác định cần; ghi rõ trong Assignment.
