# TỔNG QUAN VỀ DIRECT ADMIN

## Direct Admin là gì?
- DirectAdmin (AD) là bảng điều khiển lưu trữ web cho phép bạn quản lý nhiều khía cạnh khác nhau của trang web của mình. Nó được xây dựng trên công nghệ ngăn xếp LAMP vững chắc. Với DirectAdmin, bạn có thể xử lý tài khoản người dùng, cơ sở dữ liệu, tài khoản email, tên miền, bản ghi DNS, bảo mật, v.v. Đó là bảng điều khiển hiệu quả yêu cầu tài nguyên hệ thống tối thiểu, lý tưởng cho nhiều tình huống lưu trữ khác nhau, từ các đơn vị VPS cấp thấp đến các máy chủ chuyên dụng có tải trọng lớn

- DirectAdmin hướng đến sự đơn giản, tiện dụng, tốc độ và sự ổn định. Nhưng vẫn có đầy đủ các tính năng cần thiết cho một quản trị hosting server. Đặc biệt khi sử dụng DirectAdmin, các nhiệm vụ đều sẽ được tự động hoá. Việc quản trị máy chủ và chia sẻ trang web sẽ được thực hiện một cách dễ dàng hơn.

- Tương tự như cPanel, DirectAdmin có thể chạy rất tốt trong Linux và các bản phân phối chính của nó - CloudLinux, CentOS, Ubuntu, Debian, Red Hat,... và không hỗ trợ Windows

## Cấu hình tối thiểu để sử dụng DirectAdmin
- Bộ xử lý 1 Core: 1GHz
- Bộ nhớ: 1 GB 
- Không gian ổ cứng: tối thiểu 2 GB không gian miễn phí (sau khi cài đặt Linux)
- Cấu hình tối thiểu này vẫn có thể chạy được DA, tuy nhiên lượng tài nguyên dành cho website sẽ không còn nhiều. Dễ gây tình trạng chậm, quá tải khi lượng traffic nhiều.
- Cấu hình đề xuất: VPS có từ 2 CPU, Ram từ 2GB và ổ cứng lưu trữ từ 15GB trở lên để sử dụng DirectAdmin được mượt mà nhất.

## Ưu và nhược điểm của DirectAdmin

### Ưu điểm

**Phương thức sử dụng đơn giản**
- Giao diện sử dụng của DirectAdmin mặc dù tương đối đơn giản nhưng vẫn đầy đủ những tính năng cần thiết. Phần mềm này đươc phân cấp thành 3 loại tài khoản, thứ tự từ cấp quyền cao đến thấp là Administrator, Reseller, và User. Đặc biệt hơn cả, chỉ trong một lần đăng nhập với phần mềm này, người dùng có thể dễ dàng chuyển đổi giữa 3 loại tài khoản một cách dễ dàng.

**Tốc độ xử lý cực nhanh, ít tiêu tốn ít tài nguyên**
- Ưu điểm của DirectAdmin là tốc độ xử lý cực kỳ nhanh chóng và khả năng thích ứng cao. Bên cạnh đó, giao diện của phần mềm này cũng được thiết kế theo hướng tối giản, dễ sử dụng và ít tiêu tốn tài nguyên hệ thống.

**Ổn định**
- Đặc biệt, tính ổn định của DirectAdmin rất cao. Nó có thể hoạt động trong thời gian dài mà không mắc phải lỗi hệ thống như các phần mềm quản trị hosting khác. Thêm vào đó, DirectAdmin còn có khả năng tự phục hồi trong trường hợp xảy ra lỗi bằng cách khởi động lại hệ thống.

**Giá bản quyền thấp**
- Dù có nhiều tính năng vượt trội nhưng giá bản quyền của DirectAdmin khá thấp, chỉ với 89$ có thể sử dụng trọn đời.

**Two-Factor Authentication**
- Với chức năng này, tài khoản đăng nhập Directadmin có thể sử dụng trên điện thoại di động. 

### Nhược điểm 
- Các tính năng chưa được hoàn thiện đầy đủ như cPanel hay một số phần mềm quản trị khác.
- Có ít tài liệu và sách hướng dẫn so với các đối thủ lớn.
- Ngôn ngữ: Không được hỗ trợ ngôn ngữ tiếng Việt. Bạn phải sử dụng phần mềm hoàn toàn bằng tiếng Anh.
- Sự tương thích: DirectAdmin không tương thích với dòng font unicode Bởi vậy nên rất khó để để sửa khi file sử dụng các ngôn ngữ không phải là tiếng Anh.

## Tính năng của DirectAdmin

### Tính năng phục vụ quản lý của admin
- Giúp cho việc tạo và thay đổi các tài khoản quản lý và đại lý trở nên nhanh chóng, dễ dàng hơn.
- Tạo ra các gói tài nguyên cho tài khoản đại lý và phân phối đến tài khoản user cuối.
- Xem, sắp xếp và thay đổi thông tin của người dùng.
- Xây dựng, sửa hoặc xóa các bản ghi DNS trên hệ thống.
- Cài đặt địa chỉ IP trên máy chủ cho người dùng.
- Cho phép truy cập thông tin về trạng thái hoạt động của các dịch vụ trên máy chủ.
- Hỗ trợ thống kê các thông số của hệ thống và các thông tin về tài nguyên đã sử dụng.

### Tính năng cho đại lý
- Giúp cài đặt và quy định mục đích sử dụng IP trên máy chủ và quy định mục đích sử dụng IP cho người dùng.
- Cho phép đại lý thống kê, sắp xếp các thông tin về tài nguyên sử dụng của khách hàng.
- Hỗ trợ tạo, thay đổi và xóa tài khoản dễ dàng hơn.
- Tự tạo các gói tài nguyên riêng cho khách hàng.
- Cho phép thêm và thay đổi giao diện hệ thống.
- Cho phép truy cập thông tin về trạng thái hoạt động của các dịch vụ trên máy chủ.
- Tạo ra thông tin máy chủ ảo với khách hàng.

### Tính năng cho người dùng 
- Tạo email, tự động trả lời hoặc từ chối email, lọc, bản ghi MX, webmail, xác thực SMTP.
- Tạo, thay đổi và xóa tài khoản FTP, tên miềm phụ, quy định đăng nhập nặc danh, tạo FTP cho tài khoản với tên miền phụ.
- Thay đổi DNS, bản ghi A, bản ghi CNAME, bản ghi NS, bản ghi MX và bản ghi PTR.
- Thống kê và kiểm tra tài nguyên đã sử dụng, thông tin về tài khoản, cáclượt truy cập…
- Tối ưu hóa việc sử dụng các website tạo bởi MS FrontPage.
- Quản lý, sao chép, di chuyển, đổi tên, xóa và thay đổi quyền truy cập, sửa và tạo file.
- Tạo và xóa CSDL, tạo tài khoản có quyền truy cập, thay đổi mật khẩu truy cập, sử dụng phpMyAdmin.
- Tạo bản sao và khôi phục website từ các bản sao.
- Cho phép người dùng tạo tài khoản và mật khẩu để hạn chế quyền truy cập vào một số thư mục nhất định.
- Cài đặt xác thực SSL, xem các thông tin về máy chủ, cài đặt các tác vụ định kỳ, liên kết các domain song song…

## Cách đăng nhập DirectAdmin
- Để đăng nhập vào DirectAdmin, đầu tiên bạn phải đăng ký tài khoản hosting. Sau khi đăng ký thành công, sẽ có 1 email được gửi đến bạn, trong đó có link truy cập, tên đăng nhập và mật khẩu đăng nhập DirectAdmin. Bạn chỉ việc làm theo hướng dẫn như trong email là được.

- Trong trường hợp đã có tài khoản Hosting, bạn chỉ cần truy cập vào website https://tenmiencuaban.com:2222 và nhập thông tin đăng nhập.

## Các cấp độ user trong DirectAdmin
Các cấp độ user trong DirectAdmin được phân thành 3 nhóm: Admin, Reseller, và User

### Admin (Administrator)
**Ý Nghĩa**:
- Tài khoản Admin là người quản trị cao cấp, chịu trách nhiệm quản lý toàn bộ hệ thống DirectAdmin. Admin có quyền hạn cao nhất và có thể thực hiện các tác vụ quản lý, cấu hình, và giám sát hệ thống.
- Sử dụng cho quản trị viên hệ thống hoặc nhóm quản trị viên chịu trách nhiệm quản lý và duy trì hệ thống hosting.
Có quyền cấu hình và tùy chỉnh hệ thống để đáp ứng nhu cầu cụ thể.

**Quản Lý Hệ Thống**:
- Cấu hình và quản lý toàn bộ hệ thống DirectAdmin.
- Thiết lập các tùy chọn và cấu hình hệ thống như SSL, PHP, Apache, ...

**Quản Lý Tài Khoản**:
- Tạo, quản lý và xóa tài khoản Reseller và User.
- Quản lý quyền truy cập và tài nguyên cho từng tài khoản.

**Thống Kê và Giám Sát**:
- Xem các bản ghi log và thống kê hệ thống.
- Giám sát tài nguyên hệ thống như bộ nhớ, CPU, băng thông, ...

### Reseller (Đại Lý):
**Ý Nghĩa**: 
- Tài khoản Reseller được thiết kế để chủ các doanh nghiệp hosting nhỏ hoặc cá nhân. Reseller có thể tạo và quản lý các tài khoản User, cũng như thực hiện một số tác vụ quản lý dịch vụ hosting.
- Sử dụng cho doanh nghiệp hosting nhỏ hoặc cá nhân muốn bán các dịch vụ hosting cho các khách hàng của họ.
- Có khả năng quản lý và tùy chỉnh các tài khoản User theo yêu cầu.

**Quản Lý Tài Khoản**:
- Tạo, quản lý và xóa các tài khoản User.
- Thiết lập giới hạn tài nguyên và quyền truy cập cho từng tài khoản User.

**Quản Lý Domain và DNS**:
- Thêm, sửa, xóa domain và subdomain.
- Quản lý các thiết lập DNS.

**Quản Lý Email và File**:
- Tạo và quản lý tài khoản email.
- Quản lý file và thư mục.

### User (Người Dùng):
**Ý Nghĩa**:
- Tài khoản User là người cuối cùng sử dụng dịch vụ hosting trong hệ thống DirectAdmin. User có thể quản lý và triển khai các trang web, tài khoản email, và các tài nguyên khác được cấp phát cho họ.
- Sử dụng cho người sử dụng cá nhân, doanh nghiệp nhỏ hoặc tổ chức muốn triển khai trang web hoặc ứng dụng. Khách hàng cá nhân hoặc doanh nghiệp sử dụng dịch vụ hosting mà không cần quản lý toàn bộ hạ tầng.

**Quản Lý Website**:
- Tạo, quản lý và triển khai website.
- Quản lý domain, subdomain, và các cài đặt liên quan.

**Quản Lý Email**:
- Tạo và quản lý tài khoản email.
- Cấu hình các tùy chọn email như chống spam, chữ ký email, ...

**Quản Lý File và Database**:
 - Sử dụng giao diện quản lý file để tải lên và tải xuống dữ liệu.
 - Tạo, quản lý và sao lưu cơ sở dữ liệu.


