# OpenLiteSpeed
## OpenLiteSpeed là gì?
- OpenLiteSpeed là một phiên bản mã nguồn mở miễn phí của máy chủ LiteSpeed ​​Web Server Enterprise. Cả hai phiên bản máy chủ website này đều do cùng một nhóm phát triển và duy trì, chúng có cùng một tiêu chuẩn mã hóa chất lượng cao.

- OpenLiteSpeed có dung lượng khá nhẹ, hiệu suất hoạt động cao, giúp người dùng load các trang web nhanh chóng. OpenLiteSpeed có hầu hết các tính năng có sẵn như bản doanh nghiệp LiteSpeed Enterprise bao gồm cả LSCache (một plugin quan trọng trong WordPress). Đồng thời có thể hiển thị liên kết tài khoản để hỗ trợ cộng đồng mã nguồn mở.

## Các tính năng nổi bật về hiệu suất (Performance Features)

- Là một phiên bản khác của LiteSpeed ​​Web Server Enterprise, OpenLiteSpeed được sử dụng miễn phí với mục đích cá nhân hoặc thương mại. Mặc dù nó không có đủ các tính năng như bản trả phí LiteSpeed Web Server Enterprise nhưng OpenLiteSpeed vẫn thể hiện các ưu điểm nổi bật về hiệu suất như sau.

### Giảm sử dụng băng thông
**Dữ liệu được nén bằng các công nghệ mới nhất:**
- Hỗ trợ Sendfile(): Có tác dụng đọc file dạng .html rồi gửi nội dung đến trình duyệt.

- Nén Gzip: Phương pháp nén giúp giảm dung lượng các file dữ liệu ở server để gửi đến client, cách làm này giúp tiết kiệm băng thông sử dụng, tăng tốc độ tải web.

- Nén Brotli cho các tệp tĩnh: Nén Brotli là cách nén dữ liệu có ưu điểm vượt trội hơn hẳn so với nén Gzip, giúp các file nhẹ hơn khi truyền tải, tiết kiệm tài nguyên băng thông, tăng tốc độ load dữ liệu web.

### Công nghệ siêu nhanh

OpenLiteSpeed có các tính năng mới với công nghệ hỗ trợ cực nhanh:
- Hỗ trợ tất cả các phiên bản SPDY/2, 3, 3.1 và HTTP/2.

- Yêu cầu liên kết.

- Hỗ trợ TCP_FASTOPEN.

- Đẩy máy chủ HTTP/2.

### Điểm nhấn quan trọng OpenLiteSpeed
So với máy chủ Apache, OpenLiteSpeed có các điểm nhấn đáng chú ý là:
- Nội dung tĩnh nhanh gấp 5 lần Apache.

- Tốc độ PHP nhanh hơn Apache gấp 3 lần.

- Tốc độ HTTPS nhanh gấp 4 lần Apache.

## OpenLiteSpeed hỗ trợ ứng dụng bên ngoài

Khi kết nối với các ứng dụng bên ngoài, OpenLiteSpeed thể hiện tính tương thích cao.

- Hỗ trợ nhiều ứng dụng bên ngoài khác như là Python, PHP, Java, Ruby, Perl.

- Tích hợp chế độ LSAPI trên máy chủ nhằm cải thiện hiệu quả server, tăng tốc độ PHP, Python, Ruby.

- Ủy quyền cho các ứng dụng ngoài thực hiện các quy trình riêng biệt, tăng hiệu quả hoạt động.

- Daemon CGI hiệu quả.

- Tương thích với các trình tăng tốc PHP được đưa ra từ bên thứ ba.

- Tăng hiệu quả truyền thông nhờ vào việc kiểm soát quy trình, giảm sử dụng tài nguyên server giúp tăng khả năng mở rộng các ứng dụng web.

## Tính năng bảo mật của OpenLiteSpeed
Máy chủ OpenLiteSpeed hỗ trợ bảo đảm an toàn, bảo mật hiệu quả với các cơ chế:

### Hỗ trợ SSL

Tính bảo mật được nâng cao khi server web hỗ trợ SSL.

- Hỗ trợ SSL tương thích với máy chủ Apache.

- Hỗ trợ SSL và tăng tốc cho phần cứng.

- Hỗ trợ các phiên bản của giao thức bảo mật TLS (Transport Layer Security) 1.0, 1.1, 1.2, 1.3.

- Chống các cuộc tấn công SSL BEAST và hỗ trợ khả năng tấn công lại.

- Hỗ trợ triển khai mã nguồn mở LibreSSL.

### Kiểm soát an ninh
OpenLiteSpeed tiến hành việc kiểm soát chặt chẽ các vấn đề an ninh, an toàn trong các hoạt động trên web.

- Điều chỉnh băng thông và các kết nối hợp lý.

- Kiểm soát các truy cập dựa trên địa chỉ IP.

- Tiến hành xác thực các yêu cầu HTTP nghiêm ngặt.

- Giới hạn người giới thiệu.

- Giới hạn tỷ lệ hồi đáp.

### Cảnh báo máy chủ

OpenLiteSpeed cũng đưa ra các cảnh báo đối với máy chủ để phát hiện và ngăn chặn các hiện tượng tràn bộ nhớ đệm.