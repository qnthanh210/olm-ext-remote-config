# Changelog — Remote Config

Versioning độc lập với extension. Chỉ đổi dữ liệu thì chỉ bump `configVersion` ở đây.

Xem quy tắc chi tiết:
[`docs/REMOTE-CONFIG.md`](https://github.com/qnthanh210/Extension_OLM/blob/main/docs/REMOTE-CONFIG.md)

---

## 1.0.0 — 2026-10-06

Bản baseline đầu tiên, khớp với extension **1.4.0**.

### Added

* Nhóm `selectors`: `quizHost`, `quizHostFallbackPattern`, `mcOption`, `tfRow`,
  `mcBlock`, `tfBlock`, `legacyBlock`, `legacyRoot`, `legacyOption`, `answerDom`,
  `stripDisplay` — theo UI olm.vn đã kiểm chứng (lit `default-root` và legacy `data-id`).
* Nhóm `matching`: `chipMaxText`, `rearmCyclesMax`, `tfListNamePattern`.
* Nhóm `ui.qtypeLabels`: nhãn + class CSS cho 7 loại câu hỏi.
* Nhóm `compatibility`: `olmDomains`, `knownUiVariants`.
* Nhóm `features`: 4 feature flag.

### Integrity

* `configBytes` = 3236
* `configSha256` = `f195de471462d2a8fcf419d360c7ee47150e24205043e18cf8b71ca4acca2b8e`

### Notes

* `chipMaxText`, `rearmCyclesMax` và toàn bộ selector **giữ nguyên giá trị hardcode**
  của v1.3.12 → áp dụng config này **không làm thay đổi hành vi** cho tới khi có bản
  config sau thực sự khác.
