## Chỉnh sưa quota account email trong Zimbra

- Một "account quota" là giới hạn lưu trữ được phép cho một tài khoản. Những tin nhắn email, tệp đính kèm, danh bạ, cuộc hẹn lịch, công việc và tệp tin trong Briefcase đều đóng góp vào giới hạn này. Quota tài khoản có thể được thiết lập bởi COS (Class of Service - Lớp Dịch vụ) hoặc cho từng tài khoản cụ thể. Khi giới hạn quota được đạt đến, tất cả các email gửi đến tài khoản đó sẽ bị từ chối.

- Tại web admin, tại **Home >> Management Account**

![Imgur](https://i.imgur.com/LHHFTYt.png)

- Chọn tài khoản muốn thiết lập quota

![Imgur](https://i.imgur.com/cktorXO.png)

- Vào **Advanced >> quotas**

![Imgur](https://i.imgur.com/21P3plm.png)

Trong đó: 
- **Limit user-specified forwarding addresses field to (chars)**: giới hạn địa chỉ chuyển tiếp theo người dùng trong phạm vi (ký tự)

- **Maximum number of user-cpecified forwarding addresses**: số lượng tối đa các địa chỉ chuyển tiếp theo người dùng

- **Account quota**: Giới hạn kích thước hộp thư tính bằng megabyte ( MB). Đây là giới hạn dung lượng ổ đĩa được chỉ định mà một tài khoản có thể sử dụng trên máy chủ hộp thư. Khi hộp thư đạt đến giới hạn được chỉ định, tin nhắn sẽ không thể gửi được. Mặc định là 0, có nghĩa là không giới hạn. Điều này có nghĩa là người dùng có thể sử dụng tất cả dung lượng ổ đĩa trên máy chủ.

- **Maximum number of contacts allowed in address book:** Số lượng mục nhập tối đa mà người dùng có thể có trong danh sách liên hệ cá nhân của họ. Mặc định là 10.000.

- **Percentage threshold for quota warning message (%):** Phần trăm ngưỡng của giới hạn quota mà cần đạt trước khi thông báo cảnh báo được gửi. Mặc định là một ngày.

- **Minimum duration of time between quota warnings**: Tần suất mà thông báo cảnh báo giới hạn quota nên được gửi.

- **Quota warning message template**: Hộp văn bản này chứa nội dung của thông điệp được gửi khi giới hạn quota gần đạt tới. Bạn có thể thêm thông tin bổ sung.