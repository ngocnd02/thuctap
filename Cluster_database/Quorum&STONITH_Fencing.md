# Tổng quan về Quorum, STONITH/Fencing

## Tổng quan về Quorum
- Trong hệ thống phân tán, **quorum** là một khái niệm để xác định số lượng tối thiểu các thành phần (như các nút trong cụm máy chủ) cần được chấp nhận hoặc tham gia trong quyết định trước khi một hành động cụ thể có thể được thực hiện.

- Trong một cụm máy chủ, quorum đóng vai trò quan trọng trong việc đảm bảo tính nhất quán của cụm. Quandrum đảm bảo rằng chỉ khi có đủ số lượng các nút trong cụm hoạt động và kết nối với nhau thì cụm mới có thể tiếp tục hoạt động. Điều này giúp tránh được các tình huống split-brain, khi mà các nút trong cụm không thể trao đổi dữ liệu với nhau nhưng vẫn cố gắng hoạt động độc lập.

- Trong một cụm máy chủ, quorum thường được xác định bằng cách tính toán số lượng nút cần có trong cụm để đạt được hành động quorum, dựa trên tổng số nút trong cụm. Điều này có thể được cấu hình dựa trên một số tiêu chí như số lượng nút chính, số lượng nút dự phòng, hoặc các yếu tố khác.

- Quorum cũng có thể áp dụng trong các hệ thống phân tán khác, không chỉ hệ thống máy chủ. Đối với ví dụ, trong các hệ thống blockchain, quorum có thể áp dụng để xác định số lượng tối thiểu các nút cần đồng thuận về một giao dịch trước khi nó được coi là chính thức.

- Quorum được thiết lập bằng cơ chế voting. Khi node thuộc cluster xảy ra sự cố hoặc mất kết nối với phần còn lại của cluster, các node đang hoạt động sẽ vote cho việc node nào sẽ bị đóng băng cô lập, node nào sẽ tiếp tục hoạt động.

- Kỹ thuật Quorm được hỗ trợ mặc định trong pacemaker, với 2 kỹ thuật:

	- Hỗ trợ kỹ thuật Resource-driven cluster - Kỹ thuật phân cấp, nhóm tài nguyên để quản lý độc lập

	- Hỗ trợ kỹ thuật Quorate Clusters - Kỹ thuật tính điểm của các node thuộc cluster, ý tưởng của kỹ thuật là khi cụm lớn bị phân mảnh thành 2 phần, cluster sẽ đánh giá so sánh số điểm của 2 cụm để quyết định cụm nào sẽ tiếp tục chạy, cụm nào sẽ bị đóng băng hoặc tắt hẳn.


- Công thức tính quorum (tức số node tối thiểu để cụm hoạt động bình thường)

```
(Số node hoạt động) > (tổng số node của cụm) / 2
```

**Split-brain** là gì?
- Split-brain là một tình trạng xảy ra trong hệ thống phân tán khi các thành phần của hệ thống không còn có khả năng giao tiếp với nhau, nhưng vẫn tiếp tục hoạt động độc lập và đưa ra các quyết định riêng lẻ. Trong một tình huống split-brain, hệ thống có thể chia thành nhiều phần (hoặc "não") riêng biệt mà mỗi phần đều tin rằng nó là phần duy nhất hoặc "chính thống".

- Ví dụ, trong một cụm máy chủ, nếu kết nối mạng giữa các nút bị mất đi nhưng các nút vẫn tiếp tục hoạt động độc lập, có thể dẫn đến tình trạng split-brain. Mỗi nút có thể tiếp tục hoạt động như thường lệ và đưa ra quyết định, mặc dù không có sự đồng thuận từ các nút khác.

- Tình trạng split-brain có thể gây ra các vấn đề như mất dữ liệu, mâu thuẫn về trạng thái của hệ thống, và gây ra tình trạng không ổn định. Để giải quyết vấn đề split-brain, thường cần có các cơ chế như fencing để cô lập các nút gặp sự cố và khôi phục tính nhất quán của hệ thống.

### Ví dụ về Quorum
- Đối với Cluster gồm 2 node, tổng số vote là 2. Dựa theo kỹ thuật voting quorum sẽ chỉ hoạt động nếu số vote lớn hơn 1 nửa số node hoạt động (tức lớn hơn 1 node). Vì vậy nếu có 1 node xảy ra sự cố, cả cluster sẽ dừng hoạt động

![Imgur](https://i.imgur.com/pUbJdhz.png)

- Đối với Cluster gồm 3 node, tổng số vote là 3. Dựa theo kỹ thuật voting quorum sẽ chỉ hoạt động nếu số vote lớn hơn 1 nửa số node hoạt động (tức lớn hơn 1 node). Vì vậy nếu có hơn 2 node xảy ra sự cố, cả cluster sẽ dừng hoạt động

![Imgur](https://i.imgur.com/qKORtJl.png)


- Trong trường hợp cluster gồm 6 node bị phân mảnh thì cần ít nhất 4 node cùng hoạt động trong cluster để hình thành quorum. Trong trường hợp bị phân mảnh nhỏ hơn pacemaker sẽ cô lập hoặc ngừng cung cấp dịch vụ.

![Imgur](https://i.imgur.com/sIi0tWL.png)


Các tùy chọn khi pacemaker mất Quorum (Số node hiện có không thể tạo thành quorum):
- ignore: Tiếp tục quản trị duy trì hoạt đông cluster kể cả khi mất quorum

- freeze: Tiếp tục quản trị duy trì hoạt đông cluster nhưng đóng băng tài nguyên xảy ra sự cố, không cố gắng khôi phục

- stop: Ngừng cung cấp dịch vụ cluster khi mất quorum

- suicide: Cô lập các node đang xảy ra sự cố


## Tổng quan về STONITH/Fencing
- STONITH (Shoot The Other Node In The Head) là một dịch vụ trên Linux được sử dụng để duy trì tính toàn vẹn của các nút trong một cụm máy chủ có khả năng hoạt động (HA). STONITH tự động tắt nguồn một nút không hoạt động đúng cách.

- STONITH được sử dụng như một phần của chiến lược  cluster's fencing. Fencing cung cấp một cơ chế để giám sát trạng thái của tài nguyên và nút trong cụm và sau đó thực hiện hành động nếu có điều gì đó không đúng với một trong số chúng. Vì lý do này, phân vùng (fencing) thường được xác định là một phương pháp để đưa một cụm vào trạng thái đã biết. Nó đảm bảo rằng không có tài nguyên hoặc nút nào đang hoạt động trong trạng thái không xác định và có thể thực hiện các hành động có thể gây hại cho hệ thống hoặc dữ liệu.

Có hai loại fencing trong một cụm máy chủ Linux:  resource-level and node-level.

- **Resource-level fencing:** đảm bảo rằng một nút không thể truy cập vào cùng một tài nguyên trên nhiều hơn một nút. Ví dụ, cơ chế fencing có thể ngăn một tài nguyên chạy trên tất cả các nút ngoại trừ nút đang hoạt động hiện tại.

- **Node-level fencing:** đảm bảo rằng một nút không chạy bất kỳ tài nguyên nào. Điều này được thực hiện bằng cách tắt máy chủ hoặc thay đổi trạng thái của nó bằng cách nào đó, chẳng hạn như khởi động lại nó và đặt nó làm máy chủ dự phòng.


- Dịch vụ STONITH được sử dụng cho Node-level fencing. Nếu một nút không phản hồi hoặc hoạt động không bình thường, STONITH đảm bảo rằng nút không thể gây thiệt hại nào, đặc biệt là trong trường hợp của kịch bản split-brain (khi hai nút đều nghĩ rằng chúng là máy chủ chính).

- Ví dụ, nếu một nút cơ sở dữ liệu chính tự động chuyển giao sang một nút dự phòng do sự cố về dịch vụ, nút đầu tiên có thể vẫn cố gắng ghi dữ liệu vào hệ thống lưu trữ chia sẻ vào cùng một thời điểm với nút chính mới, điều này có thể làm hỏng dữ liệu hoặc ảnh hưởng đến tính toàn vẹn của nó. Để ngăn điều này xảy ra, STONITH sẽ tắt nút đầu tiên hoặc khởi động lại nó và đặt nó làm máy chủ dự phòng.

- Với pacemaker, khi nhận thấy node xảy ra sự cố, nó sẽ thông báo cho các node đang hoạt động về node lỗi và cô lập node thông qua STONITH.

- Cô lập node thông STONITH có thể được thực hiện thông qua nhiều mức, dựa trên nhiều loại thiết bị hỗ trợ
	- Uninterruptible Power Supply (UPS): Cô lập tài nguyên cung cấp năng lượng bằng bộ lưu điện, sử dụng khi hệ thống cung cấp năng lượng xảy ra sự cố

	- Power Distribution Unit (PDU): Cô lập tài nguyên cung cấp năng lượng bằng thiết bị cấp phát nguồn, sử dụng khi hệ thống cung cấp năng lượng xảy ra sự cố

	- Blade power control device: Hệ thống chuyên dụng trong các datacenter, sử dụng để cô lập các cluster node xảy ra sự cố.

	- Lights-out device: Thiết bị gắn mạng hỗ trợ giao thức quản trị từ xa có phép cố lập tài nguyên dựa trên thao tác tắt bật. VD: HP Integrated Lights-Out - (HP ILO); Dell Remote Access Controller (DRAC)


- Các giao thức hỗ trợ STONITH:
	- IPMI - intelligent Platform Management Interface ( General Standard )

	- IDRAC - Integrated Dell Remote Access ( Dell )

	- ILO - Integrated Lights-Out ( HP )

	- IMM - Integrated Management Module ( IBM )

- Ví dụ minh họa: Trong trường hợp Node 3 xảy ra sự cố, cluster hình thành giữa node 1 và node 2 sẽ tắt nóng node 3 thông qua cấu hình STONITH (ILO, IDRAC, …)

![Imgur](https://i.imgur.com/fngs19i.png)