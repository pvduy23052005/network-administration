# 📚 ÔN TẬP LÝ THUYẾT MẠNG MÁY TÍNH (CHƯƠNG 1)

---

## 1. TỔNG QUAN MẠNG VÀ THIẾT BỊ MẠNG (Câu 1 - 2)

*   **Các thành phần chính của mạng:**
    *   **Thiết bị đầu cuối (End Devices):** PC, Laptop, Server, Smartphone, Máy in...
    *   **Thiết bị kết nối/chuyển mạch (Intermediary Devices):** Hub, Switch, Router, Access Point, Firewall.
    *   **Phương tiện truyền dẫn (Media):** Cáp đồng, cáp quang, sóng vô tuyến.
    *   **Dịch vụ & Giao thức (Services & Protocols):** TCP/IP, HTTP, DNS, DHCP...
*   **Phân biệt Hub, Switch và Router:**
    *   **Hub (Tầng 1 - Physical):** Khuếch đại tín hiệu và phát tán (broadcast) dữ liệu tới tất cả các cổng. Thuộc **1 miền va chạm (Collision Domain)** và **1 miền quảng bá (Broadcast Domain)**.
    *   **Switch (Tầng 2 - Data Link):** Chuyển mạch dữ liệu dựa trên **địa chỉ MAC**. Chia nhỏ miền va chạm (mỗi cổng là 1 Collision Domain), thuộc **1 Broadcast Domain**.
    *   **Router (Tầng 3 - Network):** Định tuyến và chuyển tiếp gói tin giữa các mạng khác nhau dựa trên **địa chỉ IP**. Chia nhỏ **Broadcast Domain** (mỗi cổng là 1 Broadcast Domain).

---

## 2. MÔ HÌNH THAM CHIẾU OSI & TCP/IP (Câu 3 - 5)

*   **Mô hình OSI (7 tầng):**
    1.  **Physical (Vật lý):** Truyền dòng bit nhị phân qua môi trường truyền dẫn.
    2.  **Data Link (Liên kết dữ liệu):** Đóng gói thành Frame, quản lý địa chỉ MAC, phát hiện lỗi chặng.
    3.  **Network (Mạng):** Đóng gói thành Packet, định tuyến dữ liệu dựa trên địa chỉ IP.
    4.  **Transport (Giao vận):** Đóng gói thành Segment/Datagram, truyền dữ liệu end-to-end, kiểm soát luồng, sửa lỗi (TCP/UDP).
    5.  **Session (Phiên):** Thiết lập, duy trì và giải phóng các phiên kết nối giữa ứng dụng.
    6.  **Presentation (Biểu diễn):** Mã hóa/giải mã, nén/giải nén và định dạng dữ liệu.
    7.  **Application (Ứng dụng):** Giao tiếp trực tiếp với người dùng và ứng dụng (HTTP, FTP, SMTP, DNS).
*   **Mô hình TCP/IP (4 tầng):**
    1.  **Network Access (Truy nhập mạng):** Tương ứng tầng 1 & 2 của OSI.
    2.  **Internet (Mạng):** Tương ứng tầng 3 của OSI (IP, ICMP, ARP).
    3.  **Transport (Giao vận):** Tương ứng tầng 4 của OSI (TCP, UDP).
    4.  **Application (Ứng dụng):** Tương ứng tầng 5, 6 & 7 của OSI.
*   **So sánh Giao thức TCP và UDP:**
    *   **TCP (Transmission Control Protocol):** Hướng kết nối (Connection-oriented), đảm bảo tin cậy (gửi lại gói mất, sắp xếp đúng thứ tự), tốc độ chậm hơn, overhead lớn.
    *   **UDP (User Datagram Protocol):** Không kết nối (Connectionless), không đảm bảo tin cậy, không gửi lại gói mất, tốc độ nhanh, overhead nhỏ (dùng cho Video Streaming, VoIP, DNS).

---

## 3. CÁC GIAO THỨC TẦNG MẠNG VÀ TẦNG LIÊN KẾT (Câu 6 - 8)

*   **Giao thức IP (Internet Protocol):** Qui ước địa chỉ tầng mạng, cấu trúc gói dữ liệu và cách xử lý/định tuyến gói tin.
*   **Giao thức ICMP (Internet Control Message Protocol):** Thông báo lỗi và trạng thái truyền dữ liệu (dùng trong lệnh `ping`, `traceroute`).
*   **Giao thức ARP (Address Resolution Protocol):** Tìm địa chỉ MAC khi đã biết địa chỉ IP.

---

## 4. PHƯƠNG TIỆN TRUYỀN DẪN VÀ CHUẨN CÁP (Câu 9 - 15)

*   **Phân loại truyền dẫn:**
    *   *Hữu tuyến (Có dây):* Cáp xoắn đôi, cáp đồng trục, cáp quang.
    *   *Vô tuyến (Không dây):* Sóng Radio, Microwave, Hồng ngoại, Wi-Fi, Bluetooth.
*   **Cáp xoắn đôi (Twisted Pair):**
    *   *Cấu tạo:* Các cặp dây đồng xoắn lại từng cặp để giảm nhiễu điện từ.
    *   *Phân loại:* UTP (không bọc kim), STP (bọc kim chống nhiễu). Phân hạng Cat5e, Cat6, Cat6a...
    *   *Ứng dụng:* Dùng trong mạng LAN gia đình, văn phòng.
*   **Cáp Console:** Cáp dùng để kết nối cổng COM/USB của máy tính với cổng Console của Router/Switch để cấu hình thiết bị.
*   **Quy tắc chọn loại cáp bấm:**
    *   **Kết nối PC với Switch:** Cáp thẳng (Straight-through).
    *   **Kết nối Switch với Router:** Cáp thẳng (Straight-through).
    *   *(Lưu ý: Khác thiết bị dùng cáp thẳng; Cùng thiết bị hoặc PC-Router dùng cáp chéo).*
*   **Cáp đồng trục (Coaxial Cable):** Lõi đồng, lớp bọc điện, lưới kim loại chống nhiễu và vỏ bảo vệ. Dùng cho truyền hình cáp, mạng LAN chuẩn cũ.
*   **Cáp quang (Fiber Optic):** Truyền tín hiệu bằng ánh sáng qua lõi thủy tinh/nhựa. Gồm Single-mode (truyền xa, 1 tia sáng) và Multi-mode (truyền ngắn, nhiều tia sáng). Băng thông rất cao, không bị nhiễu điện từ.

---

## 5. ĐỊA CHỈ MAC VÀ CÁC CHUẨN ETHERNET (Câu 16 - 23)

*   **Địa chỉ MAC (Physical Address):**
    *   Độ dài: **48 bit** (6 byte), biểu diễn dạng Hex (ví dụ: `00-1A-2B-3C-4D-5E`).
    *   **3 byte đầu (OUI):** Mã số định danh nhà sản xuất thiết bị.
    *   **3 byte sau:** Mã số định danh thiết bị do nhà sản xuất gán.
*   **Tốc độ truyền dữ liệu cơ bản:**
    *   **Ethernet (Chuẩn):** 10 Mbps.
    *   **Fast Ethernet:** 100 Mbps.
    *   **Gigabit Ethernet:** 1000 Mbps (1 Gbps).
*   **Tốc độ theo chuẩn cụ thể:**
    *   **10BASE-F:** 10 Mbps (cáp quang).
    *   **100BASE-TX:** 100 Mbps (cáp xoắn đôi Cat5).
    *   **1000BASE-T:** 1000 Mbps / 1 Gbps (cáp xoắn đôi Cat5e/Cat6).

---

## 6. ĐỊA CHỈ IPV4 VÀ CHIA MẠNG CON (SUBNETTING) (Câu 24 - 43)

*   **Vị trí gán IP:** Địa chỉ IP được gán ở **Tầng Mạng (Network Layer)** trong mô hình TCP/IP.
*   **Các lớp địa chỉ IPv4 (Classful):**
    *   **Lớp A:** IP `1.0.0.0` - `127.255.255.255` | NetID: **8 bit**, HostID: **24 bit**.
        *   Số mạng: $2^7 - 2 = 126$ mạng.
        *   Số host/mạng: $2^{24} - 2 = 16,777,214$ host *(cung cấp nhiều host nhất trên 1 NetID)*.
    *   **Lớp B:** IP `128.0.0.0` - `191.255.255.255` | NetID: **16 bit**, HostID: **16 bit**.
        *   Số mạng: $2^{14} = 16,384$ mạng.
        *   Số host/mạng: $2^{16} - 2 = 65,534$ host.
    *   **Lớp C:** IP `192.0.0.0` - `223.255.255.255` | NetID: **24 bit**, HostID: **8 bit**.
        *   Số mạng: $2^{21} = 2,097,152$ mạng.
        *   Số host/mạng: $2^8 - 2 = 254$ host.
*   **Địa chỉ IPv4 đặc biệt:**
    *   **Private IP:** `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
    *   **Loopback IP:** `127.0.0.0/8` (dùng kiểm tra card mạng nội bộ).
    *   **Link-Local IP (APIPA):** `169.254.0.0/16` (tự gán khi lỗi DHCP).
*   **Độ dài tiền tố (Prefix length `/x`):** Số bit `1` liên tiếp trong Subnet Mask dành cho phần Mạng (Network ID).
*   **Phân loại IP trong 1 Subnet:**
    *   **Địa chỉ Mạng:** Bit phần Host bằng `0` hết.
    *   **Địa chỉ Quảng bá (Broadcast):** Bit phần Host bằng `1` hết.
    *   **Địa chỉ Máy trạm (Host):** Nằm giữa địa chỉ Mạng và Quảng bá.

### Kết quả & Đáp án bài tập tính toán Subnet (Câu 33 - 43):

*   **Câu 33 (`203.178.142.0/24`):**
    *   a) `203.178.142.0`: Địa chỉ Mạng (Network).
    *   b) `203.178.142.128`: Địa chỉ Máy trạm (Host).
    *   c) `203.178.142.255`: Địa chỉ Quảng bá (Broadcast).
*   **Câu 34 (Subnet mask thập phân):**
    *   a) `/8` $\rightarrow$ `255.0.0.0` | b) `/16` $\rightarrow$ `255.255.0.0` | c) `/24` $\rightarrow$ `255.255.255.0`
    *   d) `/25` $\rightarrow$ `255.255.255.128` | e) `/26` $\rightarrow$ `255.255.255.192`
    *   f) `/27` $\rightarrow$ `255.255.255.224` | g) `/28` $\rightarrow$ `255.255.255.240`
*   **Câu 35 (`172.16.1.200/20`):** Subnet mask nhị phân: `11111111.11111111.11110000.00000000` (`255.255.240.0`).
*   **Câu 36 (`192.168.1.70`, mask `255.255.255.240` /28):** Mạng con chứa IP này là **`192.168.1.64/28`**.
*   **Câu 37:**
    *   a) `133.27.4.128/25`: Host `133.27.4.129 - 133.27.4.254`, Broadcast `133.27.4.255`.
    *   b) `144.28.16.0/24`: Host `144.28.16.1 - 144.28.16.254`, Broadcast `144.28.16.255`.
*   **Câu 38:** Mạng `/24` chia 8 mạng con ($2^3=8 \rightarrow$ mượn 3 bit $\rightarrow$ Prefix `/27`): Số host tối đa = $2^{32-27} - 2 =$ **30 host**.
*   **Câu 39:** Mạng lớp B (`/16`) mượn 5 bit Host ID $\rightarrow$ Prefix `/21`: Subnet Mask = **`255.255.248.0`**.
*   **Câu 40:** Mạng `69.121.96.0/19` chia 4 mạng con ($2^2=4 \rightarrow$ mượn 2 bit $\rightarrow$ Prefix `/21`): Mặt nạ mạng con là **`255.255.248.0`**.
*   **Câu 41 (`139.63.0.0/17` chia 4 subnet $\rightarrow$ `/19`, bước nhảy 32 ở octet 3):**
    1. Subnet 1: Net `139.63.0.0/19`, Host `139.63.0.1 - 139.63.31.254`, Broadcast `139.63.31.255`.
    2. Subnet 2: Net `139.63.32.0/19`, Host `139.63.32.1 - 139.63.63.254`, Broadcast `139.63.63.255`.
    3. Subnet 3: Net `139.63.64.0/19`, Host `139.63.64.1 - 139.63.95.254`, Broadcast `139.63.95.255`.
    4. Subnet 4: Net `139.63.96.0/19`, Host `139.63.96.1 - 139.63.127.254`, Broadcast `139.63.127.255`.
*   **Câu 42 (`198.119.40.64/26` chia 4 subnet $\rightarrow$ `/28`, bước nhảy 16):**
    1. Subnet 1: Net `198.119.40.64/28`, Host `198.119.40.65 - 198.119.40.78`, Broadcast `198.119.40.79`.
    2. Subnet 2: Net `198.119.40.80/28`, Host `198.119.40.81 - 198.119.40.94`, Broadcast `198.119.40.95`.
    3. Subnet 3: Net `198.119.40.96/28`, Host `198.119.40.97 - 198.119.40.110`, Broadcast `198.119.40.111`.
    4. Subnet 4: Net `198.119.40.112/28`, Host `198.119.40.113 - 198.119.40.126`, Broadcast `198.119.40.127`.
*   **Câu 43 (VLSM với `223.1.17.0/24`):**
    *   Subnet 2 (89 host $\rightarrow$ cần 128 IP $\rightarrow$ `/25`): Net `223.1.17.0/25`, Host `223.1.17.1 - 223.1.17.126`, Broadcast `223.1.17.127`.
    *   Subnet 1 (50 host $\rightarrow$ cần 64 IP $\rightarrow$ `/26`): Net `223.1.17.128/26`, Host `223.1.17.129 - 223.1.17.190`, Broadcast `223.1.17.191`.
    *   Subnet 3 (16 host $\rightarrow$ cần 32 IP $\rightarrow$ `/27`): Net `223.1.17.192/27`, Host `223.1.17.193 - 223.1.17.222`, Broadcast `223.1.17.223`.

---

## 7. LÝ THUYẾT ĐỊA CHỈ IPV6 (Câu 44 - 51)

*   **Độ dài & Ví dụ:** Độ dài **128 bit**, biểu diễn dưới dạng Hexadecimal gồm 8 nhóm (mỗi nhóm 16 bit), cách nhau bởi dấu `:`. Ví dụ: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
*   **Quy tắc rút gọn IPv6:**
    1.  Bỏ các số `0` đứng đầu trong mỗi nhóm.
    2.  Thay thế dãy liên tiếp các nhóm toàn số `0` bằng `::` (chỉ áp dụng `::` **duy nhất 1 lần** trong 1 địa chỉ).
*   **Cấu trúc địa chỉ IPv6:**
    *   **Network Prefix (Phần mạng):** Thường 64 bit (Global Prefix + Subnet ID).
    *   **Interface ID (Định danh giao diện):** 64 bit.
    *   *Độ dài tiền tố khuyến nghị cho LAN:* **/64**.
*   **Phân loại địa chỉ IPv6:**
    *   **Unicast:** Truyền từ 1 nguồn đến 1 đích duy nhất.
    *   **Multicast:** Truyền từ 1 nguồn đến nhóm thiết bị lắng nghe.
    *   **Anycast:** Truyền từ 1 nguồn đến 1 thiết bị gần nhất trong nhóm. *(IPv6 **không** có Broadcast)*.
*   **Các loại IPv6 Unicast:**
    *   *Global Unicast (GUA):* Địa chỉ định tuyến Internet (bắt đầu bằng `2000::/3`).
    *   *Link-Local (LLA):* Địa chỉ nội bộ chặng (bắt đầu bằng `fe80::/10`).
    *   *Unique Local (ULA):* Địa chỉ riêng (bắt đầu bằng `fc00::/7`).
*   **Tạo địa chỉ LLA từ MAC (Quy tắc EUI-64):**
    1.  Lấy Prefix LLA: `fe80::/64`.
    2.  Chèn `FF-FE` vào giữa địa chỉ MAC 48-bit.
    3.  Đảo bit thứ 7 (từ trái sang) của byte đầu tiên.
    *   *Đáp án Câu 51 (MAC `54-A0-50-A8-E6-72`):* LLA IPv6 là **`fe80::56a0:50ff:fea8:e672`**.

---

## 8. CẤU HÌNH THIẾT BỊ CISCO VÀ LỆNH CLI (Câu 52 - 75)

*   **Cách cấp phát IP cho máy trạm:**
    1.  Tĩnh (Static IP): Nhập tay.
    2.  Động (Dynamic IP): Dùng DHCP (cho IPv4/v6) hoặc SLAAC (cho IPv6).
*   **Thành phần phần cứng Router:** CPU, RAM, NVRAM (lưu startup-config), Flash (lưu file IOS), ROM (POST, Bootstrap).
*   **Phần mềm mô phỏng terminal:** PuTTY, Tera Term, SecureCRT, Minicom.
*   **Các chế độ cấu hình Cisco (CLI modes):**
    *   `Router>` : User EXEC Mode (chế độ xem cơ bản).
    *   `Router#` : Privileged EXEC Mode (chế độ quản trị/lệnh `enable`).
    *   `Router(config)#` : Global Configuration Mode (cấu hình chung/lệnh `configure terminal`).
    *   `Router(config-if)#` : Interface Configuration Mode (cấu hình cổng/lệnh `interface ...`).
    *   `Router(config-line)#` : Line Configuration Mode (cấu hình console/VTY/lệnh `line ...`).

### Bảng tổng hợp câu lệnh Cisco IOS:

| Mục đích cấu hình | Câu lệnh trong Cisco CLI |
| :--- | :--- |
| Đặt tên Router/Switch | `hostname <Tên_thành_viên>` |
| Đặt banner thông báo | `banner motd # <Nội_dung_thông_báo> #` |
| Mật khẩu User EXEC (Console) | `line console 0` $\rightarrow$ `password <pass>` $\rightarrow$ `login` |
| Mật khẩu Privileged EXEC | `enable secret <pass>` |
| Mật khẩu Telnet/SSH (VTY) | `line vty 0 4` $\rightarrow$ `password <pass>` $\rightarrow$ `login` |
| Mã hóa tất cả mật khẩu văn bản | `service password-encryption` |
| Gán địa chỉ IPv4 cho Interface | `interface fa0/0` $\rightarrow$ `ip address 192.168.10.1 255.255.255.0` $\rightarrow$ `no shutdown` |
| Gán địa chỉ IPv6 cho Interface | `interface se0/2/0` $\rightarrow$ `ipv6 address 2001::1/64` $\rightarrow$ `no shutdown` |
| Lưu cấu hình từ RAM sang NVRAM | `copy running-config startup-config` (hoặc `write memory`) |
| Xem thông tin bộ nhớ Flash | `show flash:` |
| Xem thông tin hệ điều hành IOS | `show version` |
| Xem bảng tương ánh ARP | `show ip arp` |
| Xem cấu hình đang chạy trên RAM | `show running-config` |
| Xem cấu hình đã lưu ở NVRAM | `show startup-config` |
| Xem trạng thái và tên Interface | `show ip interface brief` / `show ipv6 interface brief` |
