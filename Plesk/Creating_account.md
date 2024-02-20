## Tạo tài khoản

- Khi đăng ký được tạo, tài khoản người dùng cho chủ sở hữu đăng ký sẽ được tạo cùng với đăng ký đó. Đây là tài khoản bạn sử dụng để đăng nhập vào Plesk. Bạn có thể thực hiện bất kỳ hoạt động nào mà nhà cung cấp dịch vụ lưu trữ đã cấp quyền. Tuy nhiên, bạn có thể muốn cấp cho người khác - ví dụ: nhân viên khác trong tổ chức của bạn hoặc nhà thầu - quyền truy cập vào Plesk để họ có thể thực hiện một số thao tác. Nhưng điều gì sẽ xảy ra nếu bạn không muốn họ có toàn quyền kiểm soát đăng ký của bạn khi họ đăng nhập?

- Trong trường hợp này, bạn có thể tạo thêm người dùng để có thể đăng nhập vào Plesk và có quyền truy cập vào một số chức năng được xác định trước, chẳng hạn như tạo hộp thư, quản lý cơ sở dữ liệu hoặc thực hiện sao lưu. Chức năng có sẵn cho người dùng bổ sung được xác định bằng cách tạo, định cấu hình và chỉ định vai trò người dùng cho người dùng bổ sung.

- Để tạo thêm tài khoản người dùng, đi tới **User** -> **User Accounts** và click **Create User Account**

![Imgur](https://i.imgur.com/n7ezafa.png)

- Điền các thông tin cần thiết để tạo một tài khoản. 

![Imgur](https://i.imgur.com/x9K6hX1.png)


Trong đó: 
- **Email address**: Địa chỉ email sẽ được sử dụng làm tên người dùng để đăng nhập vào Plesk, trừ khi bạn chỉ định một tên khác trong hộp Username.

- **External email address**: Chỉ định email sẽ được sử dụng để đặt lại mật khẩu nếu người dùng mất quyền truy cập vào địa chỉ email chính của họ.

- **User role**: Hãy chọn vai trò người dùng 
	- **Administrator**: Có toàn quyền quản lý các chức năng có trong web WordPress. Có thể thực hiện được tất cả các hoạt động quản lý, cài đặt, cấu hình và kiểm soát trên Plesk. Đây là vai trò phù hợp cho người quản trị hệ thống. 

	- **Webmaster**: cho phép người dùng quản lý hầu hết các khía cạnh của các gói đăng kí (subcriptions) mà họ được gán, bao gồm tạo trang web mới và cấu hình các dịch vụ như DNS, email và FTP. Tuy nhiên, webmaster không thể tạo người dùng mới trong Plesk hoặc quản lý các vai trò khác. 

	- **Application user**: là người dùng được tạo ra để quản lý một ứng dụng cụ thể trên Plesk. Thông qua application user, bạn có thể gán quyền truy cập và tài khoản cho ứng dụng mà không cần sử dụng tài khoản người dùng chính của Plesk. Điều này giúp tách biệt quyền truy cập giữa các ứng dụng và đảm bảo an toàn cho hệ thống.

	- **Accountant** là vai trò có giới hạn nhất trong Plesk Người dùng với vai trò này có thể xem chi tiết về các gói đăng ký (subscriptions) mà họ được cấp quyền truy cập, chẳng hạn như tài nguyên đã sử dụng và các tùy chọn hosting hiện tại. Tuy nhiên, họ không thể thay đổi bất kỳ cài đặt nào. Vai trò Accountant phù hợp cho việc theo dõi và kiểm tra thông tin mà không cần thay đổi cài đặt.

- **Access to subscriptions**: Cho phép người dùng chỉ truy cập vào một đăng ký được chỉ định. Giá trị **All** cấp cho họ quyền truy cập vào tất cả các đăng ký trong tài khoản khách hàng của bạn.

- **Username**: tên tài khoản truy cập vào Plesk
- **Password**: mật khẩu truy cập vào Plesk

- **User is active**: Nếu hộp kiểm này bị bỏ chọn, người dùng sẽ không thể đăng nhập vào Plesk. Theo mặc định, hộp kiểm được chọn. Nếu bạn cần vô hiệu hóa một tài khoản người dùng bổ sung mà không xóa tài khoản đó, hãy đi tới User > User Account, nhấp vào người dùng bạn muốn vô hiệu hóa, nhấp vào Thay đổi cài đặt và bỏ chọn User is Active.


- Sau khi đặt xong sẽ có thông báo tạo tài khoản thành công

![Imgur](https://i.imgur.com/tey7x5D.png)