# IPV4

### MỤC LỤC
[Tổng quan về chia mạng con IPv4](#tong-quan-ve-chia-mang-con)

- [Định nghĩa mạng con](#dinh-nghia-mang-con)
- [Phân tích mạng con và giải quyết nhu cầu](#phan-tich-mang-con)
- [Đưa ra lựa chọn thiết kế](#dua-ra-lua-chon-thiet-ke)

[Analyzing Subnet Mask](#analyzing-subnet-mask)

- [Subnet Mask Conversion](#subnet-mask-conversion)
- [Indentify Subnet Design Choices Using Masks](#indentify-subnet-design-choices-using-masks)

[Analyzing Existing Subnets](#analyzing-existing-subnets)

- [Defining a Subnet](#define-a-subnet)
- [Subnet Broadcast Address](#subnet-broadcast-address)
- [Analyzing Existing Subnets Binary](#analyzing-existing-subents-binary)
- [Analyzing Existing Subnets Decimal](#analyzing-existing-subnets-decimal)


# Tổng quan về chia mạng con IPv4
## Định nghĩa mạng con
- Một mạng con IP đơn giản chỉ là một phần của một mạng Class A, B hoặc C. Trong thực tế, thuật ngữ **"subnet"** là một phiên bản rút gọn của cụm từ **"subdivided network"** (mạng đã được phân chia). Ví dụ, một subnet của mạng Class B 172.16.0.0 có thể là tập hợp của tất cả các địa chỉ IP bắt đầu bằng 172.16.1 và sẽ bao gồm 172.16.1.0, 172.16.1.1, 172.16.1.2 và tiếp tục cho đến 172.16.1.255. Một subnet khác của cùng mạng Class B đó có thể là tất cả các địa chỉ bắt đầu bằng 172.16.2.

![Imgur](https://i.imgur.com/TBlFLrD.png)

## Phân tích mạng con và giải quyết nhu cầu.
### Quy tắc về máy chủ nào thuộc mạng con nào
Các địa chỉ IP phải được gán theo một số quy tắc cơ bản—và với những lý do hợp lý. Để làm cho quá trình định tuyến hoạt động hiệu quả, các quy tắc địa chỉ IP nhóm các địa chỉ thành các nhóm gọi là **subnets** (mạng con). Những quy tắc là như sau:
- Các địa chỉ trong cùng một mạng con không được tách biệt bởi một router.
- Các địa chỉ ở các mạng con khác nhau được tách biệt bởi ít nhất một router. 

![Imgur](https://i.imgur.com/lFQV6Em.png)

## Đưa ra lựa chọn thiết kế.
### Chose a Classful Network
#### Public IP Network
**Đặc điểm**:
- Là các mạng IP được đăng ký và quản lý toàn cầu bởi các tổ chức như ARIN (American Registry for Internet Numbers), RIPE (Réseaux IP Européens), APNIC (Asia-Pacific Network Information Centre), và các tổ chức quản lý IP khác.
- Các địa chỉ IP trong mạng này là duy nhất và có thể truy cập trực tiếp từ Internet.
- Được sử dụng để kết nối các thiết bị và máy tính trực tiếp với Internet.

Ví dụ:
- Địa chỉ IP công cộng có thể là các địa chỉ như 203.0.113.0, 8.8.8.8 (Google DNS),...

#### Growth Exhausts the Public IP Address Space
- Với sự phổ biến của các thiết bị kết nối, bao gồm máy tính, điện thoại thông minh, máy tính bảng, thiết bị IoT (Internet of Things), và nhiều hơn nữa, nhu cầu về địa chỉ IP đã vượt qua nguồn cung có sẵn. Sự cạn kiệt địa chỉ IP công cộng IPv4 này đặt ra một thách thức, khi các tổ chức và các nhà cung cấp dịch vụ Internet (ISP) đang đối mặt khó khăn trong việc cấp phát địa chỉ duy nhất cho các thiết bị mới.
- Để giải quyết vấn đề này 
	- Một phiên bản IP mới (IPv6), với giải địa chỉ lớn hơn (128 bit)
	- Phân chia một phần của mạng IP công cộng cho mỗi công ty, thay vì toàn bộ mạng IP công cộng, để giảm lãng phí, sử dụng một tính năng được gọi là 'Classless Interdomain Routing' (CIDR)
	- Network Address Translation (NAT), cho phép sử dụng private IP networks.

#### Private IP Network
**Đặc điểm**:
- Là các mạng IP được sử dụng nội bộ trong các tổ chức, doanh nghiệp, hoặc mạng cá nhân.
- Các địa chỉ IP trong mạng này thường được sử dụng trong mạng nội bộ và không trực tiếp truy cập từ Internet.
- Có một số dãy địa chỉ IP đã được quy định để sử dụng riêng tư, như dãy A: 10.0.0.0 - 10.255.255.255, dãy B: 172.16.0.0 - 172.31.255.255, và dãy C: 192.168.0.0 - 192.168.255.255.
**Ví dụ**:
- Địa chỉ IP riêng tư có thể là 10.0.0.1, 192.168.1.1, 172.16.0.2,...

### Chose The Mask
#### Classful IP Networks Before Subnetting
- Khi nghĩ về một mạng lớp chưa được chia, các địa chỉ trong mạng chỉ có hai phần: phần mạng và phần máy chủ. 

![Imgur](https://i.imgur.com/yPiflJy.png)

- N và H lần lượt đại diện cho số bit mạng và và số bit host
- Số lượng địa chỉ trong một mạng IP lớp có thể được tính bằng công thức 2H – 2. Cụ thể, kích thước của một mạng lớp A, B hoặc C chưa được chia là như sau: 
	- Class A: 2^24 – 2 = 16,777,214
	- Class B: 2^16 – 2 = 65,534
	- Class C: 2^8 – 2 = 25

#### Borrowing Host Bits to Create Subnet Bits (Mượn các bit máy chủ để tạo các bit mạng con)
- Để chia mạng con, người thiết kế xem xét phần mạng và phần máy chủ, như thể hiện trong hình dưới đây, và sau đó thêm một phần thứ ba ở giữa:the subnet part (phần mạng con). Tuy nhiên, người thiết kế không thể thay đổi kích thước của phần mạng hoặc kích thước của toàn bộ địa chỉ (32 bit). Để tạo một phần mạng con trong cấu trúc địa chỉ, phải mượn các bit từ phần máy chủ.

![Imgur](https://i.imgur.com/KKfVm5s.png)

#### Choosing Enough Subnet and Host Bits (Lựa chọn đủ bit mạng con và bit máy chủ)

![Imgur](https://i.imgur.com/SjA38yT.png)

#### Example Design: 172.16.0.0, 200 Subnets, 200 Hosts
Để chọn **the mask**, người thiết kế mạng cần hỏi những câu hỏi sau: 
**Cần bao nhiêu bit subnet (mạng con) để tạo ra 200 mạng con**
- Bạn có thể thấy rằng nếu s=7 thì không đủ lớn (2^7=128), nhưng S=8 thì đủ (2^8=256). Như vậy ta cần ít nhất 8 bit subnet.

**Cần bao nhiêu bit máy chủ để có đủ 200 host cho mỗi subnet.
- Bạn có thể thấy rằng H = 7 không đủ lớn (2^7 – 2 = 126), nhưng H = 8 là đủ (2^8 – 2 = 254).

![Imgur](https://i.imgur.com/mccWbZV.png)


# Analyzing Subnet Mask
## Subnet Mask Conversion
### Converting Between Binary and DDN Masks

![Imgur](https://i.imgur.com/BUAptsa.png)

### Converting Between Prefix and DDN Masks

![Imgur](https://i.imgur.com/YVGddOo.png)

![Imgur](https://i.imgur.com/vmhmPTj.png)

## Indentify Subnet Design Choices Using Masks
### Masks Divide the Subnet’s Addresses into Two Parts
- The subnet mask subdivides the IP addresses in a subnet into two parts: the prefix, or subnet part, and the host part
	- **Prefixt (subnet) part: Equal in all addresses in the same subnet.
	- **Host part**: Different in all addresses in the same subnet.

![Imgur](https://i.imgur.com/3osdBml.png)

### Masks and Class Divide Addresses into Three Parts
- You can think about think IPv4 as having 3 parts. the prefix into two parts: the network part and the subnet part. The class defines the length of the network part, with the subnet part simply being the rest of the prefix.

![Imgur](https://i.imgur.com/w51kige.png)


- The combined network and subnet parts act like the prefix because all addresses in the same
subnet must have identical values in the network and subnet parts. 

- Example:

![Imgur](https://i.imgur.com/fCGp4Uw.png)

- In that example, the subnet uses mask 255.255.255.0, and the addresses are all in Class A network 10.0.0.0. The class defines 8 network bits, and the mask defines 24 prefix bits, meaning that 24 – 8 = 16 subnet bits exist. The host part remains as 8 bits per the mask.


### Classful and Classless Addressing
- **Classless addressing**: The concept that an IPv4 address has two parts—the prefix part plus the host part—as defined by the mask, with no consideration of the class (A, B, or C).
- **Classful addressing**: The concept that an IPv4 address has three parts—network, subnet, and host—as defined by the mask and Class A, B, and C rules.

**NOTE**: *Unfortunately, the networking world uses the terms classless and classful in a couple of different ways. In addition to the classless and classful addressing described here, each routing protocol can be categorized as either a classless routing protocol or a classful routing protocol. In another use, the terms classless routing and classful routing refer to some details of how Cisco routers forward (route) packets using the default route in some cases. As a result, these terms can be easily confused and misused. So, when you see the words classless and classful, be careful to note the context: addressing, routing, or routing protocols.*

### Calculations Based on the IPv4 Address Format
- **Hosts in the subnet**: 2H – 2, where H is the number of host bits.
- **Subnets in the network**: 2S, where S is the number of subnet bits. Only use this formula if
only one mask is used throughout the network

![Imgur](https://i.imgur.com/7ilelqb.png)

- You should be able to find all the information in Figure 13-8 and then calculate the number of hosts/subnet and the number of subnets in the network.The following process spells out the steps: 
	- **Step 1.** Convert the mask to prefix format (/P) as needed.
	- **Step 2.** Determine N based on the class.
	- **Step 3.** Calculate S = P – N.
	- **Step 4.** Calculate H = 32 – P.
	- **Step 5.** Calculate hosts/subnet**: 2H – 2.
	- **Step 6.** Calculate number of subnets: 2S.

- For example, consider the case of IP address 8.1.4.5 with mask 255.255.0.0 by following this process:
	- **Step 1.** 255.255.0.0 = /16, so P=16.
	- **Step 2.** 8.1.4.5 is in the range 1–126 in the first octet, so it is Class A; so N=8.
	- **Step 3.** S = P – N = 16 – 8 = 8.
	- **Step 4.** H = 32 – P = 32 – 16 = 16.
	- **Step 5.** 216 – 2 = 65,534 hosts/subnet.
	- **Step 6.** 28 = 256 subnets.


# Analyzing Existing Subnets
## Defining a Subnet
### Subnet ID Concepts
- A subnet ID is simply a number used to succinctly represent a subnet. When listed along with its matching subnet mask, the subnet ID identifies the subnet and can be used to derive the subnet broadcast address and range of addresses in the subnet.
- The terms subnet ID, subnet number, and subnet address are synonyms.

![Imgur](https://i.imgur.com/ZUOlKkh.png)

## Subnet Broadcast Address
- The subnet broadcast address has two main roles: to be used as a destination IP address for the purpose of sending packets to all hosts in the subnet, and as a means to find the high end of the range of addresses in a subnet.

![Imgur](https://i.imgur.com/9hZRX3M.png)

### Range of Usable Addresses
- To find the range of usable IP addresses in a subnet, first find the subnet ID and the subnet broadcast address. Then, just add 1 to the fourth octet of the subnet ID to get the first (lowest) usable address, and subtract 1 from the fourth octet of the subnet broadcast address to get the last (highest) usable address in the subnet.
- For example, subnet ID 172.16.128.0, mask /18. The first usable address is simply one more than the subnet ID (in this case, 172.16.128.1). That same figure showed a subnet broadcast address of 172.16.191.255, so the last usable address is one less, or 172.16.191.254.

## Analyzing Existing Subnets: Binary
### Finding the Subnet ID: Binary
- The subnet ID is the lowest numeric value in the subnet, so its host part, in binary, is all 0s. To find the subnet ID in binary, you take the IP address in binary and change all host bits to binary 0. 
- For example: 172.16.150.41, mask /18

![Imgur](https://i.imgur.com/4lbIAxw.png)

### Finding the Subnet Broadcast Addres: Binary
- Finding the subnet broadcast address uses a similar process. To find the subnet broadcast address, use the same binary process used to find the subnet ID, but instead of setting all the host bits to the lowest value (all binary 0s), set the host part to the highest value (all binary 1s).

![Imgur](https://i.imgur.com/gH4VqsI.png)

### Binary Practice Problems
- The following process summarizes those steps in written form for easier reference and practice:
	- Step 1. Convert the mask to prefix format to find the length of the prefix (/P) and the length of the host part (32 – P).

	- Step 2. Convert the IP address to its 32-bit binary equivalent.

	- Step 3. Copy the prefix bits of the IP address.

	- Step 4. Write down 0s for the host bits.

	- Step 5. Convert the resulting 32-bit number, 8 bits at a time, back to decimal.

## Analyzing Existing Subnets: Decimal
### Finding the Subnet ID: Difficult Masks
- The following written process lists all the steps to find the subnet ID, using only decimal math:
	- Step 1. If the mask octet = 255, copy the decimal IP address.
	- Step 2. If the mask octet = 0, write a decimal 0.
	- Step 3. If the mask is neither, refer to this octet as the **interesting octet**:
		A. Calculate the **magic number** as 256 – mask.
		B. Set the subnet ID’s value to the multiple of the magic number that is closest to the IP address without going over.

- The term **interesting octet** is the octet with the mask that is neither 255 nor 0
- The term **magic number** is the number you add to one subnet ID to get the next subnet ID in order

#### Resident Subnet Example

![Imgur](https://i.imgur.com/hINwT92.png)

![Imgur](https://i.imgur.com/KdZmUVT.png)

### Finding the Broadcast Address: Difficult Masks
- To find a subnet’s broadcast address, a similar process can be used. For simplicity, this process begins with the subnet ID, rather than the IP address. If you happen to start with an IP address instead, use the processes in this chapter to first find the subnet ID, and then use the following process to find the subnet broadcast address for that same subnet. For each octet:
	- Step 1. If the mask octet = 255, copy the subnet ID.
	- Step 2. If the mask octet = 0, write 255.
	- Step 3. If the mask is neither, identify this octet as the interesting octet:
		A. Calculate the magic number as 256 – mask.
		B. Take the subnet ID’s value, add the magic number, and subtract 1 (ID + magic – 1).

#### Resident Subnet Example

![Imgur](https://i.imgur.com/7sXcW43.png)