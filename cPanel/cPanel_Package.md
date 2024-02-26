## Creating a package
- Trong WHM, chọn **Package** > **Add a Package**

![Imgur](https://i.imgur.com/axGqqgw.png)

- Điền tên cho package mà bạn mong muốn . 
**Quan trọng**: Bạn không thể sửa đổi tên gói. Vì lý do này, hãy tránh tên gói bao gồm các chi tiết mà bạn có thể muốn thay đổi sau này, chẳng hạn như giá cả.

**Chú ý:**
	- Bởi vì hệ thống lưu trữ các gói như các tệp, bạn có thể sử dụng bất kỳ tên tệp hợp lệ nào. Tuy nhiên, để ngăn chặn xung đột với Package Extension, bạn không thể đặt tên cho các gói mở rộng.

	- Giao diện cPanel chỉ hiển thị tên gói (ví dụ, reseller_package xuất hiện dưới dạng package).

	- Để quản lý gói dễ dàng hơn, hãy tạo ít gói hơn và sử dụng các tên ngắn.

- Nhập thông tin cần thiết vào các phần Tài nguyên và Cài đặt.Sau đó ấn **Add**

![Imgur](https://i.imgur.com/ezcYZjY.png)

![Imgur](https://i.imgur.com/dBA5bvg.png)

## Resource options
**Disk Space Quota (MB)**
- Số lượng tối đa dung lượng trên ổ cứng máy chủ mà tài khoản có thể sử dụng, được đo lường bằng megabyte (MB).

Lưu ý:
- Hãy xem xét loại nội dung mà người dùng của bạn có ý định lưu trữ, vì điều này ảnh hưởng lớn đến lượng dung lượng đĩa mà họ cần.

**Monthly Bandwidth Limit (MB)**
- Lượng thông tin mà tài khoản có thể chuyển giao mỗi tháng, được đo lường bằng megabyte (MB).

Lưu ý:
- Hãy xem xét loại nội dung mà người dùng của bạn có ý định lưu trữ, vì điều này ảnh hưởng lớn đến lượng dung lượng đĩa mà họ cần.

**Max FTP Accounts**
- Số tài khoản FTP tối đa cho tài khoản cPanel

**Max Email Accounts**
- Số tài khoản Email tối đa cho tài khoản cPanel

**Max Quota per Email Address (MB)**
- Dung lượng tối đa mà tài khoản có thể xác định khi tạo một tài khoản email, tính bằng megabyte (MB). Giá trị này mặc định là Không giới hạn.

Lưu ý:
- Khi bạn điều chỉnh giá trị này, nó không ảnh hưởng đến các tài khoản email đã tồn tại.

**Max Mailing Lists:** Số lượng tối đa của danh sách gửi Mailman cho tài khoản. Để biết thêm thông tin, đọc tài liệu của chúng tôi về Mailing Lists.

**Max SQL Databases:** Số lượng tối đa cho mỗi loại cơ sở dữ liệu SQL có sẵn. Ví dụ, nếu bạn đặt giá trị này là 5 và cho phép cả cơ sở dữ liệu MySQL® và PostgreSQL®, tài khoản có thể tạo tối đa năm cơ sở dữ liệu MySQL và năm cơ sở dữ liệu PostgreSQL.

**Max Sub Domains:** Số lượng tối đa của các subdomain cho tài khoản.

**Max Parked Domains:** Số lượng tối đa của các domain được "park" (tên miền định danh) cho tài khoản.

**Max Addon Domains:** Số lượng tối đa của các domain addon cho tài khoản.

**Max Passenger Applications:** Số lượng tối đa của ứng dụng Passenger cho tài khoản.

**Maximum Hourly Email by Domain Relayed:** Số lượng tối đa của các email mà bất kỳ domain nào trên tài khoản có thể gửi mỗi giờ. Giá trị mặc định là Không giới hạn. Giá trị 0 đại diện cho Không giới hạn.

**Maximum Percentage of Failed or Deferred Messages a Domain May Send Per Hour:** Tỷ lệ tối đa của các tin nhắn thất bại hoặc trì hoãn mà một domain trên tài khoản có thể gửi trước khi máy chủ tạm thời chặn thư đi từ domain đó. Hệ thống kiểm tra thư đi và thư nội địa trong giờ trước để xác định liệu domain có vượt quá giới hạn hay không. Khi một domain vượt quá giới hạn, nó sẽ không thể gửi thư cho đến khi domain không còn vượt quá giới hạn nữa. Giá trị mặc định là Không giới hạn.

**Max Team Users:** Số lượng tối đa của người dùng trong nhóm cho tài khoản.

## Settings options
**Dedicated IP**
- Địa chỉ IP tĩnh mà tài khoản sẽ không chia sẻ với các tài khoản khác trừ khi người dùng chỉ định một tài khoản cụ thể để chia sẻ địa chỉ IP.

- Lưu ý: Bạn không thể chỉnh sửa tùy chọn này sau khi tạo gói. Để thay đổi cài đặt này, bạn phải tạo một gói mới. Chúng tôi khuyến nghị cài đặt này cho các gói sẽ áp dụng cho các tài khoản reseller.

**Shell Access**
- Cho phép người dùng truy cập máy chủ thông qua giao diện dòng lệnh.

**CGI Access:** Cho phép tài khoản thực thi các kịch bản CGI.

**Digest Authentication at account creation**
- Bật hỗ trợ Xác thực Digest cho việc truy cập Web Disk qua kết nối văn bản hoặc không mã hóa. Người dùng sử dụng các hệ điều hành Microsoft® Windows Vista®, Windows® 7 và Windows® 8 yêu cầu sự hỗ trợ này.

- Lưu ý: Cài đặt này là bắt buộc nếu máy chủ của bạn không có một chứng chỉ SSL mà một cơ quan chứng nhận chính thức đã ký.

**cPanel Theme:** Chọn một giao diện từ menu.

**Feature List**
- Chọn một danh sách tính năng từ menu. Danh sách tính năng xác định tính năng nào của cPanel mà người dùng của bạn có thể truy cập. Để xem hoặc chỉnh sửa tính năng được chọn hiện tại, nhấp vào Xem để di chuyển đến giao diện Quản lý Tính năng của WHM (WHM » Home » Packages » Feature Manager).

- Chú ý: Danh sách tính năng đã tắt không được dùng cho tài khoản cPanel hoặc gói. Thay vào đó, hãy chỉ định tài khoản cPanel hoặc gói danh sách tính năng mặc định, nhưng xác định tính năng bạn không muốn có trên máy chủ trong danh sách tính năng đã tắt.

