## Database Management

### Add database

![Imgur](https://i.imgur.com/q5cHeTf.png)

Để tạo một cơ sở dữ liệu mới, đầu tiên nhập tên cơ sở dữ liệu, chọn định dạng mã hóa, nhập mật khẩu và đặt quyền truy cập để tạo thành công một cơ sở dữ liệu.

- TênDB: Tên của cơ sở dữ liệu mới, chọn định dạng mã hóa, mặc định là định dạng UTF-8.

- Mật khẩu: Mặc định là một mật khẩu ngẫu nhiên, bạn có thể tự thay đổi nó.

- Quyền truy cập: Quyền mặc định là quyền truy cập máy chủ cục bộ. Các tùy chọn bao gồm: Tất cả mọi người, chỉ định IP.

- Bắt buộc SSL: Bắt buộc người dùng sử dụng kết nối SSL, điều này có thể làm cho người dùng không có chứng chỉ không thể truy cập (chứng chỉ có thể được tải về trong mục quản lý MySQL trong phần SSL).

### Change root password
Chỉnh sửa mật khẩu root database

![Imgur](https://i.imgur.com/IT9YEQj.png)

- Nếu bạn không thể thêm dữ liệu hoặc nhận thông báo về mật khẩu sai, bạn có thể thử thay đổi mật khẩu root để giải quyết.

- Lưu ý: Mật khẩu mặc định là một mật khẩu ngẫu nhiên và root là mật khẩu cho tài khoản có đặc quyền cao nhất. Hãy thận trọng khi thực hiện thao tác này.


### Backup database
Manual backup

![Imgur](https://i.imgur.com/safHyc0.png)

![Imgur](https://i.imgur.com/HylMp14.png)

Automatic backup

![Imgur](https://i.imgur.com/aQdqEkK.png)

![Imgur](https://i.imgur.com/wdD5AGT.png)


### Permission management

![Imgur](https://i.imgur.com/IT9YEQj.png)

- Local server: Hạn chế cơ sở dữ liệu hiện tại và chỉ có thể truy cập trên máy chủ này.

- Anyone: Bất kỳ ai cũng có thể kết nối vào cơ sở dữ liệu từ xa.

- IP address: Chỉ cho phép truy cập từ địa chỉ IP cụ thể, chỉ hỗ trợ một địa chỉ IP.

- Nếu bạn cần kích hoạt quyền truy cập từ mạng ngoại vi, bạn vẫn cần mở cổng MySQL trong tường lửa (mặc định là 3306).

- Force SSL: Bắt buộc người dùng sử dụng kết nối SSL, điều này có thể làm cho người dùng không có chứng chỉ không thể truy cập (chứng chỉ có thể được tải về trong mục quản lý MySQL trong phần SSL).





