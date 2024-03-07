# Thực hiện Backup và Restore trong Zimbra

## 1.Backup
Sao lưu hộp thư trên máy chủ địa chỉ thư điện tử thường xuyên có thể giúp bạn khôi phục dịch vụ email nhanh chóng nếu xảy ra một sự cố đột ngột. Bạn nên bao gồm việc sao lưu dữ liệu máy chủ Zimbra Collaboration trong quy trình sao lưu toàn hệ thống của bạn.

Trước khi sao lưu dữ liệu Zimbra Collaboration, tất cả các máy chủ phải được dừng. Để dừng máy chủ, sử dụng lệnh dòng lệnh CLI, `zmcontrol stop`. Sau khi sao lưu hoàn tất, để khởi động lại máy chủ, sử dụng `zmcontrol start`.

```
su zimbra
zmcontrol stop
```

Tạo bản sao lưu: 
- Đảm bảo rằng vị trí sao lưu có đủ dung lượng để chứa bản sao
- Tất cả thành phần mà Zimbra cần đều nằm trong thư mục chính, nên việc backup trong Zimbra được thực hiện bằng cách copy toàn bộ thư mục này sang 1 vị trí khác

```
cp -rp /opt/zimbra /mnt/zimbra_backup.$(date"7/3/2024")
```

## Restore

- Để khôi phục dữ liệu Zimbra Collaboration, Máy chủ phải được dừng trước khi khôi phục dữ liệu.

```
su zimbra
zmcontrol restore
```

- Bạn có thể di chuyển thư mục zimbra cũ tại /opt đi chỗ khác để đảm bảo sự an toàn. 

- Sau đó, chuyển bản backup zimbra vừa backup ở trên vào thư mục /opt và đặt tên là zimbra

```
cp -rp /mnt/zimbra_backup/ /opt
mv /opt/zimbra_backup /opt/zimbra
```

- Cài đặt lại zimbra

```
cd zcs-9.0.0_GA_1.RHEL7_64.20200411070311.tgz
./install.sh
```

- Khi có thông báo Do you wish to upgrade? [Y] thì nhập Y để đồng ý. Trình cài đặt sẽ xóa bỏ các gói hiện tại và cài đặt lại chúng, nó sẽ dừng dịch vụ Zimbra cũ và chạy với những file đã sao lưu

- Đặt lại quyền

```
chown -R zimbra:zimbra /opt/zimbra/store
chown -R zimbra:zimbra /opt/zimbra/index
/opt/zimbra/libexec/zmfixperms
```


