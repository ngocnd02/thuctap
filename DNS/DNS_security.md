[DNS security](#dns-security)
- [Tại sao bảo mật DNS lại quan trọng](#tai-sao-bao-mat-dns-lai-quan-trong)
- [Những tấn công DNS phổ biến](#nhung-tan-cong-dns-pho-bien)
- [DNSSEC](#dnssec)
- [DNS firewall](#dns-filewall)

# DNS security
- Bảo mật DNS là biện pháp bảo vệ cơ sở hạ tầng DNS khỏi các cuộc tấn công mạng nhằm giữ cho cơ sở hạ tầng này hoạt động nhanh chóng và đáng tin cậy. Chiến lược bảo mật DNS hiệu quả kết hợp một số biện pháp phòng vệ chồng chéo, bao gồm thiết lập máy chủ DNS dự phòng, áp dụng các giao thức bảo mật như DNSSEC và yêu cầu ghi nhật ký DNS nghiêm ngặt.

## Tại sao bảo mật DNS lại quan trọng
- Giống như nhiều giao thức Internet, hệ thống DNS không được thiết kế chú trọng đến tính bảo mật và có một số hạn chế về thiết kế. Những hạn chế này, kết hợp với những tiến bộ trong công nghệ, khiến máy chủ DNS dễ bị tấn công trên phạm vi rộng, bao gồm giả mạo, khuếch đại, DoS (Từ chối dịch vụ) hoặc chặn thông tin cá nhân riêng tư. Và vì DNS là một phần không thể thiếu trong hầu hết các yêu cầu Internet nên nó có thể là mục tiêu hàng đầu cho các cuộc tấn công.

Ngoài ra, các cuộc tấn công DNS thường xuyên được triển khai cùng với các cuộc tấn công mạng khác để đánh lạc hướng các đội bảo mật khỏi mục tiêu thực sự. Một tổ chức cần có khả năng giảm thiểu nhanh chóng các cuộc tấn công DNS để không quá bận rộn xử lý các cuộc tấn công đồng thời thông qua các vectơ khác.

## Những tấn công DNS phổ biến
Những kẻ tấn công đã tìm ra một số cách để nhắm mục tiêu và khai thác các máy chủ DNS. Dưới đây là một số cuộc tấn công DNS phổ biến nhất:

- DNS spoofing/cache poisioning: Đây là cuộc tấn công trong đó dữ liệu DNS giả mạo được đưa vào bộ đệm của trình phân giải DNS, dẫn đến trình phân giải trả về địa chỉ IP không chính xác cho một miền. Thay vì truy cập đúng trang web, lưu lượng truy cập có thể được chuyển hướng đến một máy độc hại hoặc bất kỳ nơi nào khác mà kẻ tấn công mong muốn; thường thì đây sẽ là bản sao của trang gốc được sử dụng cho mục đích xấu như phát tán phần mềm độc hại hoặc thu thập thông tin đăng nhập.

- DNS tunneling: Cuộc tấn công này sử dụng các giao thức khác để tạo đường hầm thông qua các truy vấn và phản hồi DNS. Những kẻ tấn công có thể sử dụng SSH, TCP hoặc HTTP để chuyển phần mềm độc hại hoặc thông tin bị đánh cắp vào các truy vấn DNS mà hầu hết các tường lửa không phát hiện được.

- DNS hijacking: Trong việc chiếm quyền điều khiển DNS, kẻ tấn công chuyển hướng truy vấn đến một máy chủ tên miền khác. Điều này có thể được thực hiện bằng phần mềm độc hại hoặc bằng việc sửa đổi trái phép máy chủ DNS. Mặc dù kết quả tương tự như kết quả giả mạo DNS, nhưng đây là một cuộc tấn công khác về cơ bản vì nó nhắm mục tiêu vào bản ghi DNS của trang web trên máy chủ tên chứ không phải bộ đệm của trình phân giải.

![Imgur](https://i.imgur.com/A20DmyI.png)

- NXDOMAIN attack: Đây là một loại tấn công tràn DNS trong đó kẻ tấn công làm tràn ngập máy chủ DNS với các yêu cầu, yêu cầu các bản ghi không tồn tại nhằm cố gắng gây ra sự từ chối dịch vụ đối với lưu lượng truy cập hợp pháp. Điều này có thể được thực hiện bằng cách sử dụng các công cụ tấn công phức tạp có thể tự động tạo các tên miền phụ duy nhất cho mỗi yêu cầu. Các cuộc tấn công NXDOMAIN cũng có thể nhắm mục tiêu vào trình phân giải đệ quy với mục tiêu lấp đầy bộ đệm của trình phân giải bằng các yêu cầu rác.

- Phantom domain attack: Cuộc tấn công miền ảo có kết quả tương tự như cuộc tấn công NXDOMAIN vào trình phân giải DNS. Kẻ tấn công thiết lập một loạt các máy chủ miền 'ảo' phản hồi các yêu cầu rất chậm hoặc hoàn toàn không phản hồi. Sau đó, trình phân giải sẽ nhận được vô số yêu cầu đến các miền này và trình phân giải sẽ bị ràng buộc trong việc chờ phản hồi, dẫn đến hiệu suất chậm và bị từ chối dịch vụ.

- Random subdomain attack: Trong trường hợp này, kẻ tấn công gửi truy vấn DNS cho một số tên miền phụ ngẫu nhiên, không tồn tại của một trang web hợp pháp. Mục đích là tạo ra sự từ chối dịch vụ đối với máy chủ tên có thẩm quyền của miền, khiến không thể tra cứu trang web từ máy chủ tên. Là một tác dụng phụ, ISP phục vụ kẻ tấn công cũng có thể bị ảnh hưởng vì bộ đệm của trình phân giải đệ quy của họ sẽ chứa các yêu cầu xấu.

- Domain look-up attack: Những kẻ tấn công dàn dựng hình thức tấn công này bằng cách thiết lập các miền và trình phân giải đặc biệt để tạo kết nối TCP với các trình phân giải hợp pháp khác. Khi trình phân giải được nhắm mục tiêu gửi yêu cầu, các miền này sẽ gửi lại các luồng gói ngẫu nhiên chậm, làm tắc nghẽn tài nguyên của trình phân giải.

- Botnet based CPE attack: Các cuộc tấn công này được thực hiện bằng cách sử dụng thiết bị CPE (Thiết bị tại chỗ của khách hàng; đây là phần cứng do các nhà cung cấp dịch vụ cung cấp để khách hàng của họ sử dụng, chẳng hạn như modem, bộ định tuyến, hộp cáp, v.v.). Những kẻ tấn công xâm phạm CPE và các thiết bị trở thành một phần của mạng botnet, được sử dụng để thực hiện các cuộc tấn công tên miền phụ ngẫu nhiên chống lại một trang web hoặc tên miền.

## DNSSEC
- DNS Security Extentions (DNSSEC) là một giao thức bảo mật được tạo để giảm thiểu vấn đề này. DNSSEC bảo vệ khỏi các cuộc tấn công bằng cách ký dữ liệu kỹ thuật số để giúp đảm bảo tính hợp lệ của dữ liệu. Để đảm bảo tra cứu an toàn, việc ký kết phải diễn ra ở mọi cấp độ trong quy trình tra cứu DNS.
- Quá trình ký tên này tương tự như việc ai đó ký một văn bản pháp luật bằng bút; người đó ký bằng một chữ ký duy nhất mà không ai khác có thể tạo được và chuyên gia tòa án có thể xem chữ ký đó và xác minh rằng tài liệu đó có chữ ký của người đó. Những chữ ký số này đảm bảo rằng dữ liệu không bị giả mạo.
- DNSSEC triển khai chính sách ký kỹ thuật số phân cấp trên tất cả các lớp DNS. Ví dụ: trong trường hợp tra cứu 'google.com', máy chủ DNS gốc sẽ ký khóa cho máy chủ tên .COM và sau đó máy chủ tên .COM sẽ ký khóa cho máy chủ tên có thẩm quyền của google.com.
- Mặc dù tính bảo mật được cải thiện luôn được ưu tiên nhưng DNSSEC được thiết kế để tương thích ngược nhằm đảm bảo rằng việc tra cứu DNS truyền thống vẫn giải quyết chính xác, mặc dù không có biện pháp bảo mật bổ sung. DNSSEC được thiết kế để hoạt động với các biện pháp bảo mật khác như SSL/TLS như một phần của chiến lược bảo mật Internet toàn diện.
- DNSSEC tạo ra một tuyến tin cậy giữa cha mẹ và con cái đi đến tận vùng gốc. Chuỗi tin cậy này không thể bị xâm phạm ở bất kỳ lớp DNS nào, nếu không yêu cầu sẽ trở thành cơ hội cho một cuộc tấn công trên đường đi.
- Để đóng chuỗi tin cậy, bản thân vùng gốc cần phải được xác thực (được chứng minh là không bị giả mạo hoặc lừa đảo) và điều này thực sự được thực hiện bằng cách sử dụng sự can thiệp của con người. Điều thú vị là, trong cái được gọi là Lễ ký kết vùng gốc, các cá nhân được chọn từ khắp nơi trên thế giới gặp nhau để ký tập bản ghi tài nguyên DNSKEY gốc theo cách công khai và được kiểm toán.

## DNS firewall
Một tường lửa DNS là một giải pháp bảo mật giúp bảo vệ mạng và hệ thống khỏi nhiều mối đe dọa mạng bằng cách lọc và giám sát lưu lượng DNS. Nó hoạt động bằng cách phân tích các truy vấn và phản hồi DNS, cho phép tổ chức áp dụng chính sách bảo mật, chặn các miền độc hại và giảm thiểu các mối đe dọa tiềm ẩn. Dưới đây là các đặc điểm và khía cạnh quan trọng của tường lửa DNS:

Lọc Miền:
- Tường lửa DNS lọc các yêu cầu miền dựa trên các chính sách đã được định nghĩa trước. Nó duy trì một danh sách các miền độc hại đã biết và chặn quyền truy cập đến chúng, ngăn chặn người dùng kết nối đến các trang web có thể gây hại.

Tích Hợp Thông Tin Đối Phó:
- Tường lửa DNS thường tích hợp với các nguồn thông tin đối phó, đó là các cơ sở dữ liệu chứa thông tin về các miền độc hại đã biết, địa chỉ IP và các chỉ số của việc tấn công. Tích hợp này giúp tường lửa chặn truy cập đến các trang web liên quan đến mối đe dọa mạng.

Thực Hiện Chính Sách:
- Tổ chức có thể định nghĩa và thực hiện các chính sách về loại trang web mà người dùng có thể truy cập. Tường lửa DNS cho phép quản trị viên chặn các danh mục cụ thể của trang web, chẳng hạn như cờ bạc, nội dung cho người lớn hoặc mạng xã hội, để đảm bảo tuân thủ các yêu cầu bảo mật và tuân thủ quy định.

Bảo Vệ Chống Malware và Lừa Đảo:
- Tường lửa DNS giúp ngăn chặn nhiễm malware và tấn công lừa đảo bằng cách chặn quyền truy cập đến các trang web chứa nội dung độc hại. Chúng có thể xác định và chặn kết nối đến các máy chủ điều khiển và điều khiển được sử dụng bởi malware.

Phát Hiện Botnet:
- Tường lửa DNS có thể phát hiện và chặn giao tiếp với botnet bằng cách giám sát các truy vấn DNS phù hợp với các mô hình liên quan đến hoạt động botnet. Điều này giúp ngăn chặn các thiết bị bị nhiễm malware kết nối đến máy chủ điều khiển.

Phát Hiện Bất Thường:
- Một số tường lửa DNS sử dụng các kỹ thuật phát hiện bất thường để xác định các mô hình không bình thường trong lưu lượng DNS. Điều này có thể bao gồm sự gia tăng đột ngột trong yêu cầu từ một người dùng cụ thể hoặc hành vi không bình thường có thể biểu hiện một sự cố bảo mật.

Ghi Chép và Báo Cáo:
- Tường lửa DNS duy trì các bản ghi của các truy vấn và phản hồi DNS, có thể hữu ích để phân tích hoạt động mạng và xác định các sự cố bảo mật tiềm ẩn. Các tính năng báo cáo cung cấp cái nhìn tổng quan về các yêu cầu bị chặn và các sự kiện bảo mật.

Hỗ Trợ DNSSEC:
- Một số tường lửa DNS tiên tiến hỗ trợ DNS Security Extensions (DNSSEC), tăng cường tính an toàn của DNS bằng cách xác minh chữ ký số trên phản hồi DNS và ngăn chặn việc làm giả mạo DNS.

Danh Sách Trắng và Đen Tùy Chỉnh:
- Quản trị viên có thể tạo danh sách trắng và đen tùy chỉnh để cho phép hoặc chặn các miền cụ thể dựa trên yêu cầu tổ chức. Sự linh hoạt này giúp tổ chức điều chỉnh tường lửa DNS theo nhu cầu cụ thể của họ.

Tích Hợp với Hệ Sinh Thái An Toàn:
- Tường lửa DNS thường tích hợp với các hệ sinh thái an toàn tổng thể, chẳng hạn như các giải pháp SIEM (Quản lý Thông tin và Sự kiện An toàn) để cung cấp một cái nhìn tổng thể về các sự kiện an toàn trên mạng.

## Truy vấn DNS có riêng tư không
- Truy vấn DNS theo mặc định không được bảo vệ bởi tính riêng tư, vì thông tin về các truy vấn DNS có thể được ghi lại và theo dõi bởi cả người quản trị mạng và các bên thứ ba. Khi bạn thực hiện một truy vấn DNS thông qua máy chủ DNS, thông tin về truy vấn này có thể được lưu trữ trong các bản ghi log của máy chủ DNS đó.
- Tính riêng tư của truy vấn DNS có thể bị đặt ra thách thức, đặc biệt là khi thông tin này có thể bị thu thập và sử dụng cho các mục đích theo dõi, quảng cáo, hoặc theo dõi hành vi trực tuyến. Để cải thiện tính riêng tư trong truy vấn DNS, có một số biện pháp bạn có thể thực hiện:
	- DNS over HTTPS (DoH): Sử dụng DoH để mã hóa truy vấn DNS, giúp bảo vệ dữ liệu truy vấn khỏi việc theo dõi trên đường truyền mạng. DoH chuyển đổi truy vấn DNS thành dữ liệu HTTPS, sử dụng cổng 443.
	- DNS over TLS (DoT): Giống như DoH, DoT cũng mã hóa truy vấn DNS, nhưng nó sử dụng cổng 853 và truyền thông qua TLS (Transport Layer Security).
	- Private DNS Servers: Sử dụng máy chủ DNS riêng để giảm khả năng thu thập thông tin từ các nhà cung cấp dịch vụ internet (ISP). Một số tổ chức và dịch vụ cung cấp máy chủ DNS riêng với cam kết bảo vệ tính riêng tư.
	- DNSCrypt: Một công nghệ mã hóa khác để bảo vệ truy vấn DNS. DNSCrypt sử dụng mã hóa đối với cả truy vấn và phản hồi DNS.
	- Cài đặt Bảo Mật và Tùy Chỉnh Mức Độ Riêng Tư: Nếu có thể, bạn có thể cài đặt cấu hình bảo mật cao và tùy chỉnh cài đặt để giảm thiểu ghi log và lưu trữ thông tin truy vấn DNS.

Tuy nhiên, việc cải thiện tính riêng tư trong truy vấn DNS đôi khi là một sự đánh đổi với hiệu suất và tính tiện ích. Một số dịch vụ internet và tổ chức có thể theo dõi thông tin DNS để cung cấp dịch vụ tối ưu và bảo mật. Người dùng cần cân nhắc giữa tính riêng tư và hiệu suất khi triển khai các biện pháp bảo vệ riêng tư cho truy vấn DNS.