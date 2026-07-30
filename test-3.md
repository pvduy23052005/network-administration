# 📚 ÔN TẬP LÝ THUYẾT MẠNG MÁY TÍNH (CHƯƠNG 3: CHUYỂN MẠCH TRONG MẠNG LAN)

---

## 1. MIỀN ĐỤNG ĐỘ VÀ MIỀN QUẢNG BÁ (Câu 1 - 4)

*   **Miền đụng độ (Collision Domain):**
    *   Là môi trường mạng mà nếu hai thiết bị cùng truyền dữ liệu đồng thời thì tín hiệu sẽ bị va chạm (collision).
    *   **Hub / Repeater:** KHÔNG chia miền đụng độ (tất cả các cổng thuộc **1 Collision Domain**).
    *   **Bridge / Switch / Router:** MỖI CỔNG là **1 Collision Domain** riêng biệt.
*   **Miền quảng bá (Broadcast Domain):**
    *   Là phạm vi mạng mà khi một thiết bị gửi gói tin Broadcast, tất cả thiết bị khác trong phạm vi đó đều nhận được.
    *   **Hub / Bridge / Switch (Layer 2):** KHÔNG chia miền quảng bá (tất cả các cổng thuộc **1 Broadcast Domain**, ngoại trừ khi chia VLAN).
    *   **Router / Switch Layer 3:** MỖI CỔNG là **1 Broadcast Domain** riêng biệt.
*   **Hoạt động của các thiết bị:**
    *   *Hub (Layer 1):* Nhận tín hiệu từ 1 cổng, khuếch đại và phát tất cả các cổng còn lại (Flood).
    *   *Bridge (Layer 2):* Thiết bị 2 cổng, lọc và chuyển tiếp khung dữ liệu dựa vào bảng địa chỉ MAC.
    *   *Switch (Layer 2):* Cầu nối đa cổng (Multi-port Bridge), chuyển mạch tốc độ cao dựa vào bảng địa chỉ MAC (bảng CAM).
*   **Phân tích sơ đồ mạng ở Câu 4:**
    *   **Số miền đụng độ (Collision Domains): 5**
        1. Vùng Hub 1 + Hub 2 + các PC liên quan + Cổng trái Bridge (1 domain).
        2. Liên kết giữa Cổng phải Bridge và Cổng Switch (1 domain).
        3. Cổng Switch nối PC riêng lẻ (1 domain).
        4. Cổng Switch nối Hub 3 + 3 PC (1 domain).
        5. Cổng Switch nối Router (1 domain).
    *   **Số miền quảng bá (Broadcast Domains): 1** (Do toàn bộ hệ thống nối vào 1 cổng Router và chưa chia VLAN).

---

## 2. KHÁI NIỆM VÀ CẤU HÌNH VLAN (VIRTUAL LAN) (Câu 5 - 8)

*   **VLAN (Virtual Local Area Network):** Là kỹ thuật phân chia một Switch vật lý thành nhiều mạng LAN ảo độc lập về mặt logic. Mỗi VLAN tạo thành **1 miền quảng bá (Broadcast Domain)** riêng biệt.
*   **Các lệnh cấu hình VLAN cơ bản:**
    ```cisco
    Switch(config)# vlan 10                   ! Tạo VLAN 10
    Switch(config-vlan)# name TTDL            ! Đặt tên VLAN
    Switch(config-vlan)# exit
    Switch(config)# interface range fa0/1 - 5
    Switch(config-if-range)# switchport mode access            ! Cấu hình chế độ Access
    Switch(config-if-range)# switchport access vlan 10         ! Gán cổng vào VLAN 10
    ```
*   **Lệnh `show vlan` (hoặc `show vlan brief`):** Hiển thị danh sách các VLAN hiện có, trạng thái hoạt động (active) và danh sách các cổng gán vào từng VLAN.
*   **Cấu hình sơ đồ Câu 8:**
    ```cisco
    Switch(config)# vlan 10
    Switch(config-vlan)# exit
    Switch(config)# vlan 20
    Switch(config-vlan)# exit
    Switch(config)# vlan 30
    Switch(config-vlan)# exit

    Switch(config)# interface range fa0/1 - 5
    Switch(config-if-range)# switchport mode access
    Switch(config-if-range)# switchport access vlan 10
    Switch(config-if-range)# exit

    Switch(config)# interface range fa0/6 - 8
    Switch(config-if-range)# switchport mode access
    Switch(config-if-range)# switchport access vlan 20
    Switch(config-if-range)# exit

    Switch(config)# interface range fa0/9 - 11
    Switch(config-if-range)# switchport mode access
    Switch(config-if-range)# switchport access vlan 30
    ```

---

## 3. ĐƯỜNG TRUNK VÀ GIAO THỨC ĐÓNG GÓI (Câu 9 - 12)

*   **Đường Trunk (Trunk Link):** Đường kết nối vật lý (thường giữa Switch-Switch hoặc Switch-Router) truyền tải lưu lượng dữ liệu của **nhiều VLAN khác nhau** qua cùng một liên kết.
*   **Giao thức đóng gói đường Trunk:**
    *   **IEEE 802.1Q (Dot1q):** Chuẩn mở quốc tế, chèn 4-byte Tag chứa VLAN ID vào Ethernet frame.
    *   **ISL (Inter-Switch Link):** Chuẩn độc quyền cũ của Cisco, bọc khung dữ liệu với header 26-byte và trailer 4-byte.
*   **Các lệnh cấu hình đường Trunk:**
    ```cisco
    Switch(config)# interface fa0/1
    Switch(config-if)# switchport trunk encapsulation dot1q   ! (Nếu switch hỗ trợ nhiều chuẩn encap)
    Switch(config-if)# switchport mode trunk                   ! Đặt cổng ở chế độ Trunk
    ```
*   **Cấu hình sơ đồ Câu 12 (trên SW1 cổng Fa0/1 và SW2 cổng Fa0/2):**
    ```cisco
    SW1(config)# interface fa0/1
    SW1(config-if)# switchport mode trunk

    SW2(config)# interface fa0/2
    SW2(config-if)# switchport mode trunk
    ```

---

## 4. GIAO THỨC VTP (VLAN TRUNKING PROTOCOL) (Câu 13 - 15)

*   **Hoạt động của VTP:** Giao thức tầng 2 độc quyền Cisco giúp tự động đồng bộ cấu hình VLAN (tạo, xóa, đổi tên) giữa các Switch thuộc cùng một **VTP Domain** qua đường Trunk.
*   **Các chế độ hoạt động của VTP (VTP Modes):**
    1.  **Server Mode (Mặc định):** Cho phép tạo/xóa/sửa VLAN. Gửi và đồng bộ thông tin VLAN tới các Switch khác. Cấu hình được lưu trong file `vlan.dat`.
    2.  **Client Mode:** KHÔNG cho phép tạo/xóa/sửa VLAN. Nhận và cập nhật thông tin VLAN từ Server.
    3.  **Transparent Mode:** Cho phép tạo/xóa/sửa VLAN cục bộ. KHÔNG cập nhật cấu hình từ Server, chỉ **chuyển tiếp** bản tin VTP tới các Switch tiếp theo.
*   **Lệnh kiểm tra:** `show vlan brief` (kiểm tra VLAN), `show vtp status` (kiểm tra trạng thái VTP).
*   **Cấu hình sơ đồ Câu 15 (VTP Domain "KHCN", SW2 làm Server, SW1 làm Client):**
    *   *Trên SW2 (Server):*
        ```cisco
        SW2(config)# vtp domain KHCN
        SW2(config)# vtp mode server
        SW2(config)# interface fa0/2
        SW2(config-if)# switchport mode trunk
        SW2(config)# vlan 10
        SW2(config-vlan)# name TTDL
        SW2(config)# vlan 20
        SW2(config-vlan)# name TTHC
        SW2(config)# vlan 30
        SW2(config-vlan)# name TTTH
        ```
    *   *Trên SW1 (Client):*
        ```cisco
        SW1(config)# vtp domain KHCN
        SW1(config)# vtp mode client
        SW1(config)# interface fa0/1
        SW1(config-if)# switchport mode trunk
        ```

---

## 5. ĐỊNH TUYẾN GIỮA CÁC VLAN (INTER-VLAN ROUTING) (Câu 16, 19)

*   **Các thiết bị thực hiện định tuyến Inter-VLAN:**
    1.  **Router:** Sử dụng kỹ thuật **Router-on-a-Stick** (chia 1 cổng vật lý thành các sub-interface tương ứng với từng VLAN).
    2.  **Switch Layer 3 (Multilayer Switch):** Sử dụng các giao diện ảo **SVI (Switch Virtual Interface - `interface vlan <id>`)** kết hợp bật lệnh `ip routing`.
*   **Cấu hình Router-on-a-Stick trên Router R1 (Cho sơ đồ Câu 19):**
    ```cisco
    R1(config)# interface g0/0/0
    R1(config-if)# no shutdown
    R1(config-if)# exit

    ! Sub-interface cho VLAN 10
    R1(config)# interface g0/0/0.10
    R1(config-subif)# encapsulation dot1Q 10
    R1(config-subif)# ip address 192.168.1.254 255.255.255.0

    ! Sub-interface cho VLAN 20
    R1(config)# interface g0/0/0.20
    R1(config-subif)# encapsulation dot1Q 20
    R1(config-subif)# ip address 192.168.2.254 255.255.255.0

    ! Sub-interface cho VLAN 30
    R1(config)# interface g0/0/0.30
    R1(config-subif)# encapsulation dot1Q 30
    R1(config-subif)# ip address 192.168.3.254 255.255.255.0
    ```

---

## 6. GIAO THỨC SPANNING TREE PROTOCOL (STP) (Câu 17 - 18)

*   **Mục đích của STP (IEEE 802.1D):** Ngăn chặn hiện tượng **lặp switching loop** (gây ra bão quảng bá Broadcast Storm, trùng lặp khung tin, không ổn định bảng MAC) trong sơ đồ mạng Switch có đường truyền dự phòng.
*   **Quá trình bầu chọn Root Switch (Root Bridge):**
    *   Các Switch trao đổi bản tin BPDU chứa giá trị **Bridge ID (BID)**.
    *   Công thức: **$\text{BID} = \text{Bridge Priority} + \text{MAC Address}$**.
    *   Switch có giá trị **BID NHỎ NHẤT** sẽ được bầu làm **Root Switch**.
    *   *(Nếu Bridge Priority bằng nhau, Switch có địa chỉ MAC nhỏ hơn sẽ thắng)*.
*   **Ví dụ minh họa:**
    *   Switch 1: Priority `32768`, MAC `0001.43A0.1111`
    *   Switch 2: Priority `32768`, MAC `0001.43A0.2222`
    *   $\rightarrow$ **Switch 1** có MAC nhỏ hơn $\rightarrow$ Switch 1 trở thành **Root Switch**.
