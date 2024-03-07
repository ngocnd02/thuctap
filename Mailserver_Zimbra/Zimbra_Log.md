## Kiểm tra log gửi và nhận trong Zimbra
- Việc kiểm tra log trong zimbra giúp ta biết được một email có được gửi thành công hay không. 

- Log của gửi và nhận mail trong Zimbra được lưu trữ tại **var/log/maillog**

![Imgur](https://i.imgur.com/2B1TaOZ.png)

- Quá trình gửi mail được thực hiện như sau: Connect tới mailserver -> MTA kiểm tra địa chỉ người nhận -> Kiểm tra qua các rule filter, đánh giá spam, virus -> Xếp vào queue -> Gửi thư -> Xóa khỏi queue -> Thông báo "Message accepted for delivery"

Quá trình nhận mail được thực hiện như sau: Chấp nhận kết nối từ email server gửi -> Kiểm tra qua các rule filter, đánh giá spam, virus -> Xếp vào queue -> Nhận thư và xóa khỏi queue -> Thông báo nhận thư