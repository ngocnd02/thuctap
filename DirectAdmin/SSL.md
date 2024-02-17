## Certificate Installation Requirements

- Để sử dụng tính năng SSL, trang web của bạn phải có một địa chỉ IP tĩnh (cố định). Nếu bạn không có địa chỉ IP cố định, bạn sẽ nhận được thông báo lỗi khi truy cập menu SSL:

Could not execute your request
**Detail**: you are not allowed to modify your SSL

-Ở đây chúng ta sẽ sử dụng Let's Encrypt

## Cài đặt SSL Let's Encrypt
- Let's Encrypt là một tổ chức cung cấp chứng chỉ SSL/TLS miễn phí, tự động và mã nguồn mở. Chứng chỉ SSL/TLS được sử dụng để bảo vệ thông tin truyền tải qua internet giữa máy khách và máy chủ, đảm bảo tính bí mật và toàn vẹn của dữ liệu.

- Điểm độc đáo của Let's Encrypt là khả năng tự động hóa quá trình cài đặt và gia hạn chứng chỉ, giúp người quản trị web giảm bớt công việc thủ công và chi phí liên quan đến việc có được chứng chỉ SSL. Dịch vụ này được cung cấp miễn phí với mục tiêu là tạo ra một internet an toàn và bảo mật hơn.

- Để sử dụng Let's Encrypt, người quản trị chỉ cần thực hiện một số bước đơn giản để yêu cầu, xác minh và cài đặt chứng chỉ SSL/TLS cho trang web của họ. Nó đã trở thành một lựa chọn phổ biến trong cộng đồng web hosting và phát triển web nhờ tính tiện lợi và chi phí thấp.

- Let’s Encrypt sẽ không cung cấp chứng chỉ cho một địa chỉ IP trống. Nếu bạn cần một chứng chỉ EV, hoặc một chứng chỉ Wildcard, Let’s Encrypt không phải là một lựa chọn tốt. Lưu ý rằng Let’s Encrypt có thể tạo một chứng chỉ với tối đa 100 tên máy chủ lưu trữ, vì vậy có thể bạn không thực sự cần một Wildcard cho trường hợp sử dụng của mình, bạn chỉ cần có chứng chỉ bao gồm tất cả các tên miền phụ hiện có của bạn.

**CÀI ĐẶT SSL LET'S ENCRYPT TRÊN DA**
- Tại menu chính của User, chọn mục **SSL Certificates**

![Imgur](https://i.imgur.com/dbHiHXc.png)

- Chọn chứng chỉ Let's Encrypt và thiết lập chứng chỉ như sau: 

![Imgur](https://i.imgur.com/qnF0BR7.png)

- Sau đó ấn **save** và chờ xác nhận 
