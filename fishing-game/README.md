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
- Bảng dưới màn hình có 7 tab: **Nâng cấp**, **Thuyền**, **Khu vực**, **Skin**, **Thú cưng**, **Trùm**, **Bộ sưu tập**.
- Mỗi khu vực có thanh tiến độ riêng ngay trên ô của khu vực đó: khu còn khóa hiển thị % hoàn thành yêu cầu (xu, cần câu, lưỡi câu, dây câu), khu đã mở hiển thị tiến độ gặp trùm. Thanh ngay dưới HUD luôn cho biết khu đang câu.
- **Skin nhân vật (20 bộ)**: mua trong tab Skin rồi đổi tự do. Mỗi skin có nội tại riêng (chờ cắn, lực kéo, cá hiếm, xu, giá bán, vòng cắn) và một chiêu cuối riêng. Skin đã mua không mất khi tái sinh.
- **Chiêu cuối**: nút tròn ở góc phải phía trên bảng dưới, hoặc phím `Q`. Nút hiển thị vòng hồi chiêu; chiêu tác động theo skin đang dùng (bắt ngay, choáng cá, đánh trùm, x2 xu, hóa giải thời tiết, dụ cá hiếm).
- **Thuyền (11 cấp)**: cấp 1 trở lên tự câu, cấp 2 tăng xu, cấp 5 mở tự bán. Tự bán rất chậm: mỗi **300 giây** ở cấp 5, giảm dần còn **180 giây** ở cấp 10 và chỉ nhận **70%** giá trị (trước đây là 15–40 giây, 80%).
- **Độ bền thuyền**: bão làm cá mập đâm thuyền, mỗi lần mất 1 điểm bền. Thuyền hỏng (0 bền) sẽ dừng tự câu và tự bán cho đến khi bấm **Sửa** trong tab Thuyền. Nâng cấp thuyền cũng vá thêm 1 điểm bền.
- **Thời tiết và hiệu ứng bất lợi**: thời tiết đổi khoảng mỗi phút và luôn kéo theo một debuff hiển thị ở HUD:
  - Nắng gắt — **Kiệt Sức**: cá lặn sâu, chờ cắn lâu hơn 30% và lực kéo giảm.
  - Mưa — **Dây Rỉ Sét**: dây câu dễ rối hơn gấp đôi.
  - Bão — **Bão Điện**: sét đánh làm tê tay 1,5 giây (không nhấn cần được), cá mập đâm thuyền.
  - Sương mù — **Mù Sương**: che gần hết mặt nước và bóng cá.
- 35 loài sinh vật/đồ vật, 5 trùm, 9 thú cưng có chỗ đậu riêng, hồ cá sinh xu theo thời gian, sự kiện đổi mỗi 5 phút.
- Tái sinh khi đã mở khu vực cuối: đổi tiến độ lấy hệ số thưởng vĩnh viễn (+50% xu mỗi lần).

## Cân bằng kinh tế

Giá nâng cấp dùng hệ số nhỏ hơn trước và mốc mở khu vực tăng đều, để đầu game không quá nhanh còn cuối game không bị hụt hơi.

| Hạng mục | Giá gốc | Hệ số mỗi cấp | Cấp tối đa |
| --- | --- | --- | --- |
| Cần câu | 40 | 1.55 | 10 |
| Mồi | 80 | 1.50 | 10 |
| Thuyền | 220 | 1.75 | 10 |
| Túi | 80 | 1.45 | 15 |
| Thú cưng | 450 | 1.70 | 10 |
| Lưỡi câu | 160 | 1.60 | 10 |
| Dây câu | 200 | 1.60 | 10 |

| Khu vực | Giá mở | Yêu cầu |
| --- | --- | --- |
| Đồng Cỏ Ngập | 0 | — |
| Sông Suối | 600 | Cần câu 2 |
| Hồ Núi | 2.400 | Cần câu 4 |
| Biển Khơi | 9.000 | Cần câu 6 |
| Vực Thẳm | 34.000 | Cần câu 8 |
| Rạn San Hô | 120.000 | Cần câu 8, lưỡi 2 |
| Đầm Lầy | 380.000 | Cần câu 9, dây 2 |
| Di Tích Chìm | 1.100.000 | Cần câu 10, lưỡi 5, dây 5 |

Giá trị trung bình mỗi khu vực tăng khoảng 2–4 lần: 17 → 44 → 106 → 548 → 1.330 → 2.157 → 3.808 → 14.160 xu. Cá hiếm ở khu sau được đẩy giá để không còn cảnh khu đắt hơn nhưng cá rẻ hơn.

## Cấu trúc

```
index.html                  Game HTML/CSS/JavaScript một tệp
.github/workflows/pages.yml Tự động triển khai GitHub Pages
.nojekyll                   Tắt xử lý Jekyll cho xuất bản từ nhánh
docs/                        Quy tắc code, thiết kế asset
  asset-thiet-ke.md          Thiết kế asset cho skin, cá, thuyền, icon
skills/                      Hướng dẫn phát triển game
fishing-game/                Bản sao tài liệu và game (giữ nguyên bố cục cũ)
```

Tiến độ chơi được lưu trong `localStorage` của trình duyệt (khóa `cau_ca_v8`, tự đọc được save `v7` trở về trước). Mỗi trình duyệt và mỗi địa chỉ web có vùng lưu riêng.
