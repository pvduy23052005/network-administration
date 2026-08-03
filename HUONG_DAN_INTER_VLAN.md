# 🌐 HƯỚNG DẪN CẤU HÌNH ĐỊNH TUYẾN GIỮA CÁC VLAN (INTER-VLAN ROUTING)

Mặc định các thiết bị thuộc hai VLAN khác nhau (ví dụ: VLAN 10 và VLAN 20) **không thể liên lạc trực tiếp được với nhau** ở Tầng 2 (Data Link) nhằm mục đích cô lập và bảo mật. Để 2 VLAN giao tiếp được với nhau, ta phải cấu hình **Định tuyến Inter-VLAN**.

Tài liệu này hướng dẫn 2 phương pháp cấu hình chuẩn trên thiết bị Cisco CLI:
1. **Phương pháp 1: Router-on-a-Stick** (Sử dụng 1 Router + 1 Switch Layer 2) – *Phương pháp phổ biến nhất trong bài tập thực hành*.
2. **Phương pháp 2: Định tuyến trên Switch Layer 3** (Multilayer Switch - SVI) – *Áp dụng khi dùng Switch Layer 3*.

---

## 🛠️ PHƯƠNG PHÁP 1: ROUTER-ON-A-STICK (1 ROUTER + 1 SWITCH LAYER 2)

### Sơ đồ giả định:
- **VLAN 10** (Tên: `KETOAN`, Mạng: `192.168.10.0/24`) kết nối vào cổng `Fa0/1` của Switch.
- **VLAN 20** (Tên: `KYTHUAT`, Mạng: `192.168.20.0/24`) kết nối vào cổng `Fa0/6` của Switch.
- Cáp nối giữa cổng `Fa0/24` của Switch và cổng `GigabitEthernet0/0` của Router là **đường Trunk**.

```text
[PC1 (VLAN 10)] --- (Fa0/1)  [Switch0] (Fa0/24) ======= (g0/0) [Router0]
[PC2 (VLAN 20)] --- (Fa0/6)  
```

---

### BƯỚC 1: Cấu hình trên Switch Layer 2 (Switch0)

#### 1. Tạo các VLAN 10 và VLAN 20:
* **Lệnh đầy đủ:**
```text
configure terminal
vlan 10
 name KETOAN
exit
vlan 20
 name KYTHUAT
exit
```
* **Lệnh viết tắt:**
```text
conf t
vlan 10
 name KETOAN
ex
vlan 20
 name KYTHUAT
ex
```

#### 2. Gán cổng Access cho các máy tính thuộc VLAN:
* **Lệnh đầy đủ:**
```text
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
exit

interface FastEthernet0/6
 switchport mode access
 switchport access vlan 20
exit
```
* **Lệnh viết tắt:**
```text
int fa0/1
 sw mo acc
 sw acc vlan 10
ex

int fa0/6
 sw mo acc
 sw acc vlan 20
ex
```

#### 3. Cấu hình cổng kết nối với Router thành đường Trunk:
* **Lệnh đầy đủ:**
```text
interface FastEthernet0/24
 switchport mode trunk
exit
```
* **Lệnh viết tắt:**
```text
int fa0/24
 sw mo tr
ex
```

---

### BƯỚC 2: Cấu hình trên Router (Router0)

Trên Router, ta kích hoạt cổng vật lý `GigabitEthernet0/0`, sau đó chia thành các giao diện con ảo (**Sub-interfaces**: `g0/0.10` và `g0/0.20`) tương ứng với từng VLAN.

#### 1. Bật cổng vật lý của Router:
* **Lệnh đầy đủ:**
```text
configure terminal
interface GigabitEthernet0/0
 no shutdown
exit
```
* **Lệnh viết tắt:**
```text
conf t
int g0/0
 no shut
ex
```

#### 2. Tạo Sub-interface cho VLAN 10 (Làm Gateway cho VLAN 10):
* **Lệnh đầy đủ:**
```text
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit
```
* **Lệnh viết tắt:**
```text
int g0/0.10
 encap dot1Q 10
 ip add 192.168.10.1 255.255.255.0
ex
```

#### 3. Tạo Sub-interface cho VLAN 20 (Làm Gateway cho VLAN 20):
* **Lệnh đầy đủ:**
```text
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit
```
* **Lệnh viết tắt:**
```text
int g0/0.20
 encap dot1Q 20
 ip add 192.168.20.1 255.255.255.0
ex
```

#### 4. Lưu cấu hình Router:
* **Lệnh đầy đủ:** `end` ➔ `write memory`
* **Lệnh viết tắt:** `end` ➔ `wr`

---

### BƯỚC 3: Cấu hình IP tĩnh và Gateway trên các Máy tính (PC)

- **Cấu hình trên PC1 (VLAN 10):**
  - IP Address: `192.168.10.10`
  - Subnet Mask: `255.255.255.0`
  - **Default Gateway:** `192.168.10.1` *(IP của Sub-interface g0/0.10)*

- **Cấu hình trên PC2 (VLAN 20):**
  - IP Address: `192.168.20.10`
  - Subnet Mask: `255.255.255.0`
  - **Default Gateway:** `192.168.20.1` *(IP của Sub-interface g0/0.20)*

---

### BƯỚC 4: Kiểm tra kết nối giữa 2 VLAN

1. Click vào **PC1 (VLAN 10)** ➔ chọn tab **Desktop** ➔ chọn **Command Prompt**.
2. Thực hiện lệnh Ping sang IP của **PC2 (VLAN 20)**:
   ```cmd
   ping 192.168.20.10
   ```
3. Nếu nhận được phản hồi `Reply from 192.168.20.10: bytes=32 time<1ms TTL=127` là hai VLAN đã định tuyến và truyền thông dữ liệu thành công!

---

## ⚡ PHƯƠNG PHÁP 2: ĐỊNH TUYẾN TRÊN SWITCH LAYER 3 (MULTILAYER SWITCH)

Nếu bài bài thực hành sử dụng Switch Layer 3 (như dòng 3560 hoặc 3650 trong Cisco Packet Tracer), ta không cần dùng Router ngoài mà bật định tuyến trực tiếp qua các giao diện ảo **SVI (Switch Virtual Interface)**.

### Chuỗi lệnh cấu hình trên Switch Layer 3:

* **Lệnh đầy đủ:**
```text
configure terminal
ip routing

vlan 10
 name KETOAN
exit
vlan 20
 name KYTHUAT
exit

interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
exit

interface FastEthernet0/6
 switchport mode access
 switchport access vlan 20
exit

end
write memory
```

* **Lệnh viết tắt:**
```text
conf t
ip routing

vlan 10
 name KETOAN
ex
vlan 20
 name KYTHUAT
ex

int vlan 10
 ip add 192.168.10.1 255.255.255.0
 no shut
ex

int vlan 20
 ip add 192.168.20.1 255.255.255.0
 no shut
ex

int fa0/1
 sw mo acc
 sw acc vlan 10
ex

int fa0/6
 sw mo acc
 sw acc vlan 20
ex

end
wr
```

*Giải thích câu lệnh mấu chốt:*
- `ip routing`: Lệnh bắt buộc để kích hoạt tính năng định tuyến gói tin giữa các VLAN trên Switch Layer 3.
- `interface vlan 10` & `interface vlan 20`: Đóng vai trò là IP Gateway trực tiếp cho thiết bị ở từng VLAN tương ứng.

---
