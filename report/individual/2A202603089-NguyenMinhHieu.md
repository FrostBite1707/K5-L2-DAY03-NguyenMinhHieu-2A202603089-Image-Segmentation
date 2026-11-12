# Báo cáo thực hành Day 3

- Mã học viên theo lớp: `2A202603089`
- Ngày / CVAT local: `2026-11-12`; các ZIP thể hiện là export từ CVAT local.
- Công cụ đã dùng: CVAT local (theo định dạng export); scorer Python để tự đánh giá. Công cụ gợi ý tự động/SAM: chưa xác nhận.

## 1. Bài đã nộp

Số ảnh dưới đây được đếm từ các ZIP hiện có trong `submissions/`. Có ZIP không tự xác nhận trạng thái Save trong CVAT.

| Task | File ZIP đúng tên | Ảnh trong ZIP | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 000000181542.jpg, vị trí ở gần giữa ảnh phía trước xe máy đang đi về phía bên phải
- Class và quy tắc tôi dùng để chọn biên: tô phần thân xe nhìn thấy theo đường viền vật, không lấy bóng đổ hoặc mặt đường. Nếu người hay vật khác che một phần, chỉ tô phần còn nhìn thấy; không đoán phần bị che.
- Nếu dùng gợi ý sau đó: không dùng
- Nếu không dùng gợi ý: Không dùng gợi ý tự động. Tôi gán class car và chỉ tô phần thân xe nhìn thấy, không lấy bóng đổ.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `easy_semantic`, toàn bộ export.
- Lỗi thuộc loại: Khác — sai định dạng export.
- Bằng chứng tôi nhìn thấy: Bản ZIP trước đó chứa `annotations.xml`, sau đó là COCO `annotations/instances_default.json`; scorer báo không tìm thấy image masks. Bản ZIP hiện tại có `SegmentationClass/` và `SegmentationObject/` cho đủ ba ảnh và scorer chạy được.
- Quy tắc và hành động sửa: Easy yêu cầu `Segmentation mask 1.1`; đã export lại đúng định dạng từ CVAT.
- Sau sửa đã Save và export lại chưa? ZIP mới đã được export và chấm; trạng thái Save trong CVAT không thể xác minh từ ZIP.
- Kết quả tự đánh giá sau khi xem reference: Easy **15.2/20**, mIoU **0.742**, coverage **82.7%**; Medium **4.1/32**; Hard **8.4/30**. Scorecard ba tier: **27.7/82**. Đây là tự đánh giá, không phải điểm cuối trên 100.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Các hàng dưới đây là điểm nên đối chiếu với CVAT dựa trên tự đánh giá; chúng không khẳng định đây là những do dự đã có khi vẽ. Học viên cần xác nhận quyết định thực tế trước khi nộp.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Easy, ranh road–sidewalk trên ba ảnh | Pixel sát bó vỉa thuộc road hay sidewalk | IoU sidewalk là 0.637; ranh cần theo chức năng/bó vỉa, không chỉ màu | Đối chiếu từng ranh trong CVAT; ghi quyết định thực tế hoặc hỏi coach về đoạn mơ hồ. |
| Medium, các vật thể bị bỏ sót/thêm | Một vật nhỏ/che khuất bị bỏ sót hay không thuộc taxonomy; mask dư là vật riêng hay nền | So với reference: 43 TP, 18 FP, 28 FN; submitted 61 object so với GT 71 | Kiểm ảnh và object list trong CVAT; nêu một trường hợp thật và quyết định. |
| Hard, person và traffic light | Thing nhỏ/che khuất bị bỏ sót hay không đủ pixel nhìn thấy để gán | Scorer ghi nhận person 0/9 và traffic light 0/4 TP; chỉ vẽ phần nhìn thấy theo quy tắc | Kiểm hai ảnh Hard; xác nhận nguyên nhân và hỏi coach tại vùng không chắc. |
