# Thực hiện triển khai Web server
- Để triển khai một Web server hoàn chỉnh trên CentOS ta thường sử dụng cơ sở dữ liệu MySQL/MariaDB, máy chủ web Apache, và ngôn ngữ lập trình PHP (PHP stack) , cùng với Wordpress là một phương pháp phổ biến. 

[I.Cài đặt Apache, PHP và mySQL trên CentOS 7 (LAMP)](#cai-dat-apache-php-va-mysql-tren-centos-7-lamp)

- [Cài đặt MySQL/MariaDB](#cai-dat-mysql/mariadb)
- [Cài đặt Apache2](#cai-dat-apache2)
- [Cài đặt PHP7.3](#Cai-dat-php7.3)
- [Cài đặt phpMyAdmin](#cai-dat-phpmyadim)

[II.Cài đặt WordPress trên CentOS](#cai-dat-wordpress-tren-centos)

- [Giới thiệu](#gioi-thieu)
- [Tạo cơ sở dữ liệu và người dùng mysql cho wordpress](#tao-csdl)
- [Cài đặt WordPress](#cai-dat-wordpress)
- [Cấu hình WordPress](#cau-hinh-wordpress)


## I.Cài đặt Apache, PHP và mySQL trên CentOS 7 (LAMP)
- Trước khi cài đặt LAMP ta cài đặt 2 gói sau: 
	```sh
	rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*
	yum -y install epel-release
	```
**rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY***
- Lệnh rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY* được sử dụng để nhập các chữ ký GPG (GNU Privacy Guard) từ các tệp chứa chúng vào hệ thống RPM của bạn. Cụ thể, nó nhập tất cả các chữ ký từ các tệp trong thư mục /etc/pki/rpm-gpg/ có tên bắt đầu bằng RPM-GPG-KEY.

- Các chữ ký GPG này được sử dụng để xác minh tính toàn vẹn của gói RPM (Red Hat Package Manager). Mỗi gói RPM thường được ký bởi một chữ ký số để đảm bảo rằng nó không bị thay đổi và là của người phát triển đáng tin cậy.

- Khi bạn chạy lệnh này, hệ thống sẽ thêm các chữ ký GPG vào cơ sở dữ liệu chứa chúng. Điều này giúp đảm bảo rằng các gói mà bạn cài đặt từ CentOS hoặc các kho lưu trữ RPM khác được xác minh và không bị sửa đổi từ trước.

**yum -y install epel-release**
 - Gói epel-release chứa các gói mở rộng bổ sung cho CentOS từ Dự án Fedora. Các gói này cung cấp nhiều ứng dụng và tiện ích hữu ích mà bạn có thể cần khi triển khai một máy chủ web. Việc này giúp đảm bảo rằng bạn có thể cài đặt và sử dụng các công cụ phổ biến mà không gặp vấn đề về phụ thuộc và tương thích.

### Cài đặt MySQL/MariaDB
- MariaDB là một nhánh của MySQL của nhà phát triển MySQL gốc Monty Widenius. MariaDB tương thích với MySQL và ở đây ta chọn sử dụng MariaDB thay vì MySQL:
```yum -y install mariadb-server mariadb```

- Sau đó chúng ta tạo các liên kết khởi động hệ thống cho MySQL (để MySQL khởi động tự động mỗi khi hệ thống được khởi động) và khởi động máy chủ MySQL:
```sh
systemctl start mariadb.service
systemctl enable mariadb.service
```

- Tiếp theo ta cần thiết lập mật khẩu cho tài khoản root MySQL:
```mysql_secure_installation```

Sau khi nhập lệnh thiết lập mật khẩu xong sẽ hiện ra như sau, và khi đó chúng ta sẽ làm như sau: 

*/usr/bin/mysql_secure_installation: line 379: find_mysql_client: command not found

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): **<--ENTER**
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] 
New password: **<--yourmariadbpassword**
Re-enter new password: **<--yourmariadbpassword**
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] **<--ENTER**
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] **<--ENTER**
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] **<--ENTER**
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] **<--ENTER**
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!*

### Cài đặt Apache2
- CentOS 7 được cài sẵn Apache 2.4. Apache2 có sẵn trực tiếp dưới dạng gói CentOS 7.0, do đó chúng ta có thể cài đặt nó như sau:
```yum -y install httpd```

- Cấu hình hệ thống để khởi động Apache khi khởi động
```
systemctl start httpd.service
systemctl enable httpd.service
```
**systemctl start httpd.service**: Lệnh này khởi động dịch vụ Apache HTTP Server ngay lập tức. Nếu Apache chưa được chạy, nó sẽ khởi động dịch vụ.

**systemctl enable httpd.service**: Lệnh này thiết lập Apache HTTP Server để tự động khởi động mỗi khi hệ thống được khởi động. Nó tạo ra các liên kết khởi động hệ thống để đảm bảo rằng Apache sẽ khởi động tự động khi hệ thống được reboot.

- Trong CentOS 7 có sử dụng Firewall cmd, bởi vậy ta phải cấu hình để cho phép truy cập bên ngoài vào cổng 80 (http) và cổng 443(https)
```
firewall-cmd --permanent --zone=public --add-service=http 
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```

- Bây giờ ta có thể truy cập vào trang web của ta thông qua địa chỉ ip của máy. 

![Imgur](https://i.imgur.com/n2khNgE.png)

### Cài đặt PHP7.3
**Bước 1**
PHP 7.3 có sẵn cho các bản phân phối CentOS 7 và Fedora từ kho Remi. Thêm nó vào hệ thống của bạn bằng cách chạy:
```
sudo yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm 
sudo yum -y install epel-release yum-utils
```
**sudo yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm**: Lệnh này cài đặt gói remi-release, cung cấp cấu hình cho kho lưu trữ Remi. Kho lưu trữ Remi cung cấp các gói phần mềm bổ sung và cập nhật cho CentOS, thường được sử dụng cho việc cập nhật PHP lên các phiên bản mới.

**sudo yum -y install epel-release yum-utils**: Lệnh này cài đặt gói epel-release, cung cấp cấu hình cho kho lưu trữ EPEL (Extra Packages for Enterprise Linux). Kho lưu trữ EPEL chứa nhiều gói mở rộng và bổ sung mà không có sẵn trong kho chính thức của CentOS. yum-utils cài đặt các tiện ích bổ sung cho yum để quản lý các gói và kho lưu trữ dễ dàng hơn.

**Bước 2 Tắt repo cho php 5.4**
- Theo mặc định, kho lưu trữ được kích hoạt là dành cho PHP 5.4. Tắt repo này và bật cho PHP 7.3:
```
yum-config-manager --disable remi-php54
yum-config-manager --enable remi-php73
```
**Bước 3: Cài đặt PHP 7.3 trên CentOS**
- Câu lệnh: 
```
yum -y install php php-cli php-fpm php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json
```
Các gói trên là các gói phổ biến và thường được cài đặt khi triển khai một máy chủ web chạy PHP

- Sau đó kiểm tra phiên bản của php, sử dụng 
```
php -v
```

- Tiếp theo khởi động lại dịch vụ httpd
```
systemctl restart httpd
```
### Kiểm tra PHP 7.3 / Lấy thông tin chi tiết về php đã cài đặt
- Thư mục gốc của trang web mặc định là /var/www/html. Bây giờ chúng ta sẽ tạo một tệp PHP nhỏ (info.php) trong thư mục đó và gọi nó trong trình duyệt. Tệp sẽ hiển thị nhiều chi tiết hữu ích về cài đặt PHP của ta,  chẳng hạn như phiên bản PHP đã cài đặt.
```
vi /var/www/html/info.php
```
Thêm vào tệp đoạn sau: 
```
<?php
phpinfo();
?>
```
Sau đó nhập địa chị ip máy vào trình duyệt như sau: 192.168.249.132/info.php

![Imgur](https://i.imgur.com/8J3I4fV.png)

### Cài đặt phpMyAdmin
- phpMyAdmin là một giao diện web thông qua đó bạn có thể quản lý cơ sở dữ liệu MySQL của mình.
- phpMyAdmin bây giờ có thể được cài đặt như sau:
```
yum install phpMyAdmin
```
- Bây giờ chúng ta cấu hình phpMyAdmin. Chúng tôi thay đổi cấu hình Apache để phpMyAdmin cho phép kết nối không chỉ từ localhost (<Directory "/usr/share/phpmyadmin">):
```
vi /etc/httpd/conf.d/phpMyAdmin.conf
```
- Sau đó ta chỉnh sửa và cấu hình file **phpMyAdmin.conf** như sau: 

![Imgur](https://i.imgur.com/XxlcfMY.png)

- Tiếp theo, chúng tôi thay đổi xác thực trong phpMyAdmin từ cookie sang http, mục đích của việc này là để tăng tính bảo mật. 
```
vi /etc/phpMyAdmin/config.inc.php
```

![Imgur](https://i.imgur.com/xlZuhfO.png)

- Tiếp theo ta khởi động lại dịch vụ web
```
systemctl restart httpd
```
- Và bây giờ ta có thể truy cập vào phpMyAdmin, bằng tài khoản root, và mật khẩu là mật khẩu ta đã thiết lập khi cài đặt MariaDB

![Imgur](https://i.imgur.com/WtZ7896.png)

## II. Cài đặt Wordpress trên CentOS
### Giới thiệu
WordPress là một trang web và công cụ viết blog miễn phí, mã nguồn mở sử dụng PHP và MySQL. WordPress hiện là CMS (Content management system) phổ biến nhất trên Internet và có hơn 20.000 plugin để mở rộng chức năng của nó. Điều này làm cho WordPress trở thành một lựa chọn tuyệt vời để thiết lập và chạy một trang web một cách nhanh chóng và dễ dàng.

### Tạo cơ sở dữ liệu và người dùng mysql cho WordPress
- Bước đầu tiên chúng ta sẽ thực hiện là chuẩn bị. WordPress sử dụng cơ sở dữ liệu quan hệ để quản lý thông tin cho trang web và người dùng. Chúng ta đã cài đặt MariaDB (một nhánh của MySQL), có thể cung cấp chức năng này, nhưng chúng ta cần tạo cơ sở dữ liệu và người dùng để WordPress hoạt động.
- Chúng ta có thể tạo cơ sở dữ liệu và tài khoản của người dùng bằng câu lệnh trên Centos. Tuy nhiên để đơn giản ta có thể tạo trực tiếp trên giao diện của phpMyAdmin.

- Tạo một database tên **wordpress**:

![Imgur](https://i.imgur.com/S0ay5ax.png)

- Vào phần Privileges để thêm người dùng 

![Imgur](https://i.imgur.com/RPEMNaJ.png)

![Imgur](https://i.imgur.com/6yEatC6.png)

### Cài đặt WordPress
- Trước khi tải xuống WordPress, có một mô-đun PHP mà chúng ta cần cài đặt để đảm bảo nó hoạt động bình thường. Nếu không có mô-đun này, WordPress sẽ không thể thay đổi kích thước hình ảnh để tạo hình thu nhỏ. Chúng ta có thể lấy gói đó trực tiếp từ kho lưu trữ mặc định của CentOS bằng yum:
```
yum install php-gd
```
- Sau đó ta khởi động lại Apache
```
systemctl restart httpd
```
- Chúng ta đã sẵn sàng để tải xuống và cài đặt WordPress từ trang web dự án. Nhóm phát triển WordPress luôn liên kết phiên bản ổn định mới nhất của phần mềm của họ với cùng một URL, vì vậy chúng ta có thể lấy phiên bản WordPress mới nhất bằng cách nhập lệnh sau:
```
cd ~
yum install wget
wget http://wordpress.org/latest.tar.gz
```
- Trong đó: 
	- cd ~: Lệnh này chuyển đến thư mục người dùng. Dấu chấm (~) thường đại diện cho thư mục người dùng của bạn.

	- yum install wget: Cài đặt tiện ích wget bằng trình quản lý gói YUM. wget là một công cụ dòng lệnh giúp tải xuống tệp tin từ internet.

	- wget http://wordpress.org/latest.tar.gz: Sử dụng wget để tải xuống tệp tin latest.tar.gz từ trang web chính thức của WordPress. Tệp tin này chứa mã nguồn của WordPress.

- Điều này sẽ tải xuống một tệp lưu trữ nén chứa tất cả các tệp WordPress cần thiết. Chúng ta có thể giải nén các tệp đã lưu trữ để xây dựng lại thư mục WordPress bằng lệnh `tar`:
```
tar -xzvf latest.tar.gz

cp -r ~/wordpress/* /var/www/html/

mkdir /var/www/html/wp-content/uploads
```
- Sau khi giải nén ta sẽ được một thư mục là **wordpress**. Và ta copy toàn bộ thư mục trong wordpress vào /var/www/html. Sau đó tạo một thư mục uploads trong thư mục wp-content của WordPress để lưu trữ tập tin được tải lên từ trang web.

- Bây giờ chúng ta cần gán quyền sở hữu và quyền truy cập đúng cho các tệp và thư mục của WordPress. Điều này sẽ tăng cường bảo mật trong khi vẫn giữ cho WordPress hoạt động như dự kiến. Để thực hiện điều này, chúng ta sẽ sử dụng lệnh chown để gán quyền sở hữu cho người dùng và nhóm của Apache:
```
chown -R apache:apache /var/www/html/*
```
- Lệnh này đảm bảo rằng tất cả các tệp và thư mục trong thư mục /var/www/html/ đều thuộc sở hữu của người dùng và nhóm apache, điều này là quan trọng để đảm bảo rằng máy chủ web Apache có quyền truy cập và quản lý tệp mà nó cần để chạy WordPress.
- Đồng thời: Với thay đổi này, máy chủ web sẽ có thể tạo và sửa đổi các tệp WordPress, đồng thời cũng sẽ cho phép chúng tôi tải nội dung lên máy chủ.

### Cấu hình Wordpress
- Hầu hết các cấu hình cần thiết để sử dụng WordPress sẽ được hoàn thành thông qua giao diện web sau này. Tuy nhiên, chúng ta cần thực hiện một số công việc từ dòng lệnh để đảm bảo rằng WordPress có thể kết nối với cơ sở dữ liệu MySQL mà chúng ta đã tạo cho nó.

- Bắt đầu bằng cách di chuyển vào thư mục gốc của Apache nơi bạn đã cài đặt WordPress:
```
cd /var/www/html
```

- Tệp cấu hình chính mà WordPress phụ thuộc vào được gọi là wp-config.php. Một tệp cấu hình mẫu có đầy đủ các thiết lập chúng ta cần thường được bao gồm theo mặc định. Chúng ta chỉ cần sao chép nó đến vị trí tệp cấu hình mặc định, để WordPress có thể nhận diện và sử dụng tệp:
```
cp wp-config-sample.php wp-config.php
```

- Bây giờ khi chúng ta đã có một tệp cấu hình để làm việc, hãy mở nó trong một trình soạn thảo văn bản.
```
vi wp-config.php
```
- Các sửa đổi duy nhất mà chúng ta cần thực hiện trên tệp này là đối với các tham số giữ thông tin cơ sở dữ liệu của chúng ta. Chúng ta sẽ cần tìm đến phần có tiêu đề "MySQL settings" và thay đổi các biến DB_NAME, DB_USER, và DB_PASSWORD để WordPress có thể kết nối và xác thực đúng với cơ sở dữ liệu chúng ta đã tạo.

![Imgur](https://i.imgur.com/j5mksQj.png)

### Hoàn tất cài đặt qua giao diện Web
Truy cập vào địa chỉ ip và thiết lập cài đặt WordPress

![Imgur](https://i.imgur.com/c7ITnSX.png)

![Imgur](https://i.imgur.com/IAukmv5.png)

![Imgur](https://i.imgur.com/XQEdiFl.png)
