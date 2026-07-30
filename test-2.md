# 📚 ÔN TẬP LÝ THUYẾT MẠNG MÁY TÍNH (CHƯƠNG 2: CÁC KỸ THUẬT ĐỊNH TUYẾN)

---

## 1. KHÁI NIỆM VLSM VÀ PHÂN LOẠI GIAO THỨC ĐỊNH TUYẾN (Câu 1 - 6)

*   **VLSM (Variable Length Subnet Mask):** Mặt nạ mạng con độ dài biến đổi. Kỹ thuật cho phép chia một mạng thành các subnet có kích thước lớn/nhỏ khác nhau tùy theo nhu cầu host, tối ưu hóa không gian địa chỉ IP.
*   **Giao thức Distance - Vector (Khoảng cách - Hướng):**
    *   Định kỳ gửi toàn bộ bảng định tuyến cho các router láng giềng trực tiếp (*Routing by rumor*).
    *   Thuật toán: Bellman-Ford.
    *   Ví dụ: RIP, IGRP.
*   **Giao thức Link - State (Trạng thái liên kết):**
    *   Các router trao đổi bản tin LSA để thu thập toàn bộ sơ đồ mạng (Topology), độc lập tính toán đường đi ngắn nhất bằng thuật toán **Dijkstra (SPF)**.
    *   Chỉ cập nhật khi có sự thay đổi trong mạng (*Triggered update*).
    *   Ví dụ: OSPF, IS-IS.
*   **Giao thức Classful (Theo lớp):**
    *   **Không** gửi kèm Subnet Mask trong bản tin cập nhật định tuyến.
    *   Tự động gộp mạng về lớp chuẩn (Class A, B, C). **Không** hỗ trợ VLSM, CIDR và mạng gián đoạn.
    *   Ví dụ: RIPv1, IGRP.
*   **Giao thức Classless (Không phân lớp):**
    *   **Có** gửi kèm Subnet Mask trong bản tin cập nhật định tuyến.
    *   Hỗ trợ đầy đủ VLSM, CIDR và mạng gián đoạn.
    *   Ví dụ: RIPv2, OSPF, EIGRP, BGP.
*   **Mạng gián đoạn (Discontiguous Network):**
    *   Là mô hình mạng trong đó các mạng con (subnet) thuộc cùng một địa chỉ mạng chính (Major Network, ví dụ `10.0.0.0/8`) bị chia cắt bởi một địa chỉ mạng chính khác (ví dụ `192.168.1.0/24`).
    *   *Ví dụ:* Subnet A (`10.1.0.0/16`) $\rightarrow$ Router 1 $\rightarrow$ Network X (`192.168.1.0/24`) $\rightarrow$ Router 2 $\rightarrow$ Subnet B (`10.2.0.0/16`).

---

## 2. THAM SỐ ĐỊNH NGHĨA TRONG ĐỊNH TUYẾN (Câu 7 - 9)

*   **Hai tham số quan trọng nhất:**
    1.  **Administrative Distance (AD):** Tham số đo lường **độ tin cậy** của các nguồn định tuyến khác nhau (AD càng nhỏ càng ưu tiên).
    2.  **Metric:** Tham số đo lường **độ tối ưu (chi phí)** của các đường đi trong cùng một giao thức định tuyến (Metric càng nhỏ càng ưu tiên).
*   **Giá trị AD mặc định phổ biến:**
    *   Connected (Trực tiếp): `0`
    *   Static Route (Tĩnh): `1`
    *   EIGRP: `90`
    *   OSPF: `110`
    *   RIP: `120`

---

## 3. CÂU LỆNH CẤU HÌNH ĐỊNH TUYẾN TĨNH (STATIC ROUTE) (Câu 10 - 13)

*   **Định tuyến tĩnh IPv4:**
    `Router(config)# ip route <destination-network> <subnet-mask> <next-hop-IP | exit-interface>`
*   **Default Route IPv4 (Tuyến mặc định):**
    `Router(config)# ip route 0.0.0.0 0.0.0.0 <next-hop-IP | exit-interface>`
*   **Định tuyến tĩnh IPv6:**
    `Router(config)# ipv6 route <destination-IPv6-prefix/prefix-length> <next-hop-IPv6 | exit-interface>`
*   **Default Route IPv6:**
    `Router(config)# ipv6 route ::/0 <next-hop-IPv6 | exit-interface>`
    *(Lưu ý: Phải bật lệnh `ipv6 unicast-routing` ở chế độ Global Config trước khi cấu hình).*

---

## 4. GIAO THỨC ĐỊNH TUYẾN RIP VÀ CHỐNG LẶP (Câu 14 - 18)

*   **Đặc điểm giao thức RIP (Routing Information Protocol):**
    *   Là giao thức định tuyến động Distance-Vector.
    *   Cập nhật bảng định tuyến định kỳ **30 giây/lần**.
    *   Khoảng cách tối đa: **15 hop** (16 hop được coi là Unreachable - không thể tới).
*   **Tham số tính Metric của RIP:** Dựa vào **Hop Count** (Số lượng router phải đi qua).
*   **So sánh RIPv1 và RIPv2:**
    *   **RIPv1:** Classful, định kỳ gửi bản tin Broadcast (`255.255.255.255`), không gửi Subnet Mask, không hỗ trợ VLSM, không xác thực.
    *   **RIPv2:** Classless, gửi bản tin Multicast (`224.0.0.9`), có gửi kèm Subnet Mask, hỗ trợ VLSM/CIDR, có xác thực bảo mật.
*   **Hiện tượng lặp định tuyến (Routing Loop):** Tình trạng gói tin bị chuyển tiếp quẩn quanh giữa các router do thông tin bảng định tuyến không đồng bộ kịp khi có đường đi bị hỏng.
*   **Các giải pháp chống lặp của RIP:**
    1.  **Maximum Hop Count:** Giới hạn Hop count tối đa bằng 15.
    2.  **Split Horizon:** Không gửi thông tin tuyến đường ngược lại giao diện mà nó vừa nhận được.
    3.  **Poison Reverse:** Gửi thông tin tuyến đường bị hỏng ngược lại với Metric = 16 để báo mạng đã chết.
    4.  **Holddown Timers:** Đợi một khoảng thời gian (180s) trước khi chấp nhận thông tin đường đi mới kém hơn.
    5.  **Triggered Updates:** Gửi bản tin cập nhật ngay lập tức khi phát hiện sự thay đổi topology.

---

## 5. GIAO THỨC ĐỊNH TUYẾN OSPF (Câu 19 - 22)

*   **Đặc điểm giao thức OSPF (Open Shortest Path First):**
    *   Là giao thức định tuyến động Classless kiểu **Link-State**.
    *   Sử dụng thuật toán **Dijkstra** để tính đường đi ngắn nhất.
    *   Phân chia mạng thành các **Area** (vùng) để giảm bớt kích thước bảng định tuyến.
    *   Dùng địa chỉ Multicast `224.0.0.5` (cho tất cả OSPF Router) và `224.0.0.6` (cho DR/BDR).
*   **Tham số tính Metric của OSPF:** Dựa vào **Cost (Chi phí)**, tính theo băng thông giao diện:
    $$\text{Cost} = \frac{\text{Reference Bandwidth (Mặc định } 10^8 \text{ bps)}}{\text{Bandwidth của Interface}}$$
*   **Ý nghĩa `process-id` (`router ospf <process-id>`):** Mã số nhận diện tiến trình OSPF chạy **nội bộ trên Router** (giá trị 1 - 65535, chỉ có ý nghĩa cục bộ trên router đó, không cần giống nhau giữa các router).
*   **Ý nghĩa `area-id` (`network <address> <wildcard-mask> area <area-id>`):** Mã số vùng mà interface tham gia định tuyến. Các router muốn trao đổi dữ liệu OSPF trực tiếp phải nằm **cùng một `area-id`** (Area 0 là vùng Backbone bắt buộc).

---

## 6. GIAO THỨC ĐỊNH TUYẾN EIGRP (Câu 23 - 25)

*   **Đặc điểm giao thức EIGRP (Enhanced Interior Gateway Routing Protocol):**
    *   Là giao thức định tuyến nâng cao của Cisco kết hợp đặc điểm của Distance-Vector và Link-State (Hybrid).
    *   Sử dụng thuật toán **DUAL (Diffusing Update Algorithm)** để tính đường đi và đảm bảo không bị lặp loop.
    *   Tốc độ hội tụ cực nhanh do có sẵn đường đi dự phòng (*Feasible Successor*).
    *   Dùng địa chỉ Multicast `224.0.0.10`.
*   **Tham số tính Metric của EIGRP:** Dựa vào công thức K-values tổng hợp, mặc định sử dụng **Bandwidth (Băng thông)** và **Delay (Độ trễ)**.
*   **Ý nghĩa `autonomous-system` (`router eigrp <autonomous-system>`):** Số hiệu Hệ thống tự trị (AS number, giá trị 1 - 65535). Các router EIGRP **bắt buộc phải có cùng số AS** thì mới có thể thiết lập quan hệ láng giềng (Neighbor) và trao đổi bảng định tuyến với nhau.

---

## 7. TỔNG HỢP CÂU LỆNH CẤU HÌNH ĐỊNH TUYẾN ĐỘNG (Câu 26)

| Giao thức | Lệnh khởi tạo | Lệnh quảng bá mạng (Network command) |
| :--- | :--- | :--- |
| **RIPv2** | `router rip`<br>`version 2`<br>`no auto-summary` | `network <major-network-address>` |
| **OSPF** | `router ospf <process-id>` | `network <network-address> <wildcard-mask> area <area-id>` |
| **EIGRP** | `router eigrp <AS-number>`<br>`no auto-summary` | `network <network-address> [wildcard-mask]` |
