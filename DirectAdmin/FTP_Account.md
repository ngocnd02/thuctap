## Creating FTP Accounts
Để tạo tài khoản FTP, đầu tiên nhấp vào biểu tượng "FTP Menu" trên màn hình chính của bảng điều khiển. Bạn sẽ thấy một danh sách các tài khoản FTP hiện tại giống như sau:

![Imgur](https://i.imgur.com/bigcWcm.png)

#### Default FTP Account

Tài khoản FTP mặc định và tài khoản bảng điều khiển có cùng tên đăng nhập và mật khẩu. Bạn không thể xóa tài khoản FTP mặc định, nhưng bạn có thể tạo mật khẩu khác cho nó so với mật khẩu bảng điều khiển của bạn.

Quan trọng:

Nếu bạn thay đổi mật khẩu bảng điều khiển của mình, mật khẩu tài khoản FTP mặc định vẫn giữ nguyên mật khẩu cũ của bảng điều khiển. Bạn phải cập nhật tài khoản FTP mặc định trong menu FTP nếu bạn muốn cả hai mật khẩu khớp nhau.

### Creating A New Account
- Chọn **Create FTP Account**

![Imgur](https://i.imgur.com/xGxLDRY.png)

- Trước tiên chọn tên cho tài khoản FTP, sau đó nhập password. Sau đó chọn level truy cập cho tài khoản FTP

	- **Domain**: Người dùng FTP này có quyền truy cập vào các thư mục public_html, private_html, mail, domains và backup.

	- **FTP**: Người dùng FTP này chỉ có quyền truy cập vào thư mục public_ftp.

	- **User**: Người dùng FTP này chỉ có quyền truy cập vào thư mục public_html/username/. Nếu chúng ta chọn tùy chọn này trong hình ảnh ở trên, người dùng FTP sẽ chỉ có quyền truy cập vào public_html/share/ hoặc https://www.sale.com/share/. (Nếu có một subdomain có tên là share.sale.com, người dùng FTP này cũng sẽ có quyền truy cập vào nó. Nếu thư mục chưa tồn tại, nó sẽ được tạo tại giai đoạn này.

- Cuối cùng, nhấp vào nút "Create".

![Imgur](https://i.imgur.com/MzddiKY.png)


### Sử dụng FileZilla để kết nối đến FTP Server
- Nhập địa chỉ ip máy chủ và thông tin tài khoản mà tạo ở phía trên để kết nối vào FTP server

![Imgur](https://i.imgur.com/K26qsxj.png)
