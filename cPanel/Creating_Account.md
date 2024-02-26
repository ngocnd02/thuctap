## cPanel Users
cPanel được cài đặt trên hệ thống Linux bởi quản trị viên máy chủ. Với sự trợ giúp của Phần mềm máy chủ cPanel, một quản trị viên có thể tạo các máy chủ ảo riêng (Virtual Private Servers) hoặc có thể dành toàn bộ máy chủ cho môi trường shared hosting. Shared hosting của cPanel có ba loại cấp độ người dùng.

1. **Server Administrator:** Người dùng này là người dùng root của một máy chủ Linux cPanel và có tất cả các quyền trên máy chủ. Quản trị viên máy chủ có thể tạo, sửa đổi hoặc xóa bất kỳ tài khoản nào từ máy chủ cPanel. Quản trị viên máy chủ có quyền truy cập vào cPanel WHM (Web Host Manager), có thể hiểu đây là phần backend của cPanel.

2. **Reseller Accounts:** Người dùng này được tạo bởi quản trị viên máy chủ và quản trị viên máy chủ có thể chọn loại quyền nào sẽ được cấp cho tài khoản bán lại. Một tài khoản bán lại có thể tạo các tài khoản người dùng khác và có quyền truy cập vào tất cả các tài khoản đó mà họ đã tạo. Một tài khoản bán lại không có quyền truy cập vào các tài khoản người dùng được tạo bởi các tài khoản bán lại khác. Họ cũng có quyền truy cập vào WHM với các quyền hạn hạn chế.

3. **User Account:** Đây là các tài khoản người dùng thông thường, mỗi người dùng đăng ký dịch vụ lưu trữ web từ một công ty được cấp loại tài khoản này. Họ không có quyền truy cập vào Web Host Manager. Tài khoản người dùng có thể lưu trữ một hoặc nhiều trang web tùy thuộc vào kế hoạch mà họ đã mua từ nhà cung cấp dịch vụ lưu trữ web.

## Creating Account
- Trên WHM, trong navigate chọn **Account Funtions** > **Create a New Account**

![Imgur](https://i.imgur.com/L2bf4Sz.png)

- Điền đầy đủ các thông tin để tạo tài khoản

![Imgur](https://i.imgur.com/QH90vmR.png)

- Sau khi tạo thành công chọn **Create**, và sẽ hiển thị ra thông tin của tài khoản sau khi tạo thành công

![Imgur](https://i.imgur.com/4Et8UOB.png)


## Modifing Account

- Trong WHM, chọn **Account Funtions** > **Modify an Account**

![Imgur](https://i.imgur.com/rIx5lzO.png)

- Chọn một tài khoản mà bạn muốn sửa đổi, và sửa đổi thông tin mà bạn mong muốn

![Imgur](https://i.imgur.com/SBE5Ezk.png)

![Imgur](https://i.imgur.com/JQ97ynX.png)

Trong đó: 
	- Domain: Chỉ định tên miền chính của tài khoản.

	- Username: Tên người dùng của tài khoản cPanel.

	- Password: Mật khẩu cho tài khoản cPanel.


	- **Disk Space Quota (Giới hạn Dung lượng Đĩa):** Đặt giới hạn về dung lượng đĩa mà tài khoản có thể sử dụng.

	- **Monthly Bandwidth Limit (Giới hạn Băng thông hàng tháng):** Xác định lượng dữ liệu mà tài khoản có thể truyền tải qua mạng trong một tháng.

	- *Max FTP Accounts (Số tài khoản FTP tối đa):** Xác định số lượng tài khoản FTP mà tài khoản có thể sử dụng.

	- **Max Email Accounts (Số tài khoản Email tối đa):** Đặt giới hạn về số lượng tài khoản email có thể tạo ra.

	- **Max Mailing Lists (Số danh sách gửi tối đa):** Xác định số lượng danh sách gửi mà tài khoản có thể tạo.

	- **Max SQL Databases (Số cơ sở dữ liệu SQL tối đa):** Đặt giới hạn về số lượng cơ sở dữ liệu SQL mà tài khoản có thể tạo.

	- *Max Parked Domains (Số Domain Parked tối đa):** Xác định số lượng domain mà tài khoản có thể "park" (kết nối) với domain chính.

	- **Max Addon Domains (Số Domain Addon tối đa):** Đặt giới hạn về số lượng domain mà tài khoản có thể thêm vào.

	- **Max Passenger Applications (Số ứng dụng Passenger tối đa):** Xác định số lượng ứng dụng Passenger mà tài khoản có thể chạy.

Các giới hạn này giúp quản trị viên máy chủ kiểm soát và giới hạn việc sử dụng tài nguyên của mỗi tài khoản cPanel, đồng thời đảm bảo rằng máy chủ hoạt động một cách ổn định và hiệu quả.


## Terminate Account
- Để loại bỏ một tài khoản nào đó, ta chọn **Account Funtions** > **Terminate Accounts**

![Imgur](https://i.imgur.com/hOumOI3.png)

- Chọn tài khoản bạn muốn loại bỏ và ấn **Remove selected accounts**

![Imgur](https://i.imgur.com/zqQXxHH.png)

- Lưu ý: Nếu bạn xóa một tài khoản bạn không thể hoàn tác hành động này, nên backup đầy đủ cho các tài khoản trước khi xóa