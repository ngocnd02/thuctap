# TỔNG QUAN VỀ LAMP STACK

## LAMP stack là gì?
- LAMP stack là một gói gồm bốn công nghệ phần mềm khác nhau mà các nhà phát triển sử dụng để xây dựng trang web và ứng dụng web. LAMP là từ viết tắt của hệ điều hành Linux; máy chủ web, Apache; máy chủ cơ sở dữ liệu MySQL; và ngôn ngữ lập trình PHP. Tất cả bốn công nghệ này đều là nguồn mở, có nghĩa là chúng được cộng đồng duy trì và cung cấp miễn phí cho mọi người sử dụng. Các nhà phát triển sử dụng ngăn xếp LAMP để tạo, lưu trữ và duy trì nội dung web. Đó là một giải pháp phổ biến hỗ trợ nhiều trang web bạn thường sử dụng ngày nay.

## Tại sao LAMP stack lại quan trọng 	
**Chi phí**
- Tất cả các công nghệ LAMP đều là nguồn mở, có nghĩa là bất kỳ nhà phát triển hoặc công ty nào cũng có thể sử dụng chúng mà không phải trả phí cấp phép. Thay vì mua các thành phần ngăn xếp độc quyền, bạn có thể tải xuống miễn phí hệ điều hành, máy chủ web, cơ sở dữ liệu và ngôn ngữ kịch bản. Điều này làm giảm chi phí xây dựng các ứng dụng web.

**Hiệu quả**
Việc thiết lập một nhóm phát triển web mới yêu cầu phải kiểm tra nghiêm ngặt các khung, mô-đun, thư viện và công cụ khác nhau. Mặt khác, ngăn xếp LAMP là một giải pháp phát triển web đã được thử nghiệm. Các nhà phát triển web có thể ưu tiên và tăng tốc độ phát triển ứng dụng để tập trung vào những gì họ đang xây dựng thay vì cách họ xây dựng nó.

**Bảo trì**
Các chuyên gia phần mềm từ khắp nơi trên thế giới đóng góp vào sự phát triển của công nghệ ngăn xếp LAMP bằng cách thay đổi, nhận xét và xem xét các mã nguồn có sẵn công khai. Họ thường xuyên duy trì và cập nhật các công nghệ để chúng luôn phù hợp và an toàn.

**Hỗ trợ**
Các công nghệ nguồn mở phổ biến, chẳng hạn như ngăn xếp LAMP, nhận được sự hỗ trợ của cộng đồng CNTT toàn cầu rộng lớn. Do đó, người dùng ngăn xếp LAMP có thể dễ dàng tìm thấy thông tin hơn trên các diễn đàn CNTT công cộng. Các nhà phát triển web có thể tham khảo các mã ví dụ hoặc sử dụng các plugin đã được thử nghiệm do cộng đồng nguồn mở tạo ra.

**Linh hoạt**
Ngăn xếp LAMP mang lại cả độ tin cậy và tính linh hoạt cho các nhà phát triển web. Mặc dù kiến trúc LAMP chỉ định các thành phần phần mềm cho từng lớp, nhưng các nhà phát triển có thể thay thế chúng khi thấy phù hợp. Ví dụ, họ có thể sử dụng hệ điều hành khác ngoài Linux làm nền tảng ngăn xếp.

## Kiến trúc của LAMP
- Ngăn xếp phần mềm là một tập hợp các công cụ, thư viện, ngôn ngữ lập trình và công nghệ phân lớp được sử dụng để xây dựng, quản lý và chạy một ứng dụng. Ngăn xếp bao gồm các thành phần phần mềm hỗ trợ ứng dụng theo nhiều cách khác nhau, chẳng hạn như trình bày trực quan, cơ sở dữ liệu, mạng và bảo mật.

- Tương tự, kiến trúc LAMP bao gồm bốn công nghệ phần mềm phối hợp với nhau ở hậu trường để tạo ra một ứng dụng web hoạt động được. Nó mô tả cách mỗi công nghệ phát triển web này tương tác với nhau trong máy chủ. Kiến trúc LAMP bao gồm các lớp sau.

**Linux**
- Linux là một hệ điều hành nguồn mở mà bạn có thể cài đặt và cấu hình để đáp ứng các yêu cầu ứng dụng khác nhau. Linux nằm ở cấp độ đầu tiên của ngăn xếp LAMP và hỗ trợ các thành phần khác ở các lớp trên.

**Apache**
- Apache là một máy chủ web nguồn mở tạo thành lớp thứ hai của ngăn xếp LAMP. Mô-đun Apache lưu trữ các tệp trang web và trao đổi thông tin với trình duyệt bằng HTTP, một giao thức internet để truyền thông tin trang web ở dạng văn bản thuần túy. Ví dụ: khi trình duyệt yêu cầu một trang web, máy chủ HTTP Apache sẽ thực hiện như sau:
	- Nhận được yêu cầu
	- Xử lý yêu cầu và tìm tệp trang được yêu cầu
	- Gửi thông tin liên quan trở lại trình duyệt

**MySQL**
- MySQL là một hệ thống quản lý cơ sở dữ liệu quan hệ nguồn mở và là lớp thứ ba của ngăn xếp LAMP. Mô hình LAMP sử dụng MySQL để lưu trữ, quản lý và truy vấn thông tin trong cơ sở dữ liệu quan hệ. Ví dụ: nhà phát triển lưu trữ dữ liệu ứng dụng, chẳng hạn như hồ sơ khách hàng, doanh số bán hàng và hàng tồn kho. Khi người dùng tìm kiếm thông tin, máy chủ web sẽ truy vấn dữ liệu được lưu trữ trong MySQL. Truy vấn đề cập đến các hướng dẫn đặc biệt để thao tác dữ liệu trong cơ sở dữ liệu quan hệ bằng ngôn ngữ SQL.

**PHP**
- PHP, viết tắt của PHP: Hypertext Preprocessor, là lớp thứ tư và cuối cùng của ngăn xếp LAMP. Đó là ngôn ngữ kịch bản cho phép các trang web chạy các quy trình động. Một quy trình năng động bao gồm thông tin trong phần mềm luôn thay đổi. Các nhà phát triển web nhúng ngôn ngữ lập trình PHP vào HTML để hiển thị thông tin cập nhật hoặc thời gian thực trên các trang web. Họ sử dụng PHP để cho phép máy chủ web, cơ sở dữ liệu và hệ điều hành xử lý các yêu cầu từ trình duyệt một cách liền mạch.

HTML so với PHP
Các nhà phát triển web sử dụng HTML để phát triển giao diện người dùng, chẳng hạn như thiết kế bố cục trang web. Trong khi đó, họ sử dụng PHP để xác định hành vi của một số thành phần nhất định khi người dùng tải trang web. Ví dụ: các nhà phát triển web thiết kế bố cục đồ họa của danh mục sản phẩm trực tuyến bằng HTML. Sau đó, họ sử dụng mã PHP để lấy giá sản phẩm mới nhất từ máy chủ phụ trợ.

## Cách LAMP stack hoạt động
Các ứng dụng web sử dụng ngăn xếp LAMP để đáp ứng các yêu cầu từ trình duyệt web. Máy chủ web Apache và cơ sở dữ liệu MySQL chạy trên hệ điều hành Linux và giao tiếp bằng PHP. Khi bạn mở một trang web trong trình duyệt, ngăn xếp LAMP sẽ thực hiện quy trình sau.

**Nhận yêu cầu**
- Máy chủ web Apache nhận được yêu cầu đến từ trình duyệt. Nếu yêu cầu tải một tệp tĩnh, máy chủ Apache sẽ phản hồi trực tiếp với nội dung phù hợp. Nếu yêu cầu dành cho nội dung động, máy chủ Apache sẽ chuyển yêu cầu đó đến thành phần PHP. Thành phần PHP tìm và tải tệp PHP thích hợp có thể xử lý yêu cầu.

**Xử lý yêu cầu**
- Tệp PHP chứa các hàm PHP là mã để tạo nội dung động. Thành phần PHP xử lý các hàm PHP, chẳng hạn như chuyển đổi đơn vị đo lường hoặc tạo biểu đồ bán hàng. Một số hàm PHP có thể yêu cầu thông tin từ cơ sở dữ liệu. Trong những trường hợp như vậy, mã PHP lấy thông tin được lưu trữ từ cơ sở dữ liệu và sử dụng nó để xử lý hàm.

**Trả về phản hồi**
- PHP chuyển kết quả tính toán đến máy chủ web ở định dạng HTML. Đồng thời, nó còn lưu trữ dữ liệu mới trong cơ sở dữ liệu MySQL. Máy chủ HTTP Apache gửi kết quả HTML động tới trình duyệt của người dùng.