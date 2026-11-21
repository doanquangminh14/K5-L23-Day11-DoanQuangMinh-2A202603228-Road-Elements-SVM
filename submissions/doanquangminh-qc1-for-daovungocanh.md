# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): daovungocanh        Người kiểm (học viên): doanquangminh (Đoàn Quang Minh)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `daovungocanh-front.zip`, `daovungocanh-fisheye.zip` (em không nhận được file manifest từ bạn nên không có số `revision`)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 99 (75 shape + 24 tag)  

Ảnh đã kiểm: A03, A04, A08, A14 (front); B04, B06 (fisheye). Mẫu chọn kiểm có đủ ca đèn và biển dày (A03, A08), vạch vàng đôi (A04, A14), ảnh chụp đêm (A14), camera sau (B04) và camera bên sườn (B06).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 2 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 16 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 23 | 1 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 45 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 22 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 9 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách em đếm "Số mục kiểm": QC1-01 và QC1-02 đếm theo từng ảnh; QC1-03 đến QC1-06 đếm theo từng đường polyline `lane`; QC1-07 đếm tổng drivable (10), crosswalk (4) và road_curb (2); QC1-08 đếm hộp đèn; QC1-09 đếm tổng số đèn cộng biển; QC1-10 đếm biển; QC1-11 đếm mọi hình vẽ trên ảnh fisheye B; QC1-12 đếm số file nộp.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A14 | traffic_light #10 | nặng | Đèn đang sáng **xanh** (bóng dưới sáng xanh ngọc) nhưng bạn gán `color = red`, `facing = front` (đèn quay thẳng về hướng xe) |
| 2 | QC1-03 | B04 | lane #3 (R1) | nặng | Polyline nằm đè lên mép vỉa hè bên phải, thực tế không có vạch sơn nào. Chỗ này là `road_curb`, không phải lane R1 |
| 3 | QC1-06 | A14 | lane #1 (L1) | chính | Vạch tim đường là vạch vàng đôi nhưng bạn gán `color = white` |
| 4 | QC1-05 | A14 | lane #3 (L2) | chính | Nét thứ hai của **cùng** một vạch vàng đôi bị vẽ tách thành polyline riêng (gán L2, white). Vạch đôi phải vẽ chung 1 polyline, `kind = double` |
| 5 | QC1-05 | A04 | lane #1 (L2) | chính | Nét thứ hai của vạch vàng đôi (lane #3, L1 yellow double) bị vẽ tách thành polyline riêng, gán L2 / white / single |
| 6 | QC1-07 | A08 | drivable #24 (direct) | chính | Polygon dừng hụt ở mép trên vạch ngựa vằn (y ≈ 440), bỏ sót phần mặt đường từ crosswalk tới sát capô xe. Vùng lái bị thiếu nhiều |
| 7 | QC1-07 | A08 | drivable #25 (alternative) | chính | Tương tự lỗi #6: vùng lái làn bên cạnh dừng hụt ở mép trên crosswalk, không kéo xuống mép capô |

Ảnh kiểm tra thấy bạn làm rất tốt, không phát hiện lỗi: **B06** (tag `fisheye_left` đúng chuẩn theo hậu tố MVL; vạch lane #0 đặt `position = other` rất đúng; drivable cắt chuẩn ở mép thân xe; crosswalk gom thành 1 polygon). Ảnh A03 em soi kỹ không thấy lỗi hình học rõ ràng, chỉ có băn khoăn về occluded đã ghi ở mục ca mơ hồ.

Ghi chú khi em chạy lint (`road_check lint`): Lệnh có báo QC1-02 "chưa có R1" ở ảnh A14 nằm trong mẫu kiểm. Em đối chiếu ảnh thực tế thì bên phải chỉ có mép đường/vỉa hè (bạn đã vẽ 2 road_curb) chứ không có vệt sơn, nên em không tính lỗi này cho bạn. Ngoài mẫu kiểm, lint có báo thêm QC1-02 ở A05, A06 và 3 biển thấp dưới 8 px ở A10 (nhẹ, không bắt buộc). Ảnh A11 (ngoài mẫu kiểm) cũng dính lỗi tương tự là vạch vàng đôi bị vẽ tách thành hai polyline L1 + L2 riêng lẻ.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B04 (cả B03) | Camera sau nhìn ngược chiều xe chạy: L1/R1 tính theo trái/phải của **ảnh** hay theo **hướng tiến của xe**? Bạn Ánh gán L1 ở bên trái ảnh nên em muốn hỏi lại lead cho rõ ràng | |
| A04, A14 | Nét thứ hai của vạch đôi bị vẽ tách thành lane riêng: tính lỗi QC1-05 (vạch bị tách rời) hay QC1-03 (vạch thừa, mức nặng)? Em đang tạm tính là QC1-05 | |
| A08 | Tấm biển chữ nhật nhỏ "PASSENGER CARS ONLY" gắn phía trên biển chỉ dẫn lớn (traffic_sign #8): nên gán `information` hay `supplementary`? Bạn đang gán là information | |
| A03 | Checkpoint ghi ảnh A03 có đoạn vạch bị che (`occluded`). Bài của bạn không bật occluded ở vạch nào, nhưng em soi trên ảnh cũng chưa khẳng định được chắc chắn đoạn nào bị che khuất | |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 5 / 99 nhãn = 5,1 %   Lỗi nhẹ: 0   Ca chờ lead: 4  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô của bạn Ánh còn 2 lỗi nặng (QC1-08 gán nhầm đèn xanh thành đỏ ở hướng xe chạy tại A14; QC1-03 vẽ lane đè lên mép vỉa hè ở B04), theo quy chế bài lab chỉ cần 1 lỗi nặng là phải Rework. Ngoài ra, tỉ lệ lỗi chính là 5,1% (5 / 99 nhãn đã kiểm), đã vượt mức 5% cho phép. Bốn ca mơ hồ không làm thay đổi kết luận này nên em quyết định trả về để bạn sửa lại (Rework).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
