# Backup and Restore in Kerio

## Backup
### Cấu hình backup trong Kerio Connect
- Bạn có thể sao lưu các mục sau trong Kerio Connect:
	- Hộp thư người dùng

	- Thư mục công cộng

	- Danh sách gửi thư

	- Tệp cấu hình

	- Giấy phép

	- Chứng chỉ SSL

	- Cơ sở dữ liệu SpamAssassin

- Bạn có thể sử dụng bất kỳ đĩa cứng di động hoặc mạng nào để lưu trữ các bản sao lưu.

- Cấu hình sao lưu trong mục **Configuration > Archiving and Backup.**

### Các loại backup
- Kerio Connect hỗ trợ **Full backup** lưu trữ tất cả các tệp và mục, và cũng hỗ trợ **Differential backup** lưu trữ các tệp đã được thêm mới hoặc thay đổi kể từ lần sao lưu đầy đủ cuối cùng.

- Bạn có thể lên lịch bất kỳ số lượng sao lưu đầy đủ và chênh lệch nào bằng cách xem xét các yếu tố sau:

1. Kích thước của kho dữ liệu. Kích thước ảnh hưởng đến thời gian mỗi sao lưu mất và kích thước của nó.

2. Quan trọng của dữ liệu. Khi giao tiếp qua email và lưu trữ tin nhắn quan trọng đối với công ty của bạn, hãy lên lịch sao lưu thường xuyên hơn.

![Imgur](https://i.imgur.com/8QuUQb4.png)

### Thực hiện backup
- Trước khi ta thực hiện backup ta vào một tài khoản email bất kì để kiểm tra dữ liệu để sau khi thực hiện backup và xóa các email đi sau đó restore xem dữ liệu đó có còn giữ nguyên không. 

![Imgur](https://i.imgur.com/8S5NdK4.png)


- 1.Trong giao diện quản trị, điều hướng đến **Configuration > Archiving and Backup > Backup.**

- 2.Tích chọn **Enable message store and configuration recovery backup**.

![Imgur](https://i.imgur.com/wtQC9HZ.png)


- Nhấn **Add**.

- Nhập mô tả cho bản sao lưu.

- Chọn thời gian và loại bản sao lưu, sau đó nhấn OK.

![Imgur](https://i.imgur.com/okmgY78.png)


- Lặp lại các bước 3-5 để thêm các bản sao lưu khác.

- Nhấn **Advanced** và chỉ định kích thước tối đa và số lượng bản sao lưu. Nhấn OK.

![Imgur](https://i.imgur.com/hOcOouK.png)

- Trong phần Target backup directory, chỉ định thư mục để lưu trữ tất cả các bản sao lưu. Nếu ổ đĩa mạng yêu cầu xác thực, nhấn Specify và nhập tên người dùng và mật khẩu (chỉ áp dụng cho Microsoft Windows).

**LƯU Ý:** Không được phép sử dụng ký tự đặc biệt trong tên thư mục.

- Trong phần Notification, nhập địa chỉ email của bạn để nhận thông báo về bản sao lưu.

- Nhấn Apply.

- Nếu bạn muốn tạo một bản sao lưu đầy đủ ngay lập tức, độc lập với các bản sao lưu khác, nhấn nút Start Now.

![Imgur](https://i.imgur.com/lEp5I35.png)


- Sau đó ta vào máy chủ theo đường dẫn **cd /opt/kerio/mailserver/store/backup** sẽ thấy 1 file backup được tạo

![Imgur](https://i.imgur.com/qDvpHqm.png)


- Sau đó ta vào email trên và xóa tất các các  tin nhắn đã gửi đi đi.

![Imgur](https://i.imgur.com/b8ducOP.png)


## Restore
- Để khôi phục dữ liệu sao lưu, sử dụng công cụ đặc biệt là Kerio Connect Recover. Công cụ này trích xuất dữ liệu đã sao lưu và lưu dữ liệu tại các vị trí ban đầu của chúng.

Để khởi chạy công cụ Kerio Connect Recover:

- Dừng Kerio Connect:

```
systemctl stop kerio-connect
```

- Vào thư mục Kerio Connect

```
cd /opt/kerio/mailserver
```

- Thực hiện câu lệnh sau để restore lại dữ liệu: 

```
./kmsrecover /opt/kerio/mailserver/store/backup
```

![Imgur](https://i.imgur.com/RtskAnm.png)


- Như vậy là đã restore thành công, sau đó ta vào lại email ở trên và thấy tất cả các email được gửi đi đã quay trở lại

![Imgur](https://i.imgur.com/tNVcNQt.png)



