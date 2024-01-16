[DNS over TLS vs DNS over HTTPS](#dns-over-tls-vs-dns-over-https)
- [Tại sao DNS lại cần thêm lớp bảo mật](#tai-sao-dns-lai-can-them-lop-bao-mat)
- [DNS over TLS](#dns-over-tls)
- [DNS over HTTPS](#dns-over-https)
- [Điểm khác biệt giữa DNS qua TLS và DNS qua HTTPS](#diem-khac-biet-giua-dns-qua-tls-va-dns-qua-https)
- [So sánh DoT và DoH](#so-sanh-dot-va-doh)

# DNS over TLS vs DNS over HTTPS
Các truy vấn DNS được gửi ở dạng văn bản gốc, nghĩa là bất kỳ ai cũng có thể đọc được chúng. DNS qua HTTPS và DNS qua TLS mã hóa các truy vấn và phản hồi DNS để giữ cho trình duyệt của người dùng an toàn và riêng tư. Tuy nhiên, cả hai cách tiếp cận đều có ưu và nhược điểm.

## Tại sao DNS lại cần thêm lớp bảo mật
- DNS là danh bạ của Internet; Trình phân giải DNS dịch tên miền mà con người có thể đọc được thành địa chỉ IP mà máy có thể đọc được. Theo mặc định, các truy vấn và phản hồi DNS được gửi ở dạng văn bản gốc (thông qua UDP), nghĩa là chúng có thể được đọc bởi các mạng, ISP hoặc bất kỳ ai có thể giám sát quá trình truyền. Ngay cả khi một trang web sử dụng HTTPS, truy vấn DNS cần thiết để điều hướng đến trang web đó vẫn bị lộ.

- Sự thiếu riêng tư này có tác động rất lớn đến an ninh và trong một số trường hợp là cả nhân quyền; nếu các truy vấn DNS không riêng tư thì chính phủ sẽ dễ dàng kiểm duyệt Internet hơn và kẻ tấn công sẽ dễ dàng theo dõi hành vi trực tuyến của người dùng hơn.

![Imgur](https://i.imgur.com/hU7zx9p.png)

- Hãy coi một truy vấn DNS bình thường, không được mã hóa giống như một tấm bưu thiếp được gửi qua thư: bất kỳ ai xử lý thư đều có thể tình cờ nhìn thấy văn bản được viết ở mặt sau, vì vậy sẽ không khôn ngoan khi gửi một tấm bưu thiếp có nội dung nhạy cảm hoặc thông tin cá nhân.

- DNS qua TLS và DNS qua HTTPS là hai tiêu chuẩn được phát triển để mã hóa lưu lượng DNS văn bản gốc nhằm ngăn chặn các bên độc hại, nhà quảng cáo, ISP và những người khác có thể giải thích dữ liệu. Tiếp tục sự tương tự, các tiêu chuẩn này nhằm mục đích đặt một phong bì bao quanh tất cả các bưu thiếp được gửi qua đường bưu điện, để bất kỳ ai cũng có thể gửi bưu thiếp mà không phải lo lắng rằng ai đó đang rình mò xem họ đang làm gì.

![Imgur](https://i.imgur.com/OPkTGOI.png)

## DNS over TLS
- DNS over TLS, hay DoT, là một tiêu chuẩn để mã hóa các truy vấn DNS nhằm giữ chúng an toàn và riêng tư. DoT sử dụng cùng một giao thức bảo mật, TLS, mà các trang web HTTPS sử dụng để mã hóa và xác thực thông tin liên lạc. (TLS còn được gọi là "SSL.") DoT thêm mã hóa TLS lên trên giao thức gói dữ liệu người dùng (UDP), được sử dụng cho các truy vấn DNS. Ngoài ra, nó đảm bảo rằng các yêu cầu và phản hồi DNS không bị giả mạo hoặc giả mạo thông qua các cuộc tấn công trên đường đi.

## DNS over HTTPS
- DNS qua HTTPS hoặc DoH là một giải pháp thay thế cho DoT. Với DoH, các truy vấn và phản hồi DNS được mã hóa nhưng chúng được gửi qua giao thức HTTP hoặc HTTP/2 thay vì trực tiếp qua UDP. Giống như DoT, DoH đảm bảo rằng kẻ tấn công không thể giả mạo hoặc thay đổi lưu lượng DNS. Lưu lượng truy cập DoH trông giống như lưu lượng truy cập HTTPS khác – ví dụ: các tương tác thông thường do người dùng điều khiển với các trang web và ứng dụng web – từ quan điểm của quản trị viên mạng.

## Điểm khác biệt giữa DNS qua TLS và DNS qua HTTPS
DNS qua TLS (DoT) và DNS qua HTTPS (DoH) đều là các phương thức bảo mật để thực hiện truy vấn DNS, nhưng chúng có một số điểm khác biệt quan trọng. Dưới đây là những điểm đặc biệt giữa chúng:

Giao Thức Sử Dụng:
- DoT sử dụng giao thức Transport Layer Security (TLS) để mã hóa truy vấn DNS, thường sử dụng cổng 853.
DoH sử dụng giao thức Hypertext Transfer Protocol Secure (HTTPS) để chuyển đổi truy vấn DNS thành gói tin HTTPS, sử dụng cổng 443.

Cổng Sử Dụng:
- DoT thường sử dụng cổng 853 để truyền thông qua TLS.
- DoH thường sử dụng cổng 443, là cổng được sử dụng rộng rãi cho HTTPS, giúp vượt qua các hạn chế mạng.

Khả Năng Chống Chống Trở Lại:
- Cả DoT và DoH đều cung cấp khả năng chống chống trở lại, ngăn chặn tấn công trung man-in-the-middle và đảm bảo tính toàn vẹn của dữ liệu DNS trong quá trình truyền.

Triển Khai và Hỗ Trợ:
- Cả DoT và DoH đều đã được triển khai rộng rãi trên nhiều nền tảng, từ trình duyệt web đến ứng dụng DNS resolver.
DoH thường được tích hợp một cách nhanh chóng trong các trình duyệt web, trong khi DoT thường được cấu hình trực tiếp trên máy chủ DNS hoặc trình duyệt.

Chính Sách DNS và Quản Lý Địa Chỉ IP:
- DoT giữ nguyên chính sách DNS truyền thống và duy trì khả năng quản lý địa chỉ IP theo cách thông thường.
DoH có thể sử dụng cùng một địa chỉ IP cho nhiều dịch vụ trên cùng một máy chủ web, gây khó khăn trong việc quản lý và lọc theo địa chỉ IP.

Chấp Nhận Tính Bảo Mật của DNSSEC:
- Cả DoT và DoH đều có khả năng chấp nhận tính bảo mật của DNSSEC, nhưng sự triển khai có thể thay đổi theo từng máy chủ DNS và ứng dụng.

Hiệu Suất:
- Hiệu suất có thể thay đổi tùy thuộc vào cách triển khai cụ thể và tình trạng mạng, nhưng cả DoT và DoH đều thường cung cấp mức độ hiệu suất tương đương.

## So sánh DoT và DoH
- Từ quan điểm an ninh mạng, DoT được cho là tốt hơn. Nó cung cấp cho quản trị viên mạng khả năng giám sát và chặn các truy vấn DNS, điều này rất quan trọng để xác định và ngăn chặn lưu lượng độc hại. Trong khi đó, các truy vấn DoH bị ẩn trong lưu lượng HTTPS thông thường, nghĩa là chúng không thể dễ dàng bị chặn nếu không chặn tất cả các lưu lượng HTTPS khác.

- Tuy nhiên, từ góc độ quyền riêng tư, DoH được cho là thích hợp hơn. Với DoH, các truy vấn DNS được ẩn trong luồng lưu lượng HTTPS lớn hơn. Điều này khiến quản trị viên mạng ít bị hiển thị hơn nhưng cung cấp cho người dùng nhiều quyền riêng tư hơn.