### Kiểm tra xem bạn đang sử dụng web server gì 
- Câu lệnh: 

```
lsof -i :80
```
- Câu lệnh này sẽ hiển thị các tiến trình đang lắng nghe trên cổng 80 (hoặc cổng bạn quan tâm) và thông tin chi tiết, bao gồm tên của ứng dụng hoặc dịch vụ đang sử dụng cổng đó.

- Nếu bạn không thể tìm thấy thông tin bằng cổng 80, bạn có thể thay thế nó bằng cổng khác mà web server của bạn đang sử dụng.

![Imgur](https://i.imgur.com/C3cFYRU.png)

- Như ví dụ trên ta thấy trên cổng 80 có litespeed đang hoạt động, như vậy web server ta đang chạy là Litespeed.

### Câu lệnh kiểm tra xem web server của bạn đang chạy trên cổng bao nhiêu
- Ở đây chúng ta sử dụng công cụ **netstat**
- Câu lệnh: 

```
netstat -tupln | grep openlitespeed
```

![Imgur](https://i.imgur.com/9Me4c1F.png)

Trong đó: 
- netstat: Hiển thị trạng thái của các kết nối mạng, cổng và các dịch vụ đang lắng nghe.

-tupln: Chỉ hiển thị các kết nối TCP (-t), hiển thị thông tin về quyền sở hữu và ID quy trình (-u và -p), hiển thị số cổng trong dạng số (-n), và hiển thị tên của dịch vụ đang lắng nghe (-l).

- grep openlitespeed: Lọc kết quả để chỉ hiển thị các dòng có chứa từ "openlitespeed".

### Kiểm tra xem dịch vụ web đang tắt hay hoạt động

- Dùng câu lệnh sau:

```
systemctl status lsws
```

![Imgur](https://i.imgur.com/AyQttHI.png)

- Câu lệnh này sẽ hiển thị trạng thái hoạt động của openlitespeed


### Xem log

- Để xem được log của web server chạy bằng openlitspeed ta dùng câu lệnh sau: 

```
less /usr/local/lsws/logs/error.log
```

![Imgur](https://i.imgur.com/9K6qiom.png)

- Nếu bạn muốn xem log truy cập bạn có thể thay thế bằng access.log

### Cơ sở dữ liệu
- Câu lệnh xem bạn đang dùng loại cơ sở dữ liệu gì

```
mysql --version
```

