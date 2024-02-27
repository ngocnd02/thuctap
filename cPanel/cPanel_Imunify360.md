##  Imunify360
### Imunify360 là gì?
- Imunify360 là một giải pháp bảo mật toàn diện, có nhiều lớp và khả năng giám sát đầy đủ cho các máy chủ chạy hệ điều hành Linux. Nó phát hiện và ngăn chặn hầu hết các cuộc tấn công web phổ biến nhắm vào các máy chủ lưu trữ chia sẻ, trang web chạy hệ thống quản lý nội dung (CMS) như WordPress hoặc Joomla, và các ứng dụng web khác.

- Với Imunify360, các quản trị viên máy chủ có thể tự động ngừng các cuộc tấn công Brute Force, tải lên mã độc hại, chèn mã độc hại và nhiều cuộc tấn công khác có thể ảnh hưởng đến trang web của khách hàng và chính máy chủ.

- Hầu hết các máy chủ lưu trữ bao gồm một bảng điều khiển cho chủ sở hữu trang web, và Imunify360 tích hợp với các ứng dụng phổ biến như cPanel, Plesk và DirectAdmin. Nó cho phép chủ sở hữu trang web và quản trị viên máy chủ giám sát hoạt động độc hại và xác định các mối đe dọa tiềm ẩn. Imunify360 sẽ tự động làm sạch các chèn mã độc hại, giúp quản trị viên máy chủ tiết kiệm thời gian chiến đấu với mã độc hại.

### Cài đặt Imunify360 trên cPanel
- Để cài đặt Imunify360 trước tiên ta vào trang chủ của nó và đăng kí một bản dùng thử. 
- Email về thông tin cài đặt sẽ được gửi về email của bạn

![Imgur](https://i.imgur.com/Yv9vhwq.png)

- Bạn cần click vào link trong email để kích hoạt tài khoản dùng thử

![Imgur](https://i.imgur.com/xUuOGlw.png)


- Tiếp theo chúng ta ssh vào server của ta và bắt đầu cài đặt imunify360 theo dòng lệnh dưới đây

```
wget https://repo.imunify360.cloudlinux.com/defence360/i360deploy.sh

bash i360deploy.sh --key IMUNPCptMfMSU2WPJO9
```

- Sau khi cài đặt xong sẽ có thông báo

![Imgur](https://i.imgur.com/nXGG9rz.png)

- Sau đó ta ta tiến hành vào cpanel để cài đặt imunify360 lên cPanel
- Tại **WHM >> Home >> Plugins >> Imunify360**

![Imgur](https://i.imgur.com/lRY3Zi6.png)

- Click **Accept**

![Imgur](https://i.imgur.com/MYHWFAV.png)

- Điền địa chỉ email mà bạn vừa đăng ký trail để kích hoạt 

![Imgur](https://i.imgur.com/KtMKrjp.png)

- Và đây là giao diện của imunify360 sau khi được cài đặt trên cPanel

![Imgur](https://i.imgur.com/IQFyN0U.png)
