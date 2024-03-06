# Cài đặt chứng chỉ SSL cho Zimbra
## Đăng kí chứng chỉ
- Bạn có thể truy cập vào trang **https://www.ssls.com** để đăng kí lấy 1 chứng chỉ SSL

![Imgur](https://i.imgur.com/RdEFwvd.png)

- Chọn 1 chứng chỉ và đăng kí dùng thử

![Imgur](https://i.imgur.com/YnNh3rB.png)

- Chọn **ACTIVE**

![Imgur](https://i.imgur.com/fUnau8E.png)

- Nhập tên miền mà bạn muốn đăng kí chứng chỉ SSL

![Imgur](https://i.imgur.com/Kngnspx.png)


- Chọn **Use my CSR**, và copy dòng lệnh được tạo ra 

![Imgur](https://i.imgur.com/7gdZbNC.png)


- Chạy đoạn lệnh ở trên ở máy server

![Imgur](https://i.imgur.com/78PHLrP.png)


- Copy đoạn **BEGIN CERTIFICATE REQUEST** vào phần **ENTER CSR** trên trình duyệt vầ ấn **ONWARDS**

![Imgur](https://i.imgur.com/a7loAfa.png)


- Chọn **Create a DNS record**

![Imgur](https://i.imgur.com/gGFY2Nu.png)


- Sau đó tạo 1 bản ghi CNAME theo mẫu:

![Imgur](https://i.imgur.com/9t55Hm7.png)


- Tiếp theo tải chứng chỉ về 

![Imgur](https://i.imgur.com/Nbuev04.png)


- Chứng chỉ tải về sau khi được giải nén: 

![Imgur](https://i.imgur.com/LERspXk.png)


## Cài đặt chứng chỉ

- Tại **/opt/zimbra/ssl/zimbra/commercial/**
- Tạo một file **commercial.crt** 
- Mở file STAR.mail.baotrung.xyz.crt, lấy nội dung trong đó và dán vào file commercial.crt vừa tạo. 

![Imgur](https://i.imgur.com/N8rPkA8.png)

- Tạo tiếp một file **commercial_ca.crt** và copy nội dung chứng chỉ từ file STAR.mail.baotrung.xyz.ca-bundle vào

```
vi commercial_ca.crt
```

![Imgur](https://i.imgur.com/l46YbR1.png


- Tiếp tục tạo một file **commercial.key**. Lấy nội dung của khóa private mà được tạo ra trong file **STAR_mail_baotrung_xyz.pem** từ đường dẫn /opt/zimbra/STAR_mail_baotrung_xyz.pem và copy vào file commercial.key. 

```
vi commercial.key
```

![Imgur](https://i.imgur.com/rxbnHyf.png)

## Xác thực chứng chỉ
- Câu lệnh: 

```
chown zimbra:zimbra * -R
su zimbra
/opt/zimbra/bin/zmcertmgr verifycrt comm
```

![Imgur](https://i.imgur.com/oa7570W.png)


- Deloy chứng chỉ: 

```
/opt/zimbra/bin/zmcertmgr deploycrt comm commercial.crt ./commercial_ca.crt
```

![Imgur](https://i.imgur.com/EvoJ2Jc.png)

- Khởi động lại Zimbra

```
zmcontrol restart
```

- Kiểm tra chứng chỉ 

[Imgur](https://i.imgur.com/WcExaqZ.png)

