## Cài đặt web server

- Ở bài LAB trước chúng ta đã thực hiện việc cài đặt Web Server sử dụng LAMP và Worpress. Có thể xem lại tại [đây](https://github.com/ngocnd02/thuctap/blob/main/Web_Server/Thuc_hien_LAP.md)

- Mặc định sau khi cài đặt xong web server thì toàn bộ code mã nguồn của trang web sẽ nằm tại thư mục **/var/www/html/**. Nhưng nếu bây giờ chúng ta không muốn chúng nằm ở thư mục này, mà chúng ta muốn nó nằm ở thư mục khác ví dụ như /web/www thì sao. 

### Các bước giải quyết. 
- Tạo 1 thư mục mới trên Centos: 

```mkdir -p /web/www```

- Sau đó, ta copy toàn bộ mã nguồn từ /var/www/html/ sang thư mục chúng ta vừa tạo ở trên: 

```cp -r /var/www/html/* /web/www/```

- Tiếp theo, ta cấp quyền cho thư mục mới để có thể có quyền truy cập

```chown -R apache:apache /web/www/*```

- Tiếp đó, chúng ta phải sửa cấu hình, thay đổi đường dẫn của thư mục mặc định bằng đường dẫn thư mục chúng ta vừa tạo trong file httpd.conf. Dùng vi để mở thư mục

```vi /etc/httpd/conf/httpd.conf```

- Chúng ta thay thế các đường dẫn đến mã nguồn mới như sau: 

![Imgur](https://i.imgur.com/0kkyJOI.png)

- Sau đó, chúng ta khởi động lại dịch vụ:

```systemctl restart httpd```

- LƯU Ý: Nếu centos của bạn đang bật SELinx thì chúng ta phải tắt dịch vụ bảo mật này đi

```setenforce 0```

- Lúc này ta truy cập vào trang web để kiểm tra, ta có vào trang info.php để kiểm tra xem đúng là đường dẫn đã thay đổi được chưa.

![Imgur](https://i.imgur.com/78EXlLq.png)

![Imgur](https://i.imgur.com/Ca0xvIz.png)


## Các triển khai nhiều trang web trên một web server

- Đầu tiên, chúng ta tạo một file cấu hình Vhots cho website của chúng ta trong thư mục **/etc/httpd/conf.d/

```vi website01.conf```

- Sau đó,thêm cấu hình Vhots như sau: 

```
<VirtualHost *:80>
    ServerName www.website01.com
    DocumentRoot /web/website01
    ServerAlias website01.com
    ErrorLog /web/website01/error.log
    CustomLog /web/website01/requests.log combined
</VirtualHost>
```

- Tiếp theo, tạo thư mục để chứa mã nguồn cho trang web như đã cấu hình ở trên: làm tương tự như khi ta triển khai web-server theo link ở trên.

```mkdir /web/website01```

- Sau đó, ta tiến hành copy mã nguồn để xây dựng trang web vào thư mục /web/website01

```cp -r ~/wordpress/* /web/website01/```

```mkdir /web/website01/wp-content/uploads```

```chown -R apache:apache /web/website01/*```

- Sau đó, ta tạo tài khoản database cho website của chúng ta trên giao diện của phpAdmin

![Imgur](https://i.imgur.com/UK2GHkh.png)

- Tiếp theo cấu hình trang web: 

```cd /web/website01/```

```cp wp-config-sample.php wp-config.php```

```vi wp-config.php```

![Imgur](https://i.imgur.com/PIU0tkB.png)

- Sau đó ta khởi động lại dịch vụ web

```systemctl restart httpd```

- Sau đó ta tiến hành nhập tên miền **www.website01.com** vào để cấu hình trang web

![Imgur](https://i.imgur.com/lV7ou4S.png)

![Imgur](https://i.imgur.com/38AHPxi.png)

![Imgur](https://i.imgur.com/rpn4cHb.png)


### Sau đó ta tiếp tục tiến hành tạo một website thứ hai
- Ta sẽ làm tương tự như đã làm với website01
- Đầu tiên ta cũng tạo một file cấu hình Vhosts cho website thứ 2 này trong thư mục **/etc/httpd/conf.d/

```vi website02.conf```

- Sau đó,thêm cấu hình Vhots như sau: 

```
<VirtualHost *:80>
    ServerName www.website02.com
    DocumentRoot /web/website02
    ServerAlias website02.com
    ErrorLog /web/website02/error.log
    CustomLog /web/website02/requests.log combined
</VirtualHost>
```
- Tiếp theo, tạo thư mục để chứa mã nguồn cho trang web như đã cấu hình ở trên: làm tương tự như khi ta triển khai web-server theo link ở trên.

```mkdir /web/website02```

- Sau đó, ta tiến hành copy mã nguồn để xây dựng trang web vào thư mục /web/website01

```cp -r ~/wordpress/* /web/website02/```

```mkdir /web/website02/wp-content/uploads```

```chown -R apache:apache /web/website02/*```

- Sau đó, ta tạo tài khoản database cho website của chúng ta trên giao diện của phpAdmin

![Imgur](https://i.imgur.com/Ws9oX6x.png)

- Tiếp theo cấu hình trang web: 

```cd /web/website02/```

```cp wp-config-sample.php wp-config.php```

```vi wp-config.php```

![Imgur](https://i.imgur.com/4hDLJd1.png)

- Sau đó ta khởi động lại dịch vụ web

```systemctl restart httpd```

- Sau đó ta tiến hành nhập tên miền **www.website02.com** vào để cấu hình trang web

![Imgur](https://i.imgur.com/PG7PS0e.png)

![Imgur](https://i.imgur.com/PuzvuWT.png)

![Imgur](https://i.imgur.com/FGyoUDC.png)

- Như vậy là ta đã tiến hành triển khai nhiều trang web trên 1 website xong.
