# 🌐 Network Administration - Cisco IOS CLI Guide

Repository này lưu trữ tài liệu hướng dẫn và tổng hợp các câu lệnh Cisco IOS CLI cơ bản dành cho môn học **Quản trị mạng** (sử dụng phần mềm **Cisco Packet Tracer**). 

Mục tiêu của tài liệu giúp người mới bắt đầu nhanh chóng nắm vững cú pháp, dễ dàng sao chép (copy & paste) các câu lệnh cấu hình thiết bị mạng (Router, Switch, PC), thiết lập địa chỉ IP, bảo mật mật khẩu và thực hiện kiểm tra kết nối từ xa qua Telnet. Mỗi bước đều cung cấp cả **Câu lệnh đầy đủ** và **Câu lệnh viết tắt (Shorthand)** thực tế hay dùng.

---

## 📌 BẢNG TỔNG HỢP CÁC CÂU LỆNH VIẾT TẮT DỄ NHỚ (QUICK CHEATSHEET)

| Tên lệnh đầy đủ | Lệnh viết tắt (Shorthand) | Chức năng |
| :--- | :--- | :--- |
| `enable` | `en` | Vào chế độ đặc quyền (Privileged EXEC) |
| `configure terminal` | `conf t` | Vào chế độ cấu hình toàn cục (Global Config) |
| `hostname <tên>` | `ho <tên>` | Đặt tên cho thiết bị |
| `interface <cổng>` | `int <cổng>` (VD: `int g0/0`, `int s0/0/0`) | Vào cấu hình cổng |
| `ip address <ip> <mask>` | `ip add <ip> <mask>` | Gán địa chỉ IP |
| `no shutdown` | `no shut` | Mở/kích hoạt cổng |
| `line console 0` | `line con 0` | Cấu hình cổng Console |
| `enable secret <pass>` | `ena sec <pass>` | Đặt mật khẩu mã hóa chế độ enable |
| `password <pass>` | `pass <pass>` | Đặt mật khẩu |
| `login` | `log` | Yêu cầu xác thực mật khẩu |
| `exit` | `ex` | Thoát ra chế độ trước đó |
| `write memory` | `wr` | Lưu cấu hình vào NVRAM |
| `show ip interface brief` | `sh ip int br` | Xem danh sách IP và trạng thái các cổng |
| `show running-config` | `sh run` | Xem cấu hình đang chạy trên RAM |
| `ipv6 unicast-routing` | `ipv6 uni` | Bật định tuyến IPv6 trên Router |
| `ipv6 address <ip>/<prefix>` | `ipv6 add <ip>/<prefix>` | Gán địa chỉ IPv6 cho cổng |
| `show ipv6 interface brief` | `sh ipv6 int br` | Xem danh sách IPv6 và trạng thái các cổng |
| `show ipv6 route` | `sh ipv6 ro` | Xem bảng định tuyến IPv6 |

---

## 1. CẤU HÌNH CHO ROUTER (Ví dụ: Router0)

*Bấm vào Router0 -> Chọn tab **CLI** -> Nhấn Enter để bắt đầu gõ.*

### Bước 1: Vào chế độ cấu hình toàn cục
* **Lệnh đầy đủ:**
```text
enable
configure terminal
```
* **Lệnh viết tắt:**
```text
en
conf t
```
*Giải thích: Di chuyển từ chế độ người dùng sang chế độ cấu hình hệ thống.*

---

### Bước 2: Đặt Hostname (Tên thiết bị)
* **Lệnh đầy đủ:**
```text
hostname Router0
```
* **Lệnh viết tắt:**
```text
ho Router0
```
*Giải thích: Đổi tên Router thành `Router0`.*

---

### Bước 3: Thiết lập Banner chào mừng/cảnh báo
* **Lệnh đầy đủ:**
```text
banner motd # Chao mung den voi Router0 - He thong quan tri mang #
```
* **Lệnh viết tắt:**
```text
ban motd # Chao mung den voi Router0 - He thong quan tri mang #
```
*Giải thích: Hiển thị thông báo chào mừng mỗi khi kết nối vào Router.*

---

### Bước 4: Đặt mật khẩu truy cập trực tiếp (Console)
* **Lệnh đầy đủ:**
```text
line console 0
password 123
login
exit
```
* **Lệnh viết tắt:**
```text
line con 0
pass 123
log
ex
```
*Giải thích: Yêu cầu mật khẩu `123` khi cắm cáp Console trực tiếp từ PC vào Router.*

---

### Bước 5: Đặt mật khẩu mã hóa để vào chế độ đặc quyền (Enable Secret)
* **Lệnh đầy đủ:**
```text
enable secret cisco123
```
* **Lệnh viết tắt:**
```text
ena sec cisco123
```
*Giải thích: Yêu cầu mật khẩu `cisco123` khi gõ lệnh `enable`.*

---

### Bước 6: Cấu hình mật khẩu truy cập từ xa (Telnet)
* **Lệnh đầy đủ:**
```text
line vty 0 4
password telnet123
login
exit
```
* **Lệnh viết tắt:**
```text
line vty 0 4
pass telnet123
log
ex
```
*Giải thích: Cho phép tối đa 5 kết nối Telnet đồng thời và yêu cầu mật khẩu là `telnet123`.*

---

### Bước 7: Cấu hình địa chỉ IP cho các cổng trên Router0 (LAN & WAN)

#### A. Cấu hình cổng LAN (Ví dụ: GigabitEthernet0/0 nối xuống Switch/PC)
* **Lệnh đầy đủ:**
```text
do show ip interface brief
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```
* **Lệnh viết tắt:**
```text
do sh ip int br
int g0/0
ip add 192.168.1.1 255.255.255.0
no shut
ex
```
*Giải thích: Gán IP LAN `192.168.1.1/24` cho cổng `GigabitEthernet0/0` và bật cổng hoạt động (mặc định các cổng trên Router đều tắt).*

#### B. Cấu hình cổng WAN Serial (Kết nối giữa các Router - ví dụ: Serial0/0/0)
*Lưu ý: Đầu cáp nào có ký hiệu đồng hồ (DCE) trong Packet Tracer thì cần cấu hình thêm lệnh `clock rate 64000` (hoặc `clock rate 9600`, `128000`...).*
* **Lệnh đầy đủ:**
```text
interface Serial0/0/0
ip address 10.0.0.1 255.0.0.0
clock rate 64000
no shutdown
exit
```
* **Lệnh viết tắt:**
```text
int s0/0/0
ip add 10.0.0.1 255.0.0.0
clock rate 64000
no shut
ex
```
*Giải thích: Gán IP mạng WAN `10.0.0.1` thuộc lớp mạng A cho cổng kết nối liên Router, thiết lập xung nhịp đồng bộ nếu là đầu DCE và bật cổng.*

---

### Bước 7.2: Ví dụ Cấu hình IP cho Router thứ hai (Router1)
*Nếu bài thực hành của bạn có thêm Router thứ hai (Router1) nối với Router0 qua cổng Serial:*

* **Lệnh đầy đủ:**
```text
enable
configure terminal
hostname Router1

interface Serial0/0/0
ip address 10.0.0.2 255.0.0.0
no shutdown
exit

interface GigabitEthernet0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

end
write memory
```

* **Lệnh viết tắt:**
```text
en
conf t
ho Router1

int s0/0/0
ip add 10.0.0.2 255.0.0.0
no shut
ex

int g0/0
ip add 192.168.2.1 255.255.255.0
no shut
ex

end
wr
```
*Giải thích: Cổng `Serial0/0/0` trên Router1 được đặt IP `10.0.0.2` (cùng đường mạng `10.0.0.0/8` với Router0) để 2 router thấy nhau. Cổng `GigabitEthernet0/0` đặt IP LAN `192.168.2.1` để làm Gateway cho nhánh mạng mới.*

---

### Bước 8: Lưu cấu hình
* **Lệnh đầy đủ:**
```text
end
write memory
```
* **Lệnh viết tắt:**
```text
end
wr
```
*(hoặc dùng lệnh `copy running-config startup-config` -> viết tắt: `cop r st`)*

---

## 2. CẤU HÌNH CHO SWITCH (Ví dụ: Switch0)

*Bấm vào Switch0 -> Chọn tab **CLI** -> Nhấn Enter.*

### Bước 1: Vào chế độ cấu hình
* **Lệnh đầy đủ:**
```text
enable
configure terminal
```
* **Lệnh viết tắt:**
```text
en
conf t
```

---

### Bước 2: Đặt Hostname
* **Lệnh đầy đủ:**
```text
hostname Switch0
```
* **Lệnh viết tắt:**
```text
ho Switch0
```

---

### Bước 3: Đặt mật khẩu Console & Enable Secret
* **Lệnh đầy đủ:**
```text
enable secret cisco123
line console 0
password 123
login
exit
```
* **Lệnh viết tắt:**
```text
ena sec cisco123
line con 0
pass 123
log
ex
```

---

### Bước 4: Cấu hình mật khẩu Telnet
* **Lệnh đầy đủ:**
```text
line vty 0 4
password telnet123
login
exit
```
* **Lệnh viết tắt:**
```text
line vty 0 4
pass telnet123
log
ex
```

---

### Bước 5: Gán địa chỉ IP quản trị trên cổng ảo VLAN 1
*Vì Switch lớp 2 không thể gán IP trực tiếp cho cổng vật lý, ta cần gán cho giao diện ảo VLAN 1 để Telnet từ xa.*
* **Lệnh đầy đủ:**
```text
interface vlan 1
ip address 192.168.1.2 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.1.1
```
* **Lệnh viết tắt:**
```text
int vlan 1
ip add 192.168.1.2 255.255.255.0
no shut
ex
ip def 192.168.1.1
```
*Giải thích: Gán IP `192.168.1.2` cho VLAN 1, kích hoạt nó và trỏ Gateway về IP của Router0 (`192.168.1.1`) để có thể liên lạc với các lớp mạng khác.*

---

### Bước 6: Lưu cấu hình
* **Lệnh đầy đủ:**
```text
end
write memory
```
* **Lệnh viết tắt:**
```text
end
wr
```

---

## 3. THIẾT LẬP IP CHO MÁY TÍNH (PC0)

### Cách 1: Thiết lập qua giao diện đồ họa (GUI)
1. Click vào **PC0** -> Chọn **Desktop** -> **IP Configuration**.
2. Nhập các thông số sau:
   - **IP Address**: `192.168.1.10`
   - **Subnet Mask**: `255.255.255.0`
   - **Default Gateway**: `192.168.1.1` *(IP cổng Router đã cấu hình ở phần 1)*

### Cách 2: Thiết lập bằng dòng lệnh (Nếu dùng Virtual PC - VPCS)
```cmd
ip 192.168.1.10 255.255.255.0 192.168.1.1
```

---

## 4. HƯỚNG DẪN CHI TIẾT CÁCH ĐĂNG NHẬP (LOGIN) VÀO THIẾT BỊ

Có hai cách đăng nhập chính tuỳ thuộc vào cách bạn kết nối với Switch hoặc Router:

### CÁCH 1: Đăng nhập từ xa bằng Telnet (Thực hiện từ PC0)

#### Bước 1: Mở Command Prompt trên PC0 và kiểm tra kết nối
1. Click vào **PC0** -> chọn tab **Desktop** -> chọn **Command Prompt**.
2. Kiểm tra đường truyền bằng lệnh:
   ```cmd
   ping 192.168.1.1
   ```
   *(Đảm bảo nhận được dòng phản hồi `Reply from 192.168.1.1: bytes=32...`)*

#### Bước 2: Khởi chạy phiên Telnet
Gõ lệnh sau tại Command Prompt của PC0 rồi nhấn **Enter**:
```cmd
telnet 192.168.1.1
```

#### Bước 3: Đăng nhập mật khẩu Telnet (VTY password)
Sau khi nhấn Enter, thiết bị sẽ hiển thị banner và yêu cầu mật khẩu:
```text
Chao mung den voi Router0 - He thong quan tri mang
User Access Verification
Password: 
```
👉 Bạn hãy gõ mật khẩu Telnet sau rồi nhấn **Enter**:
```text
telnet123
```
> ⚠️ **LƯU Ý RẤT QUAN TRỌNG:** Khi nhập mật khẩu trên cửa sổ Cisco CLI, **màn hình sẽ KHÔNG hiển thị bất kỳ ký tự nào** (không có dấu sao `*`, không hiện chữ bạn đang gõ). Đây là tính năng bảo mật. Bạn cứ gõ đúng chữ `telnet123` rồi nhấn **Enter**.

Khi đăng nhập thành công, dấu nhắc lệnh sẽ đổi thành:
```text
Router0>
```

#### Bước 4: Đăng nhập mật khẩu đặc quyền (Enable Secret) để vào cấu hình
Tại dấu nhắc `Router0>`, gõ lệnh đầy đủ `enable` hoặc viết tắt:
```text
en
```
Màn hình sẽ hiển thị dòng yêu cầu mật khẩu tiếp theo:
```text
Password: 
```
👉 Bạn hãy gõ mật khẩu đặc quyền sau (mật khẩu này cũng sẽ bị ẩn đi khi gõ) rồi nhấn **Enter**:
```text
cisco123
```

Khi đăng nhập thành công, dấu nhắc lệnh sẽ chuyển thành dấu thăng `#`:
```text
Router0#
```
Lúc này bạn đã vào được chế độ **Privileged EXEC Mode** và có toàn quyền kiểm tra, cấu hình thiết bị.

---

### CÁCH 2: Đăng nhập trực tiếp qua cổng Console (Khi cắm cáp hoặc click tab CLI)

Nếu bạn vừa mở tab **CLI** của thiết bị hoặc cắm cáp Console trực tiếp từ PC vào Router/Switch:

1. Nhấn phím **Enter**, màn hình sẽ hỏi mật khẩu đăng nhập trực tiếp:
   ```text
   Router0 con0 is now available
   Press RETURN to get started.
   Password: 
   ```
2. Nhập mật khẩu Console sau (ẩn khi gõ) rồi nhấn **Enter**:
   ```text
   123
   ```
3. Khi màn hình chuyển sang dấu nhắc chế độ người dùng `Router0>`, gõ lệnh đầy đủ `enable` hoặc viết tắt:
   ```text
   en
   ```
4. Khi màn hình hiện tiếp `Password:`, nhập mật khẩu đặc quyền (ẩn khi gõ) rồi nhấn **Enter**:
   ```text
   cisco123
   ```
   *(Dấu nhắc lệnh chuyển sang `Router0#` là bạn đã đăng nhập thành công)*

---

## 5. CÁC LỆNH KIỂM TRA NHANH (Bấm ở chế độ `Router#` hoặc `Switch#`)

### Xem trạng thái các cổng và IP (Rất quan trọng):
* **Lệnh đầy đủ:** `show ip interface brief`
* **Lệnh viết tắt:**
```text
sh ip int br
```

---

### Xem toàn bộ cấu hình đang chạy:
* **Lệnh đầy đủ:** `show running-config`
* **Lệnh viết tắt:**
```text
sh run
```

---

## 6. CẤU HÌNH ĐỊA CHỈ IPV6 VÀ ĐỊNH TUYẾN IPV6 (IPv6 CONFIGURATION)

### Bước 1: Bật tính năng định tuyến IPv6 trên Router (Bắt buộc)
Mặc định Router Cisco tắt tính năng định tuyến IPv6. Bạn phải bật lệnh này trước khi cấu hình IPv6.
* **Lệnh đầy đủ:**
```text
configure terminal
ipv6 unicast-routing
```
* **Lệnh viết tắt:**
```text
conf t
ipv6 uni
```
*Giải thích: Lệnh `ipv6 unicast-routing` cho phép Router chuyển tiếp các gói tin IPv6.*

---

### Bước 2: Cấu hình địa chỉ IPv6 cho các cổng trên Router (Router0)

#### A. Cấu hình địa chỉ IPv6 Global Unicast (GUA) & Link-Local (LLA) cho cổng LAN
* **Lệnh đầy đủ:**
```text
interface GigabitEthernet0/0
ipv6 address 2001:db8:1::1/64
ipv6 address fe80::1 link-local
no shutdown
exit
```
* **Lệnh viết tắt:**
```text
int g0/0
ipv6 add 2001:db8:1::1/64
ipv6 add fe80::1 link-local
no shut
ex
```
*Giải thích:*
- `2001:db8:1::1/64`: Gán địa chỉ IPv6 Global Unicast (dùng cho kết nối toàn mạng/Internet).
- `fe80::1 link-local`: Gán địa chỉ Link-Local cố định (dùng trao đổi thông tin trong cùng mạng LAN).

#### B. Cấu hình tự động tạo IPv6 theo chuẩn EUI-64 (Tùy chọn)
* **Lệnh đầy đủ:**
```text
interface GigabitEthernet0/0
ipv6 address 2001:db8:1::/64 eui-64
no shutdown
exit
```
* **Lệnh viết tắt:**
```text
int g0/0
ipv6 add 2001:db8:1::/64 eui-64
no shut
ex
```
*Giải thích: Tự động kết hợp Prefix `/64` với địa chỉ MAC của cổng để tạo địa chỉ IPv6 128-bit hoàn chỉnh.*

---

### Bước 3: Cấu hình địa chỉ IPv6 cho Switch (Switch0 - VLAN 1)
* **Lệnh đầy đủ:**
```text
interface vlan 1
ipv6 address 2001:db8:1::2/64
no shutdown
exit
```
* **Lệnh viết tắt:**
```text
int vlan 1
ipv6 add 2001:db8:1::2/64
no shut
ex
```
*Giải thích: Gán địa chỉ IPv6 cho giao diện ảo VLAN 1 trên Switch để quản trị từ xa.*

---

### Bước 4: Thiết lập địa chỉ IPv6 cho máy tính (PC0)

#### Cách 1: Thiết lập qua giao diện đồ họa (GUI)
1. Click vào **PC0** -> chọn tab **Desktop** -> chọn **IP Configuration**.
2. Cuộn xuống phần **IPv6 Configuration**:
   - Nếu chọn **Static**:
     - **IPv6 Address**: `2001:db8:1::10/64`
     - **IPv6 Gateway**: `fe80::1` *(hoặc IP cổng Router `2001:db8:1::1`)*
   - Nếu chọn **Auto / SLAAC**: Máy tính sẽ tự động nhận Prefix và Gateway từ Router phát ra qua gói tin Router Advertisement (RA).

#### Cách 2: Thiết lập bằng dòng lệnh (Nếu dùng Virtual PC - VPCS)
```cmd
ip 2001:db8:1::10/64 2001:db8:1::1
```

---

### Bước 5: Kiểm tra kết nối & Telnet qua IPv6 từ PC0

#### 1. Kiểm tra Ping IPv6 từ PC0:
```cmd
ping 2001:db8:1::1
```
*(Hoặc ping địa chỉ Link-Local: `ping fe80::1`)*

#### 2. Kết nối Telnet qua IPv6 từ PC0:
```cmd
telnet 2001:db8:1::1
```

---

### Bước 6: Các câu lệnh kiểm tra IPv6 nhanh (Troubleshooting)

#### 1. Xem trạng thái và địa chỉ IPv6 trên các cổng:
* **Lệnh đầy đủ:** `show ipv6 interface brief`
* **Lệnh viết tắt:**
```text
sh ipv6 int br
```

#### 2. Xem bảng định tuyến IPv6:
* **Lệnh đầy đủ:** `show ipv6 route`
* **Lệnh viết tắt:**
```text
sh ipv6 ro
```

---

