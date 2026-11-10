# Review Runs

Mỗi lần review tạo một thư mục `RUN-YYYYMMDD-HHMM-<slug>/`:

```text
RUN-YYYYMMDD-HHMM-<slug>/
├── run-manifest.yaml       # schemas/runtime/review-run-manifest.schema.json
├── task.json               # schemas/runtime/task.schema.json
├── execution-plan.json     # agent-assignment[] + dependencies
├── agent-outputs/          # mỗi assignment một review-result (<assignment_id>.json)
├── validation/             # critic-validation
├── conflicts/              # conflict-record (<conflict_id>.json)
├── decisions-log.md        # bản cho người đọc: HITL Q&A, assumptions, quyết định conflict
├── final-report.json       # schemas/runtime/final-report.schema.json
└── final-report.md
```

Quy tắc:
- Output của Agent là **bất biến**; mọi quyết định sau đó là bản ghi mới.
- Không xóa run cũ; run mới tham chiếu run trước (nếu incremental) qua manifest.
- Kết quả chạy lại có thể khác (xem reproducibility statement trong `SYSTEM_CONFIG.md`).
