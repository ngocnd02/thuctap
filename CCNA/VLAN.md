# Implementing Ethernet Virtual LANs

[Virtual LAN Concepts](#Virtual-LAN-Concepts)

[Creating Multiswitch VLANs Using Trunking](#Creating-Multiswitch-VLANs-Using-Trunking)

- [VLAN tagging concepts](#VLAN-tagging-concepts)
- [The 802.1Q and ISL VLAN Trunking Protocols](#the-802.1q-and-isl-vlan-trunking-protocols)

[Forwarding Data Between VLANs](#forwarding-data-between)


## Virtual LAN Concepts
Trước khi hiểu về VLANs, bạn cần hiểu rõ định nghĩa của một mạng LAN.

- Mạng LAN bao gồm tất cả các thiết bị trong cùng một miền phát sóng (broadcast domain).
- Miền phát sóng (broadcast domain) bao gồm tất cả các thiết bị kết nối trong mạng LAN đó, nên khi bất kỳ thiết bị nào gửi một khung phát sóng, tất cả các thiết bị khác đều nhận được một bản sao của khung đó. Vì vậy, từ một góc độ, bạn có thể nghĩ về mạng LAN và miền phát sóng như là cùng một thứ.
- Sử dụng chỉ các thiết lập mặc định, một switch xem tất cả các giao diện của nó đều thuộc cùng một miền phát sóng. Nghĩa là, đối với một switch, khi một khung phát sóng nhập vào một cổng của switch, switch sẽ chuyển tiếp khung phát sóng đó ra tất cả các cổng khác. Dựa trên logic đó, để tạo ra hai miền phát sóng LAN khác nhau, bạn phải mua hai switch mạng LAN Ethernet khác nhau, như được thể hiện trong Hình 8-1.

![Imgur](https://i.imgur.com/pnFWOky.png)

- Bằng cách sử dụng hai VLAN, một switch đơn có thể đạt được cùng mục tiêu với thiết kế trong Hình 8-1 — tạo ra hai miền phát sóng — chỉ với một switch. Với VLAN, một switch có thể cấu hình một số giao diện vào một miền phát sóng và một số vào miền phát sóng khác, tạo ra nhiều miền phát sóng. Những miền phát sóng riêng lẻ được tạo ra bởi switch được gọi là Virtual LANs (VLAN).
Imgur

![Imgur](https://i.imgur.com/cuaGXPC.png)

- Lợi ích của VLAN:
	- Giảm độ tải CPU trên mỗi thiết bị, cải thiện hiệu suất máy chủ, bằng cách giảm số lượng thiết bị nhận mỗi khung phát sóng.

	- Giảm rủi ro an ninh bằng cách giảm số lượng máy chủ nhận bản sao của các khung mà switch truyền tải (phát sóng, đa phát, và unicast không xác định).

	- Cải thiện an ninh cho các máy chủ thông qua áp dụng các chính sách an ninh khác nhau cho mỗi VLAN.

	- Tạo ra các thiết kế linh hoạt hơn nhóm người dùng theo bộ phận, hoặc theo các nhóm làm việc cùng nhau, thay vì theo vị trí vật lý.

	- Giải quyết vấn đề nhanh chóng hơn, vì miền lỗi cho nhiều vấn đề là cùng một tập hợp thiết bị như những thiết bị trong cùng một miền phát sóng.

Giảm công việc cho Giao thức Cây cầu (Spanning Tree Protocol - STP) bằng cách giới hạn một VLAN chỉ đến một switch truy cập duy nhất.

### Creating Multiswitch VLANs Using Trunking
- Khi bạn sử dụng VLAN trong các mạng có nhiều switch kết nối với nhau, các switch cần sử dụng VLAN trunking trên các liên kết giữa chúng. VLAN trunking khiến cho các switch sử dụng một quá trình được gọi là VLAN tagging, trong đó switch gửi thêm một header khác vào frame trước khi gửi nó qua trunk. Header trunking bổ sung này bao gồm một trường định danh VLAN (VLAN ID), giúp switch gửi liên kết frame với một VLAN ID cụ thể, và switch nhận biết được VLAN nào mà mỗi frame thuộc về.

![Imgur](https://i.imgur.com/FWAVpm9.png)

#### VLAN tagging concepts
- VLAN trunking tạo ra một liên kết giữa các switch hỗ trợ nhiều VLAN tùy thuộc vào nhu cầu của bạn.

![Imgur](https://i.imgur.com/weDg8EK.png)

- Hình 8-5 mô tả PC11 gửi một khung phát sóng trên giao diện Fa0/1 ở Bước 1. Để truyền khung phát sóng này, switch SW1 cần chuyển tiếp khung phát sóng đến switch SW2. Tuy nhiên, SW1 cần thông báo cho SW2 biết rằng khung phát sóng này thuộc VLAN 10, để sau khi nhận được khung, SW2 sẽ chỉ truyền khung phát sóng này vào VLAN 10 và không phải vào VLAN 20. Như vậy, như được thể hiện ở Bước 2, trước khi gửi khung phát sóng, SW1 thêm một tiêu đề VLAN vào khung Ethernet gốc, với VLAN ID là 10 trong trường hợp này.

![Imgur](https://i.imgur.com/SbZplzI.png)

- Khi SW2 nhận được khung, nó hiểu rằng khung này thuộc VLAN 10. SW2 sau đó loại bỏ tiêu đề VLAN, chuyển tiếp khung gốc ra các giao diện của nó trong VLAN 10 (Bước 3).

#### The 802.1Q and ISL VLAN Trunking Protocols

- Cisco đã hỗ trợ hai giao thức trunking khác nhau qua nhiều năm: Inter-Switch Link (ISL) và IEEE 802.1Q.

**802.1Q**
- 802.1Q chèn thêm một tiêu đề VLAN 802.1Q 4 byte vào tiêu đề Ethernet của khung gốc, như được thể hiện ở đỉnh của Hình 8-6.
- Đối với các trường trong tiêu đề 802.1Q, trường **VLAN ID** là một trường quan trọng với 12 bit. Trường 12 bit này hỗ trợ một giá trị tối đa lý thuyết là 212 (4096) VLAN, nhưng thực tế nó hỗ trợ tối đa là 4094. (Cả 802.1Q và ISL đều sử dụng 12 bit để đánh dấu VLAN ID, với hai giá trị được dành riêng [0 và 4095].)
- Các switch Cisco chia phạm vi VLAN ID (1–4094) thành hai phạm vi: phạm vi bình thường và phạm vi mở rộng. Tất cả các switch có thể sử dụng VLAN phạm vi bình thường với giá trị từ 1 đến 1005. Chỉ một số switch có thể sử dụng VLAN phạm vi mở rộng với VLAN ID từ 1006 đến 4094.

![Imgur](https://i.imgur.com/QJ5kRAF.png)

- 802.1Q cũng xác định một VLAN ID đặc biệt trên mỗi trunk là **VLAN native** (mặc định sử dụng VLAN 1). Theo định nghĩa, 802.1Q đơn giản không thêm một tiêu đề 802.1Q vào các khung trong VLAN native. Khi switch ở phía kia của trunk nhận được một khung không có tiêu đề 802.1Q, switch nhận được biết rằng khung này là một phần của VLAN native. Lưu ý rằng do hành vi này, cả hai switch phải đồng ý về VLAN nào là VLAN native.

### Forwarding Data Between VLANs
- Các switch Layer 2 thực hiện logic của chúng theo từng VLAN. Ví dụ, trong Hình 8-7, hai máy tính ở bên trái thuộc VLAN 10, trong dải mạng con 10. Hai máy tính ở bên phải thuộc một VLAN khác (20), với một dải mạng con khác (20).
- Các switch Layer 2 sẽ không chuyển tiếp dữ liệu giữa hai VLAN.
![Imgur](https://i.imgur.com/PfKFiXs.png)
- Trong thực tế, một trong những mục tiêu của VLAN là tách biệt lưu lượng trong một VLAN khỏi VLAN khác, ngăn các khung trong một VLAN từ việc rò rỉ sang các VLAN khác. Ví dụ, khi Dino (ở VLAN 10) gửi bất kỳ khung Ethernet nào, nếu SW1 là một switch Layer 2, switch đó sẽ không chuyển tiếp khung đó đến các máy tính bên phải thuộc VLAN 20.
