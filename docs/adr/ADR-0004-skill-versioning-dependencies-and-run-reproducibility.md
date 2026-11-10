# ADR-0004: Skill Versioning, Dependencies và Review Run Reproducibility

- Status: Accepted
- Date: 2026-11-10

## Context
Kết quả review phải truy vết được về đúng phiên bản tri thức và cấu hình đã dùng. Skill có thể phụ thuộc Skill khác. LLM không tất định.

## Decision
1. **SemVer** cho mọi asset. Skill có metadata: `version`, `status`, `sources`, `last_verified_at`, `verified_by`, `needs_reverification`, `depends_on`.
2. **Skill lifecycle:** `planned → draft → under-review → validated → deprecated → retired`. Áp dụng theo **effective status** (thấp nhất trong chuỗi dependency).
3. **Dependency rules:**
   - SemVer range (`^`, `~`, khoảng, pin); cấm `*`/`latest`.
   - Kiểm tra V1–V6 (tồn tại, version thỏa, không retired/planned, không vòng, độ sâu ≤ 2 cảnh báo, criterion ref tồn tại).
   - Không thỏa → loại Skill, ghi `coverage_gap`, HITL nếu Skill bắt buộc; không tự thay version.
   - Không nâng `validated` khi dependency chưa `validated`.
   - Dependency đổi MAJOR → dependent phải review lại; MINOR có thể bật `needs_reverification`.
4. **Run manifest** ghi version/hash của mọi asset, input, config, model, tools, retrieval/KB. Trường không thu thập được dùng `CapturedValue` (`captured | unavailable | not-applicable` + reason).
5. **Không cam kết output giống hệt** khi chạy lại; chỉ cam kết truy vết và re-execution với cùng cấu hình.

## Consequences
- (+) Truy vết đầy đủ; thay đổi Skill không làm mất khả năng giải thích run cũ.
- (−) Chi phí bảo trì metadata; cần validator đơn giản trong tương lai.
