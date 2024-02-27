## Cron Jobs
- Cron Jobs là các tác vụ được lên lịch mà hệ thống chạy vào những thời điểm hoặc khoảng thời gian được xác định trước. Thông thường, một cron job chứa một loạt các tác vụ đơn giản mà hệ thống chạy từ một tập lệnh.

- **Chú ý**: Hãy cẩn thận khi bạn lên lịch các công việc cron. Chúng tôi khuyên bạn để đủ thời gian giữa các công việc cron để công việc cron trước đó có thể hoàn thành. Nếu bạn lên lịch chúng để chạy quá thường xuyên, máy chủ có thể bắt đầu một công việc cron mới trước khi công việc cron trước kia kết thúc. Sự trùng lặp này có thể làm giảm hiệu suất.

### Cron Email
Phần Email Cron trong giao diện cho phép bạn nhập địa chỉ email để hệ thống gửi thông báo khi các công việc cron của bạn chạy. Để đặt địa chỉ email, thực hiện các bước sau:

1. Trong ô văn bản Email, nhập địa chỉ email mà bạn muốn nhận thông báo.
2. Nhấp vào nút Cập nhật Email.

![Imgur](https://i.imgur.com/GDtaLGK.png)

**Disable email notifications**
- Để tắt thông báo qua email cho tất cả các công việc cron, hãy xóa địa chỉ email.

- Để tắt thông báo qua email cho một công việc cron cụ thể, thực hiện các bước sau:

1. Định vị công việc cron mà bạn muốn tắt thông báo qua email trong bảng Công Việc Cron Hiện Tại và nhấp vào Chỉnh sửa.
2. Trong ô văn bản Lệnh, thêm dòng /dev/null 2>&1 vào cuối lệnh. Ví dụ:
```
   /usr/local/cpanel/bin/is_script_stuck /dev/null 2>&1
```
3. Lưu các thay đổi của bạn.

### Add a Cron Job
- Để tiến hành tạo một Cron Job, vào ""Home >> Advance >> Cron Jobs** sau đó thực hiện các bước sau:

1. Chọn khoảng thời gian mà bạn muốn chạy công việc cron từ các menu tương ứng hoặc nhập các giá trị vào các ô văn bản.

   - Common Setting — Chọn một khoảng thời gian phổ biến. Hệ thống sẽ cấu hình các thiết lập phù hợp trong các ô văn bản Phút, Giờ, Ngày, Tháng và Ngày trong Tuần cho bạn.

   - Minute — Số phút giữa mỗi lần công việc cron chạy, hoặc phút của mỗi giờ mà bạn muốn chạy công việc cron.

   - Hour — Số giờ giữa mỗi lần công việc cron chạy, hoặc giờ của mỗi ngày mà bạn muốn chạy công việc cron.

   - Day — Số ngày giữa mỗi lần công việc cron chạy, hoặc ngày trong tháng mà bạn muốn chạy công việc cron.

   - Month — Số tháng giữa mỗi lần công việc cron chạy, hoặc tháng trong năm mà bạn muốn chạy công việc cron.

   - Weekend — Các ngày trong tuần mà bạn muốn chạy công việc cron.

2. Trong ô văn bản Lệnh, nhập lệnh mà bạn muốn hệ thống thực hiện.

![Imgur](https://i.imgur.com/Nh3ePLj.png)

**Lưu ý**
- Bạn phải chỉ định các thiết lập cho các ô văn bản Phút, Giờ, Ngày, Tháng, Ngày Trong Tuần, và Lệnh.

- Hãy cẩn thận cực kỳ khi sử dụng lệnh rm trong một công việc cron. Nếu bạn không khai báo các tùy chọn đúng, có thể xóa dữ liệu trong thư mục home của bạn.

- Nếu công việc cron của bạn chạy một tập lệnh tùy chỉnh, tập lệnh đó cần có quyền thực thi. 

### Xem các công việc cron hiện tại
Bảng Công Việc Cron Hiện Tại hiển thị các công việc cron hiện tại của bạn.

![Imgur](https://i.imgur.com/iJGLMQi.png)

### Chỉnh sửa một công việc cron
Để chỉnh sửa một công việc cron, thực hiện các bước sau:

1. Định vị công việc cron mà bạn muốn chỉnh sửa và nhấp vào **Edit**.
2. Chỉnh sửa các thiết lập mà bạn muốn thay đổi và nhấp vào **Edit line**.

### Xóa một công việc cron
Để xóa một công việc cron, thực hiện các bước sau:

1. Nhấp vào **Delete** bên cạnh công việc cron mà bạn muốn xóa.
2. Nhấp vào Xóa.
