## Triển khai một trang Wordpress trỏ tới database dùng tới Cluster đã triển khai. 

#### CÀi đặt websever
- Tiến hành cài đặt apache websever

```yum install -y httpd
```

- Cấu hình hệ thống để khởi động Apache khi khởi động

```
systemctl start httpd.service
systemctl enable httpd.service
```

#### Cài đặt PHP7.3
- PHP 7.3 có sẵn cho các bản phân phối CentOS 7 và Fedora từ kho Remi. Thêm nó vào hệ thống của bạn bằng cách chạy:

```
sudo yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm 
sudo yum -y install epel-release yum-utils
```

- Theo mặc định, kho lưu trữ được kích hoạt là dành cho PHP 5.4. Tắt repo này và bật cho PHP 7.3:

```
yum-config-manager --disable remi-php54
yum-config-manager --enable remi-php73
```

- Cài đặt PHP 7.3 trên CentOS

```
yum -y install php php-cli php-fpm php-mysqlnd php-zip php-devel php-gd php-mcrypt php-mbstring php-curl php-xml php-pear php-bcmath php-json
```

#### Cài đặt wordpress

- Tải xuống và cài đặt WordPress từ trang web

```
cd ~
wget http://wordpress.org/latest.tar.gz
```

- Điều này sẽ tải xuống một tệp lưu trữ nén chứa tất cả các tệp WordPress cần thiết. Chúng ta có thể giải nén các tệp đã lưu trữ để xây dựng thư mục WordPress bằng lệnh tar:

```
tar -xzvf latest.tar.gz

cp -r ~/wordpress/* /var/www/html/

mkdir /var/www/html/wp-content/uploads
```

- Cấp quyền cho thư mục

```
chown -R apache:apache /var/www/html/*
```

- Tệp cấu hình chính mà WordPress phụ thuộc vào được gọi là wp-config.php. Một tệp cấu hình mẫu có đầy đủ các thiết lập chúng ta cần thường được bao gồm theo mặc định. Chúng ta chỉ cần sao chép nó đến vị trí tệp cấu hình mặc định, để WordPress có thể nhận diện và sử dụng tệp:

```
cp wp-config-sample.php wp-config.php
```

### Tạo cơ sở dữ liệu cho trang web
- Chúng ta tạo cơ sở dữ liệu cho trang wordpress mà ta muốn triển khai

```
mysql -u root -p

create database wordpress;
create user 'wp'@'localhost' identified by 'Welcome123';
grant all privileges on wordpress to 'wp'@'localhost' identified by 'Welcome123';
grant all privileges on wordpress to 'wp'@'%' identified by 'Welcome123';
flush privileges;
exit
```
- Tuy nhiên ở trên mặc dù ta đã cấp quyền truy cập cho người dùng "wp" từ bất kỳ máy chủ nào (%) đối với cơ sở dữ liệu "wordpress" bằng câu lệnh **grant all privileges on wordpress to 'wp'@'%' identified by 'Welcome123';** nhưng ta vẫn cần cấp quyền cho node1, node2 mà ta cấu hình cluster để đảm bảo nó có quyền truy cập cơ sở dữ liệu 

```
grant all privileges on wordpress to 'wp'@'node1' identified by 'Welcome123';
grant all privileges on wordpress to 'wp'@'node2' identified by 'Welcome123';
```

![Imgur](https://i.imgur.com/g0HMYLk.png)

![Imgur](https://i.imgur.com/4RLZalw.png)


- Tiếp theo ta vào file **wp-config.php** để cấu hình cơ sở dữ liệu

```
vi wp-config.php
```

- Điền cơ sở dữ liệu mà ta vừa tạo ở trên vào, đặc biệt chú ý phần **DB_HOST** phải điền IP VIP của cụm cluster để cơ sở dữ liệu được trỏ về cluster ta vừa cài đặt. 

```
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** Database username */
define( 'DB_USER', 'wp' );

/** Database password */
define( 'DB_PASSWORD', 'Welcome123' );

/** Database hostname */
define( 'DB_HOST', '192.168.249.175' );
```

![Imgur](https://i.imgur.com/sskCQFE.png)


- Cuối cùng ta truy cập vào IP VIP để tiến hành cài đặt trang Wordpress: ```http://192.168.249.175```

![Imgur](https://i.imgur.com/sMdc0Eo.png)

![Imgur](https://i.imgur.com/ifoKiB8.png)


- Như vậy ta đã triển khai thành công một trang wordpress cso cơ sở dữ liệu trỏ tới cụm cluster. 



## Xử lý sự cố.

Trong khi ta triển khai wordpress có thể xảy ra nhiều lỗi, và khi đó ta cần kiểm tra và xem xét lỗi từ đâu để tìm hướng giải quyết

- Kiểm tra xem có thể ping tới VIP được không. 
- Kiểm tra xem các node có thể ping tới nhau được không
- Telnet đến port 3306 của VIP xem có được không
- Đặc biệt là phần grant quyền cho các user. Cần cấp cho user quyền truy cập từ localhost và từ bất kì máy chủ nào. vd

```
create database wordpress;
grant all privileges on wordpress.* to wp@'localhost' identified by 'Welcome123';
grant all privileges on wordpress.* to wp@'%' identified by 'Welcome123';
flush privileges;
exit
```

- Nếu grant cho bất kì máy chủ nào mà vẫn chưa được thì ta cần kiểm tra xem user ta tạo cho database đã có quyền chưa. 

```mysql -h 192.168.249.175 -u wp -p'Welcome123'``` 

Nếu không vào truy cập được thì tức là user từ VIP này chưa có quyền ta cần grant quyền cho VIP này

```
grant all privileges on wordpress.* to 'wp'@'node1' by identified 'Welcome123';
grant all privileges on wordpress.* to 'wp'@'node2' by identified 'welcome123';
```

