## Kiểm tra log gửi và nhận trong Zimbra
- Việc kiểm tra log trong zimbra giúp ta biết được một email có được gửi thành công hay không. 

- Log của gửi và nhận mail trong Zimbra được lưu trữ tại **var/log/zimbra.log**

![Imgur](https://i.imgur.com/ZwQbptc.png)


- Mar 8 08:57:48 mail amavis[9172]: (09172-03) ls1V_aB8aPvl FWD from trang@baotrung.xyz -> chuong@baotrung.xyz, BODY=7BIT 250 2.0.0 from MTA(smtp:[127.0.0.1]:10030): 250 2.0.0 Ok: queued as CB3C4E0C1C:  Thông báo thư đã được chuyển thành công và được xếp hàng với id là CB3C4E0C1C

- Passed CLEAN: Thông báo rằng thư đã được quét và được xác nhận là sạch (không chứa malware hoặc virus).

- "Mar 8 08:57:48 mail postfix/smtp[16803]: B0406E0C13: to=chuong@baotrung.xyz, relay=127.0.0.1[127.0.0.1]:10026, delay=0.17, delays=0.01/0/0.01/0.15, dsn=2.0.0, status=sent (250 2.0.0 from MTA(smtp:[127.0.0.1]:10030): 250 2.0.0 Ok: queued as CB3C4E0C1C)" là dòng thông báo cho biết rằng thư đã được gửi thành công.

- Quá trình gửi mail được thực hiện như sau: Connect tới mailserver -> MTA kiểm tra địa chỉ người nhận -> Kiểm tra qua các rule filter, đánh giá spam, virus -> Xếp vào queue -> Gửi thư -> Xóa khỏi queue -> Thông báo "Message accepted for delivery"

- Quá trình nhận mail được thực hiện như sau: Chấp nhận kết nối từ email server gửi -> Kiểm tra qua các rule filter, đánh giá spam, virus -> Xếp vào queue -> Nhận thư và xóa khỏi queue -> Thông báo nhận thư