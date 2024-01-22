# Triển khai FPT server trên CentOS 7
## Giới thiệuu
- VSFTPD(Very Secure File Transport Protocol Daemon) là một FTP Server Stand Alone được phân phối bởi Red Hat Enterprise Linux .
Đây là phần mềm để tạo FTP Server với tốc độ nhanh, cấu hình đơn giản.

## Cài đặt FTP Server
### 1. Cài đặt vsftpd
- Cài đặt gói Vsftpd:
```# yum install vsftpd```

- Sau khi quá trình cài đặt hoàn tất, ta khởi động dịch vụ và cho phép nó khởi động cùng hệ thống.
```
#systemctl start vsftpd
#systemctl enable vsftpd
```
- Cấu hình tường lửa cho dịch vụ FTP và port 21:
```
#firewall-cmd --permanent --add-port=21/tcp
#firewall-cmd --permanent --add-service=ftp
#firewall-cmd --reload
```
### 2. Cấu hình vsftpd

- File cấu hình vsftpd nằm tại : /etc/vsftpd/vsftpd.conf

- Copy file cấu hình để backup.
```#cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.backup```

- Chỉnh sửa file cấu hình vsftpd.conf:
```#vi /etc/vsftpd/vsftpd.conf```

**FTP Access**: Ta không cho kết nối nặc danh, mà chỉ cho kết nối cục bộ vào FTP server
```
anonymous_enable=NO    // Không cho kết nối nặc danh 
local_enable=YES        // Cho phép kết nối cục bộ
```
**Enabling uploads**: Cho phép người dùng upload.
```write_enable=YES        //Cho phép người dùng nội bộ tải lên```

**Chroot**: kỹ thuật giữ người dùng trong thư mục của họ, không cho phép. Tại đây ta sẽ chroot tất cả user, ngoại trừ các user trong file /etc/vsftpd/chroot_list
```
chroot_local_user=YES
allow_writeable_chroot=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
```

**Giới hạn cổng kết nối cho FTP thụ động**: Giới hạn khoảng các cổng sử dụng cho FTP passive
```
pasv_min_port=30000
pasv_max_port=31000
```

**Giới hạn User được phép truy cập vào hệ thống**: Nếu muốn giới hạn các User local được đăng nhập vào hệ thống FTP server. Ta thêm vào các dòng sau. Khi đó, những User có trong file /etc/vsftpd/user_list mới được truy cập vào hệ thống.
```
userlist_enable=YES
userlist_file=/etc/vsftpd/user_list
userlist_deny=NO
```

### 3. Khởi động lại dịch vụ và cho phép các cổng FTP passive đi qua tường lửa
```
#systemctl restart vsftpd
#firewall-cmd --permanent --add-port=30000-31000/tcp
#firewall-cmd --reload
```
## Truy cập FTP Server
Để truy cập FTP server, ta cần 1 tài khoản local và được cấp quyền truy cập vào FTP server.

**1. Tạo user local**
- Tạo 1 local user là: ngocnd

# adduser ngocnd
# passwd ngocnd
Sau khi thêm xong thì thư mục mặc định của tài khoản này sẽ ở thư mục /home/ngocnd/

- Tạo một thư mục cho người dùng về thêm quyền: 
```
mkdir –p /home/ngocnd/ftp/upload
chmod 550 /home/ngocnd/ftp
chmod 750 /home/ngocnd/ftp/upload
chown –R testuser: /home/ngocnd/ftp
```

2. Cấp quyền truy cập đến FTP server
- Ta thêm user ngocnd vào file /etc/vsftpd/user_list để có thể truy cập vào server.

![Imgur](https://i.imgur.com/jMVZkbf.png)

- Thêm vào file /etc/vsftpd/chroot_list (Nếu bạn sử dụng trong file cấu hình)

- Sau đó khởi động lại dịch vụ 
```systemctl restart vsftpd```

3. Truy cập FTP server
Ở đây, ta sử dụng FileZilla để truy cập tới FTP server. Ta nhập địa chỉ IP của Server, username, password

![Imgur](https://i.imgur.com/zLfTF1b.png)
