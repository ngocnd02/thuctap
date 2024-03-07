## Tìm ID mailbox account trong email zimbra
- ID (Mailbox ID) trong Zimbra là một định danh duy nhất được gán cho mỗi tài khoản hộp thư trong hệ thống

- ID này được sử dụng để liên kết với dữ liệu liên quan đến tài khoản trong cơ sở dữ liệu của Zimbra. Nó giúp hệ thống xác định và quản lý thông tin của từng hộp thư.

- Mailbox ID là một phần quan trọng của quản lý hệ thống Zimbra. Nó được sử dụng trong các lệnh quản lý và truy vấn để thực hiện các tác vụ như sao lưu, khôi phục, quản lý quyền truy cập, và nhiều nhiệm vụ quản trị khác.

- Để lấy thông tin về ID mailbox ta dùng lệnh

```
zmprov getMailboxInfo <tên email>
```

```
su zimbra
zmprov getMailboxInfor trang@nguyenducngoc.com
```

![Imgur](https://i.imgur.com/wPIoawI.png)