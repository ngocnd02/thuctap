## Cài đặt cPanel trên AlmaLinux

### Yêu cầu cài đặt
- Operating systems: Almalinux 8.9

- RAM: Minimum 1GB (recommend 2GB RAM)

- Disk Space: Minimum 20GB (recommended 40GB)

- License cPanel (Nếu bạn không có Lincense, bạn có thể đăng kí License Trial dùng thử cho 15 ngày, bạn có thể kích hoạt License dùng thử sau khi hoàn tất cài đặt)

### Cài đặt và bật/tắt một số dịch vụ cần thiết

- Trước khi bắt đầu cài đặt cPanel, bạn phải đảm bảo rằng Perl – Curl đã được cài đặt trên máy chủ của bạn. Nếu chưa cài thì cài đặt bằng 2 lệnh bên dưới:
```
yum install -y perl
yum install -y curl
```
Trong đó: 
	- **perl**: là một ngôn ngữ lập trình thông dịch, linh hoạt và mạnh mẽ. Nó được thiết kế để xử lý và phân tích văn bản một cách dễ dàng, điều này làm cho Perl trở thành một trong những công cụ ưa chuộng trong việc xử lý dữ liệu văn bản, thậm chí là xây dựng các ứng dụng web và các đoạn mã kịch bản hệ thống. Perl được sử dụng rộng rãi trong quản trị hệ thống, phát triển web, và nhiều lĩnh vực khác.

	- **curl**: là một công cụ dòng lệnh để truyền tải dữ liệu với các giao thức internet, chẳng hạn như HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, và nhiều giao thức khác. cURL cung cấp khả năng tương tác với các máy chủ từ dòng lệnh, giúp người dùng thực hiện các tác vụ như tải xuống và tải lên tệp tin, xử lý API web, và thực hiện các yêu cầu HTTP. Nó là một công cụ quan trọng trong quá trình phát triển web và là một phần của nhiều kịch bản tự động hóa và quản trị hệ thống.

**Disabled SELinux**
- Cài đặt cPanel có thể yêu cầu vô hiệu hóa SELinux vì cPanel thường sử dụng một số tính năng và cấu hình mà SELinux có thể xem xét là không an toàn hoặc có thể tạo ra các chặn không mong muốn trong quá trình hoạt động của nó.

- SELinux là một cơ chế kiểm soát truy cập dựa trên chính sách cho hệ điều hành Linux. Nó giúp ngăn chặn các hành động bất thường của các chương trình và quy trình hệ thống. Tuy nhiên, một số ứng dụng cụ thể, như cPanel, có thể không tương thích hoặc không thích ứng tốt với các biểu thức chính sách SELinux.

- Cho nên chúng ta nên tắt SELinux, câu lệnh: 

```
sed -i 's/SELINUX=/#SELINUX=/g' /etc/selinux/config
SELINUX=disabled >> /etc/selinux/config
```
**Disable Network Manager**
- Mặc định từ phiên bản 68 trở đi cPanel sẽ không hỗ trợ dịch vụ Network Manager nên bạn cần tắt dịch vụ này trước khi cài đặt bằng lệnh sau:

```
systemctl stop NetworkManager.service
systemctl disable NetworkManager.service
```

- Kế tiếp bạn có thể khởi động dịch vụ hệ thống

```
systemctl enable network.service
systemctl start network.service
```

**Update**
- Cập nhật dịch vụ lên phiên bản mới nhất, vá các lỗ hổng cũ và cập nhật tính năng mới.

```
yum -y update
```

### Cài đặt cPanel
- Để cài đặt cPanel thực hiện những dòng lệnh sau: 

```
cd /home
curl -o latest -L https://securedownloads.cpanel.net/latest
sh latest
```
Di chuyển đến thư mục chính
Tải file cài đặt phiên bản WHM và cPanel mới nhất từ trang chủ
Chạy lệnh cài đặt

- Nếu bạn muốn cài đặt nhanh và chỉ với 1 lệnh thì có thể sử dụng lệnh bên dưới, nó sẽ kết hợp và chạy cùng lúc với các lệnh trên.

```
cd /home && curl -o latest -L https://securedownloads.cpanel.net/latest && sh latest
```

### Thiết lập cPanel
- Sau khi cài đặt xong cPanel ta truy cập vào trình duyệt và truy cập vào máy chủ với cổng 2087 theo cú pháp: **https://diachiip:2087. 

- Trang chủ quản trị cPanel sẽ xuất hiện, lúc này bạn cần đăng nhập tài khoản của máy chủ để truy cập được cPanel

![Imgur](https://i.imgur.com/q9jSp6K.png)

- Chọn **Login to cPanel store**

![Imgur](https://i.imgur.com/Ex8Ku4K.png)

- Đăng nhập tài khoản email bạn đã đăng kí cho tài khoản trial

![Imgur](https://i.imgur.com/nmUVuj5.png)


![Imgur](https://i.imgur.com/WXoAVXn.png)


- Thiết lập cPanel

![Imgur](https://i.imgur.com/Qsy04aq.png)


![Imgur](https://i.imgur.com/XgJ7Ywb.png)


- Và cuối cùng đây là giao diện để quản lý trang web của cPanel

![Imgur](https://i.imgur.com/BTQBKls.png)

