# TỔNG QUAN VỀ MARIADB
## MariaDB là gì?
- MariaDB là hệ quản trị cơ sở dữ liệu miễn phí được phát triển từ hệ quản trị cơ sở dữ liệu mã nguồn mở MySQL. MariaDB được phát triển nhằm thay thế công nghệ cơ sở dữ liệu MySQL, vì thế nó tương thích và cho một hiệu suất cao hơn so với MySQL. Ưu điểm khi sử dụng MariaDB là gì?
- MariaDB được Michael “Monty” Widenius, developer hàng đầu của MySQL dẫn dắt và phát triển. Ưu điểm lớn nhất của hệ quản trị này là tương thích với nhiều hệ điều hành, bao gồm Linux CentOS, Ubuntu và Window với các gói cài đặt tar, zip, MSI, rpm cho cả 32bit và 64bit với hiệu suất cao hơn so với MySQL. 
- Vì thế, MariaDB đang ngày càng được đông đảo các nhà phát triển sử dụng, trong đó có wikipedia, Fullstack-Station,… MariaDB đang có xu hướng thay thế cho MySQL – hệ quản trị cơ sở dữ liệu mã nguồn mở lâu đời nhất được sử dụng từ trước đến nay.

## Lịch sử của MariaDB
- Nền móng cơ sở đầu tiên của MariaDB được phát triển bởi “trụ cột” của MySQL AB là Michael “Monty” Widenius. Năm 2008, sau khi Sun mua lại MySQL AB, Michael “Monty” Widenius rời khỏi MySQL AB và tiếp tục phát triển một hệ cơ sở quản trị mới của mình.

- Đầu năm 2009, Michael cùng với 1 vài đồng nghiệp khác bắt đầu tiến hành dự án chuyên sâu về công cụ lưu trữ MySQL, sau này trở thành MariaDB. Tên gọi MariaDB được đặt tên theo tên con gái út của Widenius – Maria. Sau nhiều lần nâng cấp và phát triển, hiện tại MariaDB đã ra mắt phiên bản mới nhất là MariaDB 10.1.

- MariaDB được hình thành dựa trên nền tảng của MySQL, vì thế nó kế thừa được hầu hết các chức năng cơ bản cần thiết của MySQL. Bên cạnh đó, MariaDB cũng phát triển thêm nhiều tính năng mới và có sự nâng cấp hơn về cơ chế lưu trữ, tối ưu máy chủ.

- MariaDB có 2 bản trả phí và không cần trả phí. Tuy nhiên, với phiên bản không trả phí, người dùng vẫn có thể sử dụng đầy đủ các tính năng mà không ảnh hưởng đến việc chạy hệ thống.

## Ưu điểm của MariaDB
- Không phải ngẫu nhiên mà MariaDB được nhiều người yêu thích và sử dụng đến vậy. Những ưu điểm lớn nhất của hệ quản trị này phải kể đến bao gồm:
	- Hoàn toàn miễn phí
	- Khắc phục những hạn chế của MySQL
	- Bổ sung thêm nhiều Engine hơn
	- Kết hợp cả SQL và NoSQL
	- Hỗ trợ tiếng Việt

**Hoàn toàn miễn phí**
- Đây là một hệ quản trị sử dụng mã nguồn mở hoàn toàn miễn phí. Do đó, người dùng không cần phải bỏ tiền mua bản quyền và vẫn có thể sử dụng đầy đủ những tính năng của phần mềm này.

**Khắc phục những hạn chế của MySQL**
- MariaDB được phát triển từ MySQL, do đó nó kế thừa những đặc điểm chủ yếu của hệ quản trị này từ phiên bản 5.1 -> 5.5. Do đó, người dùng có thể chuyển từ MySQL sang MariaDB mà không ảnh hưởng đến hệ thống. 
- Đặc biệt, những hạn chế của MySQL, khi chuyển qua MariaDB đều sẽ được khắc phục một cách triệt để nhất, thậm chí có thể tăng tốc độ hơn so với MySQL từ 3-5%. Ngoài ra, hệ quản trị này còn cải thiện hiệu năng và có thêm nhiều chức năng mới hơn so với MySQL.

**Bổ sung thêm nhiều Engine hơn**
- Ngoài các storage engines cơ bản như MyISAM, BLACKHOLE, CSV, MEMORY, ARCHIVE, MERGE; MariaDB còn phát triển thêm các storage engines khác bao gồm: Aria, XtraDB, FederatedX, OQGRAPH, SphinxSE, IBM DB2I, Spider, PBXT,…

**Kết hợp cả SQL và NoSQL**
- MariaDB là sự kết hợp của cả 2 loại cơ sở dữ liệu là SQL và NoSQL. Việc kết hợp sẽ giúp hệ thống này có thể tích hợp được tất cả ưu điểm của cả 2 cơ sở dữ liệu này là Dynamic Column và Cassandra Storage Engine.

**Hỗ trợ tiếng Việt**
- Một ưu điểm tuyệt vời của MariaDB là đã có bản tiếng Việt. Mặc dù bản dịch chưa thật sự hoàn hảo nhưng vẫn có thể hỗ trợ nhiều cho người dùng.

