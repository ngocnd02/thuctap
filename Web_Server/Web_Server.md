# Web server
## Web server là gì?
- Web server được biết đến là máy chủ web được dùng để xử lý các request từ trình duyệt web máy khách và gửi thông tin đến client thông qua giao thức HTTP hoặc những giao thức khác. Có nhiều webserver phổ biến thường được sử dụng hiện nay như: Apache, Nginx, IIS...

- Những chương trình trên web server được cài đặt nhằm phục vụ ứng dụng web. Khi được tiếp nhận các request từ trình duyệt, webserver ngay lập tức sẽ gửi phản hồi đến client thông qua giao thức HTTP hoặc những giao thức khác. 

- Để làm được điều này, mỗi máy chủ web server phải là một kho có dung lượng rất lớn và có thể tải ở tốc độ rất cao để có thể lưu trữ và vận hành tốt mọi kho dữ liệu trên Internet. Thông qua các cổng giao tiếp riêng biệt, cấu hình máy chủ web được thiết lập giúp điều hành hiệu quả cho cả một hệ thống máy tính hoạt động trên Internet. 

- Xây dựng máy chủ web server phải đảm bảo được quy trình hoạt động khắc nghiệt, liên tục và không ngừng nghỉ để duy trì cung cấp dữ liệu thường xuyên cho mạng lưới máy tính. Tóm lại, đây sẽ là nơi chứa toàn bộ dữ liệu hoạt động trên internet mà nó được giao quyền quản lý. 

![Imgur](https://i.imgur.com/I5GJCNj.png)

## Chức năng của web server là gì?
Xử lý dữ liệu qua giao thức HTTP
- Xử lý và cung cấp thông tin cho khách hàng thông qua các máy tính cá nhân trên Internet qua giao thức HTTP.
- Nội dung được chia sẻ từ máy chủ web là những nội dung định dạng HTML, các thẻ style sheets, hình ảnh, những đoạn mã script hỗ trợ nội dung văn bản,.... 
- Bạn có thể hiểu đơn giản là ví dụ khi bạn truy cập vào nhanhoa.com, máy chủ sẽ cung cấp đến cho bạn tất cả dữ liệu về trang web đó thông qua lệnh giao tiếp.

Kết nối linh hoạt 
- Máy tính nào cũng có thể là một máy chủ nếu nó được cài đặt một chương trình phần mềm server và có kết nối Internet.

Chương trình chuyển đổi thông minh
- Phần mềm Web Server cũng giống như các phần mềm khác, nó cho phép người dùng cài đặt và hoạt động trên bất kỳ máy tính nào đáp ứng đủ yêu cầu về bộ nhớ.

Lưu trữ dữ liệu trên hình thức thuê các máy chủ nhỏ, máy chủ áo VPS hoặc hosting
- Vì thế khi thiết kế Website xong, cần thực hiện đăng tải website lên Web Server để giúp khách hàng có thể truy cập web ở nhiều nơi trên thế giới và hiểu được nội dung bên trong.

## Các bước lấy dữ liệu của một Website
**Bước 1: Web Server lưu trữ các file của Website - Hosting file**
Web Server lưu trữ các file của website (bao gồm các tài liệu HTML, ảnh file CSS, fonts, video, file JavaScript). Người dùng hoàn toàn có thể lưu trữ chúng trên máy tính của mình nhưng khi lưu trên máy chủ web sẽ có những lợi ích sau:

+ Luôn sẵn sàng - up and running

+ Luôn kết nối tới mạng internet

+ Địa chỉ IP cố định

+ Được bảo dưỡng và bảo vệ bởi nhà cung cấp.

**Bước 2: Giao tiếp qua HTTP**
Web Server sẽ hỗ trợ giao thức truyền phát siêu văn bản - HTTP. HTTP là tập hợp các quy tắc kết nối giữa hai máy tính bao gồm Textual và Stateless.

+ Textual: Mọi lệnh đều là văn bản thuần túy và người dùng có thể đọc được nó.

+ Stateless: Khi cả người dùng và máy chủ không nhớ kết nối trước đó.

HTTP có quy tắc rõ ràng về giao tiếp giữa client và server như sau:

+ Duy nhất client có thể tạo ra yêu cầu HTTP đến server. Các server chỉ có thể đáp trả yêu cầu HTTP của client.

+ Client phải cung cấp URL của file khi yêu cầu file đó thông qua HTTP.

+ Tất cả yêu cầu HTTP sẽ được Web Server trả lời.

HTTP có trách nhiệm xử lý và trả lời các yêu cầu đến qua các bước:

+ Khi nhận được một yêu cầu, HTTP sẽ kiểm tra URL được yêu cầu có khớp với file hiện có không.

+ Nếu trùng khớp, máy chủ web sẽ gửi nội dung file trả lại trình duyệt. Trường hợp không trùng khớp, một Application server sẽ tạo ra file được yêu cầu.

+ Web Server sẽ gửi trả lại một thông điệp lỗi cho trình duyệt (phổ biến nhất là 404 Not Found) nếu nó không thể xử lý được.

## Giới thiệu 1 số Web Server phổ biến
**Apache HTTP Server**
- Apache là Web Server được sử dụng rộng rãi nhất thế giới. Apache được phát triển và duy trì bởi một cộng đồng mã nguồn mở dưới sự bảo trợ của Apache Software Foundation. Apache được phát hành với giấy phép Apache License là được sử dụng tự do, miễn phí.
- Tính đến tháng 8 năm 2018, Apache ước tính phục vụ cho 54.2% các trang web đang hoạt động và 53.3% số máy chủ hàng đầu. Apache chạy trên các hệ điều hành như windows, linux, unix, MacOS ….

**Nginx**
- Nginx là một Web Server nhẹ (Đọc thêm Nginx là gì), không chiếm nhiều tài nguyên của hệ thống. Nginx còn là một reverse proxy mã nguồn mở. Nginx khá là ổn định, cấu hình đơn giản và hiệu suất cao.
- Nginx được phát triển bởi Igor Sysoev vào năm 2002 chủ yếu là để phục vụ cho website rambler.ru (trang web được truy cập nhiều thứ hai của nước Nga). Theo thống kê của Netcaft, trong một triệu website lớn nhất thế giới có 6.52% sử dụng Nginx.
- Nginx là phần mềm mã nguồn mở và miễn phí, được phát hành rộng rãi theo giấy phép BSD. Nginx được phát triển bằng ngôn ngữ  và chạy được trên các hệ điều hành như Linux, FreeBSD, Windows, MacOS…
- Nginx có các tính năng như chứng thực người dùng, virtual hosting, hỗ trợ CGI, FCGI, SCGI, WCGI, SSI, ISAPI, HTTPS, Ipv6, …

**Internet Information Services (IIS)**
- IIS do Microsoft phát triển, sản phẩm này được tích hợp cùng với hệ điều hành Windows Server. Trong IIS bao gồm nhiều dịch vụ như: dịch vụ Web Server, dịch vụ FTP Server. Tính đến thời điểm tháng 5 năm 2015 thì thì số lượng trang Web sử dụng máy chủ IIS gần 248 triệu trang web.
- Tất cả các tính năng của Web Server được quản lý độc lập do đó chúng ta có thể dễ dàng thêm, loại bỏ hoặc thay thế các tính năng của Web Server.
- Nhờ được tích hợp ASP.NET IIS có thể sử dụng toàn bộ sức mạnh của ASP.NET. Module ASP.NET làm cho máy chủ phát triển nhanh chóng nhờ vào giao diện quen thuộc và các dịch vụ ứng dụng của ASP.NET.

**Apache Tomcat**
- Apache Tomcat là một Java Servlet được phát triển bởi Apache Software Foundation. Tomcat thực thi các ứng dụng Java Servlet và JavaServer Pages (JSP). Tomcat cung cấp một máy chủ HTTP cho ngôn ngữ Java thuần túy.
- Apache Tomcat rất ổn định và có tất cả các tính năng của một ứng dụng web thương mại nhưng đi kèm theo giấy phép mã nguồn mở của Apache. Tomcat cũng cung cấp một số chức năng bổ sung như tomcat manager application, specialized realm implementation và tomcat valves.
- Các phiên bản của apache tomcat trùng với phiên bản và đặc điểm kỹ thuật của servlet java hoặc java servlet API. Tomcat 5.5X hỗ trợ Servlet API 2.3, tomcat 6.0X hỗ trợ servlet API 2.4 và tomcat 7.0 hỗ trợ servlet API 3.0. Ngoài Servlet versions API, phiên bản tomcat hỗ trợ phiên bản JSP API tương ứng.
- Apache Tomcat hỗ trợ các hệ điều hành như windows, linux, MacOS, BSD,…

**Lighttpd**
- Lighttpd là một phần mềm mã nguồn mở, an toàn và linh hoạt, đặc biệt miễn phí và được phân phối theo giấy phép BSD. Lighttpd được viết bởi Jan Kneschke.
- Lighttpd chiếm ít tài nguyên, memory thấp, CPU nhỏ. Lighttpd được phát triển bằng ngôn ngữ C. chạy trên hệ điều hành Linux, Windows, Mac OS,…