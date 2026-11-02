# Câu Cá Nâng Cấp

Game câu cá idle viết bằng HTML5 Canvas. Game nằm trong `index.html`, không cần cài thư viện hoặc build.

## Chạy trên máy tính

**Cách nhanh:** mở `index.html` bằng trình duyệt.

**Nếu trình duyệt chặn lưu tiến độ hoặc muốn chạy qua HTTP:** mở Terminal/PowerShell tại thư mục dự án và chạy:

```powershell
python -m http.server 8000
```

Mở <http://localhost:8000>. Giữ cửa sổ terminal mở khi chơi; nhấn `Ctrl+C` để dừng máy chủ.

Nếu lệnh `python` không có trên máy, thử `py -m http.server 8000`.

## Đưa lên GitHub và bật GitHub Pages

1. Tạo repository GitHub (ví dụ `fish`) rồi đẩy nhánh `main` lên repository.
2. Trong repository, vào **Settings → Pages** và đặt **Source** thành **GitHub Actions**.
3. Mỗi lần đẩy commit lên `main`, workflow `.github/workflows/pages.yml` sẽ tự xuất bản game. Có thể chạy thủ công tại **Actions → Deploy game to GitHub Pages → Run workflow**.
4. Mở địa chỉ GitHub Pages được hiển thị trong **Settings → Pages**. Với repository `phucm1417/fish`, địa chỉ thường là <https://phucm1417.github.io/fish/>.

Workflow đưa `index.html` ở thư mục gốc lên Pages; không cần build. `README.md` chỉ là tài liệu, còn game bắt đầu từ `index.html`.

## Cách chơi

- Chạm màn hình để thả câu. Khi có tiếng cắn, chạm lần nữa khi vòng thu nhỏ khớp với vòng chấm (cắn hoàn hảo nhận gấp đôi).
- Thuyền cấp 1 trở lên tự câu; nút thuyền bật/tắt tự động. Thuyền cấp 3 trở lên tự bán cá.
- Thú cưng (9 loài) có chỗ đậu riêng và tự bắt cá theo chu kỳ, kể cả khi bạn vắng.
- Hồ cá (nút góc trên trái): thả cá vào để sinh xu theo thời gian. Có thể đưa cá về túi để thay con khác.
- Triệu hồi trùm từ tab trùm, hoặc chờ trùm xuất hiện sau mỗi 30 lần câu trong khu vực.
- 8 khu vực, mỗi khu có bảng cá riêng, gồm cả sinh vật biển và đồ vật chìm.
- Nâng cấp cần câu, mồi, thuyền, túi, thú cưng, lưỡi câu và dây câu.
- Sự kiện đổi mỗi 5 phút, thời tiết đổi mỗi khoảng một phút.
- Hiệu ứng cản bước: dây câu bị rối (chạm để gỡ) và đàn sứa thu hẹp cửa sổ cắn.
- Tái sinh khi đã mở khu vực cuối: đổi tiến độ lấy hệ số thưởng vĩnh viễn.

## Cấu trúc

```
index.html                  Game HTML/CSS/JavaScript một tệp
.github/workflows/pages.yml Tự động triển khai GitHub Pages
.nojekyll                   Tắt xử lý Jekyll cho xuất bản từ nhánh
docs/                        Quy tắc code và thiết kế asset
skills/                      Hướng dẫn phát triển game
```

Tiến độ chơi được lưu trong `localStorage` của trình duyệt. Mỗi trình duyệt và mỗi địa chỉ web có vùng lưu riêng.
