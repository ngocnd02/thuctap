## FTP Management

### Add FTP account
- Để tạo một tài khoản FTP: **aaPanel >> FTP >> Add FTP**

![Imgur](https://i.imgur.com/FlHlnk6.png)

Nếu không thể kết nối đến FTP của bạn, hãy tuân theo hướng dẫn dưới đây để khắc phục lỗi:

- Chú ý đến IP nội mạng và IP ngoại mạng

- Kiểm tra xem dịch vụ ftp đã được bật chưa (bạn có thể xem nó trên trang chủ của bảng điều khiển)

- Kiểm tra xem cổng ftp 20, cổng 21 và cổng chuyển động 39000-40000 có được mở không (aaPanel đã được mở mặc định). Nếu đó là một máy chủ như Google Cloud / AWS Cloud, bạn cần kiểm tra nhóm bảo mật

- Xem xét xem có thể kết nối không ở chế độ hoạt động / chế độ bị động

- Tạo một người dùng mới để xem liệu có thể kết nối không

- Thay đổi trình FTP để sử dụng flashfxp, đóng lệnh feat trong cài đặt và thử kết nối

- Thử phát hành lại các cổng 20, 21, 39000-40000

- Ta thử mở một phiên kết nối bằng Filezilla

![Imgur](https://i.imgur.com/CaGlb1x.png)

### Change FTP port

![Imgur](https://i.imgur.com/Iu7Teh0.png)

### Change FTP password

![Imgur](https://i.imgur.com/aAaBQfz.png)