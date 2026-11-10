---
asset_type: skill
skill_id: <xx.skill-name>
name: <Skill Name>
domain: <domain-folder>
version: 0.1.0
status: draft                  # planned | draft | under-review | validated | deprecated | retired
applies_to: []                 # artifact types
depends_on: []                 # - { skill_id: <id>, version: "^x.y.z" }   (cấm "*" / "latest")
sources: []                    # - { source_id: SRC-XXXX, version: "<edition>", sections: ["<locator>"] }
last_verified_at: null         # YYYY-MM-DD
verified_by: null
needs_reverification: false
supersedes: null
---

# <Skill Name>

## 1. Purpose
<Skill giúp đánh giá điều gì.>

## 2. Scope
- In scope: …
- Out of scope: …

## 3. Prerequisites
- Input cần có: …
- Skill phụ thuộc (nếu có): …

## 4. Knowledge & Principles
<Tổng hợp nguyên tắc. Mỗi nguyên tắc dẫn nguồn qua source_id + locator. Không sao chép nguyên văn dài.>

## 5. Authoritative References
| source_id | Title | Version/Edition | authority_level |
|---|---|---|---|

## 6. Review Procedure
1. …

## 7. Evaluation Criteria
Xem [`criteria.yaml`](criteria.yaml). Rules cho phân tích liên tài liệu: [`rules.yaml`](rules.yaml).

## 8. Checklist
Xem [`checklist.md`](checklist.md).

## 9. Examples
Xem [`examples/`](examples/).

## 10. Expected Output
- Finding với `basis.type: criterion` (hoặc `analysis-rule`/`comparison-rule`), category thuộc: …

## 11. Limitations
- …
