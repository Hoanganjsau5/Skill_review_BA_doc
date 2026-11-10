---
asset_type: specialist-profile
id: <profile-id>
version: 0.1.0
status: draft                    # draft | active | deprecated
core_agent: { id: <core-agent-id>, version: "^0.1.0" }
capability: <capability-id>
applies_to: []                   # artifact types (xem orchestrator/routing-rules.md)
skills:                          # chỉ tham chiếu, không chứa tri thức
  - skill_id: <xx.skill-name>
    version: null                # SemVer range khi Skill có version; null khi Skill đang `planned`
    required: true               # true: thiếu Skill → coverage gap nghiêm trọng → HITL
context_fields: []               # các trường project-context cần cấp cho Assignment
finding_categories: []           # category hợp lệ cho Finding của Profile này
---

# <Profile Name>

## 1. Role
<Vai trò chuyên môn trong một câu.>

## 2. Scope
- In scope: …
- Out of scope: …

## 3. Ghi chú thực thi
- 1 Assignment = 1 Profile. Có thể chia theo artifact/section khi artifact lớn.
- Phụ thuộc Assignment khác (nếu có): …

> Profile **không** chứa criteria, checklist hay tri thức chuyên môn — những thứ đó nằm trong Skill.
