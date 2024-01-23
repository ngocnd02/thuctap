# ÔN TẬP CCNA

## VLAN, TRUNK, VLAN ROUTING
- Mở rộng mạng là nhu cầu tất yếu, cho nên các vấn đề xảy ra là không thể tránh được
- Khi mạng mở rộng thì sẽ phải gia tăng khoảng cách, Mà khoảng cách càng xa thì sự suy hao về tín hiệu càng lớn, và nó cũng có khoảng cách nhất định. Như vậy sẽ phải thêm switch. Như vậy muốn mở rộng mạng bắt buộc phải tăng switch (tăng khoảng cách, mật độ cổng)
- Các thiết bị nằm trong cùng mạng LAN gọi là physical LAN.
- Tuy nhiên khi mở rộng mạng LAN thì phải chú ý đến 2 vấn đề
	- COLLISION DOMAIN:  sw đã giải quyết vấn đề về xung đột khi tính năng full duplex ra đời. ( 1 port của sw là 1 collison domain riêng biệt).  Đây là lý do tại sao lại dung SW để xây dựng mạng LAN mà không phải repeater, không phải bridge, không phải hub. Như vậy vấn đề về xung đột thì SW đã có thể giải quyết. 

	- BROADCAST DOMAIN: SW có một hành vi là Frame Flooding với những gói tin MAC đích không có trong bảng MAC. Chính vì vậy khi chúng ta nối dài, mở rộng thêm mạng thì vô tình chúng ta kéo dài cái broadcast domain. Đó là lý do tại sao ngta dung SW để xây dụng mạng LAN, và dùng ROUTER để xây dựng mạng Wan. Vì SW không thể giải quyết các vấn đề về broadcast domain. Và Router ra đời để giải quyết vấn đề về broadcast. Chính vì vậy khi xây dựng hệ thống mạng thì phải có cả switch và router. 

- Và để giải quyết vấn đề Broadcast trong mạng LAN thì có VLAN
- VLAN (virtual LAN, logical LAN) được thiết lập trên mạng LAN vật lý.
- VLAN luôn tồn tại nhưng ban đầu Physical LAN và Logical LAN (VLAN) là giống hệt nhau
- Khi thiết lập vlan chính là thay đổi cấu trúc của logical lan trong khi giữ nguyên vị trí và cấu trúc của physical LAN

- Khi có nhiều VLAN trong mạng để giải quyết broadcast thì 1 vấn đề nữa lại xuất hiện , đó là các đường link nối các sw thì chỉ có 1 link. 

- Và với trạng thái Access Port thì chỉ cho 1 VLAN đi qua (carry traffic), cho nên giữa cách sw chỉ có thể nối được vài VLAN mà thôi, nếu có hàng tram VLAN thì không thể. Chính vì vậy phải có Trunk.

- Trunk bản chất là mạng traffic của nhiều VLAN đi qua “1 Link vật lý duy nhất”  Làm sao phân biệt được traffic của các VLAN đó. 

TAG/UNTAG
 Làm sao để thêm được cái thông tin đánh dấu vào Frame Header
- Ban đầu gói tin được đóng gói, không có bất kì thông tin nào về VLAN của gói tin đó.  Khi gói tin “Đi vào đường link Trunk” thì quá trình TRUNK ENCAPSULATION sẽ diễn ra”
- Encapsulation encapsulation : đóng gói những thông tin cần thiết để phân biệt traffic của các vlan khác nhau.

Có nhiều giao thức để làm điều này

- ISL (cisco): Với isl thì toàn bộ Ethernet Frame nó được đóng gói vào trong 1 cái header mới hoàn toàn . Và nếu chúng ta dung isl thì bắt buộc thiết bị đầu kia cũng phải là một thiết bị Cisco thì nói mới hiểu được nội dung của header.

- 802.1Q (IEEE): Với 802.1q thì nó k đóng gói toàn bộ Frame, mà nó chỉ đóng gói 1 trường nhỏ vào Etheren Frame. Ngta gọi nó là VLAN TAG. 
Vậy bản chất vlan TAG chính là 802.1q Header được đóng gói vào Ethernet Frame chứa thông tin vlan id để phân biệt các frame khi đi qua Trunk. 

Các giao thức đóng gói này sẽ được gỡ ra khi đi ra khỏi link Trunk ở đầu kia. Cho nên nếu ta có 2 link Trunk liên tiếp nhau thì ta có thể có 1 link ISL và 1 link 802.1Q.

 Đây là 2 giao thức đóng gói dữ liệu khi đi qua 2 đường link trunk. Bản chất ở đây mk phải hiểu là ban đầu nó không có nhưng sw nó muốn phân biệt được các gói khi đi qua đường link trunk thì nó phải đóng thêm các gói đấy vào. Nhưng mà nó dở Trunk là tính năng thiết lập trên 2 đầu cho nên đầu này đóng gói kiểu gì để đầu kia có thể hiểu được thì nó mới là vấn đề. Cho nên phải có giao thức để thống nhất để đóng gói dữ liệu khi đi qua Trunk. 



**THÔNG SỐ ĐẦU TIÊN KHI THIẾT LẬP TRUNK ĐÓ LÀ TRUNK ENCAPSULATION PROTOCOL**
- 2 đầu phải dung cùng một giao thức
- SW 2906 của ciso mặc định nó chỉ hỗ trợ duy nhất giao thức 802.1q . Cho nên chúng ta chỉ cần câu lệnh sw port mode trunk là xong. 

** Sau khi xác định Trunk Protocl xong thì quan tâm đến trunk mode**
1. Static trunk: Mode on (mode trunk)
2. DTP (Dynamic Trunk): Dynamic Auto, Dynamic Desirable.

Tham số thiết lập Trunk (nếu thiết lập sai 2 tham số này Trunk sẽ down)
- Switchport trunk encapsulation dot1q
- Switchport mode trunk

Sau khi thiết lập trunk có 2 tham số vận hành trên link trunk: CÁi này để xem những vlan nào được đi qua trunk. (Nếu thiết lập sai không làm down trunk nhưng nó chạy sai)
- VLAN allowed: Default allow all trên 1 số dòng sw cisco. (Để ý đến cái thiết kế của vendor để xem là mặc định nó cho những vlan nào đi qua)
- Native VLAN: Chứa các untagg traffic. Vd các control traffic sinh ra từ chính sw (DTP, STP, CDP, LACP, PAGP). ( GIẢI THÍCH : lưu lượng đến từ 1 vlan cụ thể thì gọi là tag, lưu lượng mà k thuộc về vlan nào thì gọi là untag, và chúng ta cần 1 vlan để xử lý những cái đấy thì gọi là NATVIE VLAN). 


### Inter VLAN routing: Định tuyến VLAN
Mô hình triển khai. Triển khai 3 phía
1. PC: Đặt ip và trỏ Default Gateway về VLAN tương ứng. 
2. Network trung gian (Thường là các sw): Chia Vlan và trunk về gateway, allow cho các vlan cần thiết
3. Gateway: Cần cấu hình để đáp ứng được số lượng Vlan

Spanning Tree
- Tạo ra nhằm loại bỏ “single point of failure”
- Duy trì được các đường đi dự phòng nhưng vẫn đảm bảo khả năng chống loop (loop-free redundant path)

ETHERCHANEL
- Gộp các LINK vật lý lại thành 1 link logic và quản lý qua 1 interfac logic gọi là port chanel
- Etherchannel chỉ giúp chúng ta gộp link thôi. Còn làm gì với cái link đó thì là việc của mình.

## ROUTER

Với router nó hoạt động xoanh quanh cái database với bảng định tuyến. 
1. Bảng định tuyến là gì?
Forwarding Database giống như bảng MAC của sw, CSDL để cung cấp thông tin cho Router trong quá trình “make forwarding decision”

2. Bảng định tuyến từ đâu mà có?
Router chia làm 2 loại mạng: 
- Directly Connected Networks: Khi 1 interface của router được gán địa chỉ ip và nó up lên thì router sẽ tự động học được cái mạng của interface đó.
 Các mạng kết nối trực tiếp cùng 1 router thì auto thông nhau

 Troubleshoot: Xây dựng như thế nào thì kiểm tra nó như thế. Như vậy phải nắm vững : Nguyên lý hoạt động (vì sao nó chạy?) và cấu hình cài đặt, thao tác, vận hành (làm sao cho nó chạy). 

- Remote Networks (static route, dynamic routing protocols)
 Đây là 2 kỹ thuật giúp Router xây dựng cái Forwarding Database chính là Routing table. Với static route: học qua admin (người cấu hình) thông qua các thông tin định tuyến được Admin nhập vào CLI , với danymic routing: học từ các router khác
VẬY: CÓ 2 NGUỒN ĐỂ ROUTER BUILT BẢNG ĐỊNH TUYẾN CỦA NÓ LÀ: 
Tự học từ chính các Interface của nó. 
Học từ người quản trị thông qua kĩ thuật static route
Học từ các router khác thông qua giao thức định tuyến nào đó. 
TẤT CẢ ĐỀU HƯỚNG TỚI 1 MỤC ĐÍCH GIÚP ROUTER CÀI ĐẶT ĐƯỢC THÔNG TIN CẦN THIẾT VÀO TRONG BẢNG ĐỊNH TUYẾN, VÀ TỪ ĐÓ ĐƯA RA CÁC XỬ LÝ DỰA VÀO NHỮNG THÔN TIN NÀY. 

3. Bảng định tuyến chứa thông tin gì
Lệnh xem thông tin bảng định tuyến trong router: show ip route
- Route Sources: nguồn gốc học được cái Route Entry đó (Bời vì 1 Router có thể biết nhiều đường đi tới cùng 1 đích) 
- Thông số tiếp là: Destination Prefix (Network) / Prefix Length  Thể hiện cái mạng đích mà Router đã biết. ROUTER CHỈ CÓ THỂ GỬI DỮ LIỆU TỚI NHỮNG MẠNG MÀ ĐÃ CÓ MẶT TRONG BẢNG ĐỊNH TUYẾN CỦA NÓ THÔI

- Administrative Distance (AD): là giá trị đi kèm theo 1 giao thức định tuyến, và nó thể hiện cái độ tin cậy của giao thức đó với Router. Khi 1 router biết “nhiều đường đi tới cùng 1 đích, và học qua các giao thức khác nhau” thì đường nào có AD thấp nhất sẽ trở thành đường đi tốt nhất.  Best route

- Metric: Chính là khái niệm của 1 giao thức về việc thế nào là đường đi tốt nhất mỗi giao thức sẽ có 1 công thức tính metric khác nhau, và đây là 1 giá trị cụ thể. 
 Rip: hop count: đếm số router dọc đường đi, đường nào ít hop nhất sẽ trở thành đường tốt nhất

 ospf: cost: Lấy bang thông tham chiếu chia cho bang thông của int, để tính ra cost. Đường nào có cost thấp nhất (băng thông cao nhất) sẽ thời thành đường tốt nhất. 
- Nếu các đường có AD, Metric bằng nhau thì nó sẽ xuất hiện load balancing  equal cost (path) load balancing. 

- Next-hop IP: Địa chỉ IP của router kế tiếp trên đường đi tới mạng đích

- Out/Exit/Egress Interface: là cái cổng của chính Router dùng để đẩy dữ liệu tới next-hop


4. Router sử dụng bảng định tuyến ntn?
Longest Prefix Match 

NOTE: 
Trước khi cài Route vào bảng định tuyến: 
- Router sẽ dung AD/Metric để tính toán đường đi tốt nhât. AD/Metric chỉ áp dụng cho các đường đi tới cùng 1 đích
Khi Route đã được cài vào bảng định tuyến rồi chúng đều là best route tới 1 mạng đích nào đó. 
- Lúc này router sẽ sử dụng Longest Prefix Match : cái này quyết định xem sử dụng tuyến nào để truyền dữ liệu. 
- CHỈ sử dụng phần “Prefix/Network” của Route Entry để so sánh với IP đích. Prefix nào khớp nhiều bit nhất với IP đích thì gọi là Longest Prefix Match. 
- MATCH: CÓ NGHĨA LÀ TOÀN BỘ BIT Ở PHẦN PREFIX CỦA ENTRY GIỐNG VỚI BIT CỦA IP ĐÍCH
Ví dụ: 
IP đích: 172.16.0.202
10101100.00010000.00000000.11001010
172.16.0.0 /16
10101100.00010000.		 00000000. 00000000
10101100.00010000.		00000000.11001010

 khớp 16 bit với mạng đích 
172.16.0.0 /24
10101100.00010000. 00000000.		 00000000
10101100.00010000.00000000.		11001010

 Khớp 24 bit với mạng đích 
172.16.0.128 /25
10101100.00010000. 00000000.1		0000000
10101100.00010000.00000000.1		1001010

	Khớp 25 bit
	Longest prefix match

172.16.0.192 /29
10101100.00010000. 00000000.11000		000
10101100.00010000.00000000.11001		010

	KHÔNG KHỚP/ NOT MATCH



Router nó là một Interme.. network Device, không phải là nơi phát sinh lưu lượng chính. 
 Trước khi Router có thể thực hiện chức năng của mình (Routing) thì end device cần phải có cơ chế đưa dữ liệu đến Router
 Default Gateway là ĐỊA CHỈ IP CỦA INTERFACE TRÊN BỘ ĐỊNH TUYẾN GẦN NHẤT CÙNG SUBNET VỚI CLINET”  bản chất của việc cài đặt Default Gateway đó là chúng ta đang nói cho các host biết bộ định tuyến gần nhất của nó nằm ở đâu. 
 Sau đó sử dụng ARP để đẩy dữ liệu tới gateway bằng địa chỉ MAC. 
 Với các gói tin cùng mạng, Mac đích là mac của host đích. Khi gửi gói tin ra ngoài mạng thì mac đích là mac của default gateway 

Khi Router nhận được dữ liệu thì nó xử lý thế nào? 
- Layer1: Decode và trả cho L2 Frame (bit) 
- Layer2: Đối chiếu địa chỉ MAC của Frame với MAC của Router. Nếu đúng thì chấp nhận xử lý, nếu không đúng thì Drop Frame. Và sau đó nó gỡ bỏ L2 Header

Có 2 nguyên nhân để nó gỡ bỏ L2 header
Để đọc được địa chỉ ip (L3 Header) thì bắt buộc phải gỡ L2 header đi
Router cần địa chỉ MAC nguồn, MAC đích mới trong chặng mới. 

- Layer 3: Tìm ra best path để forward dữ liệu  Thông qua bảng định tuyến. 

Sau đó muốn gửi dữ liệu đi 
- Layer 2: Đóng Layer 2 header mới với MAC nguồn và mac đích mới
- L1: encoding và signaling

 Đúng theo mô hình osi nhận thì đi từ dưới lên, chuyển thì đi từ trên xuống. Lưu ý đây đang nói về DATA FORWARDING. 


ĐỊNH TUYẾN
Static Routing
Để có thể chỉ đường cho Router thì mình phải biết là Router nó cần thông tin gì. Cần làm rõ 2 câu hỏi:
1. Đi đến đâu
2. Đi đường nào. 
Router cần thông tin gì thì mình phải chỉ cho nó cái thông tin đó. 

**IPv4 Static Route:**
1. Standard Static Route: Định tuyến cho 1 mạng cụ thể nào đó.
Ip route <mạng đích> <subnet mask> <next-hop> / <out=interface>
Ip route 192.168.1.0 255.255.255.0 fa0/1 192.168.10.1

2. Default Static Route: Định tuyến tới 0.0.0.0/0 ( để đại diện cho các mạng không có mặt trong bảng định tuyến)
Ip route 0.0.0.0 0.0.0.0 fa0/1 192.168.10.1

3. Floating Static Rotue: Đây là kỹ thuật thay đổi giá trị AD mặc định để tạo ra sự chênh lệch. Mục đích để tạo ra các đường đi dự phòng. 

Router không hề mất tí tài nguyên nào để tính toán các đường đi, mà nó chỉ cần lấy thông tin từ câu lệnh do người quản trị nhập vào CLI và cài luôn vào trong bản định tuyến. 

**Dynamic Routing Protocols**
Giao thức OSPF
Thành phần:
1. OSPF messages: Công cụ trao đổi thông tin OSPF giữa các router
- Hello packet: Sử dụng để thiết lập quan hệ hàng xóm giữa các Router. Sau khi thiết lập quan hệ hàng xóm xong thì chúng sẽ dung chính bản tin này để duy trì quan hệ hàng xóm

- Database description packet (DBD): Là bản tin dung để đồng bộ CSDL định tuyến giữa các router


- Link-state request packet (LSR): Là bản tin dung để yêu cầu những thông tin còn thiếu 

- Link -state update packet (LSU): Là bản tin để cập nhật thông tin cho 1 bản tin request trước đó

- Link-state acknowledgement packet (LsACK): là để xác nhận việc gửi thành công 1 bản tin Link State

2. 5 hoạt động chính
- Establish Neighbor Adjacencies (Thiết lập quan hệ thàng xóm)

- Exchange Link-state Advertisements: Các router sẽ đồng bộ trao đổi thông tin cho nhau

- Built the Link state Database: Xây dựng lên CSDL định tuyến OSPF

- Execute the SPF algorithm: Tính cost metric cho từng đường đi

- Choose the best route

3. Hoạt động dựa trên 3 loại CSDL
- Adjacency Database: Neighbor Table là bảng lưu trữ thông tin về hàng xóm

- Link-state Database (LSBD): Topology table lưu trữ toàn bộ thông tin định tuyến được học qua các Router khác

- Forwarding Database : Bảng routing table: là những tuyến tốt nhất do thuật toán lựa chọn được thì cài vào trong bảng định tuyến. 

4. Trong quá trình hoạt động các Router phải trải qua 8 trạng thái 

