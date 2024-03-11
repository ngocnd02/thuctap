# So sánh Imap và Pop3

## IMAP vs POP3: Tổng quan
- Internet Mail Access Protocol (IMAP) là một giao thức email cho phép truy cập email từ bất kỳ thiết bị nào. IMAP không tải xuống hoặc lưu trữ nội dung email vào thiết bị. Thay vào đó, người dùng đọc tin nhắn của mình bằng cách sử dụng dịch vụ email.

!

- Ngược lại, Post Office Protocol version 3 (POP3) là phiên bản thứ ba của một giao thức email, tải xuống tất cả email mới vào thiết bị đầu cuối và xóa chúng khỏi dịch vụ email. Sau khi được tải xuống, email chỉ có thể được truy cập từ thiết bị đầu cuối cụ thể, trừ khi cài đặt được sửa đổi bởi quản trị viên máy chủ.

## IMAP là gì?
- IMAP được ưa chuộng bởi người dùng cần truy cập email từ nhiều thiết bị khác nhau. IMAP không tải xuống hoặc lưu trữ email trên thiết bị của người dùng. Thay vào đó, người dùng đọc email trực tiếp từ dịch vụ email. Điều này cho phép người dùng kiểm tra email từ nhiều thiết bị ở mọi nơi trên thế giới, bao gồm điện thoại thông minh, máy tính, hoặc thậm chí các thiết bị truy cập tạm thời (như laptop của đồng nghiệp).

- Trong IMAP, email thường chỉ được tải xuống khi người dùng "mở" nó. Các tệp đính kèm cũng không được tải tự động, giữ nguyên băng thông internet và công suất xử lý trên thiết bị của người dùng. Điều này mang lại trải nghiệm nhanh chóng và mượt mà cho người dùng khi họ kiểm tra tin nhắn của mình.

## POP3 là gì?
- POP3 hoạt động bằng cách thiết lập kết nối với dịch vụ email và tải xuống tất cả email mới vào thiết bị đầu cuối. Sau khi quá trình tải xuống hoàn tất, thông thường email sẽ bị xóa khỏi dịch vụ trừ khi quản trị viên thay đổi cấu hình để ngăn chặn điều này.

- Về cơ bản, sau khi đã tải xuống, những email cụ thể đó chỉ có thể được truy cập trên cùng một thiết bị đầu cuối. Kết nối với dịch vụ email từ một thiết bị đầu cuối khác sẽ có nghĩa là không thể truy cập vào các thông điệp đã được tải xuống trước đó trên thiết bị mới, trừ khi máy chủ được cấu hình cụ thể để giữ lại bản sao của các thông điệp.

- Khi người dùng gửi một email qua POP3, nó cũng được lưu trữ cục bộ trên thiết bị đầu cuối của họ, và dịch vụ email không giữ lại một bản sao (trừ khi được cấu hình để làm như vậy).

## So sánh IMAP và POP3
IMAP và POP3 là các giao thức email được sử dụng để truy cập và quản lý email trên các máy chủ từ xa. IMAP cho phép quản lý và đồng bộ hóa email một cách nâng cao trên nhiều thiết bị, trong khi POP3 thích hợp hơn cho các cấu hình mà email cần được truy cập chỉ từ một thiết bị duy nhất.

### Lịch sử
**IMAP**
- IMAP được tạo ra tại Đại học Stanford vào những năm 1980. "Cha đẻ của IMAP," Mark Crispin, sau đó chuyển đến Đại học Washington và đóng góp hơn 20 năm công việc vào các đặc tả và thực hiện tham chiếu của IMAP. Đặc tả IMAP được tạo ra dưới dạng Yêu cầu Ý kiến (RFC), về cơ bản là một bản ghi giải thích cách triển khai của giao thức được chấp nhận như một tiêu chuẩn bởi Tổ chức Công nghiệp Mạng (IETF).

- Các sửa đổi thường được thực hiện trên RFC để đảm bảo rõ ràng và cập nhật được truyền đạt một cách rõ ràng, và các RFC quan trọng nhất đối với IMAP là RFC 3501 (2003) và RFC 9051 (2021). Nói cách khác, giao thức phổ biến được sử dụng ngày nay bởi các ứng dụng email hàng đầu để đồng bộ hóa tin nhắn đã có 20 năm tuổi.

- IMAP có lợi thế rõ ràng hơn so với POP về mặt đồng bộ hóa vì mục đích ban đầu của nó là làm một lựa chọn tốt hơn cho POP. Mục tiêu thiết kế của nó là cho phép thao tác trên hộp thư từ xa như chúng đang ở địa phương.

- POP hoạt động bằng cách tải email xuống thiết bị cục bộ và xóa nó khỏi máy chủ, làm cho quản lý email trên nhiều thiết bị trở nên khó khăn. Điều này không phải là một vấn đề khi máy tính còn được sử dụng chung (nghĩ về chia sẻ thời gian). Tuy nhiên, khi máy tính cá nhân trở nên phổ biến hơn, IMAP trở nên ngày càng cần thiết.

- Không có hồ sơ nào về phiên bản đầu tiên của IMAP tồn tại nữa, và phiên bản đầu tiên trở thành một tiêu chuẩn tính toán chấp nhận là IMAP2, phát hành vào năm 1988.

- Phiên bản này của IMAP hoạt động "trực tuyến," có nghĩa là nó yêu cầu ứng dụng email phải được kết nối với máy chủ trong khi người dùng xem hoặc sửa đổi tin nhắn của họ. Không thể đồng bộ hóa bản sao của hộp thư cục bộ và cập nhật nó khi máy địa phương kết nối lại với máy chủ. Điều này là do email được xác định bằng số "thứ tự," thiếu tính liên tục qua các phiên làm việc của người dùng.

- Tuy nhiên, khi internet qua điện thoại đường dây trở nên phổ biến, người dùng cần một cách để kiểm tra email mà không cần sử dụng liên tục đường dây điện thoại của họ. Đó là khi hỗ trợ cho các hoạt động IMAP4 "ngoại tuyến" được giới thiệu vào năm 1994. Với giao thức sửa đổi này là các định danh tin nhắn liên tục được biết đến là UIDs.

- Kể từ đó, giao thức cơ bản của IMAP đã giữ nguyên chủ yếu không thay đổi, với các chức năng mới được thêm vào dưới dạng các tiện ích mở rộng tùy chọn. Một số tiện ích mở rộng đã trở thành tiêu chuẩn, nhưng việc sử dụng chúng có thể thay đổi tùy thuộc vào các nhà cung cấp dịch vụ email.

**POP3
- POP có trước IMAP, với phiên bản đầu tiên của Post Office Protocol được triển khai thông qua RFC 918 của IETF vào năm 1984.

- Mục tiêu của việc phát triển POP là tạo ra một giao thức email đơn giản nhưng hiệu quả để lấy email từ máy chủ. Chức năng này khác biệt so với thiết kế "hoạt động trực tuyến" ban đầu của IMAP, cho phép người dùng truy cập tin nhắn của họ ngoại tuyến, tuy nhiên chỉ trên một thiết bị duy nhất.

- POP2 được giới thiệu trước IMAP2 vào năm 1985 thông qua RFC 937. Khi IMAP2 xuất hiện vào năm 1988, RFC 1081 được xuất bản, mô tả POP3.

- Tuy nhiên, POP3 đã trải qua các sửa đổi trong mười năm trước khi phiên bản hoàn chỉnh được xuất bản vào năm 1996.

- Mặc dù POP3 đã trải qua một số cải tiến kể từ khi được xuất bản, nó vẫn duy trì nguyên tắc cơ bản của việc thực hiện một quy trình ba bước khi lấy email. Điều này làm cho POP3 trở nên phổ biến cho một số ứng dụng cụ thể ngay cả trong thời đại hiện nay.

### Chức năng

**IMAP**
- IMAP hoạt động bằng cách đồng bộ tất cả các thiết bị kết nối với một máy chủ trung tâm duy nhất. Ví dụ, nếu người dùng có ba thiết bị: máy tính đồng bộ, laptop và điện thoại thông minh, truy cập cùng một hộp thư, chúng sẽ được đồng bộ ngay khi kết nối với internet.

- Đồng bộ bao gồm "liên tục trạng thái toàn cầu". Chẳng hạn, nếu người dùng mở một email trên bất kỳ thiết bị nào ở trên đây, nó cũng sẽ được đánh dấu là "đã mở" trên tất cả các thiết bị khác. Tương tự, khi một email bị xóa trên một thiết bị, được trả lời, và cetera, trạng thái đó sẽ được áp dụng trên tất cả các thiết bị khác.

- Liên tục này không chỉ giới hạn ở email mà còn mở rộng đến các thư mục như hộp thư đến, đã gửi và thư rác. Người dùng thậm chí có thể sử dụng IMAP để tạo các thư mục tùy chỉnh của riêng họ — những thư mục này sẽ hiển thị trên tất cả các thiết bị khác.

- Một điểm đáng chú ý khác của chức năng IMAP là độ linh hoạt nó mang lại cho người dùng khi truy cập hộp thư của họ — giao thức này có thể hoạt động trực tuyến, ngoại tuyến và thậm chí khi thiết bị không kết nối! Các chế độ hoạt động ngoại tuyến và không kết nối làm cho giao thức này đặc biệt phổ biến.

- IMAP truy cập và lấy email từ các máy chủ từ xa. Điều này cho phép người dùng truy cập email của họ trong khi một bản sao được giữ lại phía máy chủ.

- Người dùng có thể đặt cờ tin nhắn trên IMAP. Điều này cho phép theo dõi trạng thái tin nhắn (đã mở, đã xóa, v.v.) trên các thiết bị.

- IMAP hữu ích cho việc quản lý nhiều hộp thư. Người dùng có thể chuyển các thông điệp giữa các hộp thư, cũng như tổ chức thông điệp vào các danh mục khác nhau. Điều này có nhiều ứng dụng thực tế; ví dụ, người dùng đang làm việc trên các dự án khác nhau có thể phân loại email của họ tùy thuộc vào từng dự án.

- IMAP cung cấp tính linh hoạt trong việc tải xuống. Tùy thuộc vào cấu hình, IMAP có thể cho phép người dùng quyết định liệu email có cần được lấy trước khi lấy từ máy chủ hay không. Ngoài ra, người dùng có thể tải xuống các phần của các tin nhắn, như một phần của nội dung, từ phần mime-multi. Điều này hữu ích cho một số trường hợp sử dụng, chẳng hạn như khi phần yếu tố email văn bản ngắn chứa một tệp đa phương tiện lớn.

- Khác với POP3, IMAP cho phép người dùng tổ chức và quản lý email phía máy chủ. Điều này bao gồm việc tạo, xóa và đổi tên các hộp thư trên máy chủ theo yêu cầu. Người dùng cũng có thể tạo cấu trúc phân cấp thông qua tổ chức thư mục.

- Việc tìm kiếm trong nội dung của email cũng là một chức năng của IMAP. Điều này bao gồm khả năng kiểm tra tiêu đề trước khi tải email về.

- Tuy nhiên, giống như POP3 và một số giao thức ứng dụng TCP/IP khác, IMAP là một giao thức máy khách-máy chủ. IMAP4 chỉ hoạt động khi giao thức này đặt trên cùng một máy chủ như hộp thư của người dùng. Thông thường, hộp thư phải được truy cập bởi Giao thức Chuyển thư đơn giản (SMTP) để nhận email đến và IMAP để lấy và quản lý.

- Cuối cùng, IMAP sử dụng Giao thức Kiểm soát Truyền tải (TCP) để giao tiếp, giúp thuận tiện trong việc truyền tải dữ liệu mượt mà và đảm bảo thông tin được nhận theo đúng thứ tự nó được truyền đi.

**POP3**
- Việc kết nối giữa máy chủ POP3 và máy khách bắt đầu với máy chủ yêu cầu tên người dùng từ máy khách. Một khi tên người dùng được nhập, máy chủ POP3 kiểm tra xem nó có một bản ghi của nó hay không. Nếu bản ghi tên người dùng được truy xuất thành công, máy chủ gửi máy khách một thông báo "OK" và yêu cầu một mật khẩu. Việc nhập mật khẩu thành công từ phía máy khách dẫn đến việc kết nối được thiết lập thành công.

- Sau khi kết nối, người dùng có thể xem các email được liệt kê trên máy chủ POP3. Danh sách này cũng hiển thị số lượng email và kích thước của chúng. Người dùng sau đó có thể bắt đầu lấy các email mong muốn.

- Khi một email được lấy về, nó sẽ bị xóa khỏi phía máy chủ. Do đó, các email bị hạn chế chỉ đến máy cụ thể mà chúng đã được tải xuống và sẽ không thể truy cập trên các máy khác. Điều này là sự khác biệt quan trọng nhất giữa IMAP và POP3.

- Tuy nhiên, các ứng dụng POP3 hiện đại có thể được cấu hình để giữ lại một bản sao của email trên phía máy chủ, khiến cho POP3 và IMAP gần nhau hơn về chức năng.

- Một lợi ích quan trọng của POP3 là cho phép người dùng đọc email ngoại tuyến. Kết nối internet chỉ cần khi email được tải xuống từ máy chủ. Một khi quá trình tải xuống hoàn tất, email được lưu trữ cục bộ trên thiết bị đầu cuối và có thể truy cập mà không cần kết nối internet. Điều này cũng có nghĩa là email đã được tải xuống có thể được xem dễ dàng và nhanh chóng.

- Hơn nữa, POP3 không giới hạn kích thước của email được gửi hoặc nhận, mặc dù các cấu hình cá nhân có thể đặt ra giới hạn nếu cần.

- Ngoài ra, POP3 yêu cầu ít không gian lưu trữ hơn phía máy chủ vì email được chuyển đi để lưu trữ trên phía máy khách. Tuy nhiên, điều này có thể gây ra vấn đề lưu trữ phía máy khách, vì giới hạn lưu trữ của thiết bị đầu cuối hạn chế kích thước hộp thư tối đa.

- Cuối cùng, sự đơn giản của POP3 làm cho nó phổ biến cho một số trường hợp sử dụng cụ thể. Nó dễ cấu hình và sử dụng một cách trực tiếp.

### Bảo mật
- Trong những năm gần đây, vai trò của IMAP đã giảm đi khi doanh nghiệp chuyển sang các dịch vụ thư web để quản lý tin nhắn và thư mục email. Tuy nhiên, nó vẫn được triển khai và sử dụng rộng rãi, được bảo vệ qua các tường lửa và cổng. Do đó, vấn đề bảo mật của IMAP vẫn là một thách thức cho các tổ chức.

- Như nhiều tiêu chuẩn và giao thức khác cho các ứng dụng internet được giới thiệu khi internet vẫn chủ yếu được sử dụng cho mục đích học thuật và nghiên cứu, bảo mật IMAP phụ thuộc nặng nề vào người dùng triển khai nó. Ngay cả khi người dùng tuân theo đầy đủ mong đợi về bảo mật IMAP truyền thống, họ vẫn tiếp tục tiếp xúc với rủi ro do các hạn chế của nó. Ví dụ, một số cấu hình vẫn cho phép người dùng từ xa xác thực bằng cách sử dụng tên người dùng và mật khẩu dạng văn bản thuần túy.

- Tất nhiên, hầu hết các vấn đề bảo mật của IMAP đã được giải quyết trong bối cảnh doanh nghiệp hiện đại, chú trọng đến an ninh sau đại dịch. Tuy nhiên, giao thức này vẫn có những biện pháp bảo mật email chưa hoàn chỉnh trong một số triển khai đơn giản vì nó đã tồn tại lâu và phổ biến trong nhiều môi trường khác nhau.

- Ngoài việc chấp nhận thông tin đăng nhập dạng văn bản, IMAP cũng có rủi ro vì nó thiếu hỗ trợ cho các phương pháp xác thực mạnh mẽ, như xác thực đa yếu tố (MFA) cho các ứng dụng email bên thứ ba đăng nhập vào các dịch vụ IMAP được lưu trữ trên đám mây. Một ví dụ về rủi ro này là các cuộc tấn công "password spraying" nhắm vào người dùng Microsoft Office 365 - trong khi Office 365 hỗ trợ MFA, nó có thể được bỏ qua bằng cách kết nối với dịch vụ IMAP sử dụng một ứng dụng email bên thứ ba.

- Ngày nay, các rủi ro liên quan đến IMAP cho phép thông tin đăng nhập dạng văn bản đã được giảm nhẹ bằng cách chuyển đổi cấu hình mặc định để kích hoạt mã hóa TLS ngầm cho tất cả các giao thức email. Giao thức IMAP qua TLS đặt ra một tiêu chuẩn cho tất cả các giao thức email cổ điển để sử dụng TLS để mã hóa phiên thư của người dùng theo mặc định hoặc ít nhất là sử dụng giao thức STARTTLS để triển khai mã hóa cơ hội. Giao thức này được mô tả trong RFC 8314 và, ngoài IMAP, còn bao gồm SMTP và POP.

- Tuy nhiên, việc yêu cầu TLS không đủ một mình để ngăn chặn các cuộc tấn công "password spraying" trên IMAP, và hỗ trợ cho MFA vẫn chưa đầy đủ.

- Hạn chế bảo mật này không phải là một trong những vấn đề duy nhất có thể dẫn đến cấu hình không đúng và các cuộc tấn công mạng thành công. Ví dụ, các ứng dụng IMAP bên thứ ba không luôn tương thích với các chính sách đăng nhập vào Office 365 giới hạn người dùng từ xa thử nghiệm đăng nhập quá nhiều lần. Điều này có thể cho phép kẻ tấn công thử nghiệm các cuộc tấn công dò mật khẩu.

- Vậy nên, làm thế nào để làm chặt chẽ bảo mật IMAP? Như với hầu hết các thách thức an ninh mạng, sự nhận thức về các vấn đề hiện tại là bước đầu tiên để nâng cao bảo mật IMAP. Các bài tập hướng tới bảo vệ các hệ thống dễ bị tổn thương có thể bắt đầu bằng việc xác định vị trí triển khai các giao thức nhạy cảm. Tiếp theo, các bài tập này có thể làm việc để đảm bảo rằng các giao thức này được cấu hình đúng để hỗ trợ mã hóa thông qua IMAP qua TLS hoặc STARTTLS.

- Trong khi cổng mặc định cho IMAP là cổng 143 cho các yêu cầu của máy khách, cổng 993 được chỉ định cho IMAP qua TLS. Việc cấu hình lại máy chủ và máy khách để sử dụng cổng 993 có thể giúp loại bỏ các kết nối văn bản thuần túy. Tường lửa và các hệ
thống cổng khác cũng có thể được thiết lập để hạn chế kết nối với cổng 143 không an toàn. 

- Cuối cùng, các biện pháp bảo mật khác cho IMAP nên giải quyết cách máy chủ IMAP có thể được truy cập. Một số chiến thuật bao gồm:

	- Sử dụng các quy tắc tường lửa để hạn chế truy cập từ xa vào phía máy chủ.

	- Kích hoạt xác thực đa yếu tố trên càng nhiều điểm tiếp xúc từ xa nhất có thể.

	- Sử dụng các mô hình độ tin cậy không trực tiếp để hạn chế người dùng không xác thực từ tiếp cận các dịch vụ IMAP.

	- Cấu hình lại các dịch vụ email và liên quan để vô hiệu hóa việc truy cập từ xa đối với người dùng không xác thực.

- Một cách tiếp cận cấp tiến hơn có thể là hoàn toàn vô hiệu hóa việc truy cập vào các dịch vụ email cổ điển từ người dùng cuối và yêu cầu họ truy cập dịch vụ từ xa qua HTTPS. Hoặc người dùng có thể bảo vệ dịch vụ cổ điển khỏi những lỗ hổng thông thường và giảm diện tích tấn công của họ.

**POP3**
- POP3 có độ an toàn tương đối thấp hơn IMAP trong nhiều ứng dụng. Trên thực tế, một số chuyên gia an ninh mạng khuyến nghị thay thế POP3 bằng cấu hình khác như IMAP, Exchange, hoặc SMTPS, đặc biệt là đối với các thiết lập nhạy cảm.

- Một lý do chính khiến POP3 bị coi là có rủi ro là quá trình xử lý email ở cấp địa phương. Với POP3, dữ liệu không được đồng bộ hóa trên nhiều thiết bị; thay vào đó, thông tin được tải xuống vào thiết bị hiện đang đăng nhập, nơi mọi thứ được xử lý. Điều này khiến an ninh email của người dùng chỉ đảm bảo như thiết bị - nếu một đối tượng độc hại có thể truy cập thiết bị, an ninh email sẽ không còn hiệu quả.

- Tuy nhiên, điều này không phải là lý do duy nhất khiến POP3 bị xem xét không an toàn. Nhiều vấn đề bảo mật trong giao thức này xuất phát từ việc nó gần 20 năm tuổi. Khi POP3 mất đi sự ưa chuộng và sự hỗ trợ, nó đang được thay thế bằng các giao thức mới tương thích với các tính năng bảo mật email hiện đại.

- Tất nhiên, điều này không có nghĩa là POP3 hoàn toàn không an toàn. Việc thêm TLS hoặc SSL vào một máy chủ POP3 mã hóa dữ liệu được chia sẻ trong toàn bộ máy chủ. Tuy nhiên, trừ khi hỗ trợ đồng bộ hóa được kích hoạt thủ công, email không thể được truy cập trên nhiều thiết bị, giới hạn tính hữu ích của việc này.

Tại sao IMAP vượt trội hơn POP3 về mặt bảo mật? Hãy xem xét những điểm sau:

- IMAP hỗ trợ đồng bộ hóa và tất cả các thay đổi được xử lý trên phía máy chủ thay vì cục bộ. Các máy chủ tập trung dễ dàng để bảo mật hơn các điểm cuối cá nhân, làm cho dữ liệu trở nên an toàn hơn với IMAP.

- IMAP không tải các tệp đính kèm trên email cho đến khi người dùng mở chúng. Điều này giúp bảo vệ thiết bị cuối khỏi các tệp đính kèm độc hại như malware.

- Các ứng dụng email hàng đầu như Microsoft Outlook và Mozilla Thunderbird hỗ trợ IMAP hơn là POP3.

- Trong khi máy chủ POP3 có thể được bảo mật đến một mức độ nhất định, việc giao thức này thiếu hỗ trợ cho hầu hết các tính năng hiện đại khiến nó ít an toàn hơn IMAP.

### Giới hạn
**IMAP**
- Trong cấu hình IMAP "trực tuyến", việc truy cập email sẽ dừng lại nếu không có kết nối internet hoạt động. Truy cập email ngoại tuyến yêu cầu sử dụng chế độ Ngoại tuyến trong ứng dụng email.
Lưu trữ tin nhắn bị giới hạn và phụ thuộc vào kế hoạch lưu trữ của người dùng và phân bổ hộp thư. Trong trường hợp sử dụng email nặng, người dùng có thể phải trả thêm để có không gian lưu trữ hộp thư lớn hơn.

- Việc truy cập email mất một chút thời gian hơn so với POP3, vì tất cả các thư mục được đồng bộ mỗi khi sự kiện Gửi/Nhận được kích hoạt.

**POP3**
- Lưu trữ tin nhắn cục bộ có nghĩa là trừ khi máy chủ được cấu hình đặc biệt để giữ lại bản sao của email, chúng sẽ bị mất mãi mãi trong trường hợp thiết bị gặp sự cố. Những tin nhắn tài nguyên nặng có thể dẫn đến việc hệ thống cục bộ giảm tốc độ hoạt động.

- Cấu hình POP3 để gửi email đến nhiều máy tính có nghĩa là nhiều thiết bị (cũng như máy chủ) hiện tại đều lưu trữ cùng một dữ liệu, dẫn đến việc sao chép và xóa email nhiều lần.