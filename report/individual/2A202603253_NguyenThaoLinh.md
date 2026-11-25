# Báo cáo Day 13 — <Nguyễn Thảo Linh>, <2A202603253>

> Xoá mọi dấu TODO và dòng gợi ý (dòng bắt đầu bằng `>`). Mỗi con số lấy từ **bảng A** hoặc **phiếu tự kiểm** trong `submission/`, kèm đơn vị (m, °). Ảnh để trong `report/individual/images/` (nộp LMS trong file zip, không commit); trong báo cáo chỉ ghi **tên file ảnh**. Báo cáo này nằm trên repo public: không chép biển số, chữ trên biển hiệu hay biển chỉ đường, tên đường, địa danh; nhắc tới bạn khác thì ghi MSSV, không ghi họ tên. Cả báo cáo ~2 trang.

## 1. Kết luận trước
Mã số: **2A202603253**; task: **D13-2A202603253**. Lệnh `python scripts/lab.py dry` chạy thành công và chọn 10 frame: `s01f05`, `s01f52`, `s02f10`, `s02f36`, `s03f13`, `s03f55`, `s04f20`, `s04f39`, `s05f04`, `s05f23`; mỗi frame có 7 camera. Môi trường đang dùng là Windows PowerShell với `.venv`; Chrome đang mở.

Chưa có bảng A hoặc phiếu tự kiểm trong thư mục `submission/`, nên chưa xác nhận được tổng số cuboid, frame có ít nhất, hay số cuboid bị `selfcheck` gắn cờ. Cần bổ sung sau khi lưu nhãn và chạy `python scripts/lab.py sync`. Chưa ghi nhận đánh giá cá nhân về phần chắc/yếu nhất, phiên bản CVAT/tên tài khoản trong About, hoặc MSSV bạn ngồi cạnh.

Thao tác CVAT cần mô tả sau khi xác nhận đã thực hiện: (1) xoay khung 3D để nhìn từ trên xuống, kéo để xoay hoặc dời cảnh; (2) chọn **Shape**, đặt cuboid bằng nháy đúp rồi chỉnh trên Top/Side/Front; (3) bật **Cuboid orientation** để kiểm tra hướng và dùng `python scripts/lab.py preview` để xem cuboid trên ảnh camera.

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s01f05 |Phía trước (−y) ở cạnh trên; +x chỉ sang trái, +y chỉ xuống dưới |Tương đối phẳng, thấp hơn LiDAR ~1.72 m |~89 m (một xe bus cùng chiều phía trước) | Xe con, xe bus, dải phân cách, hàng cây, xe van |Phía sau (cam09): 6 xe con; bên phải: làn đường trống |Cụm điểm rất thưa phía sau, chỉ còn vài điểm rời rạc, không rõ xe hay biển báo |
| s01f52 |Phía trước (−y) ở cạnh trên; +x chỉ sang trái, +y chỉ xuống dưới|Tương đối phẳng, thấp hơn LiDAR ~1.72 m |~80 m (một xe bus đi vuông góc)  |Xe con, xe bus, dải phân cách, hàng cây, xe van |Phía sau (cam09): 2 xe con; bên phải: làn đường trống |Cụm điểm rất thưa phía sau, chỉ còn vài điểm rời rạc, không rõ xe hay biển báo | 

TODO(học viên): 3 điều **chỉ camera** cho biết và 3 điều **chỉ LiDAR** cho biết, lấy từ chính hai frame trên.
Camera cho biết: màu xe, 
Lidar cho biết: khoảng cách, 

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ  |
|---|---|---|
| s02f10 | | |
| s02f36 | | |
| s03f13 | | |
| s03f55 | | |
| s04f20 | | |
| s04f39 | | |
| s05f04 | | |
| s05f23 | | |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | TODO(học viên) | | | | | |
| (b) xe buýt hoặc xe tải | TODO(học viên) | | | | | |
| (c) người đi bộ hoặc xe hai bánh | TODO(học viên) | | | | | |

TODO(học viên): vòng hiệu chuẩn: cuboid của bạn lệch so với các bạn ở điểm nào, cả lớp chốt cách hiểu guideline nào? Và các vật bạn **bỏ qua vì không đủ cơ sở** (frame, vị trí, mô tả, loại nghi vấn như UNCERTAIN_CLASS / LOW_VISIBILITY), hoặc ghi "không có".

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | TODO(học viên) | | | |
| 2. Thưa ở xa | TODO(học viên) | | | |
| 3. Phản xạ thấp / ít điểm bất thường | TODO(học viên) | | | |
| 4. Điểm lạ | TODO(học viên) | | | |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-<MÃ SỐ>-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| TODO(học viên) | | | | | | | |
| TODO(học viên) | | | | | | | |
| TODO(học viên) | | | | | | | |

TODO(học viên): (a) cuboid **gần nhất** và **xa nhất**: `dist_m` và r của từng cái. (b) Kích thước l, w, h của một người đi bộ (hoặc xe hai bánh) và một xe con so với bảng 4.3: chiều nào ngoài khoảng, vì sao. (c) `yaw_deg` của một xe cùng chiều phía trước và một xe ngược chiều (nếu có): có gần 270° và 90° không.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| TODO(học viên) | | |

TODO(học viên): một câu quy luật ("xa gấp … lần thì số điểm còn khoảng …") và so với đường cong ở slide bài giảng (xe con: khoảng 1968 điểm ở 0–10 m, 718 ở 10–20 m, 214 ở 20–30 m, 72 ở 30–40 m, 19 ở 60–80 m). Rồi phần tự kiểm: hai cuboid bạn **đã sửa** sau `preview` / `selfcheck` (frame, idx, sửa gì), và những cảnh báo bạn **giữ nguyên** kèm lý do.

TODO(học viên): đổi kiểm: MSSV người đã kiểm chéo với bạn, hai con số nào được đối chiếu với bảng A, khớp hay lệch (lệch thì đã sửa gì).

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
TODO(học viên): (a) hai câu, nói từ phía model sẽ học trên nhãn này: vì sao nhãn 3D đo bằng mét chứ không phải pixel; vì sao vật thưa điểm cần quy tắc riêng. (b) Dùng AI? Ghi 3 dòng: công cụ, câu hỏi chính, bạn dùng kết quả thế nào. Không dùng: ghi "không dùng". (c) Điều còn chưa chắc, lỗi phát hiện sau hạn (không chấm; viết bằng lời, không chép số từ phiếu hồ sơ lỗi).
