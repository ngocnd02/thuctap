# CÀI ĐẶT WEB SERVER THỰC TẾ TRÊN WINDOWS SERVER

## I.Giới thiệu về dịch vụ Web
### 1.Dịch vụ Web là: Dịch vụ web (web service) là một loại dịch vụ cung cấp chức năng hoặc tương tác qua mạng internet. Các dịch vụ web sử dụng các giao thức tiêu chuẩn để truyền thông thông tin và tương tác với các ứng dụng khác trên mạng. 

- Dịch vụ Web dùng 2 giao thức để gửi dữ liệu tới người dùng đó là HTTP (không bảo mật) và HTTPS (có bảo mật).

- Để dịch vụ Web hoạt động được nó phải có 2 thành phần: Web Server và Web Client

- Web Server là nơi cung cấp dữ liệu Web. Người ta xây dựng lên một Website tĩnh hoặc động để người dùng truy cập vào. Web Server sẽ chạy ở Port 80 hoặc 443. Các phần mềm cài đặt trên Web Server như: Apache, PHP, Mariadb, PHPMyadmin, Code Web

- Web Client là phía người dùng. Người dùng mở IE hoặc Firefox truy cập vào tên miền của trang Web.

### 2.Cơ chế hoạt động

- Bước 1: Người dùng truy cập tên miền Website bằng Web Client là IE hoặc Firefox. Web Client sẽ sinh ra một Port cao và dữ liệu từ tầng Application sẽ chuyển xuống tầng Transport.

- Bước 2:. Đồng thời Web Client sẽ nhờ DNS Client phân giải hộ tên miền ra địa chỉ IP Web Server.

- Bước 3: Transport thấy dữ liệu là Web nó sẽ sử dụng giao thức TCP đóng Port nguồn là Port cao và Port đích là Port Web Server. Port Web Server là 80 (http) hoặc 443 (https). Sau đó sẽ truyền xuống tầng Internet.

- Bước 4: Dữ liệu sẽ được tầng Internet đóng IP máy mình và IP máy Web Server (IP Web Server được DNS Client nhờ DNS Server phân giải hộ).

- Bước 5: Sau khi dữ liệu đóng IP sẽ đưa xuống tầng Network Access. Tầng này sẽ dùng giao thức MAC kết hợp với các giao thức khác để truyền gói tin tới Swicht, tới Router và tới Máy chủ Web Server.

- Bước 6: Sau khi dữ liệu tới được Web Server nó sẽ được chuyển lên tầng Internet để kiểm tra IP, nếu đúng sẽ chuyển lên tầng Transport và chuyển lên tầng Application theo Port 80 hoặc 443.

- Bước 7: Webserver sẽ xử lý yêu cầu và Sau đó dữ liệu được đóng lại và gửi xuống đường truyền. Gói tin sẽ truyền lại tới máy Web Client

- Bước 8: Khi Client nhận được nó sẽ được Transport chuyển lên IE hoặc Firefox đúng vào Port cao khi khởi tạo (do có Port cao này nên ta có thể mở nhiều cửa sổ trên một trình duyệt với nhiều Website khác nhau mà không sợ bị trùng).

## Triển khai
### 1.Yêu cầu chuẩn bị

- Một máy chủ cài đặt Hệ điều hành Windows Server 2012

- Một máy tính cài Windows 10, ping thông tới máy chủ 

### 2.Nội dung công việc cần thực hiện

- Cài đặt dịch vụ IIS

- Cài đặt cơ sở dữ liệu SQL Server

- Cấu hình cơ sở dữ liệu cho Website

- Cấu hình file config

- Add Website lên hệ thống



