# OLM Panel — Remote Config (data only)

Repo dữ liệu cho **Remote Config engine** của
[OLM Panel by NTH](https://github.com/qnthanh210/Extension_OLM) (Chrome MV3).

> **Repo này CỐ Ý công khai** vì extension phải đọc config mà **không mang theo token**.
> Source của extension nằm ở repo private.

---

## Repo này chứa gì

| File | Ý nghĩa | Extension đọc? |
|---|---|---|
| `bundle.json` | config đã đóng gói + integrity (`configBytes`, `configSha256`) | ✅ **file duy nhất** |
| `config.json` | nguồn sự thật, người vận hành sửa | ❌ (để đọc/tham khảo) |
| `versions/*.json` | lịch sử các bản đã phát hành | ❌ (tham khảo) |
| `CHANGELOG.md` | lịch sử phiên bản config | ❌ |

## Repo này KHÔNG chứa gì

License key · device id · thông tin người dùng · Supabase secret · token ·
private key · **JavaScript** · HTML · CSS · URL tùy ý.

Config chỉ là **dữ liệu**: CSS selector, số nguyên có giới hạn, nhãn UI, feature flag.
Extension **không bao giờ** `eval` hay thực thi code từ repo này.

## Extension đọc bằng cách nào

```
https://raw.githubusercontent.com/qnthanh210/olm-ext-remote-config/main/bundle.json
```

* Kiểm tra mỗi **6 giờ** (nền), hoặc thủ công bằng `olm update`.
* Dùng `ETag`/`If-None-Match`; `304` → không tải lại.
* Kiểm tra `configBytes` + `configSha256` của canonical JSON trước khi đọc.
* Schema sai / version cũ hơn / config hỏng → **giữ config cũ**, không ghi đè.
* GitHub không truy cập được → dùng config đã cache, hoặc built-in default trong gói extension.

## Bản hiện tại

| | |
|---|---|
| `configVersion` | **1.0.0** |
| `schemaVersion` | 1 |
| `minimumExtensionVersion` | 1.4.0 |
| `configSha256` | `f195de471462d2a8fcf419d360c7ee47150e24205043e18cf8b71ca4acca2b8e` |

## Phát hành phiên bản mới

Không sửa tay `bundle.json`. Xem
[`docs/REMOTE-CONFIG.md`](https://github.com/qnthanh210/Extension_OLM/blob/main/docs/REMOTE-CONFIG.md)
trong repo private (quy trình đầy đủ).

Tóm tắt:

1. Sửa `config.json` ở repo private.
2. **Bắt buộc** tăng `configVersion`.
3. `npm run verify` (test + static-check + validate + build).
4. `node scripts/publish-config.mjs`.
5. Xác nhận: `olm update` → `olm status`.

## Kiểm tra nhanh từ xa

```bash
curl -s https://raw.githubusercontent.com/qnthanh210/olm-ext-remote-config/main/bundle.json \
  | head -8
```

## Chính sách bảo mật

Nếu phát hiện nội dung sai hoặc độc hại trong `bundle.json`:
báo qua issue ở repo private
[`Extension_OLM`](https://github.com/qnthanh210/Extension_OLM/issues).
Revert commit trên `main` sẽ được extension tự nhận trong ≤ 6 giờ;
người dùng cần dùng ngay có thể `olm rollback`.
