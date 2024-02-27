## ModSecurity
- ModSecurity là một dự án mã nguồn mở cung cấp một tường lửa ứng dụng web (Web Application Firewall - WAF) cho các máy chủ web. Mục tiêu chính của ModSecurity là bảo vệ trang web khỏi các cuộc tấn công web bằng cách theo dõi và lọc lưu lượng HTTP.

- ModSecurity có thể được triển khai ở nhiều cấp độ, từ mức máy chủ tới ứng dụng, và nó kiểm soát các yêu cầu và phản hồi HTTP dựa trên các quy tắc mà bạn có thể cấu hình. Các quy tắc này giúp phát hiện và ngăn chặn nhanh chóng các hành động độc hại hoặc tấn công web như SQL injection, cross-site scripting (XSS), và các mô hình tấn công khác.

- ModSecurity thường được tích hợp với các máy chủ web phổ biến như Apache và Nginx, và nó cũng có thể được sử dụng trong môi trường cPanel để bảo vệ trang web trên nền tảng đó. Công cụ này đóng vai trò quan trọng trong việc tăng cường bảo mật cho các ứng dụng web và giảm nguy cơ bị tấn công từ phía người dùng xấu.

### Cài đặt ModeSecurity
- Để cài đặt ModeSecurity **WHM >> Home >> Security Center >> ModeSecurity Vendors**

![Imgur](https://i.imgur.com/tYhBjXq.png)

- Chọn **Install** để cài đặt

!https://i.imgur.com/X6OuSO4.png

- Sau khi cài đặt xong sẽ có thông báo. 

### ModeSecurity Tools
- Để cấu hình ta vào **WHM >> Home >> Security Center >> ModSecurity Tool**

![Imgur](https://i.imgur.com/eIbV2p2.png)

**Hits List**
- Sử dụng phần Danh Sách Hit trong giao diện để xem lịch sử sự kiện quy tắc trên máy chủ của bạn. Để chỉnh sửa hoặc vô hiệu hóa quy tắc ModSecurity tạo ra một hit, nhấp vào Rule ID.

- Chú Ý: Danh Sách Hit chỉ hiển thị hit quan trọng nhất cho từng yêu cầu cụ thể. Bạn cần kiểm tra các nhật ký để xem toàn bộ lịch sử sự kiện quy tắc. 

**Add a Rule**
Để thêm một quy tắc, thực hiện các bước sau:

1. Nhấp vào **Add Rules**. Một giao diện mới sẽ xuất hiện.

2. Nhập quy tắc vào ô văn bản Văn bản Quy tắc.

3. Để kích hoạt quy tắc khi triển khai cấu hình, chọn hộp kiểm Kích hoạt Quy tắc.

4. Để triển khai quy tắc và khởi động lại Apache ngay lập tức, chọn hộp kiểm Triển khai và Khởi động lại Apache.

5. Nhấp vào Lưu.

![Imgur](https://i.imgur.com/YH0HQ7Q.png)
