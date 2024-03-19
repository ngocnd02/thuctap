# Tìm hiểu về Load balancing server với HAproxy

## Khái quát về HAproxy
HAproxy (High Available proxy) là ứng dụng cân bằng tải với khả năng mở rộng cao, được cài đặt cho những website chạy các ứng dụng dựa trên TCP và HTTP, được phát triển trên hệ điều hành Linux. Nó hỗ trợ chuyển mạch ngữ cảnh (content switching) cho phép người quản trị webiste có thể thiết đặt các luật chuyển mạch trong file cấu hình. HAproxy cũng hỗ trợ nhiều thuật toán phân tải phong phú, hỗ trợ cài đặt cookie và health check. HAproxy hỗ trợ cài đặt một số thuật toán LB như round robin, weighted round robin, least connection, source,… HAproxy là ứng dụng chạy độc lập. Để sử dụng HAproxy thiết lập hệ thống cân bằng tải, cần cài đặt Haproxy lên một máy chủ và thiết lập cài đặt trong file cấu hình.

### Tính năng của HAProxy

![Imgur](https://i.imgur.com/o7xgWRE.png)

HAProxy bao gồm các tính năng như:
	- Hỗ trợ cân bằng tải ở lớp 4 và lớp 7 (tương ứng với TCP và HTTP).

	- Support HTTP protocol, HTTP / 2, gRPC, FastCGI.

	- Chấm dứt SSL / TLS.

	- Lưu trữ chứng chỉ SSL động.

	- Chuyển đổi nội dung và kiểm tra.

	- Ủy quyền minh bạch.

	- Ghi nhật ký chi tiết.

	- CLI.

	- Xác thực HTTP.

	- Đa luồng.

	- Rewrite URL.

	- Kiểm tra sức khỏe nâng cao.

	- Giới hạn tần số kết nối.

### File cấu hình haproxy.cfg
File cấu hình HAproxy là nơi lưu trữ các cấu hình cho hệ thống HAproxy. Khi chạy chương trình cân bằng tải, máy chủ HAproxy sẽ đọc file cấu hình này và thực hiệu điều khiển hệ thống cân bằng tải. Đây cũng là nơi quản trị viện có thể cấu hình cho hệ thống cân bằng tải, bằng cách thay đổi các tham số được HAproxy quy định. Cấu hình của Haprox thường gồm 4 phần chính: global, defaults, fontend và backend. Các thành phần này sẽ định nghĩa cách máy chủ HAproxy tiếp nhận, xử lý yêu cầu, chọn máy chủ tiếp nhận yêu cầu và chuyển tiếp.


**Global**

Các thiết lập global nằm ở phần đầu của file cấu hình haproxy.cfg, được định danh bằng từ khóa global và chỉ được định nghĩa riêng một mình, quy định các thiết lập bảo mật, điều chỉnh hiệu năng… cho toàn hệ thống HAproxy. Một số tham số quan trọng được đặt trong global như số lượng kết nối tối đa (maxconn), đường dẫn file log, số tiến trình… Ví dụ về phần global của file cấu hình haproxy.cfg

```/etc/haproxy/haproxy.cfg```

![Imgur](https://i.imgur.com/0KPcKTY.png)

**Default**

Defaults chứa các cấu hình được thiết lập áp dụng chung cho cả phần frontend và backend trong file cấu hình. Các thiết lập defaults có thể được thiết lập nhiều lần trong file cấu hình và chúng được ghi đè lên nhau (các mục defaults sau sẽ đè lên các mục defaults trước nó), ngược lại các thiết lập trong frontend và backend sẽ đè lên defaults.

![Imgur](https://i.imgur.com/f4bgzue.png)


### Các loại cân bằng tải (Load Balancing)

**Không có cân bằng tải (No Load Balancing)**

- Đây là dạng cơ bản nhất cho một ứng dụng web, thường được sử dụng trong môi trường số lượng người dùng ít hoặc không có để test, dev.

không cân bằng tải
Mô hình về không có cân bằng tải

![Imgur](https://i.imgur.com/5ilBTGt.png)


Với mô hình này, người dùng sẽ kết nối trực tiếp với web server tại (yourdoamain.com) mà không sử dụng cân bằng tải. Nếu web server gặp sự cố, trục trặc thì người dùng sẽ không kết nối được đến ứng dụng web.

**Cân bằng tải tại tầng 4 (Layer 4 Load Balancing)**

Việc sử dụng cân bằng tải ở tầng 4 (Layer 4 Load Balancing) để có thể cân bằng tải tới nhiều server. Thì các request sẽ được điều hướng dựa trên địa chỉ IP và port. Ví dụ có một request đến http://example.com/something sẽ được điều hướng tới backend được dùng để điều hướng cho doamin example.com với port 80.

![Imgur](https://i.imgur.com/uVTUKQ8.png)



**Cân bằng tải tại tầng 7 (Layer 7 Load Balancing)**

Đây là cân bằng tải phức tạp nhất nhưng có nhiều tùy biến. Với việc sử dụng cân bằng tải tại tầng 7, bạn có thể điều hướng các request dựa trên thông tin và nội dung của request đó. Cân bằng tải tầng 7 với nhiều backend có thể dùng một domain và port.

![Imgur](https://i.imgur.com/5V8XOho.png)