## Thay đổi mật khẩu của tài khoản admin trong Zimbra

Để thay đổi mật khẩu của tài khoản admin trong Zimbra, bạn có thể sử dụng lệnh zmprov, một công cụ dòng lệnh được cung cấp bởi Zimbra Collaboration Suite. Dưới đây là cách thực hiện:

- Đăng nhập vào dòng lệnh của máy chủ Zimbra

```
su zimbra
```

- Xem tất cả các user có quyền admin

```
zmprov gaaa
```

- Thay đổi mật khẩu mới với cú pháp như sau: 
```
zmprov sp <tên_người_dùng_admin> <mật_khẩu_mới>
```

Trong đó: 
	- <tên_người_dùng_admin> là tên người dùng của admin Zimbra.

	- <mật_khẩu_mới> là mật khẩu mới mà bạn muốn thiết lập.


![Imgur](https://i.imgur.com/bURmmTS.png)