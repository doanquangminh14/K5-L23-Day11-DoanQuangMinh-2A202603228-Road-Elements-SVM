# Báo cáo cá nhân — Ngày 11
Họ tên: Đoàn Quang Minh               Mã học viên: 2A202603228  
Phiên bản CVAT (Help → About): 2.74.1  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026, khoảng 11:13 (giờ Việt Nam; XML ghi 04:13 UTC)    Số lần nộp lại sau Rework: 0  

**Ảnh thêm (điểm thưởng):** đã làm đủ 8/8 ảnh A13–A16 và B09–B12; nằm trong `doanquangminh-front.zip` (16 ảnh) và `doanquangminh-fisheye.zip` (12 ảnh).

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane, road_curb (polyline); crosswalk, drivable (polygon); traffic_light, traffic_sign (rectangle). Đã đối chiếu với file taxonomy |
| Thuộc tính và giá trị | Đúng | Khối `<meta>` trong file export có đủ thuộc tính và giá trị đúng như bảng mục 1 guideline |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source; mỗi tag là label kiểu Tag có một thuộc tính select `value` |

Cách kết thúc polyline trên bản CVAT này: bấm phím **N** sau khi click điểm cuối cùng.  
Cách đặt tag ảnh trên bản CVAT này: chọn công cụ **Tag** ở thanh bên trái, chọn label rồi bấm **Tag**; sau đó mở mục **Details** trong bảng Objects để chọn đúng giá trị `value`, tránh để CVAT tự điền giá trị đầu tiên của danh sách.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 12 | 5 | 26 | 41 | 20 |
| front-extra (đã làm 4 / 4) | 4 | 10 | 3 | 5 | 7 | 8 | 10 |
| fisheye | 8 | 2 | 6 | 10 | 10 | 1 | 6 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 1 | 4 | 5 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | vẽ L1/R1 hay không vẽ | không vẽ | Đoạn này hai bên chỉ có lề đường đất đá, không có vệt sơn nào (em đã vẽ road_curb). Lệnh lint báo QC1-02 thiếu L1/R1, nhưng do thực tế không có vạch nên em không vẽ vạch ảo để tránh bị lỗi nặng QC1-03, xin coach xem ảnh xác nhận miễn lỗi giúp em |
| A06, A09, A14 | lane R1 | vẽ R1 hay không vẽ | không vẽ R1 | Bên phải làn xe chạy sát mép lề đường/vỉa hè, không hề có vệt sơn mép làn. Em không thể vẽ đè lên vỉa hè vì sẽ bị phạt lỗi nặng QC1-03. Em để trống R1 và xin coach đối chiếu ảnh thực tế để miễn trừ QC1-02 |
| B11 | lane | vạch vàng/trắng trong bãi đỗ là lane hay vạch ô đỗ | không gán lane | Ảnh camera sau chụp trong bãi đỗ xe: có viền ô đỗ người khuyết tật, vạch chia ô và vùng kẻ sọc. Em làm theo đúng mục 4 guideline quy định vạch ô đỗ không gán vào nhãn lane |
| B11 | drivable | gồm ô đỗ hay chỉ lối đi | chỉ lối đi | Guideline quy định dải đỗ xe không tính vào direct; em cắt gọn ở mép cản sau xe mình |
| A04, A09 | lane position | vạch thứ ba tính từ làn mình là R2/L2 hay other | other | Road v1.0 chỉ phân loại đến L1/R1/L2/R2; các vạch nằm ngoài xa hơn L2/R2 em gán là `other` |
| A04, A11, A14 | lane color | white hay yellow | yellow, kind = double | Lúc mới vẽ em quen tay để mặc định white, sau khi soi kỹ lại ảnh thấy tim đường là vạch vàng đôi nên em đã mở Details chỉnh lại thành yellow và kind = double |
| B03 | traffic_sign edge_zone | bật hay tắt | bật | Tâm hộp biển báo ở tọa độ (1130, 361), cách tâm ảnh khoảng 505 px, rất sát ngưỡng 80% bán kính (512 px). Sau khi chạy lint thấy gợi ý nên em quyết định tick chọn edge_zone cho an toàn |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: daovungocanh (Đào Vũ Ngọc Ánh)  Quyết định nhận được: Rework  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 (A09, lane x ≈ 523..672 bị cho là phải R1) | 1 | Không | Không sửa: L1 là đúng |
| QC1-02 (A09, thiếu R1, kéo theo lỗi trên) | 1 | Không | Không sửa: bên phải không có vạch sơn |
| QC1-12 (xuất 4 file zip thay vì 2) | 1 | Có | Đã sửa: gộp thành `doanquangminh-front.zip` (16 ảnh) và `doanquangminh-fisheye.zip` (12 ảnh) |

Giải thích của em về ảnh A09: Khi nhìn từ góc lái (tâm capô xe ở khoảng x ≈ 640), làn đường xe em đang đi thẳng là vùng drivable direct. Vạch sơn đứt đoạn x ≈ 523..672 rõ ràng nằm ở phía bên tay trái của làn xe chạy, nên em gán thuộc tính position là L1 là hoàn toàn chính xác. Phía bên phải của xe là mép đường sát vỉa hè, chỗ này không có vệt sơn nào cả nên em đã vẽ road_curb chứ không vẽ vạch sơn ảo (trường hợp này giống hệt các ảnh A05, A06, A14). Nếu em nghe theo bạn sửa vạch bên trái thành R1 thì em sẽ bị phạt lỗi nặng QC1-03 ngay. Em xin giữ nguyên nhãn L1 và nhờ coach xem lại ảnh này để xác nhận miễn lỗi QC1-02 giúp em. Vì không thay đổi nhãn nào nên lần nộp của em vẫn giữ là `revision 1`.  
Còn lỗi QC1-12 bạn nhắc về việc xuất nhầm thành 4 file zip riêng lẻ, em thấy bạn nhận xét rất đúng. Em đã gộp task thường và task extra lại thành đúng 2 file zip hoàn chỉnh như yêu cầu nộp bài.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| doanquangminh-front.zip | Có (`road_check lint` đọc đủ 16 ảnh, 16/16 ảnh đủ 4 tag) | A01: 9 / 9 | A02: 7 / 7 | Có (`<tag label="camera">`, value = front) |
| doanquangminh-fisheye.zip | Có (`road_check lint` đọc đủ 12 ảnh, 12/12 ảnh đủ 4 tag) | B01: 2 / 2 | B02: 4 / 4 | Có (value = fisheye_front / rear / left / right theo hậu tố file) |

Manifest `doanquangminh-manifest.json`: `revision 1`, `contains_images: false` ở cả hai file; lint lúc tạo: nặng 5 (đều là cảnh báo QC1-02 ở A05, A06, A09, A14 do không có vạch sơn thật, xem mục 3), chính 0, nhẹ 0.  
Ghi chú: CVAT export riêng từng task, nên em đã gộp `front` + `front-extra` và `fisheye` + `fisheye-extra` vào một file `annotations.xml` duy nhất cho mỗi file nộp.

## 6. Ảnh chụp màn hình
1. Tab Labels của project:

   ![Tab Labels của project](images/1-labels.png)

2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển):

   Do ảnh dataset BDD100K có điều khoản bản quyền không được đưa công khai lên repo GitHub nên em lưu riêng file `2-front.png` và gửi trực tiếp cho coach kiểm tra.

3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong:

   Do ảnh dataset WoodScape có điều khoản không cho phân phối lại nên em lưu riêng file `3-fisheye.png` và gửi trực tiếp cho coach kiểm tra.

4. Một đoạn XML có `<polyline label="lane">`:

   ![Đoạn XML có polyline lane](images/4-xml.png)

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Lỗi em mắc nhiều nhất lúc làm là ở nhóm đèn và biển (QC1-08 / QC1-09): ở lần export đầu tiên, do CVAT tự chọn giá trị đầu danh sách nên toàn bộ 66 hộp đèn đều mang thuộc tính mặc định là `red · vehicle · front` và 32 biển là `prohibitory · front`. Lúc đó em vẽ xong mà chưa mở tab Details để soi lại từng hình. Ngoài ra em còn bị dính lỗi QC1-01 (quên đặt tag ở A12, B07, B09 và chọn nhầm camera ở B04, B06, B12) và QC1-06 (quên đổi vạch vàng đôi sang màu yellow). Sang Ngày 20, em sẽ rút kinh nghiệm: vẽ xong hình nào là mở Details kiểm tra thuộc tính ngay hình đó, đặt tag camera theo tên file trước tiên, và chạy lệnh `road_check lint` kiểm tra sau từng task chứ không để dồn tới cuối buổi mới kiểm.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Hộp `traffic_light` và thuộc tính `color` là dữ liệu huấn luyện đầu vào cho mô hình nhận diện và phân loại trạng thái đèn tín hiệu của xe tự hành. Lúc đầu em suýt bị sót lỗi để mặc định đèn màu đỏ (trong khi trên ảnh thực tế là đèn đang bật xanh). Nếu đem dữ liệu gán nhãn sai này đi huấn luyện, mô hình sẽ học rằng đèn xanh cũng mang nhãn đỏ. Hậu quả thực tế khi xe tự hành chạy ngoài đường là xe có thể phanh gấp nguy hiểm khi gặp đèn xanh, gây nguy hiểm cho các xe phía sau. Nguy hiểm hơn nữa là ranh giới giữa hai nhãn đỏ/xanh bị nhập nhằng khiến xe có thể nhận diện nhầm đèn đỏ thành xanh gây tai nạn nghiêm trọng. Vì đèn quay thẳng vào hướng xe chạy (`facing = front`) ảnh hưởng trực tiếp đến an toàn lái xe nên việc thang QC phân lỗi này vào mức lỗi nặng là hoàn toàn xác đáng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
