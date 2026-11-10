# Agents

Quyết định: [ADR-0002](../docs/adr/ADR-0002-core-agents-and-specialist-profiles.md)

## Hai loại định nghĩa

| | Core Agent (`core/`) | Specialist Profile (`profiles/`) |
|---|---|---|
| Là gì | Instruction template theo **kiểu suy luận** | **Cấu hình vai trò** |
| Chứa | Trách nhiệm, input/output contract, quy trình suy luận chung, ranh giới | Phạm vi, artifact áp dụng, Core Agent, Skills, finding categories |
| Không chứa | Tri thức chuyên môn | Tri thức chuyên môn, quy trình suy luận |
| Số lượng | 5 (tăng chỉ khi có ADR) | Mở rộng tự do |

Tri thức chuyên môn **chỉ** nằm trong `skills/`.

## Lắp ráp một Assignment

```text
Assignment = Core Agent instruction
           + Profile (role, scope)
           + Skills đã resolve (procedure, criteria/rules, checklist)
           + Context slice + Artifacts trong scope
           + Output contract (schema)
```

- **1 Assignment = 1 Profile.** Có thể chia 1 Profile thành nhiều Assignment; không gộp Profile.
- Critic luôn ở Assignment riêng.

## Điều kiện tạo Core Agent mới
Ít nhất một: (a) kiểu suy luận khác, (b) contract khác, (c) cần độc lập trách nhiệm. Phải có ADR.

## Core Agents

| Agent | Profiles sử dụng |
|---|---|
| [artifact-reviewer](core/artifact-reviewer.md) | requirements-review, design-review, architecture-review, database-review, diagram-review, qa-review |
| [cross-artifact-analyzer](core/cross-artifact-analyzer.md) | traceability, integration-review |
| [solution-assessor](core/solution-assessor.md) | feasibility-risk, delivery-readiness |
| [critic](core/critic.md) | — (không cần Profile) |
| [report-synthesizer](core/report-synthesizer.md) | — (không cần Profile) |
