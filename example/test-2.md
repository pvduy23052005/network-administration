# 📝 ĐỀ ÔN TẬP TRẮC NGHIỆM MẠNG MÁY TÍNH - TEST 2
**Chủ đề:** Kỹ thuật chia mạng VLSM, Định tuyến tĩnh (Static Route), Giao thức định tuyến RIP, OSPF & EIGRP  
**Số lượng:** 17 câu hỏi trắc nghiệm kèm đáp án và giải thích chi tiết.

---

### **Câu 1:** Kỹ thuật VLSM (Variable Length Subnet Mask) mang lại ưu điểm nổi bật nào nhất trong thiết kế và quản trị địa chỉ IP?
- A. Tự động mã hóa gói tin dữ liệu trên đường truyền.
- B. Cho phép chia một mạng lớn thành các subnet có độ dài mặt nạ khác nhau, tránh lãng phí không gian địa chỉ IP.
- C. Tự động phát hiện và loại bỏ các vòng lặp định tuyến (Routing Loops).
- D. Giúp thiết bị chuyển mạch (Switch) xử lý khung dữ liệu nhanh hơn.

> 💡 **Đáp án đúng:** **B. Cho phép chia một mạng lớn thành các subnet có độ dài mặt nạ khác nhau, tránh lãng phí không gian địa chỉ IP.**  
> 🔍 **Giải thích:** VLSM cho phép linh hoạt sử dụng các Subnet Mask khác nhau (ví dụ `/24`, `/29`, `/30`) trong cùng một mạng chính, cấp vừa đủ số lượng IP cho từng nhánh mạng để tránh lãng phí địa chỉ IP.

---

### **Câu 2:** Giao thức định tuyến Classful (Theo lớp) có đặc điểm nào sau đây?
- A. Có gửi kèm Subnet Mask trong các bản tin cập nhật định tuyến.
- B. Hỗ trợ đầy đủ kỹ thuật VLSM và CIDR.
- C. KHÔNG gửi kèm Subnet Mask trong các bản tin cập nhật định tuyến.
- D. Sử dụng địa chỉ Multicast để gửi các bản tin cập nhật.

> 💡 **Đáp án đúng:** **C. KHÔNG gửi kèm Subnet Mask trong các bản tin cập nhật định tuyến.**  
> 🔍 **Giải thích:** Các giao thức Classful (như RIPv1, IGRP) không gửi thông tin Subnet Mask khi cập nhật định tuyến. Do đó, chúng tự động quy về mask chuẩn của Class A, B, C và không hỗ trợ VLSM hay mạng gián đoạn (Discontiguous network).

---

### **Câu 3:** Giao thức định tuyến Link-State (như OSPF) sử dụng thuật toán nào để tính toán sơ đồ mạng và tìm ra đường đi ngắn nhất đến đích?
- A. Thuật toán Bellman-Ford
- B. Thuật toán Dijkstra (SPF - Shortest Path First)
- C. Thuật toán DUAL (Diffusing Update Algorithm)
- D. Thuật toán Spanning Tree

> 💡 **Đáp án đúng:** **B. Thuật toán Dijkstra (SPF - Shortest Path First)**  
> 🔍 **Giải thích:** OSPF là giao thức Link-State, sử dụng thuật toán Dijkstra để độc lập tính toán cây đường đi ngắn nhất từ router hiện tại đến tất cả các mạng trong hệ thống. Bellman-Ford thuộc về Distance-Vector (RIP), DUAL thuộc về EIGRP.

---

### **Câu 4:** Tham số Administrative Distance (AD) trong bảng định tuyến của Router có ý nghĩa là gì?
- A. Đo lường tốc độ đường truyền vật lý của giao diện.
- B. Đo lường độ tin cậy của nguồn thông tin định tuyến (giá trị AD càng nhỏ càng ưu tiên).
- C. Số lượng Router tối đa mà gói tin có thể đi qua.
- D. Thời gian trễ của gói tin khi truyền qua mạng.

> 💡 **Đáp án đúng:** **B. Đo lường độ tin cậy của nguồn thông tin định tuyến (giá trị AD càng nhỏ càng ưu tiên).**  
> 🔍 **Giải thích:** AD (Administrative Distance) định nghĩa mức độ ưu tiên/độ tin cậy của các nguồn định tuyến khác nhau. Ví dụ: Connected (0) > Static Route (1) > EIGRP (90) > OSPF (110) > RIP (120).

---

### **Câu 5:** Giá trị Administrative Distance (AD) mặc định của một tuyến đường định tuyến tĩnh (Static Route) là bao nhiêu?
- A. 0
- B. 1
- C. 90
- D. 110

> 💡 **Đáp án đúng:** **B. 1**  
> 🔍 **Giải thích:** Mạng kết nối trực tiếp (Directly Connected) có AD = 0. Tuyến đường tĩnh (Static Route) được cấu hình thủ công bởi người quản trị có giá trị AD mặc định = 1.

---

### **Câu 6:** Câu lệnh nào sau đây cấu hình một đường mặc định (Default Route) IPv4 trỏ tới địa chỉ IP Next-Hop `10.0.0.2` trên Router Cisco?
- A. `ip route 255.255.255.255 255.255.255.255 10.0.0.2`
- B. `ip route 0.0.0.0 0.0.0.0 10.0.0.2`
- C. `ip default-gateway 10.0.0.2`
- D. `router rip 0.0.0.0 10.0.0.2`

> 💡 **Đáp án đúng:** **B. `ip route 0.0.0.0 0.0.0.0 10.0.0.2`**  
> 🔍 **Giải thích:** Cấu trúc lệnh Default Route IPv4: `ip route 0.0.0.0 0.0.0.0 <Next-Hop-IP / Exit-Interface>`. Địa chỉ `0.0.0.0 0.0.0.0` đại diện cho tất cả các mạng đích không có trong bảng định tuyến.

---

### **Câu 7:** Để cấu hình một Default Route cho giao thức IPv6, cú pháp lệnh chuẩn là gì?
- A. `ipv6 route 0.0.0.0/0 <next-hop-ip>`
- B. `ipv6 route ::/0 <next-hop-ip>`
- C. `ipv6 route default <next-hop-ip>`
- D. `ipv6 route *:* <next-hop-ip>`

> 💡 **Đáp án đúng:** **B. `ipv6 route ::/0 <next-hop-ip>`**  
> 🔍 **Giải thích:** Ký hiệu `::/0` trong IPv6 tương đương với `0.0.0.0 0.0.0.0` trong IPv4, đại diện cho tuyến đường mặc định tới mọi đích IPv6.

---

### **Câu 8:** Giao thức định tuyến RIP (Routing Information Protocol) sử dụng thông số nào làm Metric để đánh giá chất lượng đường đi?
- A. Băng thông (Bandwidth)
- B. Độ trễ (Delay)
- C. Số lượng Router đi qua (Hop Count)
- D. Chi phí Cost

> 💡 **Đáp án đúng:** **C. Số lượng Router đi qua (Hop Count)**  
> 🔍 **Giải thích:** Metric của RIP dựa hoàn toàn vào Hop Count (mỗi router đi qua tính là 1 hop). Tuyến đường có số lượng hop nhỏ hơn sẽ được chọn vào bảng định tuyến.

---

### **Câu 9:** Giới hạn số lượng Hop Count tối đa được chấp nhận trong giao thức định tuyến RIP là bao nhiêu?
- A. 10 hop
- B. 15 hop
- C. 16 hop
- D. 255 hop

> 💡 **Đáp án đúng:** **B. 15 hop**  
> 🔍 **Giải thích:** RIP giới hạn tối đa là 15 hop. Đến hop thứ 16, RIP coi tuyến đường đó là **Unreachable** (Không thể tới) để phòng ngừa lặp định tuyến.

---

### **Câu 10:** Sự nâng cấp quan trọng nhất của **RIPv2** so với **RIPv1** là gì?
- A. RIPv2 sử dụng thuật toán Dijkstra thay vì Bellman-Ford.
- B. RIPv2 hỗ trợ Classless (gửi kèm Subnet Mask trong bản tin), hỗ trợ VLSM và gửi bản tin Multicast `224.0.0.9`.
- C. RIPv2 tăng giới hạn Hop Count lên đến 255 hop.
- D. RIPv2 không cần gửi bản tin cập nhật định kỳ.

> 💡 **Đáp án đúng:** **B. RIPv2 hỗ trợ Classless (gửi kèm Subnet Mask trong bản tin), hỗ trợ VLSM và gửi bản tin Multicast `224.0.0.9`.**  
> 🔍 **Giải thích:** RIPv1 là Classful (gửi Broadcast `255.255.255.255`, không gửi mask). RIPv2 là Classless (gửi Multicast `224.0.0.9`, có gửi kèm Subnet Mask, hỗ trợ VLSM và bảo mật MD5).

---

### **Câu 11:** Nguyên tắc hoạt động của cơ chế chống lặp **Split Horizon** trong định tuyến Distance-Vector là gì?
- A. Đợi 180 giây trước khi chấp nhận thông tin đường đi mới.
- B. Không gửi lại thông tin về một tuyến đường ra chính cổng (interface) mà Router vừa nhận được thông tin đó.
- C. Gán ngay Metric = 16 khi phát hiện tuyến đường bị hỏng.
- D. Tự động gửi bản tin cập nhật ngay khi sơ đồ mạng thay đổi.

> 💡 **Đáp án đúng:** **B. Không gửi lại thông tin về một tuyến đường ra chính cổng (interface) mà Router vừa nhận được thông tin đó.**  
> 🔍 **Giải thích:** Split Horizon ngăn việc Router quảng bá ngược lại thông tin tuyến đường tới router vừa cấp cho nó, từ đó triệt tiêu các vòng lặp đơn giản giữa 2 router láng giềng.

---

### **Câu 12:** Giao thức OSPF gửi các bản tin cập nhật định tuyến tới địa chỉ Multicast mặc định nào cho tất cả các OSPF Router?
- A. `224.0.0.9`
- B. `224.0.0.5`
- C. `224.0.0.6`
- D. `224.0.0.10`

> 💡 **Đáp án đúng:** **B. `224.0.0.5`**  
> 🔍 **Giải thích:** Địa chỉ `224.0.0.5` (All OSPF Routers) dùng cho tất cả Router chạy OSPF. Địa chỉ `224.0.0.6` dùng để giao tiếp với DR/BDR. (`224.0.0.9` của RIPv2, `224.0.0.10` của EIGRP).

---

### **Câu 13:** Giá trị Metric (Cost) của giao thức OSPF trên một giao diện được tính toán dựa trên công thức nào?
- A. $\text{Cost} = \text{Hop Count}$
- B. $\text{Cost} = \frac{\text{Reference Bandwidth (mặc định } 10^8 \text{ bps)}}{\text{Bandwidth của Interface (bps)}}$
- C. $\text{Cost} = \text{Bandwidth} + \text{Delay}$
- D. $\text{Cost} = \text{Administrative Distance} \times 10$

> 💡 **Đáp án đúng:** **B. $\text{Cost} = \frac{\text{Reference Bandwidth (mặc định } 10^8 \text{ bps)}}{\text{Bandwidth của Interface (bps)}}$**  
> 🔍 **Giải thích:** OSPF tính Cost nghịch đảo với băng thông interface. Băng thông càng lớn thì giá trị Cost càng nhỏ ➔ Đường đi càng được ưu tiên.

---

### **Câu 14:** Trong câu lệnh khai báo OSPF `Router(config)# router ospf 10`, con số `10` đại diện cho thông số gì?
- A. Số hiệu Autonomous System (AS).
- B. Giá trị `process-id` đại diện cho tiến trình OSPF nội bộ trên Router.
- C. Mã vùng `area-id`.
- D. Giá trị Administrative Distance (AD).

> 💡 **Đáp án đúng:** **B. Giá trị `process-id` đại diện cho tiến trình OSPF nội bộ trên Router.**  
> 🔍 **Giải thích:** `process-id` trong OSPF chỉ có ý nghĩa cục bộ trên chính router đó. Các router láng giềng chạy OSPF không nhất thiết phải có chung `process-id`.

---

### **Câu 15:** Trong mô hình định tuyến OSPF đa vùng (Multi-area OSPF), vùng nào bắt buộc phải có và đóng vai trò là vùng trung tâm (Backbone Area)?
- A. Area 1
- B. Area 0
- C. Area 100
- D. Area 999

> 💡 **Đáp án đúng:** **B. Area 0**  
> 🔍 **Giải thích:** Area 0 (Backbone Area) là vùng trung tâm bắt buộc. Tất cả các Area khác trong OSPF đa vùng đều phải kết nối trực tiếp vào Area 0 để luân chuyển dữ liệu định tuyến liên vùng.

---

### **Câu 16:** Giao thức định tuyến EIGRP (Enhanced Interior Gateway Routing Protocol) sử dụng thuật toán nào để tính toán đường đi không bị lặp loop và hội tụ cực nhanh?
- A. Dijkstra
- B. Bellman-Ford
- C. DUAL (Diffusing Update Algorithm)
- D. Spanning Tree Algorithm

> 💡 **Đáp án đúng:** **C. DUAL (Diffusing Update Algorithm)**  
> 🔍 **Giải thích:** DUAL là thuật toán độc quyền của EIGRP, giúp tìm đường đi tối ưu (Successor) và chuẩn bị sẵn đường đi dự phòng (Feasible Successor). Khi đường chính bị lỗi, EIGRP chuyển sang đường dự phòng ngay lập tức không cần tính toán lại.

---

### **Câu 17:** Để hai Router chạy giao thức EIGRP có thể thiết lập quan hệ láng giềng (Neighbor) và trao đổi bảng định tuyến với nhau, thông số nào sau đây **BẮT BUỘC** phải trùng khớp?
- A. Process ID
- B. Số hiệu Autonomous System (AS Number)
- C. Giá trị Hostname
- D. Địa chỉ MAC của cổng kết nối

> 💡 **Đáp án đúng:** **B. Số hiệu Autonomous System (AS Number)**  
> 🔍 **Giải thích:** Trong lệnh `router eigrp <AS-Number>`, chỉ số AS bắt buộc phải giống nhau giữa tất cả các router trong cùng miền định tuyến EIGRP thì chúng mới chịu kết nối láng giềng.
