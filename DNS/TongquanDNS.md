# TÌM HIỂU VỀ DNS SERVER
## Mục Lục
[DNS](#dns)
- [DNS là gì?](#dnslagi)
- [DNS hoạt động như thế nào?](#dnshoatdongthenao)
- [Có 4 DNS server liên quan đến việc tải một trang web](#4dnsserver)
- [Sự khác biệt giữa authoritative DNS server và recursive DNS resolver](#sukhacbiet)
	- [Recursive DNS resolver (Trình phân giải DNS đệ quy)](#trinhphangia)
	- [Authoritative DNS server (Máy chủ DNS ủy quyền)](#maychudnsuyquen)
- [8 bước tra cứu DNS](#8buoctracuudns)
- [DNS Resolver](#dnsresolver)
- [Các loại truy vấn DNS](#cacloaitruyvandns)

[DNS server](#dnsserver)

# DNS
## DNS là gì?
- **Hệ Thống Tên Miền (DNS)** là danh bạ của Internet. Con người truy cập thông tin trực tuyến thông qua tên miền, như nytimes.com hoặc espn.com. Trình duyệt web tương tác thông qua địa chỉ IP. DNS chuyển đổi tên miền thành địa chỉ IP để trình duyệt có thể tải tài nguyên trực tuyến.
- Mỗi thiết bị kết nối với Internet đều có một địa chỉ IP duy nhất mà các máy khác sử dụng để tìm thiết bị đó. Các máy chủ DNS loại bỏ nhu cầu cho con người nhớ địa chỉ IP như 192.168.1.1 (trong IPv4) hoặc địa chỉ IP chữ số chữ cái phức tạp hơn như 2400:cb00:2048:1::c629:d7a2 (trong IPv6).

## DNS hoạt động như thế nào?
- Quá trình giải quyết DNS liên quan đến chuyển đổi một tên máy chủ (như www.example.com) thành một địa chỉ IP thân thiện với máy tính (như 192.168.1.1). Mỗi thiết bị trên Internet được cấp một địa chỉ IP duy nhất và địa chỉ đó là cần thiết để tìm thiết bị Internet tương ứng - giống như địa chỉ nhà được sử dụng để tìm một ngôi nhà cụ thể. Khi người dùng muốn tải một trang web, một sự chuyển đổi phải xảy ra giữa những gì người dùng gõ vào trình duyệt web của họ (ví dụ.com) và địa chỉ thân thiện với máy tính cần thiết để định vị trang web example.com.

## Có 4 DNS server liên quan đến việc tải một trang web
- **DNS Recursor** - DNS Recursor có thể được coi như một người thư viện được yêu cầu đi tìm một cuốn sách cụ thể nào đó trong thư viện. DNS Recursor là một máy chủ được thiết kế để nhận các truy vấn từ các máy khách thông qua ứng dụng như trình duyệt web. Thông thường, Recursor sau đó chịu trách nhiệm thực hiện các yêu cầu bổ sung để đáp ứng truy vấn DNS của máy khách.

- **Root Nameserver** - Root Server là bước đầu tiên trong việc chuyển đổi (giải quyết) tên máy chủ dễ đọc của con người thành địa chỉ IP. Nó có thể được coi như một chỉ mục trong một thư viện chỉ đến các kệ sách khác nhau - thường nó phục vụ như một tham chiếu đến các vị trí cụ thể khác.

- **TLD Nameserver** - Máy chủ Top-Level Domain (TLD) có thể được coi như một kệ sách cụ thể trong một thư viện. Máy chủ này là bước tiếp theo trong quá trình tìm kiếm một địa chỉ IP cụ thể và nó chứa phần cuối cùng của một tên máy chủ (trong example.com, máy chủ TLD là "com").

- **Authoritative Nameserver** - Máy chủ cuối cùng này có thể được coi như một từ điển trên một kệ sách, trong đó một tên cụ thể có thể được dịch thành định nghĩa của nó. Máy chủ ủy quyền là điểm dừng cuối cùng trong truy vấn máy chủ DNS. Nếu máy chủ tên uy quyền có quyền truy cập vào bản ghi được yêu cầu, nó sẽ trả lại địa chỉ IP cho tên máy chủ được yêu cầu trở lại cho DNS Recursor (người thư viện) đã thực hiện yêu cầu ban đầu.

## Sự khác biệt giữa authoritative DNS server và recursive DNS resolver
### Recursive DNS resolver
- Máy tính phản hồi một yêu cầu đệ quy từ một máy khách và dành thời gian để theo dõi bản ghi DNS. Điều này được thực hiện thông qua việc thực hiện một loạt các yêu cầu cho đến khi nó đạt được máy chủ DNS ủy quyền cho bản ghi được yêu cầu (hoặc hết thời gian hoặc trả lại một lỗi nếu không tìm thấy bản ghi). Bộ giải quyết DNS đệ quy không luôn cần phải thực hiện nhiều yêu cầu để theo dõi các bản ghi cần thiết để phản hồi cho một máy khách; caching là một quy trình duy trì dữ liệu giúp rút ngắn các yêu cầu cần thiết bằng cách phục vụ bản ghi tài nguyên được yêu cầu trước đó trong quá trình tra cứu DNS.

![Imgur](https://i.imgur.com/s5bgc5D.png)

### Authoritative DNS server
- Một máy chủ DNS ủy quyền là một máy chủ thực sự giữ và chịu trách nhiệm về các bản ghi tài nguyên DNS. Đây là máy chủ ở dưới cùng của chuỗi tra cứu DNS sẽ phản hồi với bản ghi tài nguyên được truy vấn, cuối cùng cho phép trình duyệt web đang thực hiện yêu cầu đạt được địa chỉ IP cần thiết để truy cập một trang web hoặc các nguồn web khác. Một máy chủ DNS ủy quyền có thể đáp ứng các truy vấn từ dữ liệu của mình mà không cần truy vấn nguồn khác, vì nó là nguồn thông tin chính xác cuối cùng cho một số bản ghi DNS cụ thể.

## Tám bước tra cứu DNS

1. Một người dùng nhập 'example.com' vào trình duyệt web và truy vấn đi vào Internet, được nhận bởi một bộ giải quyết DNS đệ quy.

2. Bộ giải quyết sau đó truy vấn một máy chủ tên miền gốc DNS (.).

3. Máy chủ gốc sau đó phản hồi cho bộ giải quyết với địa chỉ của một máy chủ DNS Top Level Domain (TLD) (ví dụ như .com hoặc .net), nơi lưu trữ thông tin cho các miền của nó. Khi tìm kiếm example.com, yêu cầu của chúng ta được chỉ đến TLD .com.

4. Bộ giải quyết sau đó thực hiện một yêu cầu đến TLD .com.

5. Máy chủ TLD sau đó phản hồi với địa chỉ IP của máy chủ tên miền, example.com.

6. Cuối cùng, bộ giải quyết đệ quy gửi một truy vấn đến máy chủ tên miền.

7. Địa chỉ IP cho example.com sau đó được trả về cho bộ giải quyết từ máy chủ tên miền.

8. Bộ giải quyết DNS sau đó phản hồi trình duyệt web với địa chỉ IP của tên miền được yêu cầu ban đầu.

Sau khi 8 bước của tra cứu DNS đã trả về địa chỉ IP cho example.com, trình duyệt có thể thực hiện yêu cầu cho trang web:

9. Trình duyệt gửi một yêu cầu HTTP đến địa chỉ IP.

10. Máy chủ tại địa chỉ IP đó trả lại trang web để hiển thị trong trình duyệt (bước 10).

![Imgur](https://i.imgur.com/wV6JuYa.png)

## DNS Resolver
- Trình phân giải DNS (DNS resolver) là điểm dừng đầu tiên trong quá trình tra cứu DNS và nó chịu trách nhiệm xử lý ứng dụng khách đã đưa ra yêu cầu ban đầu. Trình phân giải bắt đầu chuỗi truy vấn mà cuối cùng dẫn đến việc dịch URL sang địa chỉ IP cần thiết.

Lưu ý: Tra cứu DNS không được lưu vào bộ nhớ đệm thông thường sẽ bao gồm cả truy vấn đệ quy và truy vấn lặp lại.

- Điều quan trọng là phải phân biệt giữa truy vấn DNS đệ quy (recusive DNS query) và trình phân giải DNS đệ quy (recusive DNS resolver). Truy vấn đề cập đến yêu cầu được gửi tới trình phân giải DNS yêu cầu giải quyết truy vấn. Trình phân giải đệ quy DNS là máy tính chấp nhận truy vấn đệ quy và xử lý phản hồi bằng cách thực hiện các yêu cầu cần thiết.

![Imgur](https://i.imgur.com/NtGsRLj.png)

## Các loại truy vấn DNS

## Bộ nhớ đệm DNS (DNS caching)
Mục đích của bộ nhớ đệm là lưu trữ dữ liệu tạm thời ở một vị trí nhằm cải thiện hiệu suất và độ tin cậy cho các yêu cầu dữ liệu. Bộ nhớ đệm DNS liên quan đến việc lưu trữ dữ liệu gần hơn với máy khách yêu cầu để có thể giải quyết truy vấn DNS sớm hơn và có thể tránh được các truy vấn bổ sung trong chuỗi tra cứu DNS, từ đó cải thiện thời gian tải và giảm mức tiêu thụ băng thông/CPU. Dữ liệu DNS có thể được lưu vào bộ đệm ở nhiều vị trí khác nhau, mỗi vị trí sẽ lưu trữ bản ghi DNS trong một khoảng thời gian nhất định được xác định bởi thời gian tồn tại (TTL).

### Bộ đệm DNS của trình duyệt (Brower DNS caching)
Các trình duyệt web hiện đại được thiết kế theo mặc định để lưu trữ các bản ghi DNS trong một khoảng thời gian nhất định. Mục đích ở đây rất rõ ràng; Bộ đệm DNS càng xuất hiện gần trình duyệt web thì càng phải thực hiện ít bước xử lý hơn để kiểm tra bộ đệm và thực hiện các yêu cầu chính xác tới địa chỉ IP. Khi yêu cầu bản ghi DNS được thực hiện, bộ đệm của trình duyệt là vị trí đầu tiên được kiểm tra cho bản ghi được yêu cầu.

### Operating system (OS) level DNS caching (OS level DNS caching)
- Trình phân giải DNS cấp hệ điều hành là điểm dừng cục bộ thứ hai và cuối cùng trước khi truy vấn DNS rời khỏi máy của bạn. Quá trình bên trong hệ điều hành của bạn được thiết kế để xử lý truy vấn này thường được gọi là “trình phân giải sơ khai” hoặc máy khách DNS. Khi trình phân giải sơ khai nhận được yêu cầu từ một ứng dụng, trước tiên nó sẽ kiểm tra bộ đệm của chính nó để xem liệu nó có bản ghi hay không. Nếu không, nó sẽ gửi một truy vấn DNS (với bộ cờ đệ quy), bên ngoài mạng cục bộ tới trình phân giải đệ quy DNS bên trong nhà cung cấp dịch vụ Internet (ISP).

- Khi trình phân giải đệ quy bên trong ISP nhận được một truy vấn DNS, giống như tất cả các bước trước đó, nó cũng sẽ kiểm tra xem liệu bản dịch từ địa chỉ máy chủ sang địa chỉ IP được yêu cầu đã được lưu trữ bên trong lớp lưu trữ cục bộ hay chưa.

- Trình phân giải đệ quy cũng có chức năng bổ sung tùy thuộc vào loại bản ghi có trong bộ đệm của nó:

	- Nếu trình phân giải không có bản ghi A nhưng có bản ghi NS cho máy chủ tên có thẩm quyền thì nó sẽ truy vấn trực tiếp các máy chủ tên đó, bỏ qua một số bước trong truy vấn DNS. Phím tắt này ngăn chặn việc tra cứu từ máy chủ tên gốc và .com (trong tìm kiếm của chúng tôi cho example.com) và giúp quá trình giải quyết truy vấn DNS diễn ra nhanh hơn.
	- Nếu trình phân giải không có bản ghi NS, nó sẽ gửi truy vấn đến máy chủ TLD (.com trong trường hợp của chúng tôi), bỏ qua máy chủ gốc.
	- Trong trường hợp hiếm gặp là trình phân giải không có bản ghi trỏ đến máy chủ TLD, thì nó sẽ truy vấn máy chủ gốc. Sự kiện này thường xảy ra sau khi bộ đệm DNS đã bị xóa.

# DNS server
Hệ thống tên miền (DNS) là danh bạ của Internet. Khi người dùng nhập tên miền như ‘google.com’ hoặc ‘nytimes.com’ vào trình duyệt web, DNS chịu trách nhiệm tìm địa chỉ IP chính xác cho các trang web đó. Sau đó, các trình duyệt sử dụng những địa chỉ đó để liên lạc với máy chủ gốc hoặc máy chủ biên CDN để truy cập thông tin trang web. Tất cả điều này xảy ra nhờ vào máy chủ DNS: máy chuyên trả lời các truy vấn DNS.