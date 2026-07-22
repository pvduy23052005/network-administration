# TỔNG HỢP CÂU LỆNH CISCO CLI (DỄ DÀNG COPY & PASTE)

Tài liệu này tập hợp các câu lệnh Cisco CLI ngắn gọn, có thể nhấn **Copy** trực tiếp để dán vào cửa sổ CLI của Cisco Packet Tracer.

---

## 1. CẤU HÌNH CHO ROUTER (Ví dụ: Router0)

*Bấm vào Router0 -> Chọn tab **CLI** -> Nhấn Enter để bắt đầu gõ.*

### Bước 1: Vào chế độ cấu hình toàn cục
```text
enable
configure terminal
```
*Giải thích: Di chuyển từ chế độ người dùng sang chế độ cấu hình hệ thống.*

### Bước 2: Đặt Hostname (Tên thiết bị)
```text
hostname Router0
```
*Giải thích: Đổi tên Router thành `Router0`.*

### Bước 3: Thiết lập Banner chào mừng/cảnh báo
```text
banner motd # Chao mung den voi Router0 - He thong quan tri mang #
```
*Giải thích: Hiển thị thông báo chào mừng mỗi khi kết nối vào Router.*

### Bước 4: Đặt mật khẩu truy cập trực tiếp (Console)
```text
line console 0
password 123
login
exit
```
*Giải thích: Yêu cầu mật khẩu `123` khi cắm cáp Console trực tiếp từ PC vào Router.*

### Bước 5: Đặt mật khẩu mã hóa để vào chế độ đặc quyền (Enable Secret)
```text
enable secret cisco123
```
*Giải thích: Yêu cầu mật khẩu `cisco123` khi gõ lệnh `enable`.*

### Bước 6: Cấu hình mật khẩu truy cập từ xa (Telnet)
```text
line vty 0 4
password telnet123
login
exit
```
*Giải thích: Cho phép tối đa 5 kết nối Telnet đồng thời và yêu cầu mật khẩu là `telnet123`.*

### Bước 7: Cấu hình địa chỉ IP cho các cổng trên Router0 (LAN & WAN)

#### A. Cấu hình cổng LAN (Ví dụ: GigabitEthernet0/0 nối xuống Switch/PC)
```text
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```
*Giải thích: Gán IP LAN `192.168.1.1/24` cho cổng `GigabitEthernet0/0` và bật cổng hoạt động (mặc định các cổng trên Router đều tắt).*

#### B. Cấu hình cổng WAN Serial (Kết nối giữa các Router - ví dụ: Serial0/0/0)
*Lưu ý: Đầu cáp nào có ký hiệu đồng hồ (DCE) trong Packet Tracer thì cần cấu hình thêm lệnh `clock rate 64000` (hoặc `clock rate 9600`, `128000`...).*
```text
interface Serial0/0/0
ip address 10.0.0.1 255.0.0.0
clock rate 64000
no shutdown
exit
```
*Giải thích: Gán IP mạng WAN `10.0.0.1` thuộc lớp mạng A cho cổng kết nối liên Router, thiết lập xung nhịp đồng bộ nếu là đầu DCE và bật cổng.*

---

### Bước 7.2: Ví dụ Cấu hình IP cho Router thứ hai (Router1)
*Nếu bài thực hành của bạn có thêm Router thứ hai (Router1) nối với Router0 qua cổng Serial:*
```text
enable
configure terminal
hostname Router1

# 1. Cấu hình IP cổng WAN Serial0/0/0 (để kết nối trực tiếp với Router0)
interface Serial0/0/0
ip address 10.0.0.2 255.0.0.0
no shutdown
exit

# 2. Cấu hình IP cổng LAN GigabitEthernet0/0 (nối xuống Switch/PC nhánh mạng 2)
interface GigabitEthernet0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

end
write memory
```
*Giải thích: Cổng `Serial0/0/0` trên Router1 được đặt IP `10.0.0.2` (cùng đường mạng `10.0.0.0/8` với Router0) để 2 router thấy nhau. Cổng `GigabitEthernet0/0` đặt IP LAN `192.168.2.1` để làm Gateway cho nhánh mạng mới.*

### Bước 8: Lưu cấu hình
```text
end
write memory
```
*Giải thích: Lưu toàn bộ cấu hình vừa thiết lập từ RAM vào bộ nhớ NVRAM để tránh bị mất khi mất điện/reload.*

---

## 2. CẤU HÌNH CHO SWITCH (Ví dụ: Switch0)

*Bấm vào Switch0 -> Chọn tab **CLI** -> Nhấn Enter.*

### Bước 1: Vào chế độ cấu hình
```text
enable
configure terminal
```

### Bước 2: Đặt Hostname
```text
hostname Switch0
```

### Bước 3: Đặt mật khẩu Console & Enable Secret
```text
enable secret cisco123
line console 0
password 123
login
exit
```

### Bước 4: Cấu hình mật khẩu Telnet
```text
line vty 0 4
password telnet123
login
exit
```

### Bước 5: Gán địa chỉ IP quản trị trên cổng ảo VLAN 1
*Vì Switch lớp 2 không thể gán IP trực tiếp cho cổng vật lý, ta cần gán cho giao diện ảo VLAN 1 để Telnet từ xa.*
```text
interface vlan 1
ip address 192.168.1.2 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.1.1
```
*Giải thích: Gán IP `192.168.1.2` cho VLAN 1, kích hoạt nó và trỏ Gateway về IP của Router0 (`192.168.1.1`) để có thể liên lạc với các lớp mạng khác.*

### Bước 6: Lưu cấu hình
```text
end
write memory
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
Tại dấu nhắc `Router0>`, gõ lệnh:
```text
enable
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
3. Khi màn hình chuyển sang dấu nhắc chế độ người dùng `Router0>`, gõ lệnh:
   ```text
   enable
   ```
4. Khi màn hình hiện tiếp `Password:`, nhập mật khẩu đặc quyền (ẩn khi gõ) rồi nhấn **Enter**:
   ```text
   cisco123
   ```
   *(Dấu nhắc lệnh chuyển sang `Router0#` là bạn đã đăng nhập thành công)*

---

## 5. CÁC LỆNH KIỂM TRA NHANH (Bấm ở chế độ `Router#` hoặc `Switch#`)

### Xem trạng thái các cổng và IP (Rất quan trọng):
```text
show ip interface brief
```

### Xem toàn bộ cấu hình đang chạy:
```text
show running-config
```
