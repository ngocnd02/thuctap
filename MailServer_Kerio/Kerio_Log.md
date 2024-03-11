## Kiểm tra log trong Kerio
- Log là các tệp trong đó Kerio Connect ghi lại thông tin về các sự kiện nhất định, ví dụ: báo cáo lỗi và cảnh báo cũng như thông tin gỡ lỗi. Mỗi mục đại diện cho một hàng bắt đầu bằng dấu thời gian (ngày và giờ diễn ra sự kiện).

- Trong giao diện quản trị chọn **Log**

### Cấu hình logs
- Các bản ghi có sẵn trong giao diện quản trị Kerio Connect trong mục Logs.

- Khi bạn nhấp chuột phải trong khu vực bản ghi, bạn có thể cấu hình các thiết lập sau đây (có sẵn trong tất cả các bản ghi):

#### Save log
- Bạn có thể lưu toàn bộ log hoặc chọn một phần trong định dạnh txt hoặc html.

![Imgur](https://i.imgur.com/dl0JDIc.png)

![Imgur](https://i.imgur.com/cmLwcmN.png)


- Sau đó mở bản ghi log đã tải xuống

![Imgur](https://i.imgur.com/YHelkVH.png)


#### Highlighting
- Bạn có thể làm nổi bật bất kỳ phần nào của văn bản trong bản ghi để tham chiếu tốt hơn. Xác định một chuỗi con hoặc biểu thức chính quy và tất cả các dòng chứa văn bản đó sẽ được làm nổi bật.

!


### Config log
- Config log lưu giữ toàn bộ lịch sử thay đổi cấu hình. Nó cho bạn biết người dùng nào đã thực hiện các nhiệm vụ quản trị cá nhân và khi nào.

![Imgur](https://i.imgur.com/VQJFuTs.png)

- Ví dụ log: **[11/Mar/2024 10:32:03] admin@nguyenducngoc.com - Update ConnectClientOptions {customLoginLogoEnabled="True", customLoginLogoFilename="loginlogo_2651b.png"}**
	- Thông báo sự thay đổi logo mà ta đã thực hiện vào lúc 10:32:03. 
	- Thay đổi bởi admin@nguyenducngoc.com


### Debug log
- Sử dụng để giám sát các loại thông tin nhất định, theo mặc định nó sẽ hiển thị các thông tin liên quan đến khởi động và dừng dịch vụ, giao thức trên Mail server Kerio Connect. Liệt kê các dịch vụ và port kết nối phục vụ cho quá trình vận hành của Mail server và các thông tin khác mô tả quá trình xử lý của mail server.

![Imgur](https://i.imgur.com/Jc3Me9N.png)

### Mail log
- Chứa thông tin về từng email được xứ lý. 

![Imgur](https://i.imgur.com/A1XAkxY.png)

**[11/Mar/2024 11:40:39] Recv: Queue-ID: 65ee8b47-00000009, Service: Kerio Connect Client, From: <ngocnd@nguyenducngoc.com>, To: <trang@nguyenducngoc.com>, Size: 985, Sender-Host: 0.0.0.0, User: ngocnd@nguyenducngoc.com, SSL: yes, Subject: Check log, Msg-Id: <735055329-3299@mail.nguyenducngoc.com>**

- Log này thông báo nhận thư thành công. Nó cho biết rằng một email đã được gửi từ địa chỉ email ngocnd@nguyenducngoc.com đến địa chỉ email trang@nguyenducngoc.com, thông qua dịch vụ Kerio Connect Client. 
- Email này có kích thước là 985 bytes, được gửi qua kết nối SSL, có chủ đề là "Check log"
- Email này dược gửi lúc 11:40:39


**[11/Mar/2024 11:40:40] Sent: Queue-ID: 65ee8b47-00000009, Recipient: <trang@nguyenducngoc.com>, Result: delivered, Status: 2.0.0 , Remote-Host: 127.0.0.1, Msg-Id: <735055329-3299@mail.nguyenducngoc.com>**

- Thông báo này xác nhận rằng email đã được gửi thành công từ Queue-ID có mã là 65ee8b47-00000009 đến địa chỉ email trang@nguyenducngoc.com. Trạng thái 2.0.0 cho biết rằng quá trình gửi đã thành công và được xác nhận.
- Ngày/Giờ: 11/Th3/2024 11:40:40
- Queue-ID: 65ee8b47-00000009
- Người nhận: trang@nguyenducngoc.com
- Kết quả: Gửi thành công
- Trạng thái: 2.0.0
- Remote-Host: 127.0.0.1
- Msg-Id: 735055329-3299@mail.nguyenducngoc.com


### Security log

- Security log  chứa thông tin liên quan đến bảo mật của Kerio Connect. Nó cũng chứa các bản ghi về tất cả các tin nhắn không được gửi.

![Imgur](https://i.imgur.com/85rNduH.png)


**HTTP/WebMail: Invalid password for user ngocnd@nguyenducngoc.com. Attempt from IP address 192.168.249.1.**
- Log này thông báo đăng nhập thất bại do nhập mật khẩu không đúng cho tài khoản ngocnd@nguyenducngoc.com

### Operations log
- Nhật ký hoạt động thu thập thông tin về các mục đã bị xóa và di chuyển (thư mục, tin nhắn, danh bạ, sự kiện, tác vụ và ghi chú) trong hộp thư của người dùng. Nó đặc biệt hữu ích nếu người dùng không thể tìm thấy một tin nhắn cụ thể trong hộp thư của họ.


![Imgur](https://i.imgur.com/wkdU0Ru.png)

**[11/Mar/2024 10:02:45] {MOVE} Protocol: HTTP/WebMail, User: trang@nguyenducngoc.com, IP: 192.168.249.1, Folder: ~trang@nguyenducngoc.com/Drafts, Destination Folder: ~trang@nguyenducngoc.com/Sent Items, From: "Trang Nguyen" <trang@nguyenducngoc.com>, Subject: "Checking signature", Msg-Id: <<729180286-3301@mail.nguyenducngoc.com>>, Delivered: 11/Mar/2024 10:02:45, Size: 1043**

Bản ghi log này có ý nghĩa như sau:

- Ngày/Giờ: 11/Th3/2024 10:02:45
- Hành động: {MOVE} (Di chuyển)
- Giao thức: HTTP/WebMail
- Người dùng: trang@nguyenducngoc.com
- Địa chỉ IP: 192.168.249.1
- Thư mục: ~trang@nguyenducngoc.com/Drafts (Nháp)
- Thư mục Đích: ~trang@nguyenducngoc.com/Sent Items (Mục đã gửi)
- Người gửi: "Trang Nguyen" trang@nguyenducngoc.com
- Chủ đề: "Checking signature"
- Msg-Id: <729180286-3301@mail.nguyenducngoc.com> (ID của thông điệp)
- Đã gửi thành công: 11/Th3/2024 10:02:45
- Kích thước: 1043 bytes

- Bản ghi này cho biết rằng có một hoạt động di chuyển thư được thực hiện bởi người dùng trang@nguyenducngoc.com thông qua giao thức HTTP/WebMail. Thư đã được di chuyển từ thư mục Nháp đến thư mục Mục đã gửi. Thông tin chi tiết về thư bao gồm người gửi, chủ đề, ID của thông điệp, ngày gửi thành công, và kích thước của thư.

### Error log
- Nhật ký lỗi hiển thị các lỗi có tầm quan trọng lớn thường ảnh hưởng đến hoạt động của máy chủ thư (ngược lại với Nhật ký cảnh báo).

- Các thông báo lỗi điển hình được hiển thị trong quá trình khởi tạo dịch vụ liên quan đến nhật ký lỗi (thường là do xung đột cổng), phân bổ dung lượng ổ đĩa, khởi tạo kiểm tra phần mềm chống vi-rút, xác thực người dùng không đúng cách, v.v.

![Imgur](https://i.imgur.com/aBosTQ8.png)


### Spam log
Nhật ký thư rác hiển thị thông tin về tất cả các email thư rác được lưu trữ (hoặc bị đánh dấu) trong Kerio Connect.

### Warning log
- Nhật ký cảnh báo hiển thị các thông báo cảnh báo về các lỗi ít nghiêm trọng. Các sự kiện hiển thị thông báo cảnh báo trong nhật ký này không ảnh hưởng nhiều đến hoạt động của Kerio Connect. Tuy nhiên, chúng có thể chỉ ra một số vấn đề nhất định (hoặc có thể xảy ra).

- Ví dụ: Nhật ký cảnh báo có thể hữu ích nếu người dùng phàn nàn rằng một số dịch vụ nhất định không hoạt động.

![Imgur](https://i.imgur.com/AGjoD8M.png)

### Audit log
Bảng ghi Kiểm tra hiển thị thông tin về tất cả các nỗ lực xác thực thành công đối với các tài khoản Kerio Connect, bao gồm quản trị Kerio Connect, Client Kerio Connect, Microsoft Outlook với KOFF, v.v.


