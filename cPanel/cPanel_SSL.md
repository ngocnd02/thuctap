## Installing SSL certificate

Chứng chỉ SSL (chứng chỉ Secure Sockets Layer) là một chứng chỉ số dạng số giúp xác thực danh tính của một trang web và mã hóa thông tin được gửi đến máy chủ bằng cách sử dụng các giao thức SSL/TLS (Secure Socket Layer/Transport Layer Security). Việc mã hóa này đảm bảo rằng dữ liệu trao đổi giữa trình duyệt web của người dùng và máy chủ trang web là riêng tư và an toàn.

Chứng chỉ SSL self-sign sẽ được tạo và ký bởi chính máy chủ của bạn thay vì một tổ chức chứng nhận (CA) bên ngoài. Các chứng chỉ tự ký không được chứng nhận bởi bất kỳ tổ chức nào nổi tiếng, do đó, chúng không tạo ra một môi trường tin tưởng như chứng chỉ được cấp bởi CA.

- Vì vậy để cài đặt SSL, ta cần gỡ self-sign. Truy cập vào trang quản lý user qua cổng 2083 và đăng nhập tài khoản với user mà bạn muốn cài đặt cho tên miền. 

- Tại **Home** >> **Security** >> **SSL/TLS**

![Imgur](https://i.imgur.com/jw6HSQo.png)

- Chọn **Manage SSL sites**

![Imgur](https://i.imgur.com/W2eq2sv.png)

- Chọn **Uninstall**

![Imgur](https://i.imgur.com/BxKJTPu.png)


- **Home** >> **Security** >> **SSL/TLS Status**

![Imgur](https://i.imgur.com/zIv18eF.png)

- Chọn những trang bạn muốn cài chứng chỉ SSL và chọn **Run AutoSSL**

![Imgur](https://i.imgur.com/jubxNLM.png)