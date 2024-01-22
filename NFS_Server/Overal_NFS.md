# TỔNG QUAN VỀ NETWORK FILE SYSTEM (NFS)
## NFS là gì?
- Hệ thống File Mạng (NFS) là một giao thức mạng để chia sẻ tệp phân tán. Hệ thống tệp định nghĩa cách dữ liệu dưới dạng tệp được lưu trữ và truy xuất từ các thiết bị lưu trữ, như ổ đĩa cứng, ổ đĩa thể rắn và ổ đĩa băng. NFS là một giao thức chia sẻ tệp trên mạng, đặt ra cách tệp được lưu trữ và truy xuất từ các thiết bị lưu trữ trên mạng.

- Giao thức NFS định nghĩa một hệ thống tệp mạng, ban đầu được phát triển để chia sẻ tệp cục bộ giữa các hệ thống Unix và được phát hành bởi Sun Microsystems vào năm 1984. Thông số kỹ thuật giao thức NFS được công bố lần đầu tiên bởi Tổ chức Nhiệm vụ Kỹ thuật Internet (IETF) như một giao thức Internet trong RFC 1094 vào năm 1989.

- NFS cho phép quản trị viên hệ thống chia sẻ toàn bộ hoặc một phần của hệ thống tệp trên một máy chủ mạng để làm cho nó có thể truy cập được từ xa bởi người dùng máy tính ở xa. Các máy khách có Quyền truy cập vào hệ thống tệp được chia sẻ có thể gắn kết các phần chia sẻ NFS, còn được biết đến là hệ thống tệp chia sẻ. NFS sử dụng Cuộc gọi Tiến trình Xa (Remote Procedure Calls-RPCs) để định tuyến yêu cầu giữa máy khách và máy chủ.

- NFS là một trong những giao thức phổ biến nhất cho các máy chủ tệp. Các triển khai NFS có sẵn cho hầu hết các hệ điều hành hiện đại, bao gồm các hệ điều hành sau:

	- Hewlett Packard Enterprise HP-UX
	- IBM AIX
	- Microsoft Windows
	- Linux
	- Oracle Solaris
- Các nhà cung cấp đám mây cũng triển khai giao thức NFS cho lưu trữ đám mây, bao gồm Amazon Elastic File System, các phần chia sẻ tệp NFS trong Microsoft Azure và Google Cloud Filestore.

- Bất kỳ thiết bị nào có thể kết nối với hệ thống tệp máy chủ NFS đều có thể được chia sẻ qua NFS. Điều này bao gồm ổ đĩa cứng, ổ đĩa thể rắn, ổ đĩa băng, máy in và các thiết bị ngoại vi khác. Người dùng có quyền truy cập thích hợp có thể truy cập tài nguyên từ máy khách của họ như là nếu những tài nguyên đó đã được gắn kết cục bộ.

- NFS là một giao thức tầng ứng dụng, có nghĩa là nó có thể hoạt động qua bất kỳ giao thức hoặc bộ giao thức mạng nào. Tuy nhiên, trong hầu hết các trường hợp, NFS được triển khai trên các hệ thống chạy bộ giao thức TCP/IP. Mục đích ban đầu của NFS là tạo ra một giao thức đơn giản và không lưu trạng thái để chia sẻ hệ thống tệp phân tán.

- Các phiên bản sớm của NFS sử dụng Giao thức User Datagram Protocl (UDP) cho tầng vận chuyển của nó. Điều này loại bỏ cần phải định nghĩa một giao thức lưu trạng thái; tuy nhiên, NFS hiện nay hỗ trợ cả Giao thức Kiểm soát Truyền (TCP) và UDP. Hỗ trợ cho TCP như một giao thức tầng vận chuyển đã được thêm vào NFS phiên bản 3 (NFSv3) vào năm 1995.

## Cách NFS hoạt động
- NFS là một giao thức máy khách-máy chủ. Một máy chủ NFS là một máy chủ đáp ứng các yêu cầu sau:
	- Đã cài đặt phần mềm máy chủ NFS.
	- Có ít nhất một kết nối mạng để chia sẻ tài nguyên NFS.
	- Được cấu hình để chấp nhận và đáp ứng yêu cầu NFS qua kết nối mạng.

- Một máy khách NFS là một máy khách đáp ứng các yêu cầu sau:
	- Đã cài đặt phần mềm máy khách NFS.
	- Có khả năng kết nối mạng đến một máy chủ NFS.
	- Được ủy quyền để truy cập tài nguyên trên máy chủ NFS.
	- Được cấu hình để gửi và nhận yêu cầu NFS qua kết nối mạng.

- Ban đầu, NFS được tạo ra như một phương pháp để chia sẻ hệ thống tệp giữa các nhóm làm việc sử dụng Unix. Nó vẫn thường được sử dụng để chia sẻ tài nguyên linh hoạt.

- Quá trình thiết lập dịch vụ NFS bao gồm ba bước sau, cho dù trên một máy chủ tệp doanh nghiệp hay trên một máy trạm cục bộ:
	- 1. Xác nhận rằng rpc.mountd hoặc chỉ là mountd đã được cài đặt và hoạt động. Đây là tiến trình NFS -- chương trình lắng nghe trên mạng để chờ yêu cầu NFS.

	- 2. Tạo hoặc chọn một thư mục chia sẻ trên máy chủ. Đây là điểm gắn kết NFS. Sử dụng điểm gắn kết và tên máy chủ hoặc địa chỉ để xác định một cách duy nhất tài nguyên NFS.

	- 3. Cấu hình quyền truy cập trên máy chủ NFS để cho phép người dùng được ủy quyền đọc, ghi và thực thi tệp trong hệ thống tệp.

- Việc thiết lập một máy khách NFS để truy cập một máy chủ NFS có thể được thực hiện bằng cách thủ công, sử dụng lệnh mount hoặc sử dụng một tệp cấu hình NFS -- /etc/exports. Mỗi dòng trong tệp cấu hình NFS chứa một điểm gắn kết, một địa chỉ IP hoặc tên miền máy chủ và bất kỳ siêu dữ liệu cấu hình nào cần thiết để truy cập hệ thống tệp.

## Phiên bản của NFS
Phiên bản NFS 4.2 (NFSv4.2) được phát hành vào tháng 11 năm 2016. NFSv4.2 được tài liệu trong RFC 7862. Nó thêm vào những tính năng và cập nhật mới sau đây:
- Tăng cường kiến trúc lưu trữ phân tán hiện đại;
- Hỗ trợ cho việc sao chép phía máy chủ, giúp tạo ra bản sao và bảo đảm ảnh chụp của các tệp bởi bất kỳ máy chủ lưu trữ NFSv4.2 nào;
- Đặt trữ lượng không gian để đảm bảo rằng một tệp sẽ có dung lượng lưu trữ sẵn có;
- Hỗ trợ cho các tệp rải rác, chứa các khối dữ liệu không gian lớn chứa giá trị zero, được chuyển tải dưới dạng zero khi đọc từ tệp;
- Hỗ trợ cho khối dữ liệu ứng dụng, xác định định dạng của một tệp;
- Hỗ trợ cho NFS có nhãn, hỗ trợ bảo mật bổ sung khi sử dụng với Security-Enhanced Linux.

## Lợi ích khi dùng NFS
Trong số nhiều lợi ích mà các tổ chức sử dụng NFS có thể đạt được, có những điểm sau:

1. **Chín chắn (Mature):** NFS là một giao thức chín chắn, điều này có nghĩa là hầu hết các khía cạnh của việc triển khai, bảo mật và sử dụng nó đều được hiểu rõ, cũng như các yếu điểm tiềm ẩn của nó.

2. **Mở (Open):** NFS là một giao thức mở, với sự phát triển liên tục được tài liệu trong các thông số kỹ thuật internet như một giao thức mạng miễn phí và mở.

3. **Hiệu quả chi phí (Cost-effective):** NFS là một giải pháp chi phí thấp cho việc chia sẻ tệp trên mạng, dễ thiết lập vì nó sử dụng cơ sở hạ tầng mạng hiện tại.

4. **Quản lý tập trung (Centrally managed):** Quản lý tập trung của NFS giảm thiểu cần thiết cho phần mềm và không gian đĩa trên các hệ thống người dùng cá nhân.

5. **Dễ sử dụng (User-friendly):** Giao thức này dễ sử dụng và cho phép người dùng truy cập các tệp từ xa trên các máy chủ từ xa một cách giống như cách họ truy cập các tệp địa phương.

6. **Phân phối (Distributed):** NFS có thể được sử dụng như một hệ thống tệp phân tán, giảm thiểu sự cần thiết của các thiết bị lưu trữ phương tiện di động.

7. **An toàn (Secure):** Với NFS, có ít phương tiện lưu trữ di động như CD, DVD, đĩa Blu-ray, đĩa mềm và ổ đĩa USB lưu thông, làm tăng tính an toàn của hệ thống.

## Nhược điểm khi dùng NFS
Một số nhược điểm của việc sử dụng NFS bao gồm những điểm sau:

1. **Phụ thuộc vào RPCs và Bảo mật (Dependence on RPCs and Insecurity):** Sự phụ thuộc vào Cuộc gọi Tiến trình Xa (RPCs) khiến NFS có tính không an toàn theo bản chất và nên chỉ được sử dụng trên một mạng đáng tin cậy đằng sau một tường lửa. Nếu không, NFS sẽ trở nên dễ bị tổn thương trước các mối đe dọa từ internet.

2. **Giới hạn băng thông và Khả năng mở rộng (Limited Bandwidth and Scalability):** Một số đánh giá về NFSv4 và NFSv4.1 chỉ ra rằng những phiên bản này có băng thông và khả năng mở rộng hạn chế và NFS có thể giảm tốc độ trong lưu lượng mạng nặng. Vấn đề về băng thông và khả năng mở rộng được cho là đã được cải thiện với NFSv4.2.