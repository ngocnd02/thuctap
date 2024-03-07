## Thay đổi logo trong zimbra

- Logo trước khi thay đổi: 

![Imgur](https://i.imgur.com/LC4CYUi.png)

- Để có thể thay đổi logo ta ssh vào máy chủ và tiến hành các bước như sau: 

**1.Tạo thư mục chứa logo ta muốn thay đổi**

- Chúng ta truy cập vào đường dẫn : /opt/zimbra/jetty/webapps/zimbra/ và tạo một thư mục mới là logos

```
mkdir /opt/zimbra/jetty/webapps/zimbra/logos
```

**2.Upload logo mà ta muốn thay đổi vào thư mục mà ta vừa tạo ra**

- Ở đây ta có thể dùng WinSCP để upload logo lên máy server của ta

![Imgur](https://i.imgur.com/JJfXKSQ.png)


- Phân quyền cho file logo vừa upload

```
chown zimbra:zimbra logo.png
```


**3.Thực hiện thay đổi logo**

```
su zimbra
zmprov md nguyenducngoc.com zimbraSkinLogoURL /logos/logo.png
zmprov md nguyenducngoc.com zimbraSkinLogoLoginBanner /logos/logo.png
zmprov md nguyenducngoc.com zimbraSkinLogoAppBanner /logos/logozimbra.png
```

- Sau đó thực hiện restart lại mail server

```
zmcontrol restart
```

- Như vậy chúng ta đã thay đổi logo thành công và bây giờ hãy vào web quản trị để xem sự thay đổi

![Imgur](https://i.imgur.com/W8i9RXt.png)