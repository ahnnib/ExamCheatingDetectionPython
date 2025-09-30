# Ứng dụng phát hiện gian lận trong thi cử bằng AI

## 1. Ý tưởng
Trong các kỳ thi trực tuyến, học sinh có thể thực hiện nhiều hành vi gian lận như nhìn sang chỗ khác, sử dụng điện thoại, hoặc có sự xuất hiện của nhiều người ngoài khung hình. Dự án này xây dựng một hệ thống AI giám sát thời gian thực, có khả năng phát hiện và cảnh báo những hành vi bất thường để hỗ trợ giám thị đảm bảo tính công bằng trong thi cử.

## 2. Phương pháp thực hiện
- Thu thập và mô phỏng dữ liệu video các hành vi “bình thường” và “gian lận” (nhìn sang chỗ khác, dùng điện thoại, nhiều người xuất hiện…).
- Dựa vào mô hình đã được huấn luyệt sẵn YOLOv8 (đã học trên COCO dataset) để giúp phát hiện vật thể, ở đây là khuôn mặt và điện thoại.

- Áp dụng các kỹ thuật thị giác máy tính để:
    - Ước lượng tư thế đầu để phát hiện khi thí sinh quay mặt khỏi màn hình.
    - Nhận diện đối tượng (điện thoại, sách vở) trong khung hình.
    - Nhận diện đối tượng thứ ba trong khung hình giám sát.
    - Xây dựng hệ thống giám sát thời gian thực, có tính năng hiệu chỉnh trước khi bắt đầu nhận diện.

## 3. Công nghệ sử dụng
* Python: Ngôn ngữ lập trình chính.
* OpenCV: Thư viện thị giác máy tính mã nguồn mở giúp xử lý video và hình ảnh trong thời gian thực.
* MediaPipe: Theo dõi khuôn mặt bằng cách xác định các điểm mốc, giúp tính toán hướng nhìn và góc quay đầu so với hướng ban đầu.
* YOLOv8: Nhận diện điện thoại/sách vở và các đối tượng liên quan.

## 4. Kết quả đạt được
* Hệ thống demo chạy thời gian thực trên webcam/laptop.
* Có khả năng phát hiện 3 hành vi gian lận chính:
    * Nhìn sang hướng khác quá lâu.
    * Sử dụng điện thoại/sách.
    * Xuất hiện nhiều khuôn mặt trong cùng khung hình.
* Độ chính xác mong đợi đạt ≥ 80%, tốc độ xử lý < 0.5 giây/khung hình.
* Hiển thị cảnh báo trực tiếp trong cửa sổ giám sát.
* Sau khi dùng xong, chỉ cần bấm dấu X để đóng cửa sổ giám sát, chương trình sẽ in ra thống kê về tỉ lệ số lần thí sinh quay sang chỗ khác, thời gian phát hiện có điện thoại, tỉ lệ thời gian phát hiện có người thứ ba, …

## 5. Hướng phát triển
* Mở rộng dữ liệu huấn luyện để cải thiện độ chính xác và bao phủ nhiều hành vi hơn.
* Tích hợp hệ thống vào các nền tảng thi trực tuyến (Zoom, Google Meet, LMS).
* Ứng dụng ngoài phòng thi: giám sát lớp học (mất tập trung), giám sát an ninh, phân tích hành vi khách hàng.
* Phát triển mô hình nhẹ hơn để có thể chạy trên thiết bị di động hoặc edge device (Jetson Nano, Raspberry Pi).

## 6. Hướng dẫn cài đặt

Đầu tiên tải các thư viện yêu cầu:
```
pip install -r requirements.txt
```
Tải file model YOLOv8:
```
python .\download_model.py
```

Sau đó chạy chương trình chính main.py.

Nếu bị lỗi, thử lui về phiên bản cũ hơn của torch:
```
pip uninstall torch torchvision torchaudio -y
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1
```