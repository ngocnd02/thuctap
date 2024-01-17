# DNS root server
Quản lý Hệ thống Tên Miền (DNS) được tổ chức theo một cấu trúc phân cấp sử dụng các khu vực quản lý khác nhau hoặc "vùng", với vùng gốc ở đỉnh cấu trúc đó. Các máy chủ gốc là máy chủ DNS hoạt động trong vùng gốc. Những máy chủ này có thể trực tiếp trả lời các truy vấn cho các bản ghi được lưu trữ hoặc được lưu trữ trong vùng gốc, và cũng có thể chuyển hướng các yêu cầu khác đến máy chủ Miền Cấp Cao (TLD) thích hợp. Các máy chủ TLD là nhóm máy chủ DNS ở một bước dưới máy chủ gốc trong cấu trúc phân cấp DNS, và chúng là một phần quan trọng của quá trình giải quyết các truy vấn DNS.

![Imgur](https://i.imgur.com/Kpegvic.png)

Trong một truy vấn DNS không được lưu trữ, mỗi khi người dùng nhập địa chỉ web vào trình duyệt của họ, hành động này kích hoạt một cuộc tìm kiếm DNS, và tất cả các cuộc tìm kiếm DNS bắt đầu từ vùng gốc. Khi cuộc tìm kiếm đến vùng gốc, cuộc tìm kiếm sẽ di chuyển xuống theo cấu trúc phân cấp của hệ thống DNS, đầu tiên đến các máy chủ Tên Miền Cấp Cao (TLD), sau đó là các máy chủ cho các miền cụ thể (và có thể là các miền con) cho đến khi nó cuối cùng đến máy chủ tên quyền của miền đúng, chứa địa chỉ IP số của trang web được tìm kiếm. Địa chỉ IP này sau đó được trả lại cho máy khách. Thú vị là, mặc dù có nhiều bước cần thiết, quá trình này có thể diễn ra rất nhanh chóng.

Máy chủ gốc là một phần quan trọng của cơ sở hạ tầng của Internet; trình duyệt web và nhiều công cụ internet khác sẽ không hoạt động nếu thiếu chúng. Có 13 địa chỉ IP khác nhau phục vụ vùng gốc DNS, và hàng trăm máy chủ gốc dự phòng tồn tại trên toàn cầu để xử lý các yêu cầu đến vùng gốc.

## Tại sao chỉ có 13 máy chủ gốc dns trên thế giới?
Một quan niệm sai lầm phổ biến là chỉ có 13 máy chủ gốc trên thế giới. Trên thực tế, còn nhiều địa chỉ khác nhưng vẫn chỉ có 13 địa chỉ IP được sử dụng để truy vấn các mạng máy chủ gốc khác nhau. Những hạn chế trong kiến trúc ban đầu của DNS yêu cầu phải có tối đa 13 địa chỉ máy chủ trong vùng gốc. Trong những ngày đầu của Internet, chỉ có một máy chủ cho mỗi địa chỉ IP trong số 13 địa chỉ, hầu hết đều được đặt tại Hoa Kỳ.

Ngày nay, mỗi địa chỉ IP trong số 13 địa chỉ IP đều có một số máy chủ sử dụng định tuyến Anycast để phân phối các yêu cầu dựa trên tải và vùng lân cận. Hiện tại có hơn 600 máy chủ DNS gốc khác nhau được phân bổ trên mọi lục địa đông dân trên trái đất.

## Làm cách nào để trình phân giải tìm thấy máy chủ gốc DNS?
Vì vùng gốc DNS nằm ở trên cùng của hệ thống phân cấp DNS nên các trình phân giải đệ quy không thể được chuyển hướng tới chúng khi tra cứu DNS. Do đó, mọi trình phân giải DNS đều có danh sách 13 địa chỉ máy chủ IP gốc được tích hợp trong phần mềm của nó. Bất cứ khi nào quá trình tra cứu DNS được bắt đầu, lần liên lạc đầu tiên của bộ đệ quy sẽ là với một trong 13 địa chỉ IP đó.

## Điều gì xảy ra khi máy chủ gốc DNS không khả dụng?
Nhờ sử dụng định tuyến Anycast và tính dự phòng cao, các máy chủ gốc rất đáng tin cậy. Nhưng trong một số trường hợp hiếm hoi, máy chủ gốc sẽ phải cập nhật địa chỉ IP của nó. Trong trường hợp này, trình phân giải đệ quy có thể tiếp tục sử dụng 12 địa chỉ IP khác trong vùng gốc để thực hiện tra cứu DNS cho đến khi phần mềm của họ được cập nhật địa chỉ chính xác của tất cả 13 máy chủ. Vì các trình phân giải sẽ thử lại cho đến khi chúng tiếp cận được một máy chủ gốc đang hoạt động nên không có sự gián đoạn nào đối với hoạt động bình thường của Internet khi một máy chủ gốc ngừng hoạt động.