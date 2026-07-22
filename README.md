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

## 4. CÁC BƯỚC KIỂM TRA & THỰC HIỆN TELNET TỪ PC0

### Bước 1: Ping kiểm tra kết nối từ PC0 đến Router0
*Mở **Command Prompt** trên PC0 và chạy lệnh:*
```cmd
ping 192.168.1.1
```
*Nếu kết quả trả về `Reply from...` nghĩa là đường truyền đã thông.*

### Bước 2: Thực hiện Telnet vào Router0 từ PC0
```cmd
telnet 192.168.1.1
```

### Bước 3: Đăng nhập bằng mật khẩu
1. Khi màn hình hiện `Password:`, hãy gõ mật khẩu Telnet sau (Lưu ý: Mật khẩu sẽ **không hiển thị ký tự** ra màn hình, bạn cứ gõ bình thường rồi bấm Enter):
```text
telnet123
```
2. Chuyển sang chế độ đặc quyền bằng lệnh:
```text
enable
```
3. Khi màn hình tiếp tục hỏi mật khẩu, nhập mật khẩu Enable Secret sau:
```text
cisco123
```

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
