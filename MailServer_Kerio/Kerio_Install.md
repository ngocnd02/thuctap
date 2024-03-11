## Cài đặt mail server Kerio trên CentOS 7

### Chuẩn bị
Để cài đặt được Kerio ta cần tắt các dịch vụ có thể cản trở việc cài đặt như sau: 

- Tắt selinux

```
vi /etc/selinux/config/

SELINUX=disabled

```
- Tắt firewall

```
systemctl stop firewalld
systemctl disable firewalld
```

- Tắt Postfix

```
systemctl stop postfix
systemctl disable postfix
```

- Đổi hostname

```
hostnamectl set-host mail.nguyenducngoc.com
```

- Thêm thông tin trong file hosts

```
vi /etc/hosts

192.168.249.165 mail.nguyenducngoc.com mail
```

- Update lại hệ thống 

```
yum -y update
```

### Cài đặt mail server kerio

- Tải gói cài đặt

```
yum install kerio-connect-9.4.2-6498-linux-x86_64.rpm
```

- Tải về kerio

```
yum install kerio-connect-9.4.2-6498-linux-x86_64.rpm
```

- Sau khi cài đặt xong hãy truy cập vào trang quản trị Kerio tại: **https://<your-ip-add>:4040**

![Imgur](https://i.imgur.com/LUKE5lk.png)


- Thiết lập các cài đặt cho Kerio

![Imgur](https://i.imgur.com/8HP9byc.png)


![Imgur](https://i.imgur.com/zyFgCd4.png)


- Thiết lập mật khẩu cho tài khoản admin quản lý Kerio

![Imgur](https://i.imgur.com/pk78tYf.png)


- Chọn thư mục lưu trữ Kerio

![Imgur](https://i.imgur.com/0T68DTO.png)


- Nhập lincese, Nếu bạn có lincese bản quyền thì nhập lincense, không thì bạn hãy đăng ký dùng thử bản trial

![Imgur](https://i.imgur.com/9mNjxnE.png)


- Sau khi đăng kí bản trial thì Kerio sẽ gửi mã kích hoạt cho bạn về email mà bạn đã đăng kí, nhập mã kích hoạt đấy vào Kerio để hoàn tất cài đặt

![Imgur](https://i.imgur.com/bujaRnc.png)

![Imgur](https://i.imgur.com/Kl5pYVg.png)


- Sau khi cài đặt xong đăng nhập vào bằng tài khoản admin và mật khẩu là password mà bạn vừa đặt

![Imgur](https://i.imgur.com/aG0IJWa.png)


- Và cuối cùng đây là giao diện của mail server Kerio

![Imgur](https://i.imgur.com/TA8WsO4.png)