# Tổng quan về Cluster

## Khái niệm về Cluster
Clustering là một kiến trúc nhằm đảm bảo nâng cao khả năng sẵn sàng cho các hệ thống mạng máy tính. Clustering cho phép sử dụng nhiều máy chủ kết hợp với nhau tạo thành một cụm có khả năng chịu đựng hay chấp nhận sai sót (fault-tolerant) nhằm nâng cao độ sẵn sàng của hệ thống mạng. 

Cluster là một hệ thống bao gồm nhiều máy chủ được kết nối với nhau theo dạng song song hay phân tán và được sử dụng như một tài nguyên thống nhất. Nếu một máy chủ ngừng hoạt động do bị sự cố hoặc để nâng cấp, bảo trì, thì toàn bộ công việc mà máy chủ này đảm nhận sẽ được tự động chuyển sang cho một máy chủ khác (trong cùng một cluster) mà không làm cho hoạt động của hệ thống bị ngắt hay gián đoạn. Quá trình này gọi là “fail-over” và việc phục hồi tài nguyên của một máy chủ trong hệ thống (cluster) được gọi là “fail-back”.

## Tính chất
- **Cân bằng tải các cụm (load balancing)**: các node bên trong cluster hoạt động song song, chia sẻ các tác vụ để nâng cao hiệu năng

- **Tính sẵn sàng cao (high availability)**: các tài nguyên bên trong cluster luôn sẵn sàng xử lý yêu cầu, ngay cả khi có vấn đề xảy ra với các thành phần bên trong (hardware, software)

- **Khả năng mở rộng (scalability)**: khi tài nguyên có thể sử dụng của hệ thống tới giới hạn, ta có thể dễ dàng bổ sung thêm tài nguyên của cluster bằng cách bổ sung thêm các node

- **Độ tin cậy (reliability)**: hệ thống cluster giảm thiểu tần số lỗi có thể xảy ra, giảm thiểu các vấn đề dẫn tới ngừng hoạt động của hệ thống

## Các thuật ngữ quan trọng
- **Cluster**: Nhóm các server dành riêng để giải quyết 1 vấn đề, có khả năng kết nối, sản sẻ các tác vụ.

- **Node:** Server thuộc Cluster

- **Failover:** Khi 1 hoặc nhiều node trong Cluster xảy ra vấn đề, các tài nguyên (resource) tự động được chuyển tới các node sẵn sàng phục vụ

- **Failback**: Khi node lỗi phục hồi, sẵn sàng phục vụ, Cluster tự động trả lại tài nguyên cho node

- **Fault-tolerant cluster:** Để cập đến khả năng chịu lỗi của hệ thống trên các thành phần, cho phép dịch vụ hoạt động ngay cả khi một vài thành phần gặp sự cố

- **Heartbeat:** Tín hiệu xuất phát từ các node trong cụm với mục đích xác minh chúng còn sống và đang hoạt động. Nếu heartbeat tại 1 node ngừng hoạt động, cluster sẽ đánh dấu thành phần đó gặp sự cố và chuyển tài nguyên tại node lỗi sang node đang sẵn sàng phục vụ

- **Interconnect**: Kết nối giữa các node. Thường là các thông tin về trạng thái, heartbeat, dữ liệu chia sẻ.

- **Primary server, secondary server:** Trong cluster dạng Active/Passise, node đang đáp ứng giải quyết yêu cầu gọi là Primary server. Node đang chờ hay dự phòng cho node Primary server được gọi là secondary server

- **Quorum:** Trong Cluster chứa nhiều tài nguyên, nên dễ xảy ra sự phân mảnh (split-brain - Tức cluster lớn bị tách ra thành nhiều cluster nhỏ). Điều này sẽ dẫn đến sự mất đồng bộ giữa các tài nguyên, ảnh hướng tới sự toàn vẹn của hệ thống. Quorum được thiết kế để ngăn chặn hiện tượng phân mảnh.

- **Resource:** Tài nguyên của cụm, cũng có thể hiểu là tài nguyên mà dịch vụ cung cấp

- **STONITH/ Fencing:** STONITH là viết tắt của cụm từ Shoot Other Node In The Head đây là một kỹ thuật dành cho fencing. Fencing là kỹ thuật cô lập tài nguyên tại từng node trong Cluster. Mục tiêu STONITH là tắt hoặc khởi động lại node trong trường hợp Node trong trường hợp dịch vụ không thể khôi phục.

## Cơ chế hoạt động 
Mỗi máy chủ trong cluster được gọi là một node (cluster node), và có thể được thiết lập ở chế độ chủ động (active) hay thụ động (passive). Khi một node ở chế dộ chủ động, nó sẽ chủ động xử lý các yêu cầu. Khi một node là thụ động, nó sẽ nằm ở chế độ dự phòng nóng (stanby) chờ để sẵn sàng thay thế cho một node khác nếu bị hỏng.

Trong một Cluster có nhiều node có thể kết hợp cả node chủ động và node thụ động. Trong những mô hình loại này việc quyết định một node được cấu hình là chủ động hay thụ động rất quan trọng. Để hiểu lý do tại sao, hãy xem xét các tình huống sau:

- Nếu một node chủ động bị sự cố và có một node thụ động đang sẵn sàng, các ứng dụng và dịch vụ đang chạy trên node hỏng có thể lập tức được chuyển sang node thụ động. Vì máy chủ đóng vai trò node thụ động hiện tại chưa chạy ứng dụng hay dịch vụ gì cả nên nó có thể gánh toàn bộ công việc của máy chủ hỏng mà không ảnh hưởng gì đến các ứng dụng và dịch vụ cung cấp cho người dùng cuối (Ngầm định rằng các các máy chủ trong cluster có cấu trúc phần cứng giống nhau).

![Imgur](https://i.imgur.com/KXbaJzj.png)


- Nếu tất cả các máy chủ trong cluster là chủ động và có một node bị sự cố, các ứng dụng và dịch vụ đang chạy trên máy chủ hỏng sẽ phải chuyển sang một máy chủ khác cũng đóng vai trò node chủ động. Vì là node chủ động nên bình thường máy chủ này cũng phải đảm nhận một số ứng dụng hay dịch vụ gì đó, khi có sự cố xảy ra thì nó sẽ phải gánh thêm công việc của máy chủ hỏng. Do vậy để đảm bảo hệ thống hoạt động bình thường kể cả khi có sự cố thì máy chủ trong Cluster cần phải có cấu hình dư ra đủ để có thể gánh thêm khối lượng công việc của máy chủ khác khi cần.

![Imgur](https://i.imgur.com/W8z14q1.png)

Trong cấu trúc Cluster mà mỗi node chủ động được dự phòng bởi một node thụ động, các máy chủ cần có cấu hình sao cho với khối lượng công việc trung bình chúng sử dụng hết khoảng 50% CPU và dung lượng bộ nhớ.

Trong cấu trúc Cluster mà số node chủ động nhiều hơn số node bị động, các máy chủ cần có cấu hình tài nguyên CPU và bộ nhớ mạnh hơn nữa để có thể xử lý được khối lượng công việc cần thiết khi một node nào đó bị hỏng.

Các node trong một cluster thường là một bộ phận của cùng một vùng (domain) và có thể được cấu hình là máy điều khiển vùng (domain controllers) hay máy chủ thành viên. Lý tưởng nhất là mỗi Cluster nhiều node có ít nhất hai node làm máy điều khiển vùng và đảm nhiệm việc failover đối với những dịch vụ vùng thiết yếu. Nếu không như vậy thì khả năng sẵn sàng của các tài nguyên trên cluster sẽ bị phụ thuộc vào khả năng sẵn sàng của các máy điều khiển trong domain.