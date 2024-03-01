# cài đặt web server OpenLiteSpeed trên CentOS 7
## Bước 1: Cập nhật hệ thống
- Trước khi đi vào cài đặt OpenLiteSpeed, MariaDB và PHP 7.4, bạn cần cập nhật thư viện và hệ thống lên phiên bản mới nhất bằng lệnh sau:

```
yum install epel-release -y
yum update -y
```
Trong đó: 
	- Câu lệnh **yum install epel-release -y** để đảm bảo rằng kho lưu trữ EPEL (Extra Packages for Enterprise Linux) đã được thêm vào hệ thống. OpenLiteSpeed có thể sử dụng các gói từ kho lưu trữ này để đáp ứng các phụ thuộc và yêu cầu cài đặt.

Bước 2: Cài source code của openlitespeed
- Để cài đặt mã nguồn mở OpenLiteSpeed, bạn cần tải xuống và cài đặt lần lượt bằng các lệnh sau:

```
rpm -ivh http://rpms.litespeedtech.com/centos/litespeed-repo-1.1-1.el7.noarch.rpm
yum install openlitespeed -y
```

- Thời gian cài đặt có thể mất vài phút, bạn đợi đến khi nhận được thông báo Complete là thành công.

![Imgur](https://i.imgur.com/VkxgthG.png)

![Imgur](https://i.imgur.com/51MKrQB.png)

## Bước 3: Cài đặt PHP 7.4 cho OpenLiteSpeed
- Tại đây bạn có thể sử dụng lệnh sau để cài đặt PHP 7.4, trong lệnh này các tiện ích mở rộng cần thiết và phổ biến nhất đã được thêm vào.

```
yum install lsphp74 lsphp74-gd lsphp74-json lsphp74-common lsphp74-process lsphp74-mbstring lsphp74-mysqlnd lsphp74-xml lsphp74-opcache lsphp74-mcrypt lsphp74-pdo lsphp74-imap lsphp74-bcmath lsphp74-pecl-memcache lsphp74-pecl-memcached lsphp74-pecl-redis lsphp74-pgsql lsphp74-zip -y
```

- Thời gian cài đặt PHP có thể mất vài phút, các bạn đợi cho đến khi nhận được thông báo Complete như hình dưới:

![Imgur](https://i.imgur.com/ALgarwn.png)

Bước 4: Thiết lập tài khoản Admin cho GUI OpenLiteSpeed WebAdmin
- Để tạo tài khoản Quản trị viên, bạn cần chạy lệnh sau:

```
/usr/local/lsws/admin/misc/admpass.sh
```

Tiếp theo, bạn cần điền các thông tin như hình dưới:

![Imgur](https://i.imgur.com/whjUxjS.png)

Nếu nhận được thông báo Tên người dùng/mật khẩu của Quản trị viên đã được cập nhật thành công! nó thành công.

### Bước 5: Mở cổng OpenLiteSpeed

- Mặc định OpenLiteSpeed sẽ sử dụng Port 7080 nên để có thể truy cập OpenLiteSpeed bằng cổng này bạn cần mở cổng trên Tường lửa của VPS. Thông thường trên Centos 7 sẽ sử dụng Tường lửa nên bạn cần mở port bằng lệnh sau:

```
firewall-cmd --zone=public --add-port=7080/tcp --permanent
firewall-cmd --reload
```

### Bước 6: Cài đặt MariaDB
- Theo mặc định, repo CentOS chỉ có sẵn MariaDB 5. Để cài đặt MariaDB 10.x, bạn cần tạo repo của riêng mình bằng cách thực hiện như sau: Bạn mở và chỉnh sửa tệp mariadb.repo bằng lệnh:

```
vi /etc/yum.repos.d/mariadb.repo
```

- Bạn tiến hành dán nội dung bên dưới vào và lưu lại. (Bạn có thể thay thế 10.4 = phiên bản MariaDB mà bạn muốn)

```
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/rhel7-amd64/  
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
- Bây giờ bạn có thể cài đặt MariaDB. Bạn thực hiện lần lượt các lệnh sau:

```
yum install MariaDB-server MariaDB-client -y 
systemctl start mariadb   
systemctl enable mariadb  
systemctl status mariadb   
```

- Sau khi cài đặt MariaDB, bạn cần định cấu hình bảo mật cơ bản cho dịch vụ MariaDB bằng cách gõ lệnh:

```
mysql_secure_installation
```

![Imgur](https://i.imgur.com/WsBt0De.png)

![Imgur](https://i.imgur.com/mNby1h4.png)

- Như vậy chúng ta đã cài đặt thành công OpenLiteSpeed trên centos7. Bây giờ chúng ta mở openlitespeed trong webadmin.
- Truy cập Webadmin :http://diachiip_mayserver:7080. Rồi nhập user và mật khẩu mà bạn vừa tạo ở trên để đăng nhập

![Imgur](https://i.imgur.com/bQ3I8vx.png)

- Và đây là giao diện webadmin của openlitespeed

![Imgur](https://i.imgur.com/0OtIic6.png)

- Tiếp theo ta tiến hành đổi cổng để truy cập vào trang web

Openlitespeed để công mặc định là 8080 chúng ta cần phải sửa đổi chuyển thành cổng 80 để có thể chạy website được.

- **Home >> Listeners **

![Imgur](https://i.imgur.com/WoLBSz2.png)

![Imgur](https://i.imgur.com/qJ0udoA.png)

