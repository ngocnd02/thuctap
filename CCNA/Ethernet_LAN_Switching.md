# Analyzing Ethernet LAN Switching

## Ethernet Switching Concepts

### Overview of Switching Logic
- Vai trò của một swtich LAN là chuyển tiếp các khung Ethernet. Mạng LAN tồn tại dưới dạng một tập hợp các thiết bị người dùng, máy chủ và các thiết bị khác kết nối vào các swtich, với các công tắc kết nối với nhau. Swtich LAN có một công việc chính: chuyển tiếp các khung đến địa chỉ đích (MAC) đúng. Và để đạt được mục tiêu đó, các swtich sử dụng logic - logic dựa trên địa chỉ MAC nguồn và đích trong tiêu đề Ethernet của mỗi khung.

- Các swtich LAN nhận các khung Ethernet và sau đó đưa ra quyết định chuyển tiếp: hoặc chuyển tiếp khung qua các cổng khác hoặc bỏ qua khung. Để thực hiện nhiệm vụ chính này, các công tắc thực hiện ba hành động:

1. Quyết định khi nào chuyển tiếp một khung hoặc khi nào lọc (không chuyển tiếp) một khung, dựa trên địa chỉ MAC đích.
2. Chuẩn bị chuyển tiếp các khung bằng cách học địa chỉ MAC thông qua việc kiểm tra địa chỉ MAC nguồn của mỗi khung được swtich nhận.
3. Chuẩn bị chuyển tiếp chỉ một bản sao của khung đến đích bằng cách tạo môi trường không lặp (Layer 2) với các swtich khác thông qua việc sử dụng Spanning Tree Protocol (STP).

![Imgur](https://i.imgur.com/y3g9Qsy.png)

Hành động đầu tiên là công việc chính của công tắc, trong khi hai mục khác là các chức năng phụ.

### Forwarding Know Unicast Frames
- Để quyết định liệu có chuyển tiếp một khung hay không, một swtich sử dụng một bảng được xây dựng động liệt liệt kê địa chỉ MAC và các giao diện xuất đi. Các swtich so sánh địa chỉ MAC đích của khung với bảng này để quyết định liệu swtich nên chuyển tiếp một khung hay đơn giản là bỏ qua nó. Ví dụ, xem xét mạng đơn giản trong Hình 5-3, với Fred gửi một khung đến Barney.

- Trong hình này, Fred gửi một khung với địa chỉ đích là 0200.2222.2222 (địa chỉ MAC của Barney). Swtich so sánh địa chỉ MAC đích (0200.2222.2222) với bảng địa chỉ MAC, kết hợp với mục bảng đậm. Mục bảng được kết hợp này bảo cho swtich chuyển tiếp khung qua cổng F0/2 và chỉ cổng F0/2.

**NOTE** A switch’s MAC address table is also called the switching table, or bridging table, or even the Content-Addressable Memory (CAM) table, in reference to the type of physical memory used to store the table.

![Imgur](https://i.imgur.com/EaBQoWy.png)

- Bảng địa chỉ MAC của một swtich liệt kê vị trí của mỗi địa chỉ MAC liên quan đến chính công tắc đó. Trong các LAN có nhiều swtich, mỗi swtich đưa ra một quyết định chuyển tiếp độc lập dựa trên bảng địa chỉ MAC của chính nó. Cùng nhau, chúng chuyển tiếp khung để nó cuối cùng đến đích.

- Ví dụ, Hình 5-4 thể hiện quyết định chuyển mạch đầu tiên trong trường hợp Fred gửi một khung đến Wilma, với địa chỉ MAC đích là 0200.3333.3333. Topology đã thay đổi so với hình trước, lần này có hai swtich và Fred cùng Wilma được kết nối đến hai swtich khác nhau. Hình 5-3 thể hiện logic của swtich đầu tiên, phản ứng với việc Fred gửi khung ban đầu. Đơn giản, swtich nhận khung tại cổng F0/1, tìm thấy địa chỉ MAC đích (0200.3333.3333) trong bảng địa chỉ MAC, thấy cổng xuất đi là G0/1, vì vậy SW1 chuyển tiếp khung qua cổng G0/1 của nó.

![Imgur](https://i.imgur.com/VQyuRsL.png)

- Khung đó sau đó đến tới swtich SW2, đi vào cổng G0/2 của SW2. Như được thể hiện trong Hình 5-5, SW2 sử dụng các bước logic tương tự, nhưng sử dụng bảng của SW2. Bảng MAC liệt kê các hướng dẫn chuyển tiếp chỉ đối với công tắc đó. Trong trường hợp này, swtich SW2 chuyển tiếp khung qua cổng F0/3 của nó, dựa trên bảng địa chỉ MAC của SW2.

![Imgur](https://i.imgur.com/FeaSPX3.png)

### Learning MAC Addresses
- Đội ngũ kỹ thuật mạng không cần phải nhập tất cả các mục bảng địa chỉ MAC. Thay vào đó, mỗi swtich thực hiện chức năng chính thứ hai của mình: học địa chỉ MAC và các giao diện để đưa vào bảng địa chỉ của nó. Với một bảng địa chỉ MAC đầy đủ, swtich có thể đưa ra quyết định chuyển tiếp và lọc chính xác như vừa thảo luận.

- Các swtich xây dựng bảng địa chỉ bằng cách lắng nghe các khung đến và kiểm tra địa chỉ MAC nguồn trong khung. Nếu một khung đi vào swtich và địa chỉ MAC nguồn không có trong bảng địa chỉ MAC, swtich sẽ tạo một mục trong bảng. Mục bảng đó liệt kê giao diện mà khung đã đến.

- Hình 5-6 mô tả cùng một mạng đơn công tắc như Hình 5-3, nhưng trước khi swtich đã xây dựng bất kỳ mục bảng địa chỉ nào. Hình vẽ hiển thị hai khung đầu tiên được gửi trong mạng này - đầu tiên là một khung từ Fred, gửi đến Barney, và sau đó là phản hồi của Barney, gửi đến Fred.

![Imgur](https://i.imgur.com/RYgEEOd.png)

- Tập trung vào quá trình learning và cách bảng MAC mở rộng ở mỗi bước như được hiển thị ở phía bên phải của hình vẽ. swtich bắt đầu với một bảng MAC trống, như được thể hiện ở phần phía trên bên phải của hình vẽ. Sau đó, Fred gửi khung đầu tiên của mình (được đánh số "1") đến Barney, vì vậy swtich thêm một mục cho 0200.1111.1111, địa chỉ MAC của Fred, được liên kết với giao diện F0/1. Tại sao lại là F0/1? Khung được Fred gửi vào cổng F0/1 của swtich. Logic của SW1 chạy gần như như sau: "Nguồn là MAC 0200.1111.1111, khung vào F0/1 0200.1111.1111 phải có thể đến qua cổng F0/1."
- Tiếp theo ví dụ, khi Barney trả lời trong Bước 2, swtich thêm một mục thứ hai, cho 0200.2222.2222, địa chỉ MAC của Barney, cùng với giao diện F0/2. Tại sao lại là F0/2? Khung mà Barney gửi vào giao diện F0/2 của swtich. Learning luôn xảy ra bằng cách nhìn vào địa chỉ MAC nguồn trong khung và thêm giao diện đầu vào làm cổng liên quan.

### Flooding Unknown Unicast and Broadcast Frames
- Bây giờ, hãy chuyển sự chú ý của bạn lại vào quá trình forwarding, sử dụng topology trong Hình 5-5. Bạn nghĩ rằng swtich sẽ làm gì với khung đầu tiên của Fred, khung đó xảy ra khi không có mục nào trong bảng địa chỉ MAC? Như đã biết, khi không có mục phù hợp nào trong bảng, các swtich sẽ chuyển tiếp khung ra tất cả các giao diện (ngoại trừ giao diện đầu vào) bằng một quy trình gọi là flooding. Và khung mà địa chỉ đích của nó không được swtich biết được gọi là unknown unicast frame, hoặc đơn giản là unknown unicast.

- Các swtich flood unknown unicast frames. Flooding có nghĩa là swtich chuyển tiếp bản sao của khung ra tất cả các cổng, ngoại trừ cổng mà khung đã được nhận vào. Ý tưởng là đơn giản: nếu bạn không biết nơi gửi, hãy gửi nó khắp nơi để gửi đến địa chỉ. Và, theo cách đó, thiết bị đó có thể sau đó gửi một phản hồi—và sau đó swtich có thể học địa chỉ MAC của thiết bị đó và chuyển tiếp các khung sau ra khỏi một cổng như một khung đã biết.

- Các swtich cũng flood LAN Boardcast frames (khung có địa chỉ broadcast Ethernet là FFFF.FFFF.FFFF) vì quy trình này giúp gửi bản sao của khung đến tất cả các thiết bị trong LAN.

Ví dụ, Hình 5-7 thể hiện khung đầu tiên gửi bởi Fred, khi bảng địa chỉ MAC của swtich đang trống. Ở bước 1, Fred gửi khung. Ở bước 2, swtich gửi một bản sao của khung ra tất cả ba giao diện khác.

![Imgur](https://i.imgur.com/pjZS3HZ.png)

###Avoiding Loops Using Spanning Tree Protocol
- Đặc trưng chính thứ ba của các công tắc LAN là ngăn chặn vòng lặp, được thực hiện thông qua Spanning Tree Protocol - STP. Mà không có STP, bất kỳ khung lây lan nào sẽ lặp mãi mãi trong các mạng Ethernet có liên kết dự phòng về mặt vật lý. Để ngăn chặn việc khung quay vòng, STP chặn một số cổng từ việc chuyển tiếp khung để chỉ tồn tại một đường lối hoạt động duy nhất giữa mọi cặp đoạn LAN.

- Kết quả của STP là tốt: các khung không lặp vô hạn, điều này làm cho mạng LAN có thể sử dụng. Tuy nhiên, STP cũng có các đặc tính tiêu cực, bao gồm việc mất một số công việc để cân bằng lưu lượng trên các liên kết dự phòng.

- Một ví dụ đơn giản làm cho sự cần thiết của STP trở nên rõ ràng hơn. Hãy nhớ, các swtich lây lan unknown unicast frame và broadcast frame. Hình 5-8 thể hiện một unknown unicast frame, được gửi bởi Larry đến Bob, lặp vô hạn vì mạng có tính dự phòng nhưng không có STP. Lưu ý rằng hình chỉ hiển thị một hướng của khung lặp, chỉ để giảm sự rối bời, nhưng một bản sao của khung cũng sẽ lặp về hướng khác.

![Imgur](https://i.imgur.com/5W2VoOI.png)

- Việc flooding của khung này sẽ dẫn đến việc khung quay vòng liên tục xung quanh ba swtich, vì không có swtich nào liệt kê địa chỉ MAC của Bob trong bảng địa chỉ của mình—do đó mỗi swtich đều flood frame. Và trong khi quy trình flooding là một cơ chế tốt để chuyển tiếp các unicast không xác định và broadcast, việc flooding liên tục của khung như trong hình có thể làm tắc nghẽn hoàn toàn mạng LAN đến mức không thể sử dụng được.

- Một topology như Hình 5-8, với các liên kết dự phòng, là tốt, nhưng chúng ta cần ngăn chặn hiệu ứng xấu của những khung lặp đó. Để tránh các vòng lặp Layer 2, tất cả các swtich cần sử dụng STP. STP khiến cho mỗi giao diện trên một swtich định tình vào trạng thái chặn (blocking) hoặc trạng thái chuyển tiếp (forwarding). Chế độ chặn có nghĩa là giao diện không thể chuyển tiếp hoặc nhận khung dữ liệu, trong khi chế độ chuyển tiếp có nghĩa là giao diện có thể gửi và nhận khung dữ liệu. Nếu một tập hợp chính xác của các giao diện bị chặn, chỉ tồn tại một đường lối logic hiện tại duy nhất giữa mỗi cặp mạng LAN.

### LAN Switching Summary
- Các swtich sử dụng logic Layer 2, kiểm tra tiêu đề dữ liệu-liên kết Ethernet để quyết định cách xử lý các khung. Đặc biệt, các swtich đưa ra quyết định để chuyển tiếp và lọc khung, học địa chỉ MAC, và sử dụng STP để tránh vòng lặp, như sau:

**Bước 1.Các swtich chuyển tiếp khung dữ liệu dựa trên địa chỉ MAC đích:**

- A. Nếu địa chỉ MAC đích là broadcast, multicast, hoặc unicast đích không xác định (unicast không được liệt kê trong bảng địa chỉ MAC), swtich sẽ lây lan khung.
- B. Nếu địa chỉ MAC đích là một địa chỉ unicast đã biết (địa chỉ unicast được liệt kê trong bảng địa chỉ MAC):
	- i. Nếu giao diện đầu ra liệt kê trong bảng địa chỉ MAC khác với giao diện trong đó khung đã được nhận, swtich sẽ chuyển tiếp khung ra khỏi giao diện đầu ra.
	- ii. Nếu giao diện đầu ra giống với giao diện trong đó khung đã được nhận, swtich sẽ lọc khung, có nghĩa là swtich đơn giản bỏ qua khung và không chuyển tiếp nó.

**Bước 2.Các công tắc sử dụng logic sau để học các mục bảng địa chỉ MAC:**

- A. Đối với mỗi khung nhận được, kiểm tra địa chỉ MAC nguồn và ghi chú giao diện từ khung đã nhận được.
- B. Nếu nó chưa có trong bảng, thêm địa chỉ MAC và giao diện đã học được vào bảng.

**Bước 3. Các công tắc sử dụng STP để ngăn chặn vòng lặp bằng cách làm cho một số giao diện chặn, có nghĩa là chúng không gửi hoặc nhận khung.**

## Verifying and Analyzing Ethernet Switching
### Demonstrating MAC Learning
- Để xem bảng địa chỉ MAC của một swtich, sử dụng lệnh **show mac address-table**. Với không có tham số bổ sung, lệnh này liệt kê tất cả các địa chỉ MAC đã biết trong bảng địa chỉ MAC, bao gồm một số địa chỉ MAC tĩnh quản lý mà bạn có thể bỏ qua. Để xem chỉ các địa chỉ MAC đã học động, hãy sử dụng lệnh **show mac address-table dynamic**.

- Các ví dụ trong chương này sử dụng ít cấu hình, như là bạn vừa mới mua swtich và khởi động nó. Đối với các ví dụ, các swtich không có cấu hình ngoại trừ lệnh **hostname** để đặt tên máy chủ có ý nghĩa. Lưu ý rằng để thực hiện điều này trong môi trường thử nghiệm, tôi chỉ cần:
- Sử dụng lệnh `erase startup-config` trong EXEC để xóa tệp startup-config
- Sử dụng lệnh `delete vlan.dat` trong EXEC để xóa chi tiết cấu hình VLAN
- Sử dụng lệnh `reload` trong EXEC để khởi động lại công tắc (do đó sử dụng tệp startup-config trống, không có thông tin VLAN được cấu hình)
- Cấu hình lệnh `hostname SW1` để đặt tên máy chủ của công tắc

- Khi hoàn thành, swtich bắt đầu chuyển tiếp và học địa chỉ MAC, như được minh họa trong Example 5-1.

![Imgur](https://i.imgur.com/raptPVR.png)

- Trước hết, tập trung vào hai cột của bảng: cột Địa chỉ MAC và cột Cổng. Các giá trị này sẽ quen thuộc: chúng tương ứng với ví dụ về công tắc đơn trước đó, như được lặp lại ở đây trong Figure 5-9. Chú ý đến bốn địa chỉ MAC được liệt kê, cùng với các cổng tương ứng của chúng, như được hiển thị trong hình.

- Tiếp theo, hãy nhìn vào trường Type trong phần đầu của bảng kết quả. Cột này cho chúng ta biết cách swtich đã học địa chỉ MAC như đã mô tả trước đó trong chương này; trong trường hợp này, swtich đã học tất cả các địa chỉ MAC động. Bạn cũng có thể xác định trước các mục bảng địa chỉ MAC tĩnh bằng cách sử dụng một số tính năng khác nhau, bao gồm bảo mật cổng, và những mục này sẽ xuất hiện dưới dạng "Static" trong cột Type.

- Cuối cùng, cột VLAN của kết quả cho chúng ta cơ hội để tóm tắt về cách VLAN ảnh hưởng đến logic chuyển mạch. Các swtich LAN chuyển tiếp khung Ethernet bên trong một VLAN. Điều đó có nghĩa là nếu một khung đi qua một cổng thuộc VLAN 1, thì swtich sẽ chuyển tiếp hoặc lây lan khung đó ra các cổng khác chỉ thuộc VLAN 1, và không ra bất kỳ cổng nào được gán cho một VLAN khác. Chương 8, "Thực hiện Mạng LAN Ảo Ethernet (VLANs)," sẽ xem xét tất cả các chi tiết về cách các swtich chuyển tiếp khung khi sử dụng VLAN.

### Switch Interfaces
- Giả định rằng bạn đã cài đặt công tắc và cáp mạng đúng cách, và các giao diện của swtich đang hoạt động. Sau khi bạn thực hiện cài đặt và kết nối với cổng Console, bạn có thể kiểm tra trạng thái của các giao diện đó dễ dàng bằng lệnh **show interfaces status**, như được hiển thị trong Example 5-2.

![Imgur](https://i.imgur.com/O5jqvTe.png)

### Command Reference

![Imgur](https://i.imgur.com/wsObybV.png)