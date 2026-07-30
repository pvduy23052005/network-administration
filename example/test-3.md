# 📝 ĐỀ ÔN TẬP TRẮC NGHIỆM MẠNG MÁY TÍNH - TEST 3
**Chủ đề:** Chuyển mạch trong mạng LAN, Cấu hình VLAN, Đường Trunking, Giao thức VTP, Định tuyến Inter-VLAN & Spanning Tree (STP)  
**Số lượng:** 16 câu hỏi trắc nghiệm kèm đáp án và giải thích chi tiết.

---

### **Câu 1:** Thiết bị mạng nào chia nhỏ miền đụng độ (mỗi cổng là 1 Collision Domain) nhưng **KHÔNG** chia nhỏ miền quảng bá (tất cả các cổng thuộc 1 Broadcast Domain khi chưa chia VLAN)?
- A. Hub
- B. Repeater
- C. Switch Layer 2
- D. Router

> 💡 **Đáp án đúng:** **C. Switch Layer 2**  
> 🔍 **Giải thích:** Hub/Repeater thuộc 1 Collision Domain và 1 Broadcast Domain. Switch Layer 2 chia mỗi cổng thành 1 Collision Domain riêng nhưng vẫn nằm chung 1 Broadcast Domain. Router chia mỗi cổng thành 1 Broadcast Domain riêng.

---

### **Câu 2:** Giả sử một sơ đồ mạng gồm: 1 Switch nối với 4 máy tính PC và 1 cổng của Router. Nếu chưa được cấu hình chia VLAN, sơ đồ này có bao nhiêu miền đụng độ (Collision Domain) và bao nhiêu miền quảng bá (Broadcast Domain)?
- A. 5 miền đụng độ, 1 miền quảng bá.
- B. 1 miền đụng độ, 5 miền quảng bá.
- C. 5 miền đụng độ, 5 miền quảng bá.
- D. 1 miền đụng độ, 1 miền quảng bá.

> 💡 **Đáp án đúng:** **A. 5 miền đụng độ, 1 miền quảng bá.**  
> 🔍 **Giải thích:** Switch có 5 cổng hoạt động (4 cổng nối PC + 1 cổng nối Router) ➔ tạo ra **5 Collision Domain**. Do toàn bộ Switch này thuộc 1 mạng LAN vật lý chưa chia VLAN ➔ tạo ra **1 Broadcast Domain**.

---

### **Câu 3:** Lợi ích quan trọng nhất của việc phân chia mạng LAN ảo (VLAN - Virtual LAN) trên Switch là gì?
- A. Tăng tốc độ đường truyền vật lý của cáp xoắn đôi.
- B. Chia nhỏ miền quảng bá (Broadcast Domain) về mặt logic, giúp tăng tính bảo mật, tối ưu hiệu năng và dễ quản lý.
- C. Tự động cấp phát địa chỉ IP tĩnh cho máy tính.
- D. Thay thế hoàn toàn chức năng của Router trên mạng diện rộng.

> 💡 **Đáp án đúng:** **B. Chia nhỏ miền quảng bá (Broadcast Domain) về mặt logic, giúp tăng tính bảo mật, tối ưu hiệu năng và dễ quản lý.**  
> 🔍 **Giải thích:** VLAN cho phép nhóm các máy tính thuộc cùng phòng ban vào 1 miền quảng bá riêng độc lập với vị trí địa lý vật lý, giúp ngăn chặn bão tin quảng bá (Broadcast Storm) và tăng cường bảo mật dữ liệu.

---

### **Câu 4:** Để gán cổng `FastEthernet0/5` vào `VLAN 10` trên Switch Cisco, chuỗi câu lệnh chuẩn là gì?
- A. 
  ```text
  interface fa0/5
  switchport mode trunk
  switchport trunk vlan 10
  ```
- B. 
  ```text
  interface fa0/5
  switchport mode access
  switchport access vlan 10
  ```
- C. 
  ```text
  interface fa0/5
  ip address 192.168.10.1 255.255.255.0
  ```
- D. 
  ```text
  interface fa0/5
  vlan 10 enable
  ```

> 💡 **Đáp án đúng:** **B. `interface fa0/5` ➔ `switchport mode access` ➔ `switchport access vlan 10`**  
> 🔍 **Giải thích:** Cổng nối trực tiếp với thiết bị cuối (PC, máy in) phải đặt ở chế độ `access` và gán vào VLAN tương ứng bằng lệnh `switchport access vlan <VLAN-ID>`.

---

### **Câu 5:** Lệnh nào sau đây ở chế độ Privileged EXEC (dấu nhắc `#`) cho phép hiển thị danh sách tất cả các VLAN hiện có, trạng thái và các cổng được gán trên Switch Cisco?
- A. `show ip interface brief`
- B. `show vlan brief`
- C. `show running-config`
- D. `show mac address-table`

> 💡 **Đáp án đúng:** **B. `show vlan brief`**  
> 🔍 **Giải thích:** Lệnh `show vlan brief` (hoặc `show vlan`) liệt kê ngắn gọn danh sách các VLAN ID, tên VLAN, trạng thái active và danh sách các cổng đang thuộc về từng VLAN đó.

---

### **Câu 6:** Đường liên kết Trunk (Trunk Link) giữa hai thiết bị chuyển mạch Switch có vai trò chính là gì?
- A. Chỉ cho phép các gói tin thuộc VLAN 1 truyền qua.
- B. Truyền tải đồng thời lưu lượng dữ liệu của nhiều VLAN khác nhau qua cùng một đường kết nối vật lý.
- C. Tăng gấp đôi băng thông mạng cho các máy tính cuối.
- D. Tự động mã hóa tất cả dữ liệu người dùng.

> 💡 **Đáp án đúng:** **B. Truyền tải đồng thời lưu lượng dữ liệu của nhiều VLAN khác nhau qua cùng một đường kết nối vật lý.**  
> 🔍 **Giải thích:** Đường Trunk sử dụng cơ chế chèn thêm thẻ VLAN Tag vào khung Ethernet frame để giúp các Switch phân biệt dữ liệu đó thuộc VLAN nào khi truyền qua cùng một liên kết cáp nối.

---

### **Câu 7:** Chuẩn đóng gói đường Trunk quốc tế chuẩn mở **IEEE 802.1Q (Dot1q)** chèn thêm một thẻ (Tag) có độ dài bao nhiêu byte vào khung Ethernet Frame?
- A. 2 byte
- B. 4 byte
- C. 8 byte
- D. 26 byte

> 💡 **Đáp án đúng:** **B. 4 byte**  
> 🔍 **Giải thích:** Chuẩn mở IEEE 802.1Q chèn thêm 4-byte Tag chứa VLAN ID vào giữa Header của Ethernet Frame. Trong khi đó, chuẩn cũ ISL độc quyền của Cisco bọc thêm 26-byte Header và 4-byte Trailer.

---

### **Câu 8:** Câu lệnh nào sau đây được sử dụng để chuyển giao diện `FastEthernet0/24` sang chế độ đường Trunk trên Switch Cisco?
- A. `Switch(config-if)# switchport mode access`
- B. `Switch(config-if)# switchport mode trunk`
- C. `Switch(config-if)# switchport trunk access`
- D. `Switch(config-if)# vlan trunk enable`

> 💡 **Đáp án đúng:** **B. `Switch(config-if)# switchport mode trunk`**  
> 🔍 **Giải thích:** Lệnh `switchport mode trunk` thiết lập cổng hoạt động cố định ở chế độ Trunking để kết nối với Switch khác hoặc kết nối lên Router.

---

### **Câu 9:** Chế độ VTP Server (VTP Server Mode) trên Switch Cisco có đặc điểm hoạt động nào sau đây?
- A. Cho phép tạo, sửa, xóa VLAN; tự động gửi bản tin quảng bá và đồng bộ cấu hình VLAN với các Switch khác trong cùng VTP Domain.
- B. Không cho phép tạo/sửa/xóa VLAN, chỉ nhận thông tin đồng bộ từ Server khác.
- C. Cho phép tạo VLAN cục bộ nhưng không gửi và không nhận thông tin đồng bộ từ VTP Server.
- D. Tự động tắt tất cả các cổng Trunking.

> 💡 **Đáp án đúng:** **A. Cho phép tạo, sửa, xóa VLAN; tự động gửi bản tin quảng bá và đồng bộ cấu hình VLAN với các Switch khác trong cùng VTP Domain.**  
> 🔍 **Giải thích:** VTP Server là chế độ mặc định. Switch ở chế độ Server có toàn quyền quản lý bảng VLAN và đồng bộ danh sách này tới các Switch ở chế độ VTP Client qua các đường Trunk.

---

### **Câu 10:** Điểm đặc biệt của Switch khi chạy ở chế độ **VTP Transparent Mode** là gì?
- A. Tự động đồng bộ toàn bộ cấu hình VLAN từ VTP Server về máy mình.
- B. Cho phép người dùng tạo/sửa/xóa VLAN cục bộ; KHÔNG cập nhật cấu hình từ Server nhưng VẪN chuyển tiếp (forward) các bản tin VTP tới Switch tiếp theo.
- C. Khóa toàn bộ các cổng không cho dữ liệu truyền qua.
- D. Xóa toàn bộ file cấu hình `vlan.dat` khi khởi động lại.

> 💡 **Đáp án đúng:** **B. Cho phép người dùng tạo/sửa/xóa VLAN cục bộ; KHÔNG cập nhật cấu hình từ Server nhưng VẪN chuyển tiếp (forward) các bản tin VTP tới Switch tiếp theo.**  
> 🔍 **Giải thích:** VTP Transparent cho phép Switch hoạt động độc lập về VLAN (không bị đè cấu hình bởi VTP Server) nhưng vẫn chuyển tiếp gói tin VTP để bảo toàn luồng đồng bộ giữa các Switch Client/Server phía sau.

---

### **Câu 11:** Thông tin cấu hình danh sách các VLAN trên Switch Cisco (khi hoạt động ở chế độ VTP Server / Client) được lưu trữ trong tập tin nào trên bộ nhớ Flash?
- A. `config.text`
- B. `startup-config`
- C. `vlan.dat`
- D. `system.ini`

> 💡 **Đáp án đúng:** **C. `vlan.dat`**  
> 🔍 **Giải thích:** Danh sách và cấu hình các VLAN 1 - 1005 được lưu trữ riêng trong tập tin `vlan.dat` trên bộ nhớ Flash. Khi muốn xóa sạch cấu hình VLAN về mặc định, quản trị viên dùng lệnh `delete flash:vlan.dat`.

---

### **Câu 12:** Trong mô hình định tuyến giữa các VLAN kiểu **Router-on-a-Stick**, câu lệnh nào sau đây được gán trên giao diện con (Sub-interface, ví dụ `g0/0.10`) của Router để đóng gói chuẩn IEEE 802.1Q cho VLAN 10?
- A. `Router(config-subif)# encapsulation dot1q 10`
- B. `Router(config-subif)# switchport access vlan 10`
- C. `Router(config-subif)# ip vlan 10`
- D. `Router(config-subif)# vlan encapsulation 10`

> 💡 **Đáp án đúng:** **A. `Router(config-subif)# encapsulation dot1q 10`**  
> 🔍 **Giải thích:** Lệnh `encapsulation dot1q <VLAN-ID>` gán sub-interface của Router chịu trách nhiệm xử lý và đóng gói/mở gói khung dữ liệu cho đúng VLAN-ID tương ứng.

---

### **Câu 13:** Mục đích quan trọng nhất của giao thức Spanning Tree Protocol (STP - chuẩn IEEE 802.1D) trong mạng LAN là gì?
- A. Tăng tốc độ chuyển mạch frame dữ liệu từ 100 Mbps lên 1 Gbps.
- B. Ngăn chặn các vòng lặp dữ liệu ở Tầng 2 (Layer 2 Loops / Broadcast Storm) khi sơ đồ mạng có các liên kết dư thừa (Redundant Links).
- C. Tự động mã hóa mật khẩu trên đường truyền Trunk.
- D. Phân giải địa chỉ IP sang địa chỉ MAC.

> 💡 **Đáp án đúng:** **B. Ngăn chặn các vòng lặp dữ liệu ở Tầng 2 (Layer 2 Loops / Broadcast Storm) khi sơ đồ mạng có các liên kết dư thừa (Redundant Links).**  
> 🔍 **Giải thích:** Khi có sơ đồ nối vòng dư thừa giữa các Switch, gói tin Broadcast sẽ bị lặp vô tận gây bão quảng bá (Broadcast Storm) làm nghẽn mạng. Giao thức STP sẽ tự động tính toán và khóa (Block) các cổng dư thừa để tạo nên một cấu trúc cây không bị lặp.

---

### **Câu 14:** Trong một hệ thống mạng chạy giao thức STP, thiết bị Switch nào được chọn làm thiết bị gốc (Root Bridge) của cây Spanning Tree?
- A. Switch có địa chỉ IP lớn nhất.
- B. Switch có số lượng cổng hoạt động nhiều nhất.
- C. Switch có giá trị Bridge ID (gồm Priority + địa chỉ MAC) nhỏ nhất.
- D. Switch được bật lên đầu tiên trong hệ thống.

> 💡 **Đáp án đúng:** **C. Switch có giá trị Bridge ID (gồm Priority + địa chỉ MAC) nhỏ nhất.**  
> 🔍 **Giải thích:** STP chọn Root Bridge dựa vào Bridge ID (`Bridge Priority` + `MAC Address`). Switch nào có chỉ số Bridge ID **nhỏ nhất** sẽ được chọn làm Root Bridge của toàn bộ hệ thống.

---

### **Câu 15:** Trật tự đúng của 4 trạng thái cổng trong quá trình chuyển đổi của giao thức STP (chuẩn IEEE 802.1D) từ khi khởi tạo đến khi truyền dữ liệu là gì?
- A. Forwarding ➔ Learning ➔ Listening ➔ Blocking
- B. Blocking ➔ Listening ➔ Learning ➔ Forwarding
- C. Listening ➔ Blocking ➔ Forwarding ➔ Learning
- D. Learning ➔ Listening ➔ Blocking ➔ Forwarding

> 💡 **Đáp án đúng:** **B. Blocking ➔ Listening ➔ Learning ➔ Forwarding**  
> 🔍 **Giải thích:** Tiến trình trạng thái cổng của chuẩn STP 802.1D:  
> 1. **Blocking:** Khóa cổng, chỉ nhận bản tin BPDU.  
> 2. **Listening:** Lắng nghe và gửi BPDU để chuẩn bị tính toán cây (15s).  
> 3. **Learning:** Học địa chỉ MAC vào bảng CAM nhưng chưa truyền dữ liệu (15s).  
> 4. **Forwarding:** Truyền và nhận dữ liệu bình thường.

---

### **Câu 16:** Thời gian hội tụ mặc định để một cổng bị khóa (Blocking) chuyển hoàn toàn sang trạng thái truyền dữ liệu (Forwarding) trong chuẩn giao thức STP IEEE 802.1D là bao nhiêu giây?
- A. 15 giây
- B. 30 giây
- C. 50 giây
- D. 120 giây

> 💡 **Đáp án đúng:** **C. 50 giây**  
> 🔍 **Giải thích:** Tổng thời gian hội tụ mặc định của STP 802.1D = `Max Age` (20 giây) + `Forward Delay Listening` (15 giây) + `Forward Delay Learning` (15 giây) = **50 giây**.
