
# Zalo Redirect (GitHub Pages Template)

Trang đích (`redirect_uri`) để nhận `authorization_code` từ Zalo OA OAuth.

## Cấu trúc
- `index.html`: Hiển thị `code` (nếu có), tự copy vào clipboard, có nút sao chép.
- `.nojekyll`: Đảm bảo GitHub Pages phục vụ đúng các file tĩnh.
- `verify/README.txt`: Gợi ý đặt **file xác minh domain** của Zalo ở **thư mục gốc** repository.

## Hướng dẫn triển khai (tóm tắt)
1. **Fork** repo này (hoặc tải ZIP và tạo repo mới).  
2. Bật **Settings → Pages → Build and deployment → Deploy from a branch** → chọn `main` và `/ (root)`.
3. Sau khi Pages hoạt động, URL của bạn sẽ là:  
   `https://<tai-khoan>.github.io/<ten-repo>/`
4. Trên Zalo Developer:
   - Vào ứng dụng → **Miền ứng dụng** → **Thêm miền** `github.io`.
   - Tải **file xác minh** (.txt) từ Zalo → đặt **ở thư mục gốc** của repo (ví dụ `zalo-verify-xxxx.txt`).
   - Nhấn **Xác minh** → khi thành công mới có thể nhận `code`.
5. Lấy `authorization_code`:
   - Dùng link:

```
https://oauth.zaloapp.com/v4/oa/permission?app_id=APP_ID_CUA_BAN&redirect_uri=ENCODED_REDIRECT&state=abc123
```

   - Thay `APP_ID_CUA_BAN` bằng App ID.
   - Thay `ENCODED_REDIRECT` bằng URL-encode của `https://<tai-khoan>.github.io/<ten-repo>/`.
   - Sau khi **Cấp quyền**, Zalo sẽ chuyển về trang `index.html` và hiển thị `code`.

6. Dán `code` vào menu **Zalo OAuth → Nhập authorization code…** trong Google Sheets (tool Apps Script bạn đã cài) để đổi sang `refresh_token` và lưu Script Properties.

> Ghi chú: **File xác minh domain của Zalo phải đặt ở thư mục gốc** (cùng cấp với `index.html`). Không đặt trong thư mục `verify/`.

## Bảo mật
- Repo này chỉ hiển thị `code` tạm thời (hết hạn nhanh). Đừng commit bất kỳ token bí mật nào.
