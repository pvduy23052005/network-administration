# 🛡️ HƯỚNG DẪN CẤU HÌNH ACL (ACCESS CONTROL LIST) TRÊN CISCO CLI

Tài liệu này hướng dẫn chi tiết về **Mục đích, Nguyên tắc hoạt động, Cú pháp tổng quát** và **Các bước cấu hình Access Control List (ACL)** trên thiết bị mạng Cisco. Tất cả các phần đều cung cấp song song **Lệnh đầy đủ** và **Lệnh viết tắt (Shorthand)** có thể copy trực tiếp vào Cisco Packet Tracer.

---

## 📌 1. MỤC ĐÍCH VÀ VAI TRÒ CỦA VIỆC CẤU HÌNH ACL

**Access Control List (ACL)** là một danh sách các câu lệnh quy tắc được áp dụng trên Router/Switch nhằm kiểm soát, lọc và phân loại các gói tin đi qua thiết bị.

### Các mục đích chính của cấu hình ACL:
1. **Tăng cường bảo mật mạng (Network Security):** Chặn các truy cập trái phép từ bên ngoài vào mạng nội bộ hoặc ngăn cách các phòng ban nội bộ với nhau.
2. **Lọc lưu lượng theo địa chỉ IP (IP Filtering):** Cho phép (Permit) hoặc từ chối (Deny) các gói tin dựa trên địa chỉ IP nguồn (Source IP) hoặc địa chỉ IP đích (Destination IP).
3. **Kiểm soát dịch vụ và cổng giao thức (Port/Protocol Filtering):** Giới hạn hoặc cho phép từng dịch vụ cụ thể như Web (HTTP - Port 80, HTTPS - Port 443), Truyền file (FTP - Port 21), Đăng nhập từ xa (SSH - Port 22, Telnet - Port 23), Kiểm tra kết nối (ICMP/Ping).
4. **Bảo mật truy cập quản trị thiết bị:** Giới hạn chỉ cho phép các IP máy tính của Quản trị viên (Admin) được phép Telnet/SSH vào Router/Switch (thông qua `line vty`).
5. **Hỗ trợ các công nghệ mạng khác:** ACL được sử dụng làm bộ lọc tiền xử lý cho NAT (Network Address Translation), QoS (Chất lượng dịch vụ), VPN (Mạng riêng ảo) và BGP Route-Map.

---

## 🎯 2. NGUYÊN TẮC VÀNG KHI CẤU HÌNH VÀ ÁP DỤNG ACL

Để cấu hình ACL chính xác và không làm gián đoạn hệ thống mạng, bạn bắt buộc phải ghi nhớ 4 nguyên tắc sau:

### 1️⃣ Nguyên tắc Dòng ẩn Tự động Chặn Tất Cả (Implicit Deny All)
* Cuối mỗi bảng ACL luôn tồn tại một dòng lệnh ẩn: `deny ip any any` (chặn toàn bộ lưu lượng còn lại).
* ➡️ **Hệ quả:** Nếu trong bảng ACL của bạn chỉ chứa các lệnh `deny`, tất cả các lưu lượng khác cũng sẽ bị chặn sạch. Do đó, **nếu đã có lệnh `deny` thì bắt buộc phải có ít nhất một lệnh `permit`** để cho phép các lưu lượng hợp lệ khác đi qua.

### 2️⃣ Thứ tự kiểm tra từ trên xuống dưới (Top-Down Execution)
* Router đối chiếu gói tin với các dòng trong ACL theo thứ tự từ trên xuống dưới (dòng 1 ➔ dòng 2 ➔ dòng 3...).
* Khi gói tin trùng khớp (match) với một dòng nào đó, Router sẽ **thực thi ngay lập tức** (Permit hoặc Deny) và **bỏ qua tất cả các dòng phía dưới**.
* ➡️ **Hệ quả:** Đặt các quy tắc chi tiết/cụ thể (Specific rules) ở phía trên, và các quy tắc chung (General rules) ở phía dưới.

### 3️⃣ Vị trí đặt ACL chuẩn (Placement Rules)
* **Standard ACL (Chỉ lọc theo IP nguồn):** Đặt **càng gần ĐÍCH (Destination) càng tốt**. *(Vì Standard ACL không kiểm tra IP đích, nếu đặt gần nguồn sẽ vô tình chặn luôn truy cập của nguồn đó tới các mạng khác)*.
* **Extended ACL (Lọc theo IP nguồn, IP đích, Port):** Đặt **càng gần NGUỒN (Source) càng tốt**. *(Giúp chặn ngay gói tin không hợp lệ từ đầu nguồn, tránh làm Router chuyển tiếp rác qua các chặng mạng trung gian)*.

### 4️⃣ Chiều dán ACL trên cổng giao tiếp (Interface Direction: In / Out)
Mỗi cổng Interface chỉ được áp dụng **tối đa 1 ACL theo chiều IN** và **1 ACL theo chiều OUT** cho mỗi giao thức (IPv4/IPv6).
* **`in` (Incoming):** Kiểm tra gói tin **ngay khi nó vừa chui vào** cổng của Router (xử lý trước khi Router định tuyến).
* **`out` (Outgoing):** Kiểm tra gói tin **trước khi Router đẩy nó ra khỏi** cổng (xử lý sau khi Router định tuyến).

---

## 📊 3. PHÂN LOẠI VÀ CÚ PHÁP TỔNG QUÁT CÁC LOẠI ACL

| Loại ACL | Phạm vi ID số | Phân loại kiểm tra | Vị trí đặt đề xuất |
| :--- | :---: | :--- | :--- |
| **Standard ACL (Tiêu chuẩn)** | `1 - 99` & `1300 - 1999` | Chỉ kiểm tra **Source IP** | Đặt gần **ĐÍCH** (Destination) |
| **Extended ACL (Mở rộng)** | `100 - 199` & `2000 - 2699` | Source IP, Destination IP, Protocol (TCP/UDP/ICMP), Port | Đặt gần **NGUỒN** (Source) |
| **Named ACL (ACL Đặt tên)** | Đặt tên chữ (`string`) | Hỗ trợ cả Standard và Extended | Tùy thuộc vào loại Standard hay Extended |

---

## 🛠️ 4. HƯỚNG DẪN CẤU HÌNH CHI TIẾT TỪNG LOẠI ACL

---

### 4.1. Standard ACL (ID từ 1 đến 99)

#### Cú pháp tổng quát:
```text
access-list <1-99> {permit|deny} {host <IP> | <IP_Mạng> <Wildcard_Mask> | any}
```

#### Kịch bản ví dụ:
Chặn máy PC1 có IP `192.168.1.10` truy cập vào mạng Server `192.168.2.0/24`. Các máy tính khác trong mạng vẫn được phép truy cập bình thường.

#### Bảng lệnh cấu hình:
* **Lệnh đầy đủ:**
```text
configure terminal
access-list 1 deny host 192.168.1.10
access-list 1 permit any

interface FastEthernet0/0
 ip access-group 1 out
exit
end
write memory
```

* **Lệnh viết tắt:**
```text
conf t
access-list 1 deny host 192.168.1.10
access-list 1 permit any

int fa0/0
 ip access-group 1 out
ex
end
wr
```
*Giải thích:* 
- `access-list 1 deny host 192.168.1.10`: Chặn riêng IP `192.168.1.10`.
- `access-list 1 permit any`: Cho phép tất cả các IP còn lại đi qua.
- `ip access-group 1 out`: Áp dụng ACL 1 theo chiều đẩy dữ liệu **RA khỏi cổng Fa0/0** (cổng hướng về phía mạng đích Server).

---

### 4.2. Extended ACL (ID từ 100 - 199 & 2000 - 2699)

#### Cú pháp tổng quát chi tiết:
```text
Router(config)# access-list <access-list-number> {permit|deny} <protocol> <source-address> <source-wildcard> <destination-address> <destination-wildcard> <operation> <operand>
```

#### Giải thích chi tiết các thành phần trong lệnh:
- **`access-list-number`**: Số hiệu của bảng Extended ACL, có giá trị nằm trong dải **`100 – 199`** hoặc **`2000 – 2699`**.
- **`{permit|deny}`**: 
  - `permit`: Cho phép gói tin đi qua.
  - `deny`: Từ chối/chặn gói tin.
- **`protocol`**: Giao thức ở tầng mạng hoặc tầng giao vận muốn lọc, phổ biến gồm:
  - `ip`: Lọc toàn bộ lưu lượng IP (bao gồm cả TCP, UDP, ICMP...).
  - `tcp`: Giao thức Transmission Control Protocol (Web, Email, FTP, Telnet, SSH...).
  - `udp`: Giao thức User Datagram Protocol (DNS, DHCP, TFTP...).
  - `icmp`: Giao thức ICMP (các gói tin Ping, Traceroute...).
- **`<source-address> <source-wildcard>`**: Địa chỉ IP nguồn và mặt nạ Wildcard Mask của nguồn gửi.
  - Dùng `host <IP>` (ví dụ: `host 192.168.1.10`) khi chỉ định đích danh 1 máy tính nguồn.
  - Dùng `any` khi đại diện cho tất cả các địa chỉ IP nguồn.
- **`<destination-address> <destination-wildcard>`**: Địa chỉ IP đích và mặt nạ Wildcard Mask của nơi nhận.
  - Dùng `host <IP>` (ví dụ: `host 192.168.2.100`) khi chỉ định 1 máy chủ đích cụ thể.
  - Dùng `any` khi đại diện cho tất cả các địa chỉ IP đích.
- **`operation`**: Phép toán so sánh cổng dịch vụ, thường dùng nhất là:
  - `eq` (Equal): Bằng/đúng với cổng chỉ định.
  - `neq` (Not Equal): Khác với cổng chỉ định.
  - `gt` (Greater Than): Lớn hơn cổng chỉ định.
  - `lt` (Less Than): Nhỏ hơn cổng chỉ định.
  - `range`: Nằm trong khoảng cổng từ `<port1>` đến `<port2>`.
- **`operand`**: Chỉ số cổng (Port Number) hoặc Tên dịch vụ tương ứng. Ví dụ:
  - `eq 80` hoặc `eq www`: Dịch vụ Web HTTP.
  - `eq 443`: Dịch vụ Web bảo mật HTTPS.
  - `eq 21` hoặc `eq ftp`: Dịch vụ truyền file FTP.
  - `eq 22`: Dịch vụ đăng nhập bảo mật SSH.
  - `eq 23` hoặc `eq telnet`: Dịch vụ đăng nhập từ xa Telnet.
  - `eq 53` hoặc `eq domain`: Dịch vụ phân giải tên miền DNS.
  - `eq 25` hoặc `eq smtp`: Dịch vụ gửi thư điện tử SMTP.

#### Kịch bản ví dụ:
Chặn máy PC1 `192.168.1.10` truy cập dịch vụ Web (Port 80/HTTP) của Server `192.168.2.100`, nhưng vẫn cho phép Ping và truy cập các dịch vụ khác bình thường.

#### Bảng lệnh cấu hình:
* **Lệnh đầy đủ:**
```text
configure terminal
access-list 100 deny tcp host 192.168.1.10 host 192.168.2.100 eq 80
access-list 100 permit ip any any

interface FastEthernet0/1
 ip access-group 100 in
exit
end
write memory
```

* **Lệnh viết tắt:**
```text
conf t
access-list 100 deny tcp host 192.168.1.10 host 192.168.2.100 eq 80
access-list 100 permit ip any any

int fa0/1
 ip access-group 100 in
ex
end
wr
```
*Giải thích:*
- `deny tcp host 192.168.1.10 host 192.168.2.100 eq 80`: Chặn gói tin TCP từ PC1 đến Server qua cổng Port 80 (Web).
- `permit ip any any`: Cho phép tất cả các lưu lượng IP khác (bao gồm ICMP Ping, DNS, FTP...).
- `ip access-group 100 in`: Áp dụng ACL 100 theo chiều **ĐI VÀO cổng Fa0/1** (cổng kết nối trực tiếp với nguồn PC1).

---

### 4.3. Named ACL (ACL Đặt Tên - Chuẩn quản trị doanh nghiệp)

Named ACL giúp quản trị viên đặt tên gợi nhớ cho bảng ACL, đồng thời hỗ trợ **chỉnh sửa, chèn hoặc xóa từng dòng lệnh cụ thể thông qua số thứ tự dòng (Sequence Number)** mà không cần phải xóa toàn bộ bảng ACL.

#### Kịch bản ví dụ:
Tạo một Extended Named ACL có tên `CHAN_WEB_KETOAN` để chặn dịch vụ Web HTTP/HTTPS từ mạng `192.168.1.0/24` đến Web Server `10.0.0.100`.

#### Bảng lệnh cấu hình:
* **Lệnh đầy đủ:**
```text
configure terminal
ip access-list extended CHAN_WEB_KETOAN
 deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.100 eq 80
 deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.100 eq 443
 permit ip any any
exit

interface FastEthernet0/1
 ip access-group CHAN_WEB_KETOAN in
exit
end
write memory
```

* **Lệnh viết tắt:**
```text
conf t
ip access-list ext CHAN_WEB_KETOAN
 deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.100 eq 80
 deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.100 eq 443
 permit ip any any
 ex

int fa0/1
 ip access-group CHAN_WEB_KETOAN in
 ex
end
wr
```

---

### 4.4. Đặt ACL Bảo vệ Truy cập Quản trị Router/Switch (VTY Line Security)

Để bảo vệ thiết bị, chỉ cho phép máy tính của Quản trị viên (Admin IP: `192.168.1.5`) được phép Telnet/SSH vào thiết bị mạng.

#### Bảng lệnh cấu hình:
* **Lệnh đầy đủ:**
```text
configure terminal
access-list 10 permit host 192.168.1.5

line vty 0 4
 access-class 10 in
exit
end
write memory
```

* **Lệnh viết tắt:**
```text
conf t
access-list 10 permit host 192.168.1.5

line vty 0 4
 access-class 10 in
ex
end
wr
```
*Giải thích: Sử dụng lệnh `access-class 10 in` trong chế độ `line vty 0 4` để giới hạn địa chỉ IP được kết nối từ xa vào thiết bị.*

---

## 🔍 5. CÁC CÂU LỆNH KIỂM TRA VÀ QUẢN LÝ ACL (SHOW & EDIT COMMANDS)

Thực hiện các câu lệnh dưới đây tại chế độ **Privileged EXEC** (dấu nhắc `#`):

### 5.1. Xem danh sách tất cả các ACL và số lần gói tin trùng khớp (Match Counters)
* **Lệnh đầy đủ:** `show access-lists`
* **Lệnh viết tắt:**
```text
sh acc
```

---

### 5.2. Xem cổng Interface đang gắn ACL nào theo chiều In/Out
* **Lệnh đầy đủ:** `show ip interface FastEthernet 0/1`
* **Lệnh viết tắt:**
```text
sh ip int fa0/1
```

---

### 5.3. Xóa toàn bộ một bảng ACL
* **Lệnh đầy đủ:**
```text
configure terminal
no access-list 100
```
* **Lệnh viết tắt:**
```text
conf t
no acc 100
```

---

### 5.4. Chỉnh sửa / Xóa 1 dòng cụ thể trong Named ACL (Sử dụng Sequence Number)
Giả sử xem `show access-lists` thấy bảng `CHAN_WEB_KETOAN` có các dòng:
`10 deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.100 eq 80`  
`20 permit ip any any`

* **Cách xóa riêng dòng 10:**
```text
conf t
ip access-list ext CHAN_WEB_KETOAN
 no 10
ex
```

* **Cách chèn thêm dòng mới vào giữa dòng 10 và 20 (ví dụ số 15):**
```text
conf t
ip access-list ext CHAN_WEB_KETOAN
 15 deny icmp any any
ex
```

---

## 💡 6. TÓM TẮT QUY TRÌNH 3 BƯỚC CẤU HÌNH ACL CHUẨN

1. **Bước 1 (Phân tích):** Xác định mục đích (chặn/cho phép cái gì?), loại ACL phù hợp (Standard hay Extended) và vị trí cổng dán (`in` hay `out`).
2. **Bước 2 (Tạo bảng ACL):** Viết các dòng lệnh `deny` / `permit` theo thứ tự từ cụ thể đến tổng quát. Nhớ dòng cuối `permit any` nếu có dùng `deny`.
3. **Bước 3 (Gán vào cổng/tuyến):** Truy cập vào interface cần lọc và dùng lệnh `ip access-group <Tên_hoặc_ID_ACL> <in|out>`.

---
*Chúc bạn thực hành cấu hình ACL thành công!*
