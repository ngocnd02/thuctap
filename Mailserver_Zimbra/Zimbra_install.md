# Cài đặt Mail Server Zimbra trên Centos 7
## Bước 1: Cập nhật các bản ghi
- Để có thể cài đặt được Zimbra trước tiên ta cần trỏ bản ghi tên miền để phục vụ cho việc gửi và nhận email

![Imgur](https://i.imgur.com/WY811CR.png)

![Imgur](https://i.imgur.com/WTYhekr.png)


## Bước 2: Kiểm tra và cập nhật hệ thống 
- Đầu tiên bạn cần kiểm tra xem SELINUX xem có hoạt động hay không, nếu đang bật thì bạn phải tắt đi. 

- Câu lệnh kiểm tra trạng thái SELINUX :
```
sestatus
```
- Nếu SELINUX đang hoạt động bạn cần tắt nó đi. 

```
vi /etc/selinux/config

SELINUX=disabled
```

**Thực hiện stop postfix và remove postfix**
Postfix là một phầm mềm nguồn mở được dùng để gửi mail (Mail Transfer Agent-MTA). Được phát hành bởi IBM với mục tiêu thay thế trình gửi mail phổ biến là sendmail. Nó được trang bị trên hệ điều hành do đó bạn hãy xoá bỏ để sử dụng dịch vụ riêng của Zimbra.

```systemctl stop postfix
   yum remove postfix
```

**Thực hiện tắt firewall**
```
systemctl stop firewalld
systemctl disable firewalled
```

**Cập nhật hệ thống**
```
yum -y update 

reboot
```

## Bước 3: Kiểm tra và set hostname
Bạn thực hiện kiểm tra hostname hiện tại và set lại hostname cho đúng yêu cầu để có thể cài đặt được zimbra. 
- Lệnh kiểm tra: 
```
hostnamectl
```

- Lệnh đặt lại hostname
```
hostnamectl set-hostname mail.baotrung.xyz
```

Thêm hostname vào file hosts
- Câu lệnh: 
```
vi /etc/hosts

103.159.51.229 mail.baotrung.xyz
```

## Bước 4: Cài đặt Zimbra
- Đầu tiên cần cài đặt các công cụ cần thiết

```
yum install unzip net-tools sysstat openssh-clients perl-core libaio nmap-ncat libstdc++.so.6 wget -y
```

- Bước tiếp theo bạn cần Download Zimbra và cài đặt. Và bạn cần tạo một thư mục zimbra để cài vào đó.

```
mkdir zimbra && cd zimbra
wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-8.8.15_GA_3869.RHEL7_64.20190918004220.tgz --no-check-certificate
```

- Sau khi download về hoàn tất bạn tiến hành giải nén file ra

```
tar zxpvf zcs*.tgz
```

- Truy cập vào thư mục vừa giải nén và chạy lệnh ./install

```
cd zcs* && ./install.sh\
```

**Tùy chọn các cài đặt như sau: 
```
Do you agree with the terms of the software license agreement? [N] y
Use Zimbra's package repository [Y] y
Importing Zimbra GPG key
Configuring package repository
Checking for installable packages
Found zimbra-core (local)
Found zimbra-ldap (local)
Found zimbra-logger (local)
Found zimbra-mta (local)
Found zimbra-dnscache (local)
Found zimbra-snmp (local)
Found zimbra-store (local)
Found zimbra-apache (local)
Found zimbra-spell (local)
Found zimbra-memcached (repo)
Found zimbra-proxy (local)
Found zimbra-drive (repo)
Found zimbra-imapd (local)
Found zimbra-patch (repo)
Select the packages to install
Install zimbra-ldap [Y] y
Install zimbra-logger [Y] y
Install zimbra-mta [Y] y
Install zimbra-dnscache [Y] y
Install zimbra-snmp [Y] y
Install zimbra-store [Y] y
Install zimbra-apache [Y] y
Install zimbra-spell [Y] y
Install zimbra-memcached [Y] y
Install zimbra-proxy [Y] y
Install zimbra-drive [Y] y
Install zimbra-imapd (BETA - for evaluation only) [N] y
Install zimbra-chat [Y] y
Checking required space for zimbra-core
Checking space for zimbra-store
Checking required packages for zimbra-store
zimbra-store package check complete.
```
- Thay đổi domain:

![Imgur](https://i.imgur.com/FfdFTOi.png)

- Thiết lập mật khẩu cho admin:

![Imgur](https://i.imgur.com/sBPzIZ9.png)

![Imgur](https://i.imgur.com/6tyNEeY.png)

![Imgur](https://i.imgur.com/PU0lOQH.png)

![Imgur](https://i.imgur.com/1FvIU3B.png)


- Sau khi ta cài đặt xong hãy truy cập vào tên miền **https://mail.baotrung.xyz:7071/zimbraAdmin** để vào trang quản trị

![Imgur](https://i.imgur.com/ArobyjE.png)


- Với tài khoản mặc định là admin, và mật khẩu chính là mật khẩu bạn vừa thiết lập ở bên trên.

![Imgur](https://i.imgur.com/zB280y0.png)
