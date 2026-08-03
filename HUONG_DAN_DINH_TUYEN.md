# 🌐 HƯỚNG DẪN CẤU HÌNH ĐỊNH TUYẾN TĨNH & ĐỊNH TUYẾN ĐỘNG (CISCO IOS CLI)

Tài liệu này hướng dẫn chi tiết từng bước cách cấu hình **Định tuyến tĩnh (Static Routing)** và **Định tuyến động (Dynamic Routing: RIPv2, OSPF, EIGRP)** trên Router Cisco. Mỗi phần đều cung cấp song song **Câu lệnh đầy đủ** và **Câu lệnh viết tắt (Shorthand)** có thể copy trực tiếp vào Cisco Packet Tracer.

---

## 📌 BẢNG TRA CỨU NHANH BẢNG ĐỊNH TUYẾN & THAM SỐ AD

| Loại định tuyến | Ký hiệu trong `show ip route` | Administrative Distance (AD) | Metric tính bằng |
| :--- | :---: | :---: | :--- |
| **Connected (Kết nối trực tiếp)** | `C` | `0` | Không có |
| **Static Route (Định tuyến tĩnh)** | `S` | `1` | Không có |
| **EIGRP** | `D` | `90` | Bandwidth + Delay |
| **OSPF** | `O` | `110` | Cost (Reference Bandwidth / Bandwidth) |
| **RIP** | `R` | `120` | Hop Count (Số router đi qua) |

---

## 1. ĐỊNH TUYẾN TĨNH (STATIC ROUTING)

Định tuyến tĩnh do người quản trị tự cấu hình thủ công từng tuyến đường. Phù hợp cho mạng nhỏ, kết nối điểm-điểm hoặc tuyến mặc định đi ra Internet.

### 1.1. Cấu hình Định tuyến tĩnh IPv4 (Static Route)

#### Cách 1: Trỏ theo địa chỉ IP của Router kế tiếp (Next-Hop IP) - KHUYÊN DÙNG
* **Cú pháp:** `ip route <Địa_chỉ_mạng_đích> <Subnet_Mask> <IP_Next_Hop>`

* **Lệnh đầy đủ:**
```text
configure terminal
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```
* **Lệnh viết tắt:**
```text
conf t
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```
*Giải thích: Đẩy toàn bộ gói tin có đích đến mạng `192.168.2.0/24` sang cổng của Router kế tiếp có IP `10.0.0.2`.*

---

#### Cách 2: Trỏ theo Cổng đầu ra (Exit Interface)
* **Cú pháp:** `ip route <Địa_chỉ_mạng_đích> <Subnet_Mask> <Cổng_đầu_ra>`

* **Lệnh đầy đủ:**
```text
configure terminal
ip route 192.168.2.0 255.255.255.0 Serial0/0/0
```
* **Lệnh viết tắt:**
```text
conf t
ip route 192.168.2.0 255.255.255.0 s0/0/0
```
*Giải thích: Đẩy gói tin sang mạng `192.168.2.0/24` qua cổng `Serial0/0/0` của chính Router hiện tại.*

---

### 1.2. Tuyến đường mặc định IPv4 (Default Route)
Dùng khi Router không biết đường đi cụ thể tới mạng đích (thường trỏ ra ISP/Internet).

* **Lệnh đầy đủ:**
```text
configure terminal
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```
* **Lệnh viết tắt:**
```text
conf t
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```
*Giải thích: `0.0.0.0 0.0.0.0` đại diện cho "bất kỳ mạng đích nào". Gói tin không khớp với bảng định tuyến sẽ được đẩy về `10.0.0.2`.*

---

### 1.3. Định tuyến tĩnh IPv6 (IPv6 Static & Default Route)
*(Lưu ý: Bắt buộc phải chạy lệnh `ipv6 unicast-routing` ở chế độ Global Config trước).*

#### A. Định tuyến tĩnh IPv6 chuẩn:
* **Lệnh đầy đủ:**
```text
configure terminal
ipv6 unicast-routing
ipv6 route 2001:db8:2::/64 2001:db8:a::2
```
* **Lệnh viết tắt:**
```text
conf t
ipv6 uni
ipv6 route 2001:db8:2::/64 2001:db8:a::2
```

#### B. Default Route IPv6 (`::/0`):
* **Lệnh đầy đủ:**
```text
configure terminal
ipv6 route ::/0 2001:db8:a::2
```
* **Lệnh viết tắt:**
```text
conf t
ipv6 route ::/0 2001:db8:a::2
```

---

## 2. ĐỊNH TUYẾN ĐỘNG (DYNAMIC ROUTING)

Định tuyến động giúp các Router tự động trao đổi thông tin mạng với nhau, tự cập nhật khi sơ đồ mạng thay đổi hoặc khi có sự cố đứt cáp.

---

### 2.1. Giao thức RIPv2 (Routing Information Protocol Version 2)
* **Đặc điểm:** Distance-Vector, Metric = Hop Count (tối đa 15 hop), gửi Multicast `224.0.0.9`, cập nhật 30s/lần.
* **Quy tắc quảng bá:** Chỉ quảng bá các **mạng kết nối trực tiếp (Major Classful Network)** với Router.

#### Các bước cấu hình RIPv2:
* **Lệnh đầy đủ:**
```text
configure terminal
router rip
 version 2
 no auto-summary
 network 192.168.1.0
 network 10.0.0.0
 exit
```

* **Lệnh viết tắt:**
```text
conf t
router rip
 ver 2
 no auto
 net 192.168.1.0
 net 10.0.0.0
 ex
```

*Giải thích từng lệnh:*
- `version 2` (viết tắt `ver 2`): Chuyển sang dùng RIPv2 (hỗ trợ Classless và VLSM).
- `no auto-summary` (viết tắt `no auto`): Tắt tính năng tự động gộp mạng về lớp chuẩn Classful.
- `network 192.168.1.0` (viết tắt `net...`): Khai báo dải mạng trực tiếp tham gia định tuyến RIP.

---

### 2.2. Giao thức OSPF (Open Shortest Path First)
* **Đặc điểm:** Link-State, Classless, dùng thuật toán Dijkstra (SPF), Metric = Cost ($10^8 / \text{Bandwidth}$), gửi Multicast `224.0.0.5` / `224.0.0.6`.
* **Quy tắc quảng bá:** Sử dụng **Wildcard Mask** và chỉ định **Area** (`Area 0` là vùng Backbone bắt buộc).

#### A. Cấu hình OSPF đơn vùng (Single-Area OSPF - Area 0):
* **Lệnh đầy đủ:**
```text
configure terminal
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.255.255.255 area 0
 passive-interface GigabitEthernet0/0
 exit
```

* **Lệnh viết tắt:**
```text
conf t
router ospf 1
 router-id 1.1.1.1
 net 192.168.1.0 0.0.0.255 area 0
 net 10.0.0.0 0.255.255.255 area 0
 pas g0/0
 ex
```

*Giải thích từng lệnh:*
- `router ospf 1`: Khởi tạo tiến trình OSPF với Process ID = 1 (số này chỉ có giá trị nội bộ trên Router).
- `router-id 1.1.1.1`: Định danh duy nhất cho Router trong mạng OSPF.
- `network <IP_mạng> <Wildcard_Mask> area <vùng>`: Khai báo mạng và Wildcard Mask tương ứng vào `area 0`.
- `passive-interface g0/0` (viết tắt `pas g0/0`): Vẫn quảng bá mạng của cổng `g0/0` nhưng **không gửi bản tin OSPF Hello** xuống cổng này để tăng bảo mật và giảm lưu lượng rác xuống LAN.

---

#### B. Cấu hình OSPF đa vùng (Multi-Area OSPF):
* **Lệnh đầy đủ:**
```text
configure terminal
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 172.16.1.0 0.0.0.255 area 10
 exit
```
* **Lệnh viết tắt:**
```text
conf t
router ospf 1
 net 192.168.1.0 0.0.0.255 area 0
 net 172.16.1.0 0.0.0.255 area 10
 ex
```

---

### 2.3. Giao thức EIGRP (Enhanced Interior Gateway Routing Protocol)
* **Đặc điểm:** Giao thức lai (Advanced Distance-Vector / Hybrid), thuật toán DUAL, hội tụ cực nhanh, Metric = Bandwidth + Delay, gửi Multicast `224.0.0.10`.
* **Quy tắc quảng bá:** Phải dùng chung số **AS (Autonomous System)** giữa các Router.

#### Các bước cấu hình EIGRP:
* **Lệnh đầy đủ:**
```text
configure terminal
router eigrp 100
 no auto-summary
 network 192.168.1.0 0.0.0.255
 network 10.0.0.0 0.255.255.255
 passive-interface GigabitEthernet0/0
 exit
```

* **Lệnh viết tắt:**
```text
conf t
router eigrp 100
 no auto
 net 192.168.1.0 0.0.0.255
 net 10.0.0.0 0.255.255.255
 pas g0/0
 ex
```

*Giải thích từng lệnh:*
- `router eigrp 100`: Bật EIGRP với Autonomous System (AS) = 100. *(Tất cả các Router muốn bắt tay láng giềng phải có chung số AS 100 này)*.
- `no auto-summary`: Tắt gộp mạng tự động.
- `network <IP_mạng> <Wildcard_Mask>`: Khai báo mạng trực tiếp kèm Wildcard Mask.

---

## 3. CÁC CÂU LỆNH KIỂM TRA & MẸO TROUBLESHOOTING

Sau khi cấu hình định tuyến, hãy sử dụng các lệnh ở chế độ **Privileged EXEC** (dấu nhắc `#`) để kiểm tra:

### 3.1. Xem bảng định tuyến IPv4 (Quan trọng nhất)
* **Lệnh đầy đủ:** `show ip route`
* **Lệnh viết tắt:**
```text
sh ip ro
```
👉 *Kiểm tra xem các mạng từ xa đã xuất hiện trong bảng định tuyến chưa (có ký hiệu `S`, `R`, `O`, hoặc `D` ở đầu dòng).*

---

### 3.2. Xem bảng định tuyến IPv6
* **Lệnh đầy đủ:** `show ipv6 route`
* **Lệnh viết tắt:**
```text
sh ipv6 ro
```

---

### 3.3. Xem thông tin các giao thức định tuyến đang hoạt động
* **Lệnh đầy đủ:** `show ip protocols`
* **Lệnh viết tắt:**
```text
sh ip prot
```
👉 *Dùng kiểm tra số AS của EIGRP, Process ID/Area của OSPF, các mạng đã khai báo trong `network` và passive-interface.*

---

### 3.4. Xem danh sách láng giềng OSPF (OSPF Neighbors)
* **Lệnh đầy đủ:** `show ip ospf neighbor`
* **Lệnh viết tắt:**
```text
sh ip ospf nei
```
👉 *Trạng thái đúng phải là **FULL/DR**, **FULL/BDR** hoặc **FULL/DROTHER**.*

---

### 3.5. Xem danh sách láng giềng EIGRP (EIGRP Neighbors)
* **Lệnh đầy đủ:** `show ip eigrp neighbors`
* **Lệnh viết tắt:**
```text
sh ip eigrp nei
```

---

### 3.6. Xóa và làm tươi (Refresh) lại bảng định tuyến
* **Lệnh đầy đủ:** `clear ip route *`
* **Lệnh viết tắt:**
```text
clear ip ro *
```
👉 *Dùng khi vừa sửa cấu hình định tuyến mà bảng định tuyến chưa kịp cập nhật.*

---
*Chúc bạn thực hành cấu hình định tuyến thành công!*
