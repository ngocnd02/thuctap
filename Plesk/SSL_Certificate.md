## Cài đặt chứng chỉ SSL miễn phí từ Let's Encrypt

Chứng chỉ SSL nó là một loại chứng chỉ giúp nó mã hóa các thông tin trên những thiết bị hoặc các ứng dụng có hỗ trợ mã hóa này bằng chứng chỉ SSL.

Chứng chỉ SSL nó sẽ có hai phần gồm những phần Private Key và Public Key, trong đó Public Key nó sẽ được cài ở các ứng dụng đầu cuối mà trình duyệt hay các ứng dụng khác cũng có thể truy cập đọc được, còn Private Key nó sẽ được cài đặt ở các ứng dụng xử lý tiếp nhận dữ liệu.

Mục đích hoạt động của nó giống như chìa khóa để giúp giải mã những dữ liệu gửi đi từ thiết bị đầu cuối cũng đã được mã hóa thông qua Public Key rồi.

Nếu bạn muốn có chứng chỉ SSL thì bạn cũng phải đăng ký với những tổ chức xác thực như Comodo, GeoTrust, Symantec…với những chi phí nhất định, và chứng chỉ SSL nó cũng chia thành 3 loại như DV, OV hay EV còn tùy theo từng loại hình website của các bạn nữa.

Còn Let’s Encrypt nó là một tổ chức xác thực SSL giống như Comodo, GeoTrust, Symantec nhưng cái điểm khác đó là họ là tổ chức phi lợi nhuận được thành lập với sự bảo trợ của các tổ chức lớn trên thế giới Cisco, Akamai, Mozilla, Facebook…

Do đó, những chứng chỉ SSL Let’s Encrypt nó sẽ không khác gì với những loại chứng chỉ SSL khác mà nó chỉ khác ở chỗ bạn phải gia hạn mỗi 30 ngày một lần.

- Tại trang chủ của Plesk, vào **Websites & Domains** > **SSL/TLS Certificates**

![Imgur](https://i.imgur.com/esoL9aj.png)

- Chọn **Install** trong mục **Install a free basic certificate provided by Let's Encrypt**

![Imgur](https://i.imgur.com/9WE8sWz.png)

- Chọn các tùy chọn cài đặt SSL, và ấn **Get it free**

![Imgur](https://i.imgur.com/QTvpTtu.png)