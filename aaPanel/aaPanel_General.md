# aaPanel

## aaPanel là gì?
- aaPanel là một control panel miễn phí, cho phép người dùng quản lý server với giao diện GUI đơn giản. Đặc biệt, thông qua aaPanel, bạn có thể dễ dàng cài đặt một server web chạy mô hình LNMP/LAMP chỉ bằng một số thao tác đơn giản.

- Nếu bạn đã từng nghe qua về BAOTA Panel – một hosting control miễn phí nổi tiếng được phát triển tại Trung Quốc. aaPanel là phiên bản quốc tế hóa của BAOTA Panel. Phiên bản này được ra đời với mục đích đơn giản hóa việc cài đặt, quản trị VPS và server web, giúp người dùng có thể dễ dàng tiếp cận và sử dụng để phát triển ứng dụng mà không cần phải quan tâm quá nhiều đến hệ thống. 

- Mặc dù aaPanel còn khá mới (chỉ mới phát triển đến version 1.1.0) và có ít tính năng hơn BAOTA Panel, nhưng aaPanel vẫn được khuyên dùng bởi control panel này liên tục được cập nhật với nhiều tính năng hữu ích. 

## Chức năng của aaPanel
- Vì aaPanel còn khá mới nên chỉ hỗ trợ cho người dùng một số chức năng cơ bản nhất như: quản lý web, Database, FTP và File. 

- Operating System – Hệ điều hành hỗ trợ (OS) của aaPanel cũng khá đầy đủ, bao gồm: CentOS, Debian, Ubuntu, Fedora. Tuy nhiên, bạn cần lưu ý rằng OS phải Pure and Clean (tức mới và sạch sẽ) và chưa từng cài đặt các phần mềm hay nền tảng như PHP/Apache/NGINX/MySQL. Ngoài ra, để chạy aaPanel, cấu hình tối thiểu cần phải đáp ứng là VPS có RAM 128MB, CPU 1 core. Tốt nhất là bạn nên có cấu hình RAM 512 MB và Panel này chỉ tốn 10Mb để đảm bảo vận hành ổn định.

## Ưu và nhược điểm của aaPanel
aaPanel là một control panel còn khá mới nên bên cạnh những ưu điểm nổi bật sẽ không tránh khỏi việc tồn tại một số nhược điểm nhất định. Dưới đây là những ưu – nhược điểm đặc trưng của aaPanel 

### Ưu điểm
- aaPanel khá nhẹ bạn chỉ cần VPS Linux có 512MB RAM là đã có thể sử dụng được.

- Người dùng có thể cài đặt aaPanel và sử dụng dễ dàng chỉ bằng một vài thao tác chuột đơn giản.

- aaPanel cho phép bạn can thiệp, chỉnh sửa cấu hình PHP hay Webserver trực tiếp trên giao diện một cách nhanh chóng.

- Thông qua thư viện App Store với các phần mềm đã được tích hợp sẵn, bạn có thể cài đặt Redis, Memcached, Google Drive,… chỉ bằng một lần click chuột.

- Cho phép người dùng quản lý tập tin thông qua File Manager với giao diện thân thiện, đẹp mắt, hỗ trợ code editor đơn giản, tiện lợi.

- Cho phép backup web lên trên Google Drive, FTP, Amazon S3,…

- aaPanel có cộng đồng người dùng tương đối nhiều, vì vậy bạn có thể tham gia để tìm kiếm tài liệu hướng dẫn và tìm kiếm sự trợ giúp, hỗ trợ.

### Nhược điểm 
Bên cạnh những ưu điểm nổi bật trên, aaPanel vẫn còn tồn tại một số nhược điểm nhất định như:
- Cấu hình thiết lập sẵn cho MySQL/MariaDB hơi cao nên thường xuyên xảy ra tình trạng MySQL tự tắt mà không thể khởi động lại được. Khi đó, bạn có thể vào khu vực thiết lập của MySQL/MariaDB và thiết lập cấu hình ở mức thấp hơn để hạn chế trường hợp này xảy ra.

- aaPanel chưa hỗ trợ tính năng phân quyền người dùng, bạn chỉ có thể truy cập vào bảng điều khiển thông qua 1 tài khoản duy nhất. Đây là một nhược điểm gây nhiều bất tiện và cần được khắc phục của aaPanel. 

- aaPanel chỉ phù hợp với những VPS có cấu hình thấp, ít gây lỗi vặt nhưng lại đủ mạnh mẽ để sử dụng cho cá nhân. Còn những cấu hình cao hơn, bạn cần phải tìm đến một dịch vụ control panel khác.

### Cách cài đặt aaPanel cho VPS
Hiện nay, aaPanel hỗ trợ cho đa số các hệ điều hành, hầu hết các hệ điều hành đều có cách cài đặt tương tự nhau và các bước thực hiện cũng khá đơn giản. 

Trước khi bắt đầu cài đặt aaPanel, bạn cần đáp ứng các điều kiện về VPS/Server như sau: 

- Dung lượng RAM nên có từ 512MB trở lên. Tuy nhiên, để hệ thống hoạt động ổn định nhất, RAM nên từ 768MB. 

- Yêu cầu về hệ điều hành như sau: Ubuntu 16.04+, CentOS 7.1+, Debian 9.0+ và hệ điều hành chưa được cài đặt webserver hay phần mềm control panel nào.

### 