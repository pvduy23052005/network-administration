# 📝 ĐỀ ÔN TẬP TRẮC NGHIỆM MẠNG MÁY TÍNH - TEST 1
**Chủ đề:** Tổng quan mạng, Mô hình OSI/TCP-IP, Chuẩn cáp truyền dẫn, Địa chỉ MAC & Chia mạng con IPv4  
**Số lượng:** 17 câu hỏi trắc nghiệm kèm đáp án và giải thích chi tiết.

---

### **Câu 1:** Thiết bị mạng nào hoạt động ở Tầng 1 (Physical) trong mô hình OSI, có chức năng khuếch đại tín hiệu và phát tán (broadcast) toàn bộ dữ liệu tới tất cả các cổng còn lại?
- A. Switch
- B. Hub
- C. Router
- D. Firewall

> 💡 **Đáp án đúng:** **B. Hub**  
> 🔍 **Giải thích:** Hub hoạt động ở tầng Physical (Tầng 1). Khi nhận dữ liệu từ 1 cổng, Hub khuếch đại và chuyển tới tất cả các cổng còn lại. Toàn bộ các cổng trên Hub nằm trong cùng **1 Collision Domain** và **1 Broadcast Domain**.

---

### **Câu 2:** Sự khác biệt cốt lõi về việc phân chia miền quảng bá (Broadcast Domain) giữa Switch Layer 2 và Router là gì?
- A. Switch chia nhỏ miền quảng bá trên mỗi cổng, Router thì không.
- B. Router chia nhỏ miền quảng bá trên từng cổng vật lý, Switch thuộc 1 miền quảng bá duy nhất (khi chưa chia VLAN).
- C. Cả Switch và Router đều không thể chia nhỏ miền quảng bá.
- D. Cả Switch và Router đều tự động chia miền quảng bá trên từng cổng.

> 💡 **Đáp án đúng:** **B. Router chia nhỏ miền quảng bá trên từng cổng vật lý, Switch thuộc 1 miền quảng bá duy nhất (khi chưa chia VLAN).**  
> 🔍 **Giải thích:** Router hoạt động ở Tầng 3 (Network), mỗi cổng của Router là một mạng riêng biệt (một Broadcast Domain riêng). Switch Layer 2 chia nhỏ miền đụng độ (Collision Domain) nhưng tất cả các cổng vẫn thuộc cùng 1 Broadcast Domain ngoại trừ khi được phân chia VLAN.

---

### **Câu 3:** Trong mô hình tham chiếu OSI 7 tầng, tầng nào chịu trách nhiệm mã hóa/giải mã, nén/giải nén và định dạng dữ liệu?
- A. Tầng 4 - Transport
- B. Tầng 5 - Session
- C. Tầng 6 - Presentation
- D. Tầng 7 - Application

> 💡 **Đáp án đúng:** **C. Tầng 6 - Presentation**  
> 🔍 **Giải thích:** Tầng Presentation (Biểu diễn dữ liệu) đảm nhận nhiệm vụ định dạng dữ liệu (ASCII, JPEG, MP3...), mã hóa/giải mã (Encryption/Decryption) và nén/giải nén dữ liệu trước khi chuyển lên tầng ứng dụng hoặc xuống tầng dưới.

---

### **Câu 4:** Tầng Transport (Giao vận) trong mô hình 7 tầng OSI tương ứng với tầng nào trong mô hình TCP/IP 4 tầng?
- A. Network Access
- B. Internet
- C. Transport
- D. Application

> 💡 **Đáp án đúng:** **C. Transport**  
> 🔍 **Giải thích:** Mô hình TCP/IP 4 tầng gồm: Network Access (Tầng 1 & 2 OSI), Internet (Tầng 3 OSI), Transport (Tầng 4 OSI) và Application (Tầng 5, 6 & 7 OSI).

---

### **Câu 5:** Đặc điểm nào sau đây **KHÔNG ĐÚNG** đối với giao thức UDP (User Datagram Protocol)?
- A. Hoạt động theo cơ chế không kết nối (Connectionless).
- B. Đảm bảo truyền dữ liệu tin cậy và tự động gửi lại các gói tin bị mất.
- C. Tốc độ truyền tải nhanh, chi phí tiêu tốn tiêu đề (overhead) nhỏ.
- D. Thường được sử dụng cho các ứng dụng thời gian thực như Video Streaming, VoIP, DNS.

> 💡 **Đáp án đúng:** **B. Đảm bảo truyền dữ liệu tin cậy và tự động gửi lại các gói tin bị mất.**  
> 🔍 **Giải thích:** Việc đảm bảo truyền tin cậy và gửi lại gói tin bị mất là đặc điểm của **TCP**. UDP là giao thức không hướng kết nối, không đảm bảo truyền dữ liệu tin cậy nhưng đổi lại có tốc độ truyền rất nhanh.

---

### **Câu 6:** Giao thức nào hoạt động ở tầng mạng/liên kết có chức năng phân giải địa chỉ IP sang địa chỉ MAC tương ứng?
- A. ICMP
- B. DHCP
- C. ARP
- D. DNS

> 💡 **Đáp án đúng:** **C. ARP**  
> 🔍 **Giải thích:** ARP (Address Resolution Protocol) dùng để tìm địa chỉ MAC (vật lý) tương ứng với một địa chỉ IP (logic) đã biết trong mạng cục bộ.

---

### **Câu 7:** Giao thức ICMP (Internet Control Message Protocol) được ứng dụng trực tiếp trong câu lệnh kiểm tra mạng phổ biến nào?
- A. `ping` và `traceroute`
- B. `ipconfig` và `ifconfig`
- C. `telnet` và `ssh`
- D. `nslookup` và `dig`

> 💡 **Đáp án đúng:** **A. `ping` và `traceroute`**  
> 🔍 **Giải thích:** Lệnh `ping` sử dụng gói tin ICMP Echo Request và Echo Reply để kiểm tra khả năng kết nối. Lệnh `traceroute` (hoặc `tracert`) dùng ICMP và giá trị TTL để dò vết đường đi của gói tin.

---

### **Câu 8:** Để kết nối trực tiếp hai máy tính (PC đến PC) với nhau không thông qua Switch hay Hub, người ta sử dụng loại cáp xoắn đôi nào?
- A. Cáp thẳng (Straight-through Cable)
- B. Cáp chéo (Crossover Cable)
- C. Cáp Console (Rollover Cable)
- D. Cáp quang Single-mode

> 💡 **Đáp án đúng:** **B. Cáp chéo (Crossover Cable)**  
> 🔍 **Giải thích:** Quy tắc bấm cáp chuẩn:
> - Kết nối 2 thiết bị cùng loại (PC - PC, Switch - Switch, Router - Router) hoặc PC - Router: Dùng **Cáp chéo**.
> - Kết nối 2 thiết bị khác loại (PC - Switch, Switch - Router): Dùng **Cáp thẳng**.

---

### **Câu 9:** Loại cáp quang nào chỉ truyền duy nhất **một tia sáng** theo đường thẳng, có đường kính lõi nhỏ và chuyên dùng cho khoảng cách truyền tải xa?
- A. Multi-mode Fiber
- B. Single-mode Fiber
- C. Cáp UTP Cat6
- D. Cáp đồng trục (Coaxial)

> 💡 **Đáp án đúng:** **B. Single-mode Fiber**  
> 🔍 **Giải thích:** Cáp quang Single-mode (đơn mode) truyền duy nhất 1 tia sáng, góc phản xạ ít, giảm độ suy hao tín hiệu nên truyền được khoảng cách rất xa (hàng chục km). Cáp Multi-mode truyền nhiều tia sáng đồng thời, thích hợp cho khoảng cách ngắn.

---

### **Câu 10:** Địa chỉ MAC (Media Access Control) có độ dài bao nhiêu bit và 3 byte đầu tiên đại diện cho thông tin gì?
- A. 32 bit; mã định danh thiết bị.
- B. 48 bit; mã định danh nhà sản xuất (OUI).
- C. 64 bit; mã lớp mạng.
- D. 128 bit; mã quốc gia.

> 💡 **Đáp án đúng:** **B. 48 bit; mã định danh nhà sản xuất (OUI).**  
> 🔍 **Giải thích:** Địa chỉ MAC dài 48 bit (6 byte), biểu diễn bằng 12 chữ số Hex. Trong đó: 3 byte đầu là OUI (Organizationally Unique Identifier) đại diện cho nhà sản xuất; 3 byte sau là số series do nhà sản xuất gán cho thiết bị.

---

### **Câu 11:** Chuẩn Ethernet **1000BASE-T** hỗ trợ tốc độ truyền dữ liệu tối đa là bao nhiêu?
- A. 10 Mbps
- B. 100 Mbps
- C. 1000 Mbps (1 Gbps)
- D. 10 Gbps

> 💡 **Đáp án đúng:** **C. 1000 Mbps (1 Gbps)**  
> 🔍 **Giải thích:** Quy ước chuẩn Ethernet:
> - `10BASE-T`: 10 Mbps
> - `100BASE-TX` (Fast Ethernet): 100 Mbps
> - `1000BASE-T` (Gigabit Ethernet): 1000 Mbps = 1 Gbps.

---

### **Câu 12:** Địa chỉ IP `10.50.1.100` thuộc lớp địa chỉ IPv4 nào sau đây?
- A. Lớp A
- B. Lớp B
- C. Lớp C
- D. Lớp D

> 💡 **Đáp án đúng:** **A. Lớp A**  
> 🔍 **Giải thích:** Dải IP phân lớp IPv4:
> - Lớp A: `1.0.0.0` – `127.255.255.255` (Octet đầu từ 1 đến 126).
> - Lớp B: `128.0.0.0` – `191.255.255.255` (Octet đầu từ 128 đến 191).
> - Lớp C: `192.0.0.0` – `223.255.255.255` (Octet đầu từ 192 đến 223).

---

### **Câu 13:** Dải địa chỉ IP Dùng riêng (Private IP) nào sau đây thuộc **Lớp C**?
- A. `10.0.0.0` đến `10.255.255.255`
- B. `172.16.0.0` đến `172.31.255.255`
- C. `192.168.0.0` đến `192.168.255.255`
- D. `169.254.0.0` đến `169.254.255.255`

> 💡 **Đáp án đúng:** **C. `192.168.0.0` đến `192.168.255.255`**  
> 🔍 **Giải thích:** 3 dải Private IP chuẩn theo RFC 1918:
> - Lớp A Private: `10.0.0.0/8`
> - Lớp B Private: `172.16.0.0/12`
> - Lớp C Private: `192.168.0.0/16`

---

### **Câu 14:** Khi một máy tính Windows không nhận được địa chỉ IP từ dịch vụ DHCP Server, hệ thống sẽ tự động gán một địa chỉ IP có dạng `169.254.x.x`. Địa chỉ này được gọi là gì?
- A. Loopback Address
- B. Multicast Address
- C. APIPA (Automatic Private IP Addressing) / Link-Local Address
- D. Default Gateway Address

> 💡 **Đáp án đúng:** **C. APIPA (Automatic Private IP Addressing) / Link-Local Address**  
> 🔍 **Giải thích:** APIPA gán địa chỉ IP tạm thời nằm trong dải `169.254.0.0/16` khi thiết bị đặt ở chế độ DHCP nhưng không giao tiếp được với DHCP server.

---

### **Câu 15:** Địa chỉ IP Loopback chuẩn `127.0.0.1` được sử dụng để làm gì?
- A. Kiểm tra địa chỉ MAC của card mạng.
- B. Kiểm tra sự hoạt động của chồng giao thức TCP/IP và card mạng nội bộ trên chính máy đó.
- C. Kết nối ra mạng Internet ngoài.
- D. Cấp phát IP tự động cho các máy con.

> 💡 **Đáp án đúng:** **B. Kiểm tra sự hoạt động của chồng giao thức TCP/IP và card mạng nội bộ trên chính máy đó.**  
> 🔍 **Giải thích:** Lệnh `ping 127.0.0.1` gửi gói tin quay vòng nội bộ (Loopback) để kiểm tra xem card mạng vật lý và driver TCP/IP trên máy tính có đang hoạt động bình thường hay không.

---

### **Câu 16:** Cho địa chỉ IP `192.168.1.50/26`. Địa chỉ ID mạng (Network Address) của dải mạng này là bao nhiêu?
- A. `192.168.1.0`
- B. `192.168.1.32`
- C. `192.168.1.64`
- D. `192.168.1.128`

> 💡 **Đáp án đúng:** **A. `192.168.1.0`**  
> 🔍 **Giải thích:** 
> - Prefix `/26` ➔ Subnet Mask là `255.255.255.192`.
> - Bước nhảy (Block size) = $256 - 192 = 64$.
> - Các dải mạng: `192.168.1.0/26` (từ .0 đến .63), `192.168.1.64/26` (từ .64 đến .127)...
> - IP `192.168.1.50` nằm trong khoảng `.0` đến `.63` ➔ Network ID là **`192.168.1.0`**.

---

### **Câu 17:** Cho Subnet Mask có giá trị `255.255.255.240`. Giá trị Wildcard Mask tương ứng (thường dùng trong cấu hình OSPF/ACL) là bao nhiêu?
- A. `0.0.0.255`
- B. `0.0.0.15`
- C. `0.0.0.31`
- D. `0.0.0.63`

> 💡 **Đáp án đúng:** **B. `0.0.0.15`**  
> 🔍 **Giải thích:** Công thức tính Wildcard Mask = `255.255.255.255` - `Subnet Mask`.  
> ➡️ `255.255.255.255` - `255.255.255.240` = **`0.0.0.15`**.
