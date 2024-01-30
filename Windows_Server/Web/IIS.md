# Internet Information Services (IIS)
- Internet Information Services (IIS) là một máy chủ web linh hoạt và đa năng từ Microsoft, chạy trên các hệ thống Windows để phục vụ các trang HTML hoặc tệp tin được yêu cầu.

- Một máy chủ web IIS chấp nhận các yêu cầu từ máy tính khách từ xa và trả lại phản hồi phù hợp. Chức năng cơ bản này cho phép máy chủ web chia sẻ và cung cấp thông tin qua mạng cục bộ (LAN), như các mạng nội dung doanh nghiệp, và mạng rộng (WAN), như Internet.

- Một máy chủ web có thể cung cấp thông tin cho người dùng dưới nhiều hình thức, chẳng hạn như trang web tĩnh được mã hóa bằng HTML, thông qua trao đổi tệp tin như tải về và tải lên, cũng như tài liệu văn bản, tệp hình ảnh và nhiều định dạng khác.

## Web servers provide portals

Các máy chủ web hiện đại có thể cung cấp nhiều chức năng hơn cho doanh nghiệp và người dùng của nó. Máy chủ web thường được sử dụng như cổng thông tin cho các ứng dụng web phức tạp, tương tác cao, kết nối middleware doanh nghiệp và các ứng dụng backend để tạo ra các hệ thống cấp doanh nghiệp. Ví dụ, Amazon Web Services cho phép người dùng quản lý các nguồn lực điện toán công cộng thông qua một cổng thông tin trực tuyến. Trong khi đó, các dịch vụ truyền phương tiện, như Spotify cho âm nhạc và Netflix cho phim ảnh, cung cấp nội dung trực tuyến theo thời gian thực thông qua các máy chủ web.

## How IIS work
- IIS hoạt động thông qua nhiều ngôn ngữ và giao thức tiêu chuẩn. HTML được sử dụng để tạo các thành phần như văn bản, nút, địa điểm hình ảnh, tương tác/trạng thái trực tiếp và liên kết siêu văn bản. Giao thức Truyền tải Siêu Văn bản (HTTP) là giao thức truyền thông cơ bản được sử dụng để trao đổi thông tin giữa máy chủ web và người dùng. HTTPS - HTTP qua Secure Sockets Layer (SSL) - sử dụng Bảo mật Tầng Truyền (TLS) hoặc SSL để mã hóa giao tiếp để tăng cường bảo mật dữ liệu. Giao thức Truyền tải Tệp Tin (FTP), hoặc biến thể an toàn của nó, FTPS, có thể truyền tải các tệp tin.

- Các giao thức khác được hỗ trợ bao gồm Giao thức Truyền thư Đơn Giản (SMTP), để gửi và nhận email, và Giao thức Truyền tin tức Mạng (NNTP), để phân phối các bài viết trên USENET.

## IIS works with ASP.NET core
- Khung ASP.NET Core là thế hệ mới nhất của Active Server Page (ASP), một động cơ kịch bản phía máy chủ tạo ra các trang web tương tác. Một yêu cầu đến máy chủ IIS từ web, sau đó máy chủ chuyển yêu cầu đó đến ứng dụng ASP.NET Core, xử lý yêu cầu và gửi phản hồi về lại máy chủ IIS và người dùng gửi yêu cầu. Các ví dụ về ứng dụng viết bằng ASP.NET Core bao gồm các nền tảng blog và các hệ thống quản lý nội dung (CMS).

- Những nhà phát triển có thể tạo ra các trang web IIS bằng nhiều công cụ, bao gồm WebDav, có thể tạo và xuất bản nội dung web. Nhà phát triển cũng có thể sử dụng các công cụ phát triển tích hợp, như Microsoft Visual Studio.

## Version of IIS
- IIS đã phát triển cùng với Microsoft Windows. Các phiên bản đầu tiên của IIS xuất hiện với Windows NT. IIS 1.0 xuất hiện với Windows NT 3.51 và phát triển qua IIS 4.0 với Windows NT 4.0. IIS 5.0 được cài đặt với Windows 2000. Microsoft thêm IIS 6.0 vào Windows Server 2003. IIS 7.0 mang đến một sự thiết kế lại lớn với Windows Server 2008 (IIS 7.5 nằm trong Windows Server 2008 R2). IIS 8.0 đi kèm với Windows Server 2012 (Windows Server 2012 R2 sử dụng IIS 8.5). Và IIS 10 xuất hiện với Windows Server 2016 và Windows 10.

- Với mỗi phiên bản của IIS, Microsoft đã thêm các tính năng mới và cập nhật chức năng hiện tại. Ví dụ, IIS 3.0 thêm ASP cho việc kịch bản động; IIS 6.0 thêm hỗ trợ cho IPv6 và cải thiện bảo mật và độ tin cậy; và IIS 8.0 mang lại khả năng mở rộng đa lõi trên phần cứng non-uniform memory access, hỗ trợ chứng chỉ SSL tập trung và Server Name Indication.

## Features in IIS 10
- IIS 10 cũng thêm vào một số tính năng và chức năng mới.

- IIS 10 thêm hỗ trợ cho giao thức HTTP/2, để cung cấp việc sử dụng tài nguyên hiệu quả và độ trễ thấp hơn so với HTTP 1.1. IIS 10 hoạt động trên mô hình triển khai máy chủ tối giản Nano Server dưới Windows Server 2016, và có thể chạy các khối công việc ASP.NET Core, Apache Tomcat và PHP trên IIS trên Nano Server.

- IIS 10 hoạt động trong một container và máy ảo, vì vậy nhà phát triển và quản trị viên có thêm sự linh hoạt trong lựa chọn triển khai, cũng như khả năng chứa đựng một loạt các ứng dụng web.

## Security
- Để đảm bảo một trang web an toàn, tổ chức cần thực hiện các biện pháp bảo mật để bảo vệ máy chủ web khỏi các cuộc tấn công bảo mật. Các công ty có thể sử dụng các tính năng tích hợp vào IIS để làm chặt hệ thống IIS.

- Một số cách để làm chặt Windows IIS bao gồm:

1. Đảm bảo hệ điều hành Windows được cập nhật với tất cả các bản vá bảo mật.

2. Tắt bất kỳ tính năng của IIS nào không sử dụng để giảm thiểu rủi ro của các cuộc tấn công tiềm ẩn.

3. Sử dụng tường lửa để đảm bảo máy chủ chỉ nhận các gói tin hợp lệ.

4. Kiểm soát địa chỉ IP và domain nào có thể truy cập máy chủ web.

5. Sử dụng quyền ủy quyền URL để áp dụng các quy tắc cho các yêu cầu cụ thể, chẳng hạn như xử lý các URL cụ thể. Một công ty có thể sử dụng quyền ủy quyền URL để chỉ ủy quyền cho một số người dùng cụ thể xem các trang đã được yêu cầu.

6. Sử dụng logging để xem danh sách những người truy cập máy chủ web.

7. Cấu hình trang lỗi để chỉ hiển thị thông tin liên quan về vấn đề. Hãy chắc chắn rằng các trang lỗi không hiển thị quá nhiều thông tin, chẳng hạn như tên người dùng, mật khẩu, địa chỉ IP của máy chủ hoặc bất kỳ thông tin nào mà hacker có thể sử dụng để khai thác máy chủ web.

## IIS vs. Apache
Các khác biệt giữa IIS và Apache bao gồm:

1. **IIS đi kèm với Windows trong khi Apache là miễn phí và mã nguồn mở:**
   - IIS được đóng gói với Windows và thường được triển khai trong môi trường Microsoft.
   - Apache là một dự án mã nguồn mở và miễn phí, có sẵn cho nhiều hệ điều hành bao gồm macOS, UNIX và Linux, là sự lựa chọn phổ biến cho nền tảng không phải Windows.

2. **IIS chỉ chạy trên Windows, trong khi Apache có thể chạy trên nhiều hệ điều hành:**
   - IIS chỉ chạy trên hệ điều hành Windows.
   - Apache có thể chạy trên hầu hết các hệ điều hành, bao gồm macOS, UNIX và Linux, làm cho nó phù hợp cho môi trường đa nền tảng.

3. **IIS tích hợp với các sản phẩm khác của Microsoft, chẳng hạn như .NET và ngôn ngữ kịch bản ASPX:**
   - IIS liên kết chặt chẽ với các sản phẩm và công nghệ khác của Microsoft như .NET và ngôn ngữ kịch bản ASPX.
   - Apache là một máy chủ web độc lập, không có sự phụ thuộc vào các sản phẩm Microsoft.

4. **IIS có bộ phận hỗ trợ kỹ thuật để xử lý hầu hết các vấn đề, trong khi hỗ trợ cho Apache đến từ cộng đồng người dùng:**
   - IIS thường có bộ phận hỗ trợ kỹ thuật để xử lý các vấn đề và vấn đề của người dùng.
   - Hỗ trợ cho Apache thường đến từ cộng đồng người dùng và các nguồn thông tin trực tuyến.

5. **Các tính năng bảo mật của IIS làm cho nó trở thành một lựa chọn an toàn hơn so với Apache:**
   - IIS được đánh giá cao về tính an toàn và bảo mật.
   - Apache cũng có các biện pháp bảo mật mạnh mẽ, nhưng mức độ an toàn có thể phụ thuộc vào cách cấu hình và quản lý của người quản trị.

6. **Công nghệ cơ bản của IIS tương thích với các giao diện web tiêu chuẩn trên toàn cầu:**
   - Công nghệ cơ bản của IIS thường tương thích với các giao diện web tiêu chuẩn trên toàn cầu.
   - Apache cũng tuân theo các tiêu chuẩn web quốc tế và thường được coi là linh hoạt trong việc hỗ trợ các giao thức và chuẩn web khác nhau.


