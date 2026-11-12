# Báo cáo thực hành Day 3

- Mã học viên theo lớp: 2A202603116
- Ngày / CVAT local: 12/11/2026 / CVAT local
- Công cụ đã dùng: CVAT local, công cụ vẽ polygon/mask và AI assistance/SAM2 để hỗ trợ kiểm tra; kết quả cuối cùng được kiểm tra và lưu trong CVAT.

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | chưa có | chưa làm | 3 |
| cp2_slice | chưa có | chưa làm | 3 |
| cp5_occlusion | chưa có | chưa làm | 3 |
| cp3_thin | chưa có | chưa làm | 3 |
| cp4_curb | chưa có | chưa làm | 3 |
| cp6_coverage | chưa có | chưa làm | 3 |
| **Tổng tối đa** | | | **100** |

Ba ZIP chính đã được export đúng định dạng theo đề và đưa vào thư mục `submissions/`. Chưa tự ghi điểm.

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và vùng Easy đầu tiên tự vẽ: ảnh đầu tiên của `easy_semantic`, vùng đường ở phần tiền cảnh.
- Class và quy tắc mình dùng để chọn biên: chọn class `road`; bám theo ranh giới thực tế của mặt đường, không lấy phần sidewalk hoặc nền xung quanh vào cùng mask.
- Nếu dùng gợi ý sau đó: mình dùng gợi ý như tham khảo, kiểm tra lại biên và chỉnh phần mask bị ăn vào nền hoặc thiếu ở mép vùng trước khi lưu.

## 3. Một lỗi mình tìm thấy và sửa

- Task/ảnh/vùng: các ảnh có phương tiện trong `medium_instance` và `hard_panoptic`.
- Lỗi thuộc loại: biên và gộp/tách object.
- Bằng chứng mình nhìn thấy: khung gợi ý ban đầu chỉ bao quanh vùng chữ nhật của xe, chưa phải đường biên chính xác; một số vùng nền có thể bị lấy nhầm nếu giữ nguyên gợi ý.
- Quy tắc và hành động sửa: tách từng vật thể thành một instance riêng, chỉnh lại mask theo phần vật thực sự nhìn thấy, loại phần nền thừa và kiểm tra các vùng chồng lấn trước khi Save.
- Sau sửa đã Save và export lại chưa?: Đã Save và export lại các ZIP `medium_instance.zip` và `hard_panoptic.zip`.

Kết quả tự kiểm cấu trúc ZIP: `easy_semantic`, `medium_instance` và `hard_panoptic` đều hợp lệ; chưa có điểm tự đánh giá theo ground truth chính thức.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Medium: người đi xe máy | Có thể vẽ xe máy bị che bởi người hoặc vẽ tách rời người và xe | Quan sát phần xe máy đi ngang qua người và giữ ranh giới phần xe nhìn thấy | Mình vẽ xe máy ngang qua người, không gộp người vào mask xe máy |
| Hard, hình 1: cây và hàng rào | Có thể nhầm vùng cây với hàng rào do chúng chồng lên nhau | Quan sát thứ tự che khuất trong ảnh: cây nằm đè lên hàng rào | Mình vẽ theo cây đè lên hàng rào và giữ hai vùng theo phần nhìn thấy |
| Easy, hình 2: cây và bầu trời | Có thể lấy nhầm phần bầu trời vào vùng cây ở ranh giới | Dựa vào đường biên nhìn thấy của tán cây | Mình vẽ theo cây đè lên bầu trời, không gán bầu trời vào mask vegetation |
