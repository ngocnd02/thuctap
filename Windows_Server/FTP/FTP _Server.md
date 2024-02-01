# TỔNG QUAN VỀ FTP SERVER
## Định nghĩa
- Máy chủ giao thức truyền tệp- File transfer protocol server (thường được biết đến là Máy chủ FTP) là phần mềm máy tính giúp tạo điều kiện cho việc trao đổi tệp tin an toàn qua mạng TCP/IP. Nó chạy giao thức truyền tệp (FTP), một giao thức truyền thông tiêu chuẩn hoạt động ở cấp độ mạng, để thiết lập kết nối an toàn giữa các thiết bị trong kiến trúc máy khách-máy chủ và truyền dữ liệu hiệu quả qua internet.

## Hoạt động của FTP server
Máy chủ FTP là các giải pháp phần mềm được sử dụng để truyền tệp tin qua internet. Chúng chủ yếu được sử dụng cho hai chức năng quan trọng, "Đưa" và "Nhận." Nó cho phép tải lên (Đưa) các tệp tin lên máy chủ từ thiết bị máy khách và tải xuống (Nhận) các tệp tin từ máy chủ xuống thiết bị máy khách. Máy chủ FTP giúp thực hiện các chức năng sau đây.

1. **Truyền đổi Tệp Tin Kích Thước Lớn:** Các tổ chức thường gặp khó khăn khi chia sẻ các tệp tin lớn qua email. Các doanh nghiệp xử lý lượng dữ liệu lớn thường gặp gián đoạn trong quá trình chia sẻ tệp tin do tệp tin lớn. Máy chủ FTP cho phép tổ chức chia sẻ các tệp tin lớn một cách dễ dàng.

2. **Nâng Cao An Toàn:** Mục đích quan trọng nhất của việc sử dụng máy chủ FTP là đảm bảo mức độ an toàn cao khi gửi dữ liệu nhạy cảm qua mạng. Máy chủ FTP cũng hỗ trợ các loại giao thức truyền tệp an toàn khác như Giao thức Truyền Tệp SSH (SFTP) và FTP An Toàn (FTPS) để thêm một lớp bảo mật khác. Các giao thức này đảm bảo mã hóa end-to-end hiệu quả để bảo vệ tệp tin trong quá trình truyền.

3. **Tối Ưu Hóa Quy Trình Làm Việc:** Máy chủ FTP giúp doanh nghiệp tối ưu hóa quá trình chia sẻ tệp tin để vượt qua các thách thức về năng suất. Với ứng dụng phần mềm đúng, người dùng có thể chia sẻ lượng lớn dữ liệu thay vì chia sẻ một tệp tin mỗi lần. Việc lưu trữ tệp tin tập trung giảm thiểu thời gian cần để tìm kiếm một tệp tin, và việc truyền theo lịch trình giúp tránh gặp sự chậm trễ hoặc gián đoạn trong quy trình làm việc.

4. **Tăng Cường Kiểm Soát:** Máy chủ FTP giúp doanh nghiệp thực hiện kiểm soát lớn hơn đối với dữ liệu của họ bằng cách cung cấp kiểm soát truy cập thông minh. Vì mỗi người dùng cần các quyền khác nhau để truy cập các tệp tin khác nhau, các quản trị viên có thể dễ dàng xác định ai có thể chỉnh sửa, tải lên, tải xuống hoặc chia sẻ tệp tin dựa trên các quyền hạn.

5. **Khôi Phục Dữ Liệu Đáng Tin Cậy:** Một máy chủ FTP hiệu quả đảm bảo dữ liệu và tệp tin của tổ chức không bị đe dọa hoặc mất đi trong trường hợp thảm họa. Sao lưu liên tục và tự động giúp lưu trữ dữ liệu một cách chủ động tại các địa điểm khác nhau để dễ dàng khôi phục khi cần thiết.

## Phân loại 
Dưới đây là các loại FTP phổ biến:
- FTP (File Transfer Protocol): Là phiên bản cơ bản của giao thức truyền tệp, hoạt động ở cấp độ mạng để chuyển tệp tin qua internet.

- FTP Secure (FTPS): Đưa bảo mật lên một bậc so với FTP truyền thống, FTP An Toàn (FTPS) đảm bảo việc truyền tệp an toàn. Nó cung cấp một lớp mã hóa bổ sung sử dụng giao thức Secure Sockets Layer (SSL) hoặc Transport Layer Security (TLS) trong quá trình truyền dữ liệu qua mạng.

- SSH File Transfer Protocol (SFTP): Đây là một hệ thống truyền tệp an toàn cho giao thức Secure Shell (SSH). SFTP là một phương pháp được sử dụng rộng rãi để truyền tệp an toàn qua các hệ thống từ xa. Trong SFTP, cả dữ liệu và lệnh đều được mã hóa và truyền đi trong các gói nhị phân được định dạng cụ thể thông qua một kết nối đơn được bảo mật sử dụng SSH.

## FTP active vs.passive
Phiên FTP thường có hai kênh, kênh lệnh (điều khiển) và kênh dữ liệu. Trong khi kênh lệnh được sử dụng để truyền lệnh thì kênh dữ liệu được sử dụng để truyền dữ liệu. Quản trị viên có thể đặt máy chủ FTP ở hai chế độ, chế độ active và chế độ passive.

**Chế độ active**
- Đây là chế độ mặc định cho FTP ban đầu và nhiều máy chủ vẫn hỗ trợ chế độ này. Ở chế độ này, máy khách FTP tạo kết nối điều khiển; tuy nhiên, tất cả các kết nối dữ liệu đều được khởi tạo từ máy chủ đến máy khách FTP.

- Chế độ active hoạt động trong trường hợp không có tường lửa hoặc yêu cầu tường lửa hiểu giao thức FTP để tự động mở các cổng giữa máy khách và máy chủ.

- Nó được gọi là chế độ active vì máy khách tự động mở một cổng và lắng nghe trong khi máy chủ tích cực kết nối với cổng đó. Nó chỉ được khuyến nghị khi việc triển khai kế thừa yêu cầu.

**Chế độ thụ động**
- Cả kết nối dữ liệu và điều khiển đều được khởi tạo từ máy khách FTP đến máy chủ FTP ở chế độ này.Nó còn được gọi là chế độ "thân thiện với tường lửa" vì nó hoạt động trong môi trường có sẵn tường lửa cần thiết.

- Nó được gọi là chế độ thụ động vì máy chủ mở một cổng và lắng nghe một cách thụ động, cho phép máy khách kết nối với cổng đó.Chế độ thụ động được khuyên dùng để truyền tệp vì các kết nối ở chế độ này an toàn và đáng tin cậy hơn vì kết nối dữ liệu được kích hoạt từ máy khách FTP đến máy chủ FTP.

- Khác với chế độ active, yêu cầu cấu hình nhiều tường lửa, chế độ passive chỉ yêu cầu cấu hình tường lửa trên máy chủ..

## FPT vs. cloud storage
FTP và cloud đều là cách chia sẻ tệp và dữ liệu và có những điểm tương đồng và khác biệt đáng kể. Trong khi FTP cho phép chuyển tệp giữa các thiết bị qua mạng, cloud giúp truy cập dữ liệu đã lưu trữ và một loạt các dịch vụ, bao gồm tính toán, mạng, và nhiều hơn nữa, được lưu trữ trên internet thông qua trình duyệt web hoặc một ứng dụng trên máy tính. Một số điểm khác nhau quan trọng giữa FTP và lưu trữ trên cloud bao gồm:

1. **Khả Năng Truy Cập:**
- Truy cập tệp và thư mục trong một cài đặt FTP đòi hỏi việc sử dụng một trình khách FTP và thiết lập các quyền cần thiết để truy cập máy chủ.
- Truy cập dữ liệu lưu trữ trên cloud thường chỉ đòi hỏi một trình duyệt web hoặc một ứng dụng mà không cần tài khoản người dùng và mật khẩu. Tuy nhiên, mặc dù không phải là một yêu cầu, bạn vẫn có thể lưu trữ dữ liệu trong cloud với bảo mật qua mật khẩu.

2. **Bảo Mật:**
- Bảo mật là một vấn đề đối với các tổ chức sử dụng FTP. Có các trường hợp về lỗ hổng tường lửa vì một kết nối FTP đòi hỏi mở các cổng bổ sung để có khả năng truy cập đầy đủ. Các tổ chức muốn chia sẻ tệp với người khác có thể phải mở rộng quyền truy cập vào hạ tầng của họ, làm tăng rủi ro an ninh đối với máy chủ vật lý. Hơn nữa, thiếu khả năng theo dõi tạo ra nhiều lỗ hổng, vì không có cách nào để kiểm tra ai đã truy cập thông tin gì. Cuối cùng, tổ chức có thể cần một chuyên gia Công nghệ thông tin để định kỳ sao lưu ảnh máy chủ đến một địa điểm khác.
- Ngược lại, các dịch vụ cloud đã tiến xa với các điều khiển bảo mật linh hoạt để giảm thiểu rủi ro và lỗ hổng an ninh mạng.
