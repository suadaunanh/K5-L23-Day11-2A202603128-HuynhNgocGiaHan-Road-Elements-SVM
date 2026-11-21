# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): luongvanquyen        Người kiểm (học viên): huynhngocgiahan
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `luongvanquyen-front.zip` (sha256 `80607d88…e02b`), `luongvanquyen-fisheye.zip` (sha256 `91e30af0…2e6b`); revision 2. Sha256 của cả hai file khớp manifest.
Số ảnh kiểm: 6 (A01, A06, A07, B01, B03, B05) (+ 0 ảnh thêm; lô không có A13–A16, B09–B12)   Số nhãn đã kiểm (shape + tag): 70

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 5 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 3 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 16 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 11 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 18 | 2 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 7 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 15 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách đếm số mục kiểm: QC1-01 = số ảnh; QC1-02 = số ảnh cần L1/R1 (A01, A06, A07, B01, B03; B05 là camera bên nên không tính); QC1-03 đến QC1-06 = số polyline `lane`; QC1-07 = drivable + crosswalk + road_curb; QC1-08 = số đèn; QC1-09 = đèn + biển; QC1-10 = số biển; QC1-11 = số shape trên 3 ảnh fisheye; QC1-12 = số file.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A01 | lane #0, đáy ảnh x ≈ 712 | nặng | Vạch đứt bên **phải** xe ghi `L1`; đúng là `R1` |
| 2 | QC1-03 | A01 | lane #6, đáy ảnh x ≈ 118 | nặng | Vạch đứt bên **trái** xe ghi `R1`; đúng là `L1` (L1/R1 bị đảo) |
| 3 | QC1-03 | A07 | lane #0, từ (1277,483) | nặng | Vạch ở **bên phải**, cạnh làn xe tải, ghi `L2`; đúng là `R2` |
| 4 | QC1-06 | A01 | lane #0 | chính | Vạch là vạch đứt nhưng `style = solid`; đúng là `dashed` |
| 5 | QC1-09 | A06 | traffic_sign #14 (659,214)–(710,241) | chính | Biển ONE WAY ghi `group = warning`; đúng là `mandatory` |
| 6 | QC1-09 | A06 | traffic_sign #7 (854,321)–(896,362) | chính | Biển thoi vàng (cảnh báo) ghi `group = mandatory`; đúng là `warning` |
| 7 | QC1-04 | B03 | lane #5 (L1) | chính | Vẽ từ xa về gần: điểm đầu ở chân trời (674,281), điểm cuối sát thân xe (1114,654) |
| 8 | QC1-04 | B03 | lane #4 (L2) | chính | Vẽ từ xa về gần: điểm đầu (742,286), điểm cuối (1036,432) |

Ảnh được ghi "không lỗi": **B01** (tag `fisheye_front` đúng; road_curb hai bên theo cung; crosswalk một polygon; drivable cắt ở mép capô, không gán thân xe).

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07 | Mặt đường ướt, bóng nước; `weather` nên là `rain` (đường ướt rõ do mưa) hay giữ `overcast`? | |
| A06 | Trời trắng xám dưới gầm cầu; `weather = clear` hay `overcast`? | |
| B03 | Camera sau: L/R tính theo hướng xe chạy hay theo trái/phải trên ảnh? Ảnh đang có L1, L2 nhưng không có R1 | |

Các ca trên không đổi kết luận (đã có lỗi nặng), nên không cần Hold.

## Quyết định
Lỗi nặng: 3   Lỗi chính: 5 / 70 nhãn = 7,1 %   Lỗi nhẹ: 0   Ca chờ lead: 3
Quyết định (Release / Hold / Rework): **Rework**
Lý do (theo luật của phiếu): có 3 lỗi nặng (QC1-03 sai `position` ở A01 ×2 và A07); ngoài ra tỉ lệ lỗi chính 7,1 % > 5 %. Chỉ một trong hai điều kiện đã đủ để Rework.

Ghi riêng (ngoài mẫu 6 ảnh, từ `road_check lint` toàn lô):
- QC1-02 ở A05 (thiếu L1, R1) và A09 (thiếu R1): hai ảnh này thật sự không thấy vạch; cần coach xác nhận miễn, không tính vào quyết định.
- Lô không có ảnh thêm (A13–A16, B09–B12): không trừ điểm, chỉ không có điểm thưởng.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
