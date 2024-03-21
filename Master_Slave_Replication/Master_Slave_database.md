# Tổng quan về Master-Slave Replication

## Khái niệm

Cơ sở dữ liệu master-slave là một kiến trúc phân tán trong đó có một cơ sở dữ liệu chính (master) và nhiều cơ sở dữ liệu phụ (slave). Trong kiến trúc này, cơ sở dữ liệu master chịu trách nhiệm cho việc ghi dữ liệu, trong khi các cơ sở dữ liệu slave chịu trách nhiệm cho việc đọc dữ liệu và đóng vai trò như các bản sao sao lưu cho cơ sở dữ liệu master. Các thay đổi dữ liệu được thực hiện trên cơ sở dữ liệu master sẽ được sao chép và đồng bộ hóa đến các cơ sở dữ liệu slave.

## Mô hình 

Trong mô hình cơ sở dữ liệu master-slave, có một cơ sở dữ liệu master duy nhất và một hoặc nhiều cơ sở dữ liệu slave. Cơ sở dữ liệu master chịu trách nhiệm cho việc xử lý và lưu trữ các thay đổi dữ liệu từ các yêu cầu ghi. Các cơ sở dữ liệu slave, theo dõi trạng thái của cơ sở dữ liệu master và sao chép dữ liệu từ nó. Dữ liệu được sao chép từ master đến slave thông qua quá trình sao chép và đồng bộ hóa.


![Imgur](https://i.imgur.com/8IcHl1f.png)


## Các thành phần

Cơ Sở Dữ Liệu Master (Master Database): Là nơi chính xác mà các thay đổi dữ liệu được thực hiện và lưu trữ. Cơ sở dữ liệu master chịu trách nhiệm cho việc xử lý các yêu cầu ghi và đảm bảo tính nhất quán của dữ liệu.

Cơ Sở Dữ Liệu Slave (Slave Database): Là các bản sao của cơ sở dữ liệu master và chịu trách nhiệm cho việc đọc dữ liệu. Dữ liệu được sao chép từ cơ sở dữ liệu master và cập nhật đồng bộ với nó. Cơ sở dữ liệu slave có thể được sử dụng để phân tải công việc đọc và cung cấp tính sẵn sàng cao cho hệ thống.

Quá Trình Sao Chép và Đồng Bộ Hóa (Replication and Synchronization Process): Là quá trình mà dữ liệu được sao chép từ cơ sở dữ liệu master đến các cơ sở dữ liệu slave và đảm bảo rằng chúng đồng bộ với nhau. Quá trình này thường bao gồm việc gửi các bản sao nhật ký (log) từ master đến slave và áp dụng chúng để cập nhật dữ liệu.


Giao Thức Sao Chép (Replication Protocol): Là các quy tắc và quy trình mà dữ liệu tuân theo trong quá trình sao chép và đồng bộ hóa. Các giao thức này đảm bảo tính nhất quán và đồng bộ của dữ liệu giữa các cơ sở dữ liệu.

Trong tổng thể, cơ sở dữ liệu master-slave là một kiến trúc phân tán phổ biến được sử dụng để cải thiện tính sẵn sàng và hiệu suất của hệ thống cơ sở dữ liệu. Bằng cách phân tải công việc giữa các cơ sở dữ liệu và sao chép dữ liệu giữa chúng, kiến trúc này cung cấp một cách hiệu quả để quản lý và triển khai cơ sở dữ liệu trong môi trường phân tán.


## Điểm mạnh và nhược điểm

### Điểm mạnh
Lợi ích của Kiến trúc Cơ sở dữ liệu Master-Slave

1. Tạo bản sao lưu: cung cấp các bản sao lưu đáng tin cậy thông qua chuỗi các cơ sở dữ liệu slave. Cơ sở dữ liệu slave có thể được tắt mà không ảnh hưởng đến hoạt động của cơ sở dữ liệu master, bởi vì các bản chụp của dữ liệu thực tế sẽ được sao chép sang cơ sở dữ liệu slave, ngay cả sau khi có sự cố ở các cơ sở dữ liệu master.

2. Mở rộng ứng dụng: Khi số lượng người dùng tăng lên, việc cung cấp trải nghiệm người dùng mượt mà là rất quan trọng. Kiến trúc Master-Slave có thể được sử dụng để mở rộng ứng dụng của bạn bằng cách phân phối tải dữ liệu của bạn qua nhiều cơ sở dữ liệu.

3. Phân phối tải: Có thể có những tình huống khi chúng ta có một master duy nhất và muốn sao chép các cơ sở dữ liệu khác nhau sang các slave khác nhau. Ví dụ, chúng ta có thể muốn phân phối các dữ liệu bán hàng khác nhau cho các phòng ban khác nhau để giúp phân phối tải trong quá trình phân tích dữ liệu.


4. Tăng hiệu suất: Khi số lượng slave kết nối với một master tăng lên, tải đồng thời cũng tăng lên, mặc dù không đáng kể, vì mỗi slave sử dụng một kết nối khách hàng tới master. Ngoài ra, vì mỗi slave phải nhận một bản sao đầy đủ của nhật ký nhị phân của master, tải mạng trên master cũng có thể tăng lên và tạo ra một điểm nghẽn. Nếu chúng ta đang sử dụng một số lượng lớn các slave kết nối với một master duy nhất, và master đó cũng bận rộn xử lý yêu cầu (ví dụ, là một phần của một giải pháp mở rộng), thì chúng ta có thể muốn cải thiện hiệu suất của quá trình sao chép. Một cách để cải thiện hiệu suất của quá trình sao chép là tạo ra một cấu trúc sao chép sâu hơn cho phép master sao chép đến chỉ một slave, và cho các slave còn lại kết nối với slave chính này để đáp ứng yêu cầu sao chép cá nhân của họ.


### Nhược điểm

Nhược điểm của Kiến trúc Cơ sở dữ liệu Master-Slave

1. Khó mở rộng các hoạt động ghi lên master - Yêu cầu ghi lên master khó mở rộng. Một trong số ít lựa chọn duy nhất để mở rộng các yêu cầu ghi là tăng khả năng tính toán (CPU và ROM) của cơ sở dữ liệu master.

2. Sao chép không đồng bộ thất bại đôi khi - Không đồng bộ có nghĩa là hai hoặc nhiều hoạt động diễn ra trong một hệ thống độc lập và không phụ thuộc vào nhau. Quá trình sao chép không đồng bộ này được thực hiện trong cơ sở dữ liệu master-slave không đảm bảo đáng tin cậy khi các thay đổi được thực hiện trên master có thể không được phản ánh trên các node slave nếu có sự cố xảy ra trên node master.

3. Không có chuyển giao tự động - Trong trường hợp master gặp sự cố, một slave phải được đẩy để lấy chỗ của master. Không có quá trình chuyển giao tự động thay thế nào được thực hiện.

4. Nhật ký nhị phân phải được đọc mỗi lần dữ liệu được sao chép - Mỗi slave đều thêm tải lên master vì nhật ký nhị phân phải được đọc trước khi dữ liệu được sao chép đến các node slave.