# Triển khai cài đặt web server trên windows server 2022

Để triển khai một webserver hoàn chỉnh trên windows server 2022 ta tiến hành cài đặt máy chủ web là IIS, cơ sở dữ liệu mysql, và ngôn ngữ lập trình PHP, cùng với wordpress là phương pháp phổ biến. 

## Cài đặt máy chủ web IIS
- Đầu tiên trên máy chủ web server, ta vào **Server Manager**.

![Imgur](https://i.imgur.com/1fsG9GS.png)

- Sau đó ta chọn **Add roles and features** để tiến hành cài đặt IIS

![Imgur](https://i.imgur.com/UVhArGL.png)

- Ta chọn phần **Web Server (IIS)**, và đồng ý cài đặt.

![Imgur](https://i.imgur.com/yv050pt.png)

- Sau khi cài đặt xong, ta sẽ có giao diện của máy chủ web như sau: 

![Imgur](https://i.imgur.com/UBkaHEq.png)

- Lúc này web server đã được cài đặt và hoạt động, ta thử truy cập bằng địa chỉ trên trình duyệt web để kiểm tra.

![Imgur](https://i.imgur.com/EFR4t48.png)

## Cài đặt cơ sở dữ liệu
- Ta tiến hành cài đặt CSDL, hiện nay có rất nhiều cơ sở dữ liệu được sử dụng như Microsoft SQL Server, mysql, mariadb. Và ở đây chúng ta chọn mysql làm cơ sở dữ liệu
- Đầu tiên hãy dowload mysql xuống để tiến hành cài đặt, có thể download tại [đây](https://dev.mysql.com/downloads/file/?id=526408)
- Sau khi tải xuống thành công ta tiến hành cài đặt. 

![Imgur](https://i.imgur.com/31yygzl.png)

Thiết lập mật khẩu cho CSDL

- Sau đó, ta tiến hành tạo cơ sở dữ liệu cho website chúng ta muốn triển khai, các thông tin cần tạo bao gồm tên cơ sở dữ liệu, tài khoảng và mật khẩu để quản lý cơ sở dữ liệu đó. 
- Trên windows server bạn có thể tải các phần mềm giao diện để quản lý mysql hoặc chúng ta có thể sử dụng bằng dòng lệnh. 
- ở đây, chúng ta sử dụng giao diện dòng lệnh với **MYSQL COMMAND LINE CLIENT** 
- Tạo CSDL:

```create database nhanhoa;```

Trong đó: nhanhoa là tên cơ sở dữ liệu bạn đặt

- Tạo người dùng:

```create user 'ngocnd'@'localhost' identified by 'ngoc2002';```

Trong đó **ngocnd** là tên người dùng, **ngoc2002** là mật khẩu. Và để cho phép người dùng truy cập từ mọi địa chỉ IP, có thể thay thế 'localhost' bằng '%'.

- Cấp quyền cho người dùng:

```grant all privileges on nhanhoa.* to 'ngocnd'@'localhost';```

- Sau đó để áp dụng các thay đổi quyền sử dụng lệnh: 

```FLUSH PRIVILEGES;```

![Imgur](https://i.imgur.com/1UNuMx4.png)


## Cài đặt PHP và PHP Manager
- Tải xuống php từ trang web để cài đặt, có thể tải tại [đây](https://windows.php.net/download#php-8.2). Lưu ý: Hãy chọn phiên bản ** x64 Non Thread Safe**
- Sau khi tải xong, ta tiến hành giải nén, và di chuyển đến ổ C và để ở chỗ nào đó bạn thích. 
- Tải xuống php manager, tại [đây](https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10)
- Sau đó, vào IIS. Lúc này ta đã thấy PHP Manager đã xuất hiện, chọn vào php manager

![Imgur](https://i.imgur.com/QyymTfP.png)

- Bấm chọn **Register new PHP version** để trở tới php mà ta vừa cài đặt, ta chọn file php.cgi trong thư mục của php

- Sau khi chọn xong, nếu thành công ta sẽ thấy phiên bản của php mà ta vừa cài đặt đã xuất hiện

![Imgur](https://i.imgur.com/9M4UC71.png)


## Cài đặt Wordpress
- WordPress là một hệ thống quản lý nội dung (CMS - Content Management System) mã nguồn mở được sử dụng phổ biến để xây dựng và quản lý các trang web và blog. 
- Ta có thể tải xuống Wordpress tại [đây](https://wordpress.org/)
- Sau đó ta giải nén thư mục wordpress đã tải xuống. 
- Ta tạo một thư mục trên ổ C để chứa mã nguồn dẫn tới trang web là: www/nhanhoa/
- Copy toàn bộ mã nguồn wordpress vào www/nhanhoa/
- Trong thư mục mã nguồn copy file wp-config-sample.php thành file wp-config.php và cấu hình file này. Cấu hình trong file này cơ sở dữ liệu mà ta vừa tạo cho trang web

![Imgur](https://i.imgur.com/sEOgP1n.png)

- Lúc này ta vào máy chủ web (IIS) để tạo một trang web mới ta muốn triển khai
- Chọn **Sites**, kích chuột phải chọn **Add website** và thêm thông tin về trang web ta muốn triển khai. 

![Imgur](https://i.imgur.com/AyAB3JF.png)

- Lúc này, ta đã cấu hình xong web server và bây giờ ta truy cập vào **www.nhanhoa.com** và cấu hình hoàn thiện trang web

![Imgur](https://i.imgur.com/UAkGpJf.png)

![Imgur](https://i.imgur.com/HAB87OH.png)

![Imgur](https://i.imgur.com/WDTHX4b.png)

