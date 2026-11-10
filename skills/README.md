# Skill Library

Skill = tri thức chuyên môn **đã nghiên cứu, tổng hợp, chuẩn hóa** thành procedure, evaluation criteria, analysis/comparison rules và checklist. Skill độc lập dự án, không có state, có version.

Quyết định: [ADR-0004](../docs/adr/ADR-0004-skill-versioning-dependencies-and-run-reproducibility.md), [ADR-0005](../docs/adr/ADR-0005-knowledge-base-vs-skill-library.md)

> **Trạng thái hiện tại:** chưa có Skill nào. `SKILL_REGISTRY.yaml` chỉ chứa các entry `planned`. Không tạo nội dung Skill khi chưa thực hiện pipeline nghiên cứu.

## 1. Cấu trúc

```text
skills/<domain>/<skill-id-suffix>/
├── SKILL.md        # frontmatter metadata + nội dung phương pháp
├── criteria.yaml   # evaluation criteria (artifact-reviewer)
├── rules.yaml      # analysis/comparison rules (cross-artifact-analyzer) — tùy chọn
├── checklist.md    # dẫn xuất từ criteria/rules, chỉ tham chiếu ID
├── examples/       # ví dụ đạt/không đạt để validate criteria/rules
└── CHANGELOG.md
```

Template: [`_template/`](_template/). Skill ID: `<domain-prefix>.<name>` (ví dụ `re.requirement-quality`).

| Domain | Prefix | Thư mục |
|---|---|---|
| Requirement Engineering | `re` | `requirement-engineering/` |
| Software Design | `sd` | `software-design/` |
| Software Architecture | `sa` | `software-architecture/` |
| Modeling & Diagrams | `md` | `modeling-diagrams/` |
| Software Quality Assurance | `qa` | `software-quality-assurance/` |
| Feasibility & Risk Assessment | `fr` | `feasibility-risk-assessment/` |

## 2. Pipeline xây dựng Skill (bắt buộc)

1. Đăng ký nguồn trong `knowledge/source-registry.yaml`.
2. Viết research note (`knowledge/research-notes/`) — trích xuất có locator.
3. Tổng hợp, chuẩn hóa.
4. Viết procedure (`SKILL.md`).
5. Viết criteria/rules có `source_refs` và `authority_level`.
6. Validate bằng examples (đạt/không đạt).
7. Ghi version, `last_verified_at`, `verified_by`; chuyển status.

Không sao chép nguyên văn dài từ nguồn; dùng `synthesis_note` + `source_refs`. Không đưa `project-decision` vào Skill. Không lặp tri thức đã có ở Skill khác — dùng `depends_on`.

## 3. Lifecycle

`planned → draft → under-review → validated → deprecated → retired`

| Status | Dùng trong review |
|---|---|
| `planned` | Không |
| `draft`, `under-review` | Chỉ khi `allow_draft_skills: true`; report gắn cờ |
| `validated` | Có |
| `deprecated` | Có, cảnh báo |
| `retired` | Không |

**Điều kiện `validated`:** mọi criterion/rule có source_refs (hoặc origin_note với internal-convention), đã validate bằng examples, `last_verified_at` được ghi, mọi dependency đều `validated`.

## 4. Versioning

| Thay đổi | Bump |
|---|---|
| Đổi ngữ nghĩa hoặc bỏ criterion/rule | MAJOR |
| Thêm criterion/rule | MINOR |
| Sửa lời văn, không đổi ngữ nghĩa | PATCH |

`criterion_id`/`rule_id` vĩnh viễn, không tái sử dụng.

## 5. Dependency management

### 5.1 Khai báo
```yaml
depends_on:
  - { skill_id: re.requirement-quality, version: "^1.0.0" }
```
- Chỉ Skill → Skill.
- Range: `^x.y.z` (khuyến nghị), `~x.y.z`, `>=a.b.c <d.e.f`, pin `x.y.z`. **Cấm** `*`, `latest`.
- Tham chiếu chéo criterion/rule: `skill_id@range#criterion_id`; Skill đó phải có trong `depends_on`.

### 5.2 Validation (thủ công hoặc validator đơn giản)
Thời điểm: (A) khi thay đổi registry/Skill; (B) khi Orchestrator lập plan.

| # | Kiểm tra | Vi phạm |
|---|---|---|
| V1 | Dependency tồn tại trong registry | Lỗi |
| V2 | Có version thỏa range | Lỗi |
| V3 | Dependency không `retired`/`planned` | Lỗi |
| V4 | Không có circular dependency | Lỗi cho mọi Skill trong vòng |
| V5 | Độ sâu ≤ 2 (internal-convention) | Cảnh báo |
| V6 | `#criterion_id`/`#rule_id` tồn tại ở version đã resolve | Lỗi |

### 5.3 Effective status
Effective status = status thấp nhất của Skill và mọi dependency (bắc cầu), thứ tự `draft` < `under-review` < `validated`; `deprecated` = cảnh báo.

### 5.4 Khi dependency không thỏa
Orchestrator **không tự thay version**: loại Skill khỏi Assignment → ghi `coverage_gap` → nếu Skill `required` trong Profile → HITL (tiếp tục/dừng).

### 5.5 Circular dependency
Cấm. Phát hiện bằng duyệt đồ thị `depends_on` (DFS). Sửa bằng cách tách tri thức chung ra Skill thứ ba.

### 5.6 Ảnh hưởng khi dependency đổi version
| Thay đổi | Ảnh hưởng tới dependent |
|---|---|
| PATCH | Không bắt buộc hành động |
| MINOR | Trong range `^`; bật `needs_reverification` nếu dependent tham chiếu khu vực thay đổi |
| MAJOR | Range `^` không thỏa (V2) → review, cập nhật range, bump version dependent, cập nhật `last_verified_at` |
| → `deprecated` | Cảnh báo, lên kế hoạch chuyển đổi |
| → `retired` | V3 lỗi; dependent không dùng được tới khi cập nhật |

Run manifest ghi version đã resolve → run cũ vẫn truy vết được.
