## Reseller Package
**Reseller Package** là tập hợp các thông số kỹ thuật được thiết lập sẵn để phân chia tài nguyên mà một người dùng (User) có thể sử dụng. Trên gói Reseller, bạn cần thiết lập ít nhất một Package để có thể cấu hình cho các User được tạo ra. Một Package có thể sử dụng cho nhiều User khác nhau. Đây là cách để quản lý và phân chia tài nguyên cho các tài khoản hosting một cách hiệu quả

- Trong menu chính ta chọn **Manager Reseller Packages** để liệt kê ra các Reseller Packages đã có.

![Imgur](https://i.imgur.com/djk2fW7.png)

- Nếu tài khoản Admin của bạn mới được tạo, bạn sẽ thấy rằng chưa có bất kỳ Gói Reseller nào được tạo. Quan trọng là phải tạo ít nhất một gói ngay bây giờ vì các tài khoản Reseller cần được gán một gói. Nhấp vào liên kết "Add package" ở đầu trang màn hình.

![Imgur](https://i.imgur.com/gaS4XFl.png)

- Sau khi điền các thông số, sau đó nhập tên package của bạn và ấn save. 

![Imgur](https://i.imgur.com/LSEiafF.png)

## Feature Explained

### Bandwidth
- **Băng thông** (Bandwidth) được định nghĩa là tổng lưu lượng dữ liệu của tất cả Người dùng của Reseller cộng với trang web của Reseller. Băng thông được đo bằng đơn vị megabyte, vì vậy 5000 megabyte tương đương khoảng 5 gigabyte truyền tải. Khi một Reseller vượt quá băng thông của mình, trang web của họ sẽ bị tạm ngưng cho đến ngày đầu tiên của tháng tiếp theo

### Disk Space
- Đây là tổng không gian lưu trữ cho tài khoản, tính bằng megabyte. Không gian đĩa được chia sẻ giữa một Reseller và tất cả các Người dùng của họ. Khi Reseller đạt đến giới hạn không gian đĩa, họ sẽ không được phép tải lên thêm tệp cho đến khi có tệp khác được xóa đi.

### Vitual Domains
- Đây là số lượng domain thực tế mà một Reseller được phép chứa. Làm Admin, bạn có thể thiết lập tính năng này thành "Không giới hạn" và để Reseller làm việc trong giới hạn không gian đĩa và băng thông của họ. Lưu ý rằng số lượng domain ảo không bằng số lượng Người dùng, vì Người dùng có thể có nhiều domain trên một tài khoản.

### Subdomains
- Đây là tổng số lượng subdomain mà một Reseller được phép chứa. Lưu ý rằng một Người dùng có thể có nhiều subdomain, vì vậy tốt nhất là đặt giá trị này là một số lớn hoặc là "Không giới hạn."

### IPs 
- Đây là tổng số địa chỉ IP được cấp phát cho một Reseller. Mọi tính năng khác (ví dụ: nameservers cá nhân và một địa chỉ IP tĩnh/dành riêng cho trang web của Reseller) đều phụ thuộc vào số lượng địa chỉ trong trường này.

- Ví dụ, nếu bạn cuộn xuống bảng gói dịch vụ, bạn sẽ thấy cài đặt "Personal DNS's". Nếu bạn chọn tùy chọn "Sử dụng 3 IP, domain có IP riêng," Reseller sẽ nhận được một địa chỉ IP tĩnh cho trang web của họ và hai địa chỉ IP bổ sung cho nameservers. Tuy nhiên, tính năng này sẽ không hoạt động nếu số lượng địa chỉ IP trong trường "IPs" ít hơn ba (3).

- Tất nhiên, bạn có thể cấp phát nhiều địa chỉ IP hơn cần thiết cho một Reseller để Reseller có thể cung cấp địa chỉ IP tĩnh/dành riêng cho khách hàng của họ.

### Email Accounts

- Đây là số lượng tài khoản email POP3 mà một Reseller được phép cung cấp.

### E-Mail Forwarders

- Đây là số lượng địa chỉ chuyển tiếp email mà một Reseller được phép cung cấp.

### Mailing Lists

- Đây là số lượng danh sách gửi thư Majordomo mà một Reseller được phép cung cấp.

### Autoresponders

- Đây là số lượng tài khoản hồi đáp tự động mà một Reseller được phép cung cấp.

### MySQL Database

- Đây là số lượng cơ sở dữ liệu MySQL mà một Reseller được phép cung cấp. Các cơ sở dữ liệu MySQL đóng góp vào tổng lượng sử dụng không gian đĩa.

### Domain Pointers

- Đây là số lượng domain pointer mà một Reseller được phép cung cấp.

### Tài khoản FTP

- Đây là số lượng tài khoản FTP mà một Reseller được phép cung cấp. Ngay cả nếu bạn đặt số này là 0, mỗi Người dùng vẫn sẽ có một tài khoản FTP mặc định với quyền truy cập đầy đủ vào trang web của họ.

### Anonymous FTP Accounts

- Điều này cho phép Người dùng (bao gồm cả Resellers) cho phép đăng nhập ẩn danh vào site FTP của họ. Người dùng có khả năng tắt chức năng tải lên ẩn danh nhưng vẫn cho phép tải xuống ẩn danh. FTP ẩn danh có thể tạo ra rủi ro cho site của Người dùng, và nhiều Admin chọn không bật chức năng truy cập FTP ẩn danh.

### CGI Accesss

Chức năng này cho phép Người dùng chạy các tập lệnh CGI. Nếu tính năng này được bật, một thư mục /cgi-bin sẽ được tạo trong thư mục public_html của Người dùng.

### SSL Accesss

- Chức năng này cho phép Resellers cho phép Người dùng cài đặt chứng chỉ Secure Socket Layer (SSL) trên site của họ. Lưu ý rằng cần có địa chỉ IP tĩnh (dành riêng) để SSL hoạt động. Nếu bạn đang cung cấp hosting dựa trên tên, bạn có thể tắt chức năng SSL.

### SSH Accesss

- Chức năng này cho phép Resellers truy cập máy chủ qua SSH (một biến thể được mã hóa của Telnet).

### SSH Access for Users

- Chức năng này cho phép Người dùng được tạo bởi Resellers truy cập máy chủ qua SSH (một biến thể được mã hóa của Telnet). Nhiều Resellers và Admin tắt chức năng này vì có khả năng lạm dụng (Người dùng có quyền truy cập đầy đủ vào nội dung máy chủ). Bật chức năng này có nghĩa là Resellers có khả năng cung cấp truy cập SSH cho Người dùng của họ.

### DNS Control

- Chức năng này cho phép Người dùng thay đổi các bản ghi DNS của họ (ví dụ: bản ghi A, bản ghi MX, v.v.). Nhiều Resellers/Admins tắt chức năng này vì Người dùng có thể vô tình tắt toàn bộ site bằng cách xóa hoặc sửa đổi bản ghi domain.

### Personal DNS's

- Tính năng này tạo ra các máy chủ tên cá nhân cho Reseller (ví dụ: ns1.resellers-domain.com và ns2.resellers-domain.com). Có ba lựa chọn:

1. Không. Không tạo máy chủ tên cá nhân cho Reseller.

2. 2 địa chỉ IP (ns1/web site và ns2).

3. 3 địa chỉ IP (web site, ns1, ns2).

Quan trọng: Vui lòng đảm bảo số lượng địa chỉ IP phù hợp đã được đặt trong trường "IPs" (ở trên).

### Share server IP

- Tính năng này cho phép Reseller tạo các trang web dựa trên tên bằng cách sử dụng địa chỉ IP chính của máy chủ.

## Editing/Deleting Packages
- Tại menu chính Reseller Packages là danh sách tất cả các gói đã tạo.

![Imgur](https://i.imgur.com/fj1fHLf.png)

- Để xóa một hoặc nhiều gói, đặt dấu chọn bên cạnh tên gói và nhấp vào nút "Delete Selected".

**Lưu ý**:

- Việc xóa một gói sẽ không ảnh hưởng đến các Reseller có tài khoản liên kết với gói đó. Tài khoản của họ sẽ không thay đổi (với các giới hạn giống như trước). Tuy nhiên, tên gói sẽ không còn xuất hiện trong màn hình thông tin tài khoản của họ nữa.

- Để chỉnh sửa một gói, nhấp vào tên gói (cột đầu tiên của bảng). Khi bạn hoàn thành, nhấp vào nút "Save".

