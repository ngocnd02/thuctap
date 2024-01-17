[DNS record](#dns-record)

- [Các loại bản ghi DNS phổ biến](#cacloaibanghidns)
- [DNS A Record](#dns-a-record)
- [DNS CNAME Record](#dns-cname-record)
- [DNS MX Record](#dns-record)
- [DNS TXT Record](#dns-txt-record)
- [DNS NS Record](#dns-ns-record)
- [DNS SOA Record](#dns-soa-record)
- [DNS PTR Record](#dns-ptr-record)
- [DNS SPF record](#dns-spf-record)

# DNS record
- Bản ghi DNS (còn gọi là tệp vùng) là các hướng dẫn tồn tại trong các máy chủ DNS có thẩm quyền và cung cấp thông tin về miền, bao gồm địa chỉ IP nào được liên kết với miền đó và cách xử lý các yêu cầu đối với miền đó. Những bản ghi này bao gồm một loạt các tệp văn bản được viết bằng cú pháp DNS. Cú pháp DNS chỉ là một chuỗi ký tự được sử dụng làm lệnh cho máy chủ DNS biết phải làm gì. Tất cả các bản ghi DNS cũng có 'TTL', viết tắt của thời gian tồn tại và cho biết tần suất máy chủ DNS sẽ làm mới bản ghi đó.

- Bạn có thể coi một tập hợp các bản ghi DNS giống như danh sách doanh nghiệp trên Yelp. Danh sách đó sẽ cung cấp cho bạn nhiều thông tin hữu ích về doanh nghiệp như địa điểm, giờ làm việc, dịch vụ được cung cấp, v.v. Tất cả các tên miền đều phải có ít nhất một vài bản ghi DNS cần thiết để người dùng có thể truy cập trang web của họ bằng cách sử dụng một tên miền và có một số bản ghi tùy chọn phục vụ các mục đích bổ sung.

## Các loại bản ghi DNS phổ biến:
- **Bản ghi A** - Bản ghi chứa địa chỉ IP của miền.

- **Bản ghi AAAA** - Bản ghi chứa địa chỉ IPv6 cho một miền (trái ngược với bản ghi A liệt kê địa chỉ IPv4).

- **Bản ghi CNAME** - Chuyển tiếp một tên miền hoặc tên miền phụ sang tên miền khác, KHÔNG cung cấp địa chỉ IP.

- **Bản ghi MX** - Chuyển thư đến máy chủ email. Tìm hiểu thêm về bản ghi MX.

- **Bản ghi TXT** - Cho phép quản trị viên lưu trữ ghi chú văn bản trong bản ghi. Những hồ sơ này thường được sử dụng để bảo mật email. 

- **Bản ghi NS** - Lưu trữ máy chủ tên cho mục nhập DNS. Tìm hiểu thêm về bản ghi NS.

- **Bản ghi SOA** - Lưu trữ thông tin quản trị viên về một miền.

- **Bản ghi SRV** - Chỉ định cổng cho các dịch vụ cụ thể.

- **Bản ghi PTR** - Cung cấp tên miền khi tra cứu ngược.

## DNS A Record
- Chữ "A" là viết tắt của "Address" và đây là loại bản ghi DNS cơ bản nhất: nó cho biết địa chỉ IP của một miền nhất định. Ví dụ: nếu bạn lấy bản ghi DNS của cloudflare.com thì bản ghi A hiện trả về địa chỉ IP là: 104.17.210.9.
- Ví dụ về bản ghi A:

| example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| @ | A | 192.0.2.1 | 14400 |

- Ký hiệu **"@"** trong ngữ cảnh này thường được sử dụng để đại diện cho tên miền chính hoặc miền gốc. Do đó, bản ghi này áp dụng cho tên miền gốc của bạn hoặc tên miền chính mà nó đang mô tả.
- **192.168.1.1**: Đây là địa chỉ IPv4 mà tên miền được ánh xạ tới. Trong ví dụ này, tên miền chính hoặc tên miền gốc (được đại diện bởi "@") được ánh xạ đến địa chỉ IPv4 192.168.1.1.
- **TTL 14400**: TTL (Time to Live) là thời gian mà bản ghi DNS này sẽ được lưu trong bộ nhớ cache trước khi cần phải được cập nhật từ nguồn gốc. Giá trị 14400 giây tương ứng với 4 giờ. Sau thời gian này, máy chủ DNS sẽ phải thực hiện một truy vấn mới để kiểm tra xem bản ghi có sự thay đổi hay không.

### BẢn ghi A được sử dụng khi nào?
- Cách sử dụng phổ biến nhất của bản ghi A là tra cứu địa chỉ IP: khớp tên miền (như "cloudflare.com") với địa chỉ IPv4. Điều này cho phép thiết bị của người dùng kết nối và tải một trang web mà không cần người dùng ghi nhớ và nhập địa chỉ IP thực tế. Trình duyệt web của người dùng sẽ tự động thực hiện việc này bằng cách gửi truy vấn đến trình phân giải DNS.

## DNS CNAME Record
- Bản ghi "tên chuẩn" (CNAME) trỏ từ miền bí danh đến miền "chuẩn". Bản ghi CNAME được sử dụng thay cho bản ghi A khi tên miền hoặc tên miền phụ là bí danh của tên miền khác. Tất cả bản ghi CNAME phải trỏ đến một miền, không bao giờ trỏ tới địa chỉ IP.

- Ví dụ: giả sử blog.example.com có bản ghi CNAME có giá trị "example.com" (không có "blog"). Điều này có nghĩa là khi máy chủ DNS truy cập các bản ghi DNS cho blog.example.com, nó thực sự kích hoạt một tra cứu DNS khác cho example.com, trả về địa chỉ IP của example.com thông qua bản ghi A của nó. Trong trường hợp này, chúng tôi sẽ nói rằng example.com là tên chuẩn (hoặc tên thật) của blog.example.com.
- Khi các trang web có tên miền phụ như blog.example.com hoặc shop.example.com, những tên miền phụ đó sẽ có bản ghi CNAME trỏ đến tên miền gốc (example.com). Bằng cách này, nếu địa chỉ IP của máy chủ thay đổi, chỉ bản ghi DNS A cho tên miền gốc cần được cập nhật và tất cả các bản ghi CNAME sẽ tuân theo bất kỳ thay đổi nào được thực hiện đối với tên miền gốc.
- Ví dụ của bản ghi CNAME:

| blog.example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| blog.example.com | CNAME | is an alias of example.com | 32600 |

Trong ví dụ này, bạn có thể thấy rằng blog.example.com trỏ đến example.com.

### Bản ghi CNAME có thể trỏ tới bản ghi CNAME khác không?
- Việc trỏ bản ghi CNAME vào bản ghi CNAME khác là không hiệu quả vì nó yêu cầu nhiều lần tra cứu DNS trước khi có thể tải miền — điều này làm chậm trải nghiệm người dùng — nhưng điều đó là có thể. Ví dụ: blog.example.com có thể có bản ghi CNAME trỏ đến bản ghi CNAME của www.example.com, sau đó bản ghi này trỏ tới bản ghi A của example.com.

| blog.example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| blog.example.com | CNAME | is an alias of example.com | 32600 |

| www.example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| www.example.com | CNAME | is an alias of example.com | 32600 |

- Cấu hình này bổ sung thêm một bước vào quá trình tra cứu DNS và nên tránh nếu có thể. Thay vào đó, bản ghi CNAME cho cả blog.example.com và www.example.com phải trỏ trực tiếp đến example.com.

### Những hạn chế của việc sử dụng bản ghi CNAME
Bản ghi MX và NS không thể trỏ tới bản ghi CNAME; họ phải trỏ đến bản ghi A (đối với IPv4) hoặc bản ghi AAAA (đối với IPv6). Bản ghi MX là bản ghi trao đổi thư hướng email đến máy chủ thư. Bản ghi NS là bản ghi "máy chủ tên" và cho biết máy chủ DNS nào có thẩm quyền cho tên miền đó.

## DNS MX Record
- Bản ghi 'trao đổi thư' (MX) DNS sẽ chuyển email đến máy chủ thư. Bản ghi MX cho biết cách định tuyến thư email theo Giao thức truyền thư đơn giản (SMTP, giao thức chuẩn cho tất cả email). Giống như bản ghi CNAME, bản ghi MX phải luôn trỏ đến một tên miền khác.
- Ví dụ của bản ghi MX:

![Imgur](https://i.imgur.com/n3NhAtI.png)

- Số 'priority' trước tên miền của các bản ghi MX này biểu thị mức độ ưu tiên; giá trị 'priority' thấp hơn được ưu tiên. Máy chủ sẽ luôn thử mailhost1 trước vì 10 nhỏ hơn 20. Trong trường hợp gửi tin nhắn không thành công, máy chủ sẽ mặc định là mailhost2.

- Dịch vụ email cũng có thể định cấu hình bản ghi MX này để cả hai máy chủ đều có mức độ ưu tiên như nhau và nhận được lượng thư như nhau:

![Imgur](https://i.imgur.com/8KxmeuM.png)

Cấu hình này cho phép nhà cung cấp email cân bằng tải giữa hai máy chủ.

### Quá trình truy vấn bản ghi MX
- Message Tranfer Agent (MTA) chịu trách nhiệm truy vấn các bản ghi MX. Khi người dùng gửi email, MTA sẽ gửi truy vấn DNS để xác định máy chủ thư cho người nhận email. MTA thiết lập kết nối SMTP với các máy chủ thư đó, bắt đầu bằng các miền được ưu tiên (trong ví dụ đầu tiên ở trên, mailhost1).

## DNS TXT Record
- Bản ghi 'văn bản' (TXT) DNS cho phép quản trị viên tên miền nhập văn bản vào Hệ thống tên miền (DNS). Bản ghi TXT ban đầu được dự định là nơi dành cho các ghi chú mà con người có thể đọc được. Tuy nhiên, hiện nay cũng có thể đưa một số dữ liệu máy đọc được vào bản ghi TXT. Một tên miền có thể có nhiều bản ghi TXT.
- Ví dụ bản ghi MX:

![Imgur](https://i.imgur.com/ydUToRk.png)

- Ngày nay, hai trong số những ứng dụng quan trọng nhất đối với bản ghi DNS TXT là ngăn chặn spam email và xác minh quyền sở hữu tên miền, mặc dù ban đầu bản ghi TXT không được thiết kế cho những mục đích sử dụng này.

## DNS NS Record
- NS là viết tắt của 'Nameserver' và bản ghi máy chủ tên cho biết máy chủ DNS nào có thẩm quyền cho tên miền đó (tức là máy chủ nào chứa bản ghi DNS thực tế). Về cơ bản, bản ghi NS cho Internet biết nơi cần tìm để tìm địa chỉ IP của tên miền. Một miền thường có nhiều bản ghi NS có thể chỉ ra máy chủ tên chính và phụ cho miền đó. Nếu không cấu hình đúng bản ghi NS, người dùng sẽ không thể tải trang web hoặc ứng dụng.
- Ví dụ về bản ghi NS:

![Imgur](https://i.imgur.com/O7FcGKv.png)

- **NOTE**: Lưu ý rằng bản ghi NS không bao giờ có thể trỏ tới bản ghi CNAME.

### Nameserver là gì?
- Nameserver là một loại máy chủ DNS. Đây là máy chủ lưu trữ tất cả các bản ghi DNS cho một tên miền, bao gồm bản ghi A, bản ghi MX hoặc bản ghi CNAME.

- Hầu hết tất cả các miền đều dựa vào nhiều nameserver để tăng độ tin cậy: nếu một nameserver ngừng hoạt động hoặc không khả dụng, các truy vấn DNS có thể chuyển sang một nameserver khác. Thông thường có một máy chủ tên chính và một số máy chủ tên phụ lưu trữ các bản sao chính xác của bản ghi DNS trong máy chủ chính. Việc cập nhật máy chủ tên chính cũng sẽ kích hoạt cập nhật máy chủ tên phụ.

- Khi sử dụng nhiều máy chủ tên (như trong hầu hết các trường hợp), bản ghi NS sẽ liệt kê nhiều máy chủ

### Khi nào hồ sơ NS nên được cập nhật hoặc thay đổi?
- Quản trị viên tên miền nên cập nhật bản ghi NS của họ khi họ cần thay đổi máy chủ định danh của tên miền. Ví dụ: một số nhà cung cấp đám mây cung cấp máy chủ tên và yêu cầu khách hàng trỏ tới chúng.

- Quản trị viên cũng có thể muốn cập nhật bản ghi NS của mình nếu họ muốn một tên miền phụ sử dụng các máy chủ tên khác nhau. Trong ví dụ trên, máy chủ tên cho example.com là ns1.exampleserver.com. Thay vào đó, nếu quản trị viên example.com muốn blog.example.com giải quyết thông qua ns2.exampleserver.com thì họ có thể thiết lập điều này bằng cách cập nhật bản ghi NS.

- Khi bản ghi NS được cập nhật, có thể mất vài giờ để các thay đổi được sao chép trên toàn bộ DNS.

## DNS SOA record
- Bản ghi 'start of authority' (SOA) DNS lưu trữ thông tin quan trọng về miền hoặc vùng, chẳng hạn như địa chỉ email của quản trị viên, thời điểm miền được cập nhật lần cuối và máy chủ sẽ đợi bao lâu giữa các lần làm mới.

- Tất cả các vùng DNS đều cần bản ghi SOA để tuân thủ các tiêu chuẩn IETF. Các bản ghi SOA cũng rất quan trọng đối với việc chuyển vùng.

![Imgur](https://i.imgur.com/4WTE3rG.png)

- Trong đó:
	- MNAME: đại diện cho tên miền của máy chủ chính quản lý (Primary Master Server). Nó chỉ định tên miền của máy chủ chính, nơi mà mọi sự thay đổi trên tên miền được thực hiện và nơi mà các bản sao của dữ liệu tên miền được đồng bộ hóa từ.
	- RNAME: đại diện cho địa chỉ email của người quản trị tên miền. Thông số này thường được sử dụng để liên lạc với người quản trị nếu có vấn đề kỹ thuật hoặc thông tin quan trọng về tên miền.
	- SERIAL: Số này được tăng lên mỗi khi có sự thay đổi trên tên miền, và nó giúp xác định phiên bản hiện tại của dữ liệu tên miền.
	- REFRESH: xác định khoảng thời gian mà các máy chủ tên khác nhau nên chờ trước khi truy vấn máy chủ chính để lấy bản sao mới nhất của dữ liệu tên miền. Thông số này được đo bằng giây và ảnh hưởng đến tần suất mà các máy chủ tên cần liên lạc với máy chủ chính để đồng bộ hóa dữ liệu.
	- RETRY:định nghĩa thời gian mà các máy chủ tên khác nhau nên chờ trước khi cố gắng liên lạc lại với máy chủ chính nếu họ không thể kết nối được trong khoảng thời gian "Refresh". Thông số này được đo bằng giây và ảnh hưởng đến tần suất mà các máy chủ tên sẽ thử kết nối lại sau mỗi thời gian Retry.
	- EXPIRE:xác định thời gian tối đa mà dữ liệu tên miền có thể được sử dụng trước khi được coi là không còn hợp lệ. Nếu một máy chủ tên không thể cập nhật dữ liệu từ máy chủ chính trong khoảng thời gian "Expire", nó sẽ không còn được sử dụng để đáp ứng các truy vấn về tên miền đó.(Đo bằng giây)

## DNS PTR Record
Hệ thống tên miền hoặc DNS tương quan tên miền với địa chỉ IP. Bản ghi con trỏ DNS (viết tắt là PTR) cung cấp tên miền được liên kết với địa chỉ IP. Bản ghi DNS PTR hoàn toàn trái ngược với bản ghi 'A', bản ghi này cung cấp địa chỉ IP được liên kết với một tên miền.

Bản ghi DNS PTR được sử dụng trong tra cứu DNS ngược. Khi người dùng cố gắng truy cập một tên miền trong trình duyệt của họ, quá trình tra cứu DNS sẽ diễn ra, khớp tên miền với địa chỉ IP. Tra cứu DNS ngược là quy trình ngược lại với quy trình này: đó là truy vấn bắt đầu bằng địa chỉ IP và tra cứu tên miền.

### Bản ghi DNS PTR được lưu trữ như thế nào?
Trong IPv4:
- Trong khi các bản ghi DNS A được lưu trữ dưới tên miền nhất định, các bản ghi DNS PTR được lưu trữ dưới địa chỉ IP — đảo ngược và được thêm ".in-addr.arpa". Ví dụ: bản ghi PTR cho địa chỉ IP 192.0.2.255 sẽ được lưu trữ trong "255.2.0.192.in-addr.arpa".

- "in-addr.arpa" phải được thêm vì bản ghi PTR được lưu trữ trong miền cấp cao nhất .arpa trong DNS. .arpa là miền được sử dụng chủ yếu để quản lý cơ sở hạ tầng mạng và là tên miền cấp cao nhất đầu tiên được xác định cho Internet. (Tên "arpa" có từ những ngày đầu tiên của Internet: nó lấy tên từ Cơ quan Dự án Nghiên cứu Nâng cao (ARPA), cơ quan đã tạo ra ARPANET, tiền thân quan trọng của Internet.)

- in-addr.arpa là không gian tên trong .arpa để tra cứu DNS ngược trong IPv4.

### Một số ứng dụng chính của bản ghi PTR là gì?
- Bản ghi PTR được sử dụng để tra cứu DNS ngược; cách sử dụng phổ biến cho DNS ngược bao gồm:

- Chống thư rác: Một số bộ lọc chống thư rác email sử dụng DNS ngược để kiểm tra tên miền của địa chỉ email và xem liệu các địa chỉ IP được liên kết có thể được sử dụng bởi các máy chủ email hợp pháp hay không.

- Khắc phục sự cố gửi email: Vì các bộ lọc chống thư rác thực hiện các bước kiểm tra này nên sự cố gửi email có thể xảy ra do bản ghi PTR bị định cấu hình sai hoặc bị thiếu. Nếu một miền không có bản ghi PTR hoặc nếu bản ghi PTR chứa miền không đúng thì dịch vụ email có thể chặn tất cả email từ miền đó.

- Ghi nhật ký: Nhật ký hệ thống thường chỉ ghi lại địa chỉ IP; tra cứu DNS ngược có thể chuyển đổi chúng thành tên miền cho nhật ký dễ đọc hơn.

## DNS SPF record
- Một bản ghi Sender Policy Framework (SPF) là một loại bản ghi DNS TXT, liệt kê tất cả các máy chủ được ủy quyền để gửi email từ một tên miền cụ thể. Bản ghi DNS TXT ("text") cho phép người quản trị tên miền nhập văn bản tùy ý vào Hệ thống Tên Miền (DNS). Ban đầu, các bản ghi TXT được tạo ra để chứa thông báo quan trọng về tên miền, nhưng sau đó đã phát triển để phục vụ các mục đích khác.

- SPF được tạo ra vì giao thức tiêu chuẩn sử dụng cho email — giao thức Simple Mail Transfer Protocol (SMTP) — không xác thực địa chỉ "from" (từ) của một email theo cách tự nhiên. Điều này có nghĩa là nếu không có SPF hoặc các bản ghi xác thực khác, một kẻ tấn công có thể dễ dàng giả mạo người gửi và lừa người nhận thực hiện hành động hoặc chia sẻ thông tin mà họ không muốn.

- Hãy tưởng tượng bản ghi SPF như một danh sách khách mà quản lý bởi người giữ cửa. Nếu ai đó không có tên trong danh sách, người giữ cửa sẽ không cho họ vào. Tương tự, nếu một bản ghi SPF không có địa chỉ IP hoặc tên miền của người gửi trong danh sách, máy chủ nhận (người giữ cửa) sẽ enther không phân phối những email đó hoặc đánh dấu chúng là thư rác.

- Bản ghi SPF chỉ là một trong nhiều cơ chế dựa trên DNS có thể giúp máy chủ email xác nhận xem một email có đến từ nguồn đáng tin cậy hay không. Domain-based Message Authentication Reporting and Conformance (DMARC) và DomainKeys Identified Mail (DKIM) là hai cơ chế khác được sử dụng để xác thực email.

- Lưu ý rằng, vào một thời điểm nào đó, bản ghi SPF đã có một loại bản ghi DNS riêng biệt. Loại bản ghi riêng biệt này đã được loại bỏ và chỉ còn sử dụng bản ghi TXT.

### Máy chủ thư kiểm tra bản ghi SPF bằng cách nào?
Máy chủ thư trải qua một quy trình tương đối đơn giản khi kiểm tra bản ghi SPF:
- Máy chủ Một gửi email. Địa chỉ IP của nó là 192.0.2.0 và đường dẫn trả về mà email sử dụng là email@returnpath.com. (Địa chỉ đường dẫn trả về khác với địa chỉ “from” và được sử dụng riêng để thu thập và xử lý thư bị trả lại.)

- Máy chủ thư đang nhận thư (Máy chủ thứ hai) lấy miền đường dẫn trả về và tìm kiếm bản ghi SPF của nó.

- Nếu Máy chủ Hai tìm thấy bản ghi SPF cho miền của đường dẫn trả về, thì nó sẽ tìm kiếm bản ghi SPF cho địa chỉ IP của Máy chủ Một trong danh sách người gửi được ủy quyền. Nếu địa chỉ IP được liệt kê trong bản ghi SPF, quá trình kiểm tra SPF sẽ vượt qua và email sẽ được thực hiện. Nếu địa chỉ IP không được liệt kê trong bản ghi SPF thì việc kiểm tra SPF không thành công. Trong trường hợp này, email sẽ bị từ chối hoặc bị đánh dấu là thư rác.

### Bản ghi SPF trông như thế nào?
Bản ghi SPF phải tuân theo các tiêu chuẩn nhất định để máy chủ hiểu cách diễn giải nội dung của nó. Dưới đây là ví dụ về các thành phần cốt lõi của bản ghi SPF:

`v=spf1 ip4:192.0.2.0 ip4:192.0.2.1 include:examplesender.email -all`

Ví dụ này cho phép máy chủ biết đây là loại bản ghi nào, nêu rõ các địa chỉ IP được phê duyệt và bên thứ ba cho miền này, đồng thời cho máy chủ biết phải làm gì với các email không tuân thủ. Hãy chia nhỏ cách các thành phần riêng lẻ thực hiện điều này:

- **v=spf1** cho máy chủ biết rằng nó chứa bản ghi SPF. Mọi bản ghi SPF phải bắt đầu bằng chuỗi này.
- Sau đó là phần “danh sách khách” của bản ghi SPF hoặc danh sách các địa chỉ IP được ủy quyền. Trong ví dụ này, bản ghi SPF thông báo cho máy chủ rằng ip4:192.0.2.0 và ip4:192.0.2.1 được phép gửi email thay mặt cho miền.
- **include:examplesender.net** là một ví dụ về thẻ include, thẻ này cho máy chủ biết tổ chức bên thứ ba nào được ủy quyền gửi email thay mặt cho miền. Thẻ này báo hiệu rằng nội dung của bản ghi SPF cho miền được bao gồm (examplesender.net) cần được kiểm tra và các địa chỉ IP chứa trong đó cũng phải được coi là được ủy quyền. Nhiều tên miền có thể được bao gồm trong bản ghi SPF nhưng thẻ này sẽ chỉ hoạt động đối với các tên miền hợp lệ.
- Cuối cùng, **-all** cho máy chủ biết rằng các địa chỉ không được liệt kê trong bản ghi SPF không được phép gửi email và sẽ bị từ chối.
Các tùy chọn thay thế ở đây bao gồm ~all, cho biết rằng các email không công khai sẽ bị đánh dấu là không an toàn hoặc spam nhưng vẫn được chấp nhận và ít phổ biến hơn là +all, biểu thị rằng bất kỳ máy chủ nào cũng có thể gửi email thay mặt cho miền của bạn.

Mặc dù ví dụ được sử dụng trong bài viết này khá đơn giản nhưng các bản ghi SPF chắc chắn có thể phức tạp hơn. Sau đây là một số điều cần lưu ý để đảm bảo bản ghi SPF hợp lệ:

- Không thể có nhiều hơn một bản ghi SPF được liên kết với một tên miền.
Bản ghi phải kết thúc bằng thành phần all hoặc bao gồm thành phần redirect= (cho biết rằng bản ghi SPF được lưu trữ bởi một tên miền khác).
- Bản ghi SPF không thể chứa các ký tự viết hoa.

### Tại sao lại sử dụng bản ghi SPF?

Có nhiều lý do mà các nhà quản trị tên miền sử dụng bản ghi SPF:

- Ngăn chặn các cuộc tấn công: Nếu email không được xác thực, doanh nghiệp và người nhận email có nguy cơ bị tấn công phishing, thư rác và giả mạo email. Với bản ghi SPF, việc mô phỏng một tên miền trở nên khó khăn đối với những kẻ tấn công, giảm nguy cơ của những cuộc tấn công này.

- Cải thiện khả năng phân phối email: Các tên miền không có bản ghi SPF có thể gặp phải tình trạng thư bị trả lại hoặc đánh dấu là thư rác. Theo thời gian, những email bị trả lại hoặc đánh dấu là thư rác có thể làm tổn thương khả năng của tên miền đó đến hộp thư đến của khách hàng, nhân viên và các đối tác khác.

- Tuân thủ DMARC: DMARC là một hệ thống xác nhận email giúp đảm bảo rằng email chỉ được gửi bởi người dùng được ủy quyền. Các chính sách DMARC quy định các máy chủ nên xử lý email không qua các kiểm tra SPF và DKIM. Dựa trên hướng dẫn chính sách DMARC, những email này sẽ được đánh dấu là thư rác, từ chối hoặc gửi như thông thường. Quản trị viên tên miền nhận được báo cáo về hoạt động email của họ để giúp họ điều chỉnh chính sách của mình.