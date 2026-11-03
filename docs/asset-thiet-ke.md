# Thiết kế Asset — Câu Cá Nâng Cấp

Tài liệu này mô tả asset cho toàn bộ nội dung mới: 20 skin nhân vật, 9 loài cá mới, 11 cấp thuyền, 4 icon hiệu ứng bất lợi, 6 icon chiêu cuối, hiệu ứng thời tiết và các thành phần HUD mới. Asset trong game hiện được vẽ bằng vector trên Canvas (không cần tải ảnh), nhưng mỗi mục đều có thông số kích thước, bảng màu, khung hình và prompt để có thể thay bằng sprite sheet PNG sau này mà không phải sửa logic.

Quy chuẩn prompt tham chiếu `docs/thietke.md`:

```
[Subject] + [Asset Type] + [Art Style] + [View/Perspective] + [Color Palette] + [Technical Specs] + [Isolation]
```

---

## 1. Quy chuẩn chung

| Thuộc tính | Giá trị |
| --- | --- |
| Khung logic game | 400 × 600 px, tỉ lệ 2:3, HUD phía trên, mặt nước ở `y = 290` |
| Phong cách | Vector 2.5D hoạt hình, viền đậm, cel-shading, silhouette rõ |
| Viền | màu `#1b1a2e`, dày 1.5–2.5 px ở kích thước gốc |
| Nền | trong suốt (alpha), không dùng nền gradient trong sprite |
| Tỉ lệ DPR | render ở `min(devicePixelRatio, 2.5)`, asset gốc vẽ 1x rồi phóng to |
| Điểm neo | đáy-giữa cho nhân vật/thuyền/cá; tâm cho icon |
| Animation | idle 4–8 frame, hành động 6–10 frame, loop liền mạch |
| Lưu cache | sprite vẽ một lần, khóa `fa{id}_{frame}`, `sk{i}_{frame}`, `bs_{kind}_{frame}` |

### Bảng màu dùng chung

| Token | Hex | Dùng cho |
| --- | --- | --- |
| ink | `#1b1a2e` | viền, bóng đổ, chữ |
| deep | `#264653` | thân tối, đáy nước |
| teal | `#2a9d8f` | nước ngọt, rêu |
| ice | `#a8dadc` | băng, ánh nước, cá hiếm |
| blue | `#457b9d` | sông, biển |
| moss | `#8ab17d` | đầm lầy, hệ thảo mộc |
| sand | `#e9c46a` | cát, gỗ sáng |
| orange | `#f29e4c` | lửa, cá thường |
| red | `#e76f51` | nguy hiểm, vây |
| gold | `#fee440` | tiền, huyền thoại, hào quang |
| violet | `#9b5de5` | ma thuật, vực sâu |
| pink | `#f15bb5` | san hô, kawaii |
| cyan | `#6ee7f7` | công nghệ, điện, băng |

---

## 2. Skin nhân vật (20 bộ)

Kích thước gốc **64 × 96 px**, chân đặt ở `y = 96`, đầu ở `y = 23`, thân từ `y = 36` đến `y = 70`. Mỗi skin dùng chung bộ xương chibi (đầu, thân, tay, chân) và thay 4 thành phần: kiểu tóc, áo, phụ kiện, vũ khí. Hào quang (aura) vẽ phía sau bằng radial gradient, alpha 0.35.

Animation gợi ý: idle 4 frame (nhấp nhô ±1 px, mắt chớp frame 3), cast 6 frame (tay phải đưa lên rồi hạ), ult 8 frame (aura bùng sáng + vũ khí lóe).

| # | Key | Tên | Tóc / áo / phụ kiện / vũ khí | Màu nhấn | Nội tại trong game | Prompt (rút gọn) |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | `sk0` | Ngư Dân Tập Sự | tóc ngắn nâu, áo xanh biển, mũ lưỡi trai, cần câu | `#457b9d` | Không có | chibi fisherman, brown short hair, blue jacket, cap, wooden rod, 2D vector, 64x96, transparent |
| 1 | `sk1` | Tôn Thần Nhẫn Giả | tóc vàng dựng, áo cam-đen, băng trán, quả cầu xoáy | `#f4d35e` | Chờ cắn −10%, lực kéo +8% | chibi ninja, spiky blonde hair, orange black jacket, forehead band, cyan spiral orb, vector game asset |
| 2 | `sk2` | Tài Ba Khai Sáng | tóc đen dựng, võ phục cam, găng tay, hào quang vàng | `#fee440` | Xu +8%, lực kéo +10% | chibi martial artist, spiky black hair, orange gi, golden aura, gauntlet, 64x96 |
| 3 | `sk3` | Hải Vương Mũ Rơm | tóc đen ngắn, áo đỏ, mũ rơm vàng, cần câu | `#e9c46a` | Cá hiếm +15%, xu +5% | chibi pirate, straw hat, red vest, scar under eye, fishing rod, vector flat |
| 4 | `sk4` | Thần Niệm Niệm Giả | tóc xanh dựng, áo xanh lá, không phụ kiện, cần trúc | `#9b5de5` | Vòng cắn hoàn hảo +12% | chibi hunter, spiky green hair, green outdoor outfit, violet aura, bamboo rod |
| 5 | `sk5` | Ma Pháp Thiếu Nữ Card | tóc hồng dài, đầm hồng, vương miện, gậy sao | `#f15bb5` | Chờ cắn −18% | chibi magical girl, long pink hair, frilly pink dress, crown, star staff, pink glow |
| 6 | `sk6` | Mèo Máy Tương Lai | tóc xanh, áo xanh dương, tai mèo, túi thần kỳ | `#6ee7f7` | Giá bán +8%, chờ cắn −8% | chibi robot cat, blue body, yellow bell, white pocket, round head, vector |
| 7 | `sk7` | Đao Thần Tóc Đỏ | tóc đỏ đuôi ngựa, áo đỏ, băng mặt, kiếm | `#e76f51` | Vòng cắn hoàn hảo +15% | chibi swordsman, red ponytail, red kimono, face bandage, katana, white scarf |
| 8 | `sk8` | Đại Bát Vương Săn Thần | tóc xanh dựng, giáp xanh, găng tay, hào quang cyan | `#6ee7f7` | Lực kéo +15% | chibi warrior, blue spiky hair, blue white armor, gauntlet, cyan aura, 64x96 |
| 9 | `sk9` | Nhãn Thuật Ma Vương | tóc đen dài, áo choàng đen, mặt nạ, mắt đỏ | `#e76f51` | Cá hiếm +20% | chibi dark mage, long black hair, black cloak with red clouds, red eyes, no weapon |
| 10 | `sk10` | Kiếm Sĩ Tam Đao | tóc xanh ngắn, áo tối, băng trán, ba kiếm | `#8ab17d` | Lực kéo +15% | chibi swordsman, short green hair, dark outfit, three katanas, headband |
| 11 | `sk11` | Ma Đạo Thủy Tộc Gray | tóc bạc dựng, áo xám, quả cầu băng | `#a8dadc` | Vòng cắn hoàn hảo +10% | chibi ice mage, silver spiky hair, grey outfit, ice orb, pale blue aura |
| 12 | `sk12` | Hỏa Long Ma Đạo | tóc hồng dựng, áo đen, găng lửa, khăn đỏ | `#f29e4c` | Xu +10% | chibi fire mage, pink spiky hair, black coat, flame gauntlet, orange aura |
| 13 | `sk13` | Tộc Trưởng Chuột Ma Thuật | tóc vàng, áo vàng, tai chuột, đuôi tia sét | `#fee440` | Lực kéo +12% | chibi electric mouse trainer, yellow outfit, mouse ears, lightning tail, gold aura |
| 14 | `sk14` | Khai Sáng Giả Titania | tóc đỏ dài, giáp bạc, vương miện, kiếm | `#ffffff` | Lực kéo +18% | chibi valkyrie, long red hair, silver armor, crown, sword, white aura |
| 15 | `sk15` | Bạch Nhãn Nhẫn Giả | tóc tím ngắn, áo kem, băng trán, mắt trắng | `#9b5de5` | Cá hiếm +15% | chibi ninja, short violet hair, cream jacket, band, pale eyes, violet aura |
| 16 | `sk16` | Iron Armor Genius | tóc nâu, giáp đỏ-vàng, kính che mặt, găng | `#6ee7f7` | Xu +12% | chibi armored inventor, red gold armor, faceplate, glowing chest core, cyan glow |
| 17 | `sk17` | Thần Sấm Giáp Vàng | tóc vàng dài, giáp vàng, vương miện, búa sét | `#fee440` | Lực kéo +20% | chibi thunder god, long blond hair, gold armor, crown, lightning hammer |
| 18 | `sk18` | Thần Cụ Cây Bảo Hộ | tóc xanh lá, áo rêu, sừng gỗ, gậy cây | `#8ab17d` | Chờ cắn −15%, cá hiếm +5% | chibi tree guardian, green bark skin, moss outfit, wooden horns, staff, soft green aura |
| 19 | `sk19` | Phù Thủy Thời Gian | tóc đen dài, áo xanh thẫm, vòng hào quang, quả cầu | `#fee440` | Chờ cắn −20%, xu +5% | chibi time sorcerer, long black hair, dark blue robe, golden halo, glowing orb |

### Ghi chú triển khai skin

- Hàm vẽ: `skinArt(i, frame)` — cache `sk{i}_{frame}`; icon tab dùng `sprite('sk'+i)`.
- Skin đang dùng lấy từ `G.skin`; danh sách đã mua lưu ở `G.skins`.
- Nội tại đọc trong `mods()` (`wait`, `ring`, `rare`, `coin`, `pull`) và `sellAll`/`autoSellBatch` (`sell`).
- Chiêu cuối đọc từ `SKINS[i].ult`; nút HUD gọi `useUlt()`.
- Nếu thay bằng ảnh: xuất PNG 64 × 96, 4 frame idle xếp ngang (256 × 96), cùng palette và viền; thay thân hàm `skinArt` bằng `drawImage` theo `frame % 4`.

---

## 3. Cá và sinh vật mới

Cá dùng khung **64 × 40 px**, thân elip ở `(30, 20)`, đuôi bên trái, mắt bên phải. Hai lớp trang trí mới: `aura` (quầng sáng tròn bán kính 27 px phía sau) và `horn` (sừng nhọn trên lưng). Cá huyền thoại thêm `crown` (5 gai vàng dọc sống lưng).

Animation: bơi 2 frame (đuôi lệch ±5 px), frame `f` đổi mỗi 1/6 giây.

| Key | Tên | Khu vực | Palette thân / bụng / vây | Hoa văn | Trang trí | Giá | Prompt |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 26 | Cá Chiết Giang Ngũ Sắc | Vực Thẳm | teal → violet / gold / pink | 5 sọc dọc | — | 900 | small tropical fish, five neon vertical stripes, teal violet gold, side view, vector |
| 27 | Cá Anh Vũ Hoàng Gia | Vực Thẳm | gold → orange / sun / violet | bụng sáng | vương miện | 2.000 | royal parrotfish, gold scales, violet fins, small crown, regal, 64x40 |
| 28 | Cá Tai Kính San Hô | Rạn San Hô | ice → cyan / white / ice | trơn | aura cyan | 3.600 | translucent coral fish, glass body, big round eyes, cyan halo, side view |
| 29 | Rùa Cổ Đại Khổng Lồ | Rạn San Hô | moss → brown / sand / moss | đốm mai rùa | aura rêu | 6.000 | ancient giant turtle, mossy shell like island, wrinkled neck, soft green glow |
| 30 | Cá Tra Bào Ngư | Đầm Lầy | pink → orange / sand / pink | bụng sáng | — | 4.200 | pink catfish, abalone-ruffled fins, smooth glossy skin, side view |
| 31 | Cá Sấu Bò Nước Ngọt | Đầm Lầy | moss → ink / brown / moss | sọc tối | — | 6.000 | small freshwater crocodile fish, rough green scales, long flat snout, jagged teeth |
| 32 | Cá Chuối Đỏ Toxic | Đầm Lầy | red → moss / orange / moss | đốm độc | aura xanh độc | 8.000 | toxic red fish, dark red body, green slime bubbles, glowing poison aura |
| 33 | Cá Rồng Hoang Kim | Di Tích Chìm | gold → red / white / red | sọc vàng | sừng + vương miện + aura vàng | 20.000 | golden dragon fish, long serpentine body, gold red scales, horns, crown, radiant aura |
| 34 | Cá Thần Ánh Trăng | Di Tích Chìm | ice → blue / white / cyan | bụng bạc | vương miện + aura cyan | 32.000 | moon deity fish, pearl white body, silver belly, cyan crown, moonlight glow |

Bốn loài cũ được nâng cấp hình ảnh theo cùng khung: Cá Bống Tượng Sấm Sét (sọc cyan phát điện), Cá Hải Tượng Bão Tố (vảy xám như đá), Cá Rồng Huyết Kim (vương miện + viền vàng), Cá Thần Đáy Hồ (aura vàng).

---

## 4. Thuyền (11 cấp)

Khung **96 × 40 px**, mũi thuyền bên phải, đáy ở `y = 36`. Thân gỗ gradient nâu, cabin trắng từ cấp 1, đèn vàng từ cấp 2, cột cờ từ cấp 3, khiên tròn từ cấp 4, kính tiềm vọng từ cấp 5, buồm từ cấp 6, băng tuyết từ cấp 7, viền vàng từ cấp 8, đèn neon từ cấp 9, cổng không gian tím từ cấp 10.

| Cấp | Tên | Chi tiết hình ảnh | Prompt |
| --- | --- | --- | --- |
| 0 | Bè Gỗ Sinh Tồn | bè gỗ thô, dây thừng, chòi rơm nhỏ | wooden survival raft, rope lashings, tiny straw hut, side view |
| 1 | Thuyền Trúc Bát Nhã | cabin trắng, mái đỏ, đèn lồng | bamboo fishing boat, white cabin, red roof, paper lantern |
| 2 | Thuyền Hải Tặc Thousand Sunny | đầu sư tử vàng ở mũi, buồm cam | cheerful pirate boat, lion head figurehead, orange sail, cartoon |
| 3 | Thuyền Rồng Hoàng Gia | đầu rồng vàng, cờ đỏ | royal dragon boat, golden dragon prow, red silk flag |
| 4 | Chiến Tàu Viking Longship | 4 khiên tròn hai bên mạn | viking longship, round shields along hull, wooden dragon prow |
| 5 | Tàu Ngầm Nautilus | kính tiềm vọng, thân kim loại xám | steampunk submarine, periscope, riveted metal hull, brass details |
| 6 | Thuyền Hoa Sen Tiên Cảnh | buồm trắng, cánh sen hồng | lotus fairy boat, white sail, pink lotus petals, serene glow |
| 7 | Thuyền Băng Nam Cực | gai băng trắng trên mạn, hơi lạnh | ice boat, translucent frozen hull, sharp icicles, cold mist |
| 8 | Phi Thuyền Wakanda Royal | viền vàng, động cơ phản lực | futuristic royal skiff, black vibranium hull, gold trim, hover engines |
| 9 | Tàu Tuần Dương Cyberpunk | dải neon hồng/cyan, vỏ đen nhám | cyberpunk speedboat, matte black hull, neon pink cyan strips |
| 10 | Thuyền Đa Chiều TARDIS | cổng xoáy tím ở mũi, thân xanh cổ điển | dimension-hopping boat, blue police box cabin, violet portal ring at bow |

Animation: lắc dọc ±1.5 px theo `sin(t)`, sóng mũi xuất hiện từ cấp 4, khói động cơ từ cấp 5, phản chiếu mặt nước alpha 0.3.

---

## 5. Icon hiệu ứng bất lợi (24 × 24 px)

Hiển thị trong chip HUD cạnh icon thời tiết, kèm tên và số giây còn lại. Viền `ink`, nền trong suốt, nét 1.4–2 px.

| Key | Tên | Hình | Màu | Prompt |
| --- | --- | --- | --- | --- |
| `deb:heat` | Kiệt Sức | mặt trời có khuôn mặt mệt, tia ngắn | cam `#f29e4c` | sun face icon, tired expression, heat rays, game debuff icon, 24x24 |
| `deb:rust` | Dây Rỉ Sét | sợi dây gỉ rơi mảnh, vết ố | nâu `#b06a3b` | rusty fishing line icon, corroded, falling flakes, debuff icon |
| `deb:shock` | Bão Điện | tia sét vàng, hồ quang cyan hai bên | vàng `#fee440` | electric shock icon, yellow lightning bolt, cyan arcs, debuff |
| `deb:fog` | Mù Sương | 3 dải sương xếp lớp, nền xám mờ | trắng xám | fog layers icon, grey mist, blindness debuff, flat vector |

Cách dùng: `sprite('deb:'+k)`, chip `#debChip`, hiệu ứng vẽ trong `drawWeather()`.

---

## 6. Icon chiêu cuối (32 × 32 px)

Nút tròn 58 px ở góc phải, vòng hồi chiêu vẽ bằng `conic-gradient`. Icon nền trong suốt, viền đậm, có điểm sáng để đọc rõ trên nền tối.

| Key | Kiểu | Hình | Màu | Prompt |
| --- | --- | --- | --- | --- |
| `ult:catch` | Bắt ngay | lưỡi câu móc con cá nhỏ | băng + cam | fishing hook catching a fish, game skill icon, 32x32 |
| `ult:stun` | Choáng | vòng xoáy cyan + tia sét vàng | cyan/gold | stun skill icon, swirling cyan ring, lightning bolt, 32x32 |
| `ult:boss` | Đánh trùm | đầu lâu trắng trên nền vàng | trắng/gold | boss slayer skill icon, white skull, gold banner, 32x32 |
| `ult:wealth` | Tài lộc | 3 đồng xu vàng xếp chồng | gold | coin stack skill icon, three gold coins, sparkle, 32x32 |
| `ult:guard` | Hộ thân | khiên năng lượng xanh băng | ice/cyan | energy shield skill icon, layered hex shield, cyan glow |
| `ult:lure` | Dụ cá | quả cầu ma thuật tím có mắt cá | violet/gold | lure skill icon, violet magic orb, fish silhouette, sparkles |

---

## 7. Hiệu ứng thời tiết và môi trường

| Hiệu ứng | Mô tả hình ảnh | Thông số |
| --- | --- | --- |
| Nắng gắt (heat) | lớp phủ cam alpha 0.06 trên mặt nước, 4 đường sóng nhiệt uốn theo `sin`, màu `#f29e4c` alpha 0.2 | cuộn ngang 2.2 rad/s, biên độ 3 px |
| Dây rỉ sét (rust) | lớp nâu alpha 0.1, 7 vệt gỉ nhỏ giọt dọc mặt nước | vệt dài 16–56 px, alpha 0.35 |
| Bão điện (shock) | 3 cung điện cyan quanh phao, chớp trắng toàn màn hình, mưa xiên 8 px | cung quay 3 rad/s, alpha 0.35–0.7 |
| Mù sương (fog) | 4 dải sương trắng alpha 0.16 + lớp phủ xám alpha 0.26 trên mặt nước | trôi ngang 9–21 px/s |
| Sóng mũi thuyền | 2 gợn elip mờ sau đuôi thuyền | chu kỳ 0.9 s, bán kính 20 px |
| Cá mập đâm thuyền | flash đỏ quanh thuyền + float icon `deb:shock` “−1” | mỗi 16–24 s khi bão, trừ 1 độ bền |
| Cá bay về túi | parabol, tia nước nhỏ, hạt màu theo độ hiếm | 0.85 s mỗi chuyến |

---

## 8. HUD mới

| Thành phần | Kích thước | Thiết kế |
| --- | --- | --- |
| Thanh tiến độ khu vực (HUD) | cao 6 px, rộng theo màn hình | nền `#1b1a2e` alpha 0.8, viền `#3d3766`, fill gradient cam → đỏ `#f29e4c → #e76f51`; nhãn tên khu bên trái, `x/30` bên phải |
| Thanh tiến độ trong ô khu vực | cao 5 px | khu khóa: fill xanh rêu → vàng; khu mở: fill cam → đỏ; thêm `%` cỡ 9 px |
| Nút chiêu cuối | 58 × 58 px | hình tròn, nền radial `#332e5e → #17142a`, viền `#3d3766`, icon 28 px, vòng `conic-gradient` vàng theo % hồi chiêu, nhãn giây 9 px |
| Chip debuff | cao 26 px | giống `.chip`, viền đỏ cam alpha 0.7, icon 20 px + tên + số giây |
| Tab thứ 6–7 | 7 cột đều | icon thuyền (96 × 40 thu nhỏ) và icon skin đang dùng (64 × 96 thu nhỏ) |
| Độ bền thuyền | hàng chữ trong tab Thuyền | `bền/max`, nút Sửa, cảnh báo đỏ khi 0 |

---

## 9. Quy trình thay asset vector bằng PNG

1. Xuất từng sprite đúng kích thước gốc, nền trong suốt, viền giữ nguyên.
2. Đặt tên theo khóa: `sk1_idle_0..3.png`, `fish26_swim_0..1.png`, `boat_10.png`, `deb_heat.png`, `ult_stun.png`.
3. Ghép atlas theo hàng, mỗi frame cùng kích thước, padding 2 px.
4. Trong `skinArt`, `fishArt`, `boatArt`, `ultIcon`, `debIcon`: thay phần vẽ bằng `drawImage(atlas, frame*w, 0, w, h, ...)`.
5. Giữ nguyên khóa cache và `iconURL`; mọi chỗ dùng `sprite()` sẽ tự nhận asset mới.
6. Kiểm tra lại silhouette đen (`silOf`) cho cá: ảnh gốc phải có alpha sạch để tint không bị viền răng cưa.

---

## 10. Prompt mẫu đầy đủ

**Skin (2D vector):**

> Sprite sheet of a chibi ninja fisherman, spiky golden hair, orange and black jacket, metal forehead band, glowing cyan spiral orb in hand, idle animation 4 frames, 2D vector game asset, 3/4 front view, clean thick dark outline, flat cel shading, transparent background, uniform 64x96 grid, game-ready --ar 1:2

**Cá (side view):**

> Sprite sheet of a golden dragon fish, long serpentine body, gold and crimson scales, small horns and crown, radiant gold aura, swimming animation 2 frames, side view, 2D vector game asset, thick ink outline, flat shading, transparent background, 64x40 frames, game-ready

**Thuyền (side view):**

> Game asset of a cyberpunk speedboat, matte black angular hull, neon pink and cyan light strips, small cabin, side view, 2D vector game asset, thick dark outline, flat cel shading, isolated on transparent background, 96x40, game-ready

**Icon (UI):**

> Game UI icon, electric stun skill, swirling cyan ring with a yellow lightning bolt, flat vector style, thick dark outline, high contrast, isolated on transparent background, 32x32, centered, no text

---

## 11. Checklist trước khi xuất asset

- [ ] Đúng khung: skin 64 × 96, cá 64 × 40, thuyền 96 × 40, icon 32 × 32 / 24 × 24.
- [ ] Nền trong suốt, không có bóng đổ ngoài khung.
- [ ] Viền `#1b1a2e` đồng nhất, không lẫn pixel trắng.
- [ ] Silhouette đọc được khi tô đen toàn bộ.
- [ ] Idle loop kín (frame cuối nối frame đầu).
- [ ] Màu nằm trong bảng palette chung, không dùng quá 3 màu nhấn mỗi asset.
- [ ] Tên file/khóa khớp bảng trong tài liệu này.
- [ ] Đã kiểm tra trên nền tối `#0b0a16` và trên mặt nước xanh.
- [ ] Nếu phát hành thương mại, tránh dùng trực tiếp tên hoặc thiết kế nhân vật có bản quyền; các skin trong game là thiết kế lấy cảm hứng, không sao chép.
