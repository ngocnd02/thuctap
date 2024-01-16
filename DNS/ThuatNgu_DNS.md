[DNS glossary](#dns-glossary)

- [DNS Zone](#dns-zone)

- [Primary vs secondary DNS](#primary-vs-secondary-dns)

- [Top level domain](#top-level-domain)

# DNS Glossary

## DNS Zone
- DNS được chia thành nhiều vùng khác nhau. Các vùng này phân biệt giữa các vùng được quản lý rõ ràng trong không gian tên DNS. Vùng DNS là một phần của không gian tên DNS được quản lý bởi một tổ chức hoặc quản trị viên cụ thể. Vùng DNS là không gian quản trị cho phép kiểm soát chi tiết hơn các thành phần DNS, chẳng hạn như máy chủ tên có thẩm quyền. Không gian tên miền là một cây phân cấp, với tên miền gốc DNS ở trên cùng. Vùng DNS bắt đầu tại một miền trong cây và cũng có thể mở rộng xuống các miền phụ để một thực thể có thể quản lý nhiều miền phụ.

- Một lỗi phổ biến là liên kết vùng DNS với một tên miền hoặc một máy chủ DNS. Trên thực tế, một vùng DNS có thể chứa nhiều tên miền phụ và nhiều vùng có thể tồn tại trên cùng một máy chủ. Các vùng DNS không nhất thiết phải tách biệt về mặt vật lý với nhau, các vùng được sử dụng nghiêm ngặt để phân quyền kiểm soát.

- Ví dụ: hãy tưởng tượng một vùng giả định cho miền cloudflare.com và ba tên miền phụ của nó: support.cloudflare.com, Community.cloudflare.com và blog.cloudflare.com. Giả sử blog là một trang web độc lập, mạnh mẽ cần quản trị riêng nhưng các trang cộng đồng và hỗ trợ được liên kết chặt chẽ hơn với cloudflare.com và có thể được quản lý trong cùng vùng với tên miền chính. Trong trường hợp này, cloudflare.com cũng như các trang hỗ trợ và cộng đồng đều sẽ nằm trong một vùng, trong khi blog.cloudflare.com sẽ tồn tại trong vùng riêng của nó.

![Imgur](https://i.imgur.com/gtyqHKw.png)

### Reverse Lookup Zone
- Reverse lookup zone (vùng tra cứu ngược) chứa ánh xạ từ địa chỉ IP đến máy chủ (chức năng ngược lại của hầu hết các vùng DNS). Các vùng này được sử dụng để khắc phục sự cố, lọc thư rác và phát hiện bot.

### DNS zone file
- Tệp vùng là một tệp văn bản thuần túy được lưu trữ trong máy chủ DNS chứa đại diện thực tế của vùng và chứa tất cả các bản ghi cho mọi miền trong vùng. Các tệp vùng phải luôn bắt đầu bằng bản ghi SOA, chứa thông tin quan trọng bao gồm thông tin liên hệ của quản trị viên vùng.

## Primary vs secondary DNS
### Primary DNS server
- DNS, hay Hệ thống tên miền, dịch tên miền thành địa chỉ IP để người dùng có thể dễ dàng điều hướng đến các trang web trên Internet mà không cần phải ghi nhớ các chuỗi số và chữ cái cụ thể, dài dòng.

- Trong hệ thống này, máy chủ DNS chính là máy chủ lưu trữ tệp vùng chính của trang web. Đây là tệp cơ sở dữ liệu văn bản chứa tất cả thông tin đáng tin cậy cho một tên miền, bao gồm địa chỉ IP, danh tính của quản trị viên tên miền và các bản ghi tài nguyên khác nhau. Bản ghi tài nguyên liệt kê tên miền cùng với địa chỉ IP tương ứng của chúng và có thể có nhiều dạng khác nhau: A record, AAAA record, MX record, NS record. 

- Các máy chủ chính cũng chịu trách nhiệm thực hiện mọi thay đổi cần thiết đối với bản ghi DNS của vùng. Sau khi máy chủ chính hoàn tất cập nhật, nó có thể chuyển các yêu cầu thay đổi đến máy chủ phụ.

### Secondary DNS server

- Máy chủ DNS chính chứa tất cả các bản ghi tài nguyên có liên quan và xử lý các truy vấn DNS cho một miền. Ngược lại, máy chủ DNS thứ cấp chứa các bản sao tệp vùng ở chế độ chỉ đọc, nghĩa là chúng không thể sửa đổi được. Thay vì lấy thông tin từ các tệp cục bộ, họ nhận được thông tin thích hợp từ máy chủ chính trong quy trình liên lạc được gọi là chuyển vùng.

- Việc chuyển vùng trở nên phức tạp hơn khi chúng được hoàn thành giữa nhiều máy chủ phụ. Nếu một số máy chủ phụ đang được sử dụng, một máy chủ có thể được chỉ định là máy chủ phụ cấp cao hơn để nó có khả năng sao chép các bản sao tệp vùng sang nhóm máy chủ phụ còn lại.

### Lợi ích của việc dùng máy chủ phụ
Có hai lợi ích chính của việc sử dụng máy chủ DNS phụ:
- Dự phòng và khả năng phục hồi: Chỉ dựa vào một máy chủ DNS sẽ tạo ra một điểm lỗi duy nhất. Nếu máy chủ chính bị lỗi hoặc bị xâm phạm do một cuộc tấn công, khách truy cập tiềm năng sẽ không thể truy cập vào miền mong muốn nữa. Việc sử dụng máy chủ thứ cấp sẽ tạo ra sự dự phòng và khiến người dùng ít gặp phải tình trạng gián đoạn dịch vụ hơn.
- Cân bằng tải: Máy chủ DNS phụ có thể chia sẻ gánh nặng của các yêu cầu đến miền để máy chủ chính không bị quá tải và gây ra tình trạng từ chối dịch vụ. Họ thực hiện việc này bằng cách sử dụng DNS luân chuyển, một kỹ thuật cân bằng tải được thiết kế để gửi lượng lưu lượng truy cập gần bằng nhau đến mỗi máy chủ.

## Top level domain
Trong hệ thống phân cấp DNS, tên miền cấp cao nhất (TLD) đại diện cho điểm dừng đầu tiên sau vùng gốc. Nói một cách đơn giản hơn, TLD là tất cả những gì nằm sau dấu chấm cuối cùng của tên miền. Ví dụ: trong tên miền ‘google.com’, ‘.com’ là TLD. Một số TLD phổ biến khác bao gồm ‘.org’, ‘.uk’ và ‘.edu’.

TLD đóng vai trò quan trọng trong quá trình tra cứu DNS. Đối với tất cả các yêu cầu không được lưu trong bộ nhớ đệm, khi người dùng nhập tên miền như ‘google.com’ vào cửa sổ trình duyệt của họ, trình phân giải DNS sẽ bắt đầu tìm kiếm bằng cách liên lạc với máy chủ TLD. Trong trường hợp này, TLD là ‘.com’, do đó trình phân giải sẽ liên hệ với máy chủ DNS TLD, sau đó máy chủ này sẽ cung cấp cho trình phân giải địa chỉ IP của máy chủ gốc của Google.

Tập đoàn Internet cấp số và tên miền (ICANN) có thẩm quyền đối với tất cả các TLD được sử dụng trên Internet và ủy quyền trách nhiệm của các TLD này cho các tổ chức khác nhau. Ví dụ: một công ty Hoa Kỳ có tên VeriSign vận hành tất cả các TLD ‘.com’ và ‘.net’.

Một mục đích khác của TLD là giúp phân loại và truyền đạt mục đích của tên miền. Mỗi TLD sẽ cho bạn biết điều gì đó về miền đứng trước nó; Hãy xem một số ví dụ:

'.com' dành cho các doanh nghiệp thương mại.
'.gov' dành cho các tổ chức chính phủ Hoa Kỳ.
'.uk' dành cho các miền từ Vương quốc Anh.
Bản thân TLD cũng được phân loại thành một trong một số nhóm.
