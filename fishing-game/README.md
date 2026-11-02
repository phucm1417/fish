# Câu Cá Nâng Cấp

Game câu cá idle viết bằng HTML5 Canvas. Toàn bộ game nằm trong một file `index.html`, không cần build hay thư viện ngoài.

## Chạy game

Mở `index.html` trong trình duyệt, hoặc phục vụ thư mục bằng web server tĩnh:

```bash
python3 -m http.server 8000
# rồi mở http://localhost:8000
```

Giao diện thiết kế cho điện thoại màn hình dọc, vẫn chạy trên máy tính. Tiến độ được lưu trong `localStorage`.

## Cách chơi

- Chạm màn hình để thả câu. Khi có tiếng cắn, chạm lần nữa khi vòng thu nhỏ khớp với vòng chấm (cắn hoàn hảo nhận gấp đôi).
- Thuyền cấp 1 trở lên tự câu, nút thuyền bật/tắt tự động. Thuyền cấp 3 trở lên tự bán cá.
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
index.html      Toàn bộ game (HTML, CSS, JS)
docs/           Quy tắc viết code và quy tắc thiết kế asset
skills/         Bộ skill cho dự án game (core loop, rendering, economy, ...)
```

## Ghi chú kỹ thuật

- Cá, thú cưng, trùm, thuyền, người câu và đồ vật đều được vẽ bằng code (Canvas path), không dùng file ảnh.
- Nền tĩnh được cache theo khu vực. Các lớp nền và hiệu ứng vẽ ở độ phân giải theo màn hình (DPR).
- Cá bơi bằng bộ điều khiển hướng mượt, cùng cách với cá trong hồ phóng to.
- Dữ liệu lưu từ các phiên bản cũ (v3 đến v6) được đọc lại và chuyển sang định dạng mới.

## Trạng thái

Bản đang phát triển. Chưa có kiểm thử tự động. Cần chơi thử trên trình duyệt và điện thoại để kiểm tra hiệu năng, bố cục và cân bằng.

Phần nhiều người chơi chưa được làm: chế độ nhiều người chơi trực tuyến, nhiệm vụ, thành tựu.
