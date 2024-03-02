## Cài đặt Wordpress trên OpenLiteSpeed
- Trước khi cài đặt wordpress chúng ta cần thiết lập các thông số trong openlitespeed để phù hợp khi cài đặt wp.

- Ta truy cập vào openlitespeed webgui

- Tại **Server Configuration >> Externa App** cấu hình mục Address thành: uds://tmp/lshttpd/lsphp74.sock

![Imgur](https://i.imgur.com/rXvzr87.png)

- Tại **Virtual Hosts >> Example >> General**. Chúng ta thay đổi document root nơi sẽ chứa mã nguồn của wordpress

![Imgur](https://i.imgur.com/p3KYdDB.png)

- Tại **Virtual Hosts >> Example >> Rewrite**

![Imgur](https://i.imgur.com/VNiHE9n.png)


- Tại **Virtual Hosts >> Example >> Context** xóa phần Static có URI là /protected

![Imgur](https://i.imgur.com/bGm57nm.png)

- Sau đó ta vào máy chủ tiến hành download mã nguồn của wordpress và tạo cơ sở dữ liệu. 

```
cd /usr/local/lsws/Example/html
wget http://wordpress.org/latest.tar.gz
tar -zxvf latest.tar.gz
chown -R nobody:nobody /usr/local/lsws/Example/html/wordpress/
```
Lưu ý: Nếu centos của bạn chưa cài wget thì hãy cài wget trước bằng câu lệnh: **yum install wget**

- Tiếp theo đó ta tạo cơ sở dữ liệu cho trang web

![Imgur](https://i.imgur.com/ySBWNWM.png)

- Khởi động lại dịch vụ web

```systemctl restart lsws```

- Sau đó ta vào trình duyệt và truy cập vào địa chỉ của máy chủ để cấu hình trang web

- Nhập thông tin cơ sở dữ liệu bạn vừa tạo ở trên

![Imgur](https://i.imgur.com/DK8eZWx.png)

- Thiết lập thông tin cho trang web của bạn

![Imgur](https://i.imgur.com/6UIlDDY.png)

- Như vậy ta đã cài đặt thành công wordpress

![Imgur](https://i.imgur.com/6UIlDDY.png)

![Imgur](https://i.imgur.com/TkGb4d8.png)
