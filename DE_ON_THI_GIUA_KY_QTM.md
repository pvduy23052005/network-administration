# 📝 ĐỀ ÔN THI GIỮA KỲ QUẢN TRỊ MẠNG (LINUX & NETWORKING)

**Trường:** Đại học Nông Lâm TP.HCM  
**Môn học:** Quản trị mạng (Mã HP: 214271)  
**Chủ đề:** Lệnh Linux cơ bản, Quản lý User/Group, Shell Scripting, Cấu hình DHCP  

---

## 🔘 PHẦN 1: CÂU HỎI TRẮC NGHIỆM & BÀI TẬP LÝ THUYẾT

### **Câu 1:** Lệnh nào sau đây kiểm tra dung lượng dữ liệu của một **Folder (Thư mục)**?
- A. `du`
- B. `df`
- C. `free`
- D. `top`

> 💡 **Đáp án đúng:** **A. `du`**  
> 🔍 **Giải thích:**
> - `du` (Disk Usage): Kiểm tra dung lượng đĩa sử dụng bởi file hoặc folder.
> - `df` (Disk Free): Kiểm tra dung lượng trống/đã dùng của hệ thống tập tin (File System / Partition).
> - `free`: Xem dung lượng bộ nhớ RAM và Swap.
> - `top`: Hiển thị các tiến trình (process) đang chạy realtime.

---

### **Câu 2:** Phát biểu nào sau đây **ĐÚNG** đối với tên ổ đĩa `/dev/sdc2` trong Linux?
- A. Đây là partition thứ ba của ổ đĩa thứ 2
- B. Đây là partition thứ 2 của ổ đĩa C
- C. Đây là ổ đĩa SCSI
- D. Tất cả đều sai

> 💡 **Đáp án đúng:** **D. Tất cả đều sai**  
> 🔍 **Giải thích:**  
> Quy tắc đặt tên ổ đĩa SCSI/SATA trong Linux:
> - `sd`: Loại ổ đĩa (SCSI / SATA / USB).
> - `c`: Ổ đĩa thứ 3 (`sda` = ổ 1, `sdb` = ổ 2, `sdc` = ổ 3).
> - `2`: Phân vùng (partition) thứ 2.  
> ➡️ Đúng phải là: **Partition thứ 2 của ổ đĩa thứ 3**. Do đó chọn **D**.

---

### **Câu 3:** Lệnh nào sau đây được sử dụng để tạo hệ thống tập tin (File System / Format phân vùng)?
- A. `fdisk`
- B. `mkfs`
- C. `df`
- D. `make`

> 💡 **Đáp án đúng:** **B. `mkfs`**  
> 🔍 **Giải thích:**
> - `mkfs` (Make File System): Dùng để định dạng (format) và tạo hệ thống tập tin (ext4, xfs,...) trên một phân vùng.
> - `fdisk`: Dùng để phân hoạch (chia) ổ đĩa.
> - `df`: Xem dung lượng đĩa.
> - `make`: Dùng để biên dịch chương trình từ mã nguồn C/C++.

---

### **Câu 4:** Cho thông tin phân quyền của một file như sau: `----- 1 iforno 1743 Aug 9:09:44`. Cho biết `user root` và `user iforno` có những quyền gì đối với file này?

> 💡 **Trả lời:**
> - **User `root`:** Có toàn bộ quyền đọc, ghi, thực thi (**r, w, x**). Vì `root` là tài khoản quản trị tối cao trên Linux, bỏ qua hầu hết kiểm tra quyền truy cập thông thường.
> - **User `iforno` (Owner/Chủ sở hữu):** Không có quyền truy cập trực tiếp (**no permissions - `---`**) dựa theo chuỗi phân quyền `-----`, tuy nhiên do là chủ sở hữu (owner), user `iforno` vẫn có quyền thay đổi phân quyền (lệnh `chmod`) cho file này.

---

## 📜 PHẦN 2: BÀI TẬP VIẾT SHELL SCRIPT & CẤU HÌNH HỆ THỐNG

### **Câu 5:** Viết script đặt mật khẩu mặc định của `root` là `1234567` mỗi khi khởi động lại hệ thống?

> 💡 **Giải pháp:**  
> Thêm câu lệnh đổi password tự động vào file cấu hình khởi động `/etc/rc.d/rc.local`.
> 
> ```bash
> echo "1234567" | passwd --stdin root
> ```

---

### **Câu 6:** Viết các bước thực hiện tự động đặt mật khẩu `root` là `1234567` khi boot hệ thống bằng trình biên soạn `nano`?

> 💡 **Các bước thực hiện:**
> 1. Mở file cấu hình khởi động bằng trình biên soạn `nano`:
>    ```bash
>    sudo nano /etc/rc.d/rc.local
>    ```
> 2. Thêm dòng lệnh sau vào cuối file:
>    ```bash
>    echo "1234567" | passwd root --stdin
>    ```
> 3. Lưu file (`Ctrl + O`, `Enter`) và thoát (`Ctrl + X`).
> 4. Phân quyền thực thi cho file `rc.local` (nếu chưa có):
>    ```bash
>    sudo chmod +x /etc/rc.d/rc.local
>    ```

---

### **Câu 7:** Viết Shell Script kiểm tra xem một Group có tồn tại trên hệ thống hay không. Nếu có thì thông báo đã tồn tại, nếu chưa có thì tạo mới Group đó?

> 💡 **Mã nguồn Shell Script (`check_group.sh`):**
> ```bash
> #!/bin/bash
> 
> # Nhập tên nhóm cần kiểm tra
> GROUP_NAME="mygroup"
> 
> # Kiểm tra xem nhóm có tồn tại trong hệ thống hay không
> if getent group "$GROUP_NAME" > /dev/null 2>&1; then
>     echo "Nhóm '$GROUP_NAME' đã tồn tại."
> else
>     # Tạo nhóm mới nếu chưa tồn tại
>     groupadd "$GROUP_NAME"
>     echo "Nhóm '$GROUP_NAME' đã được tạo thành công."
> fi
> ```

---

### **Câu 8:** Viết Shell Script kiểm tra một File có tồn tại hay không. Nếu tồn tại thì in nội dung của File ra màn hình, ngược lại thông báo File không tồn tại?

> 💡 **Mã nguồn Shell Script (`check_file.sh`):**
> ```bash
> #!/bin/bash
> 
> # Nhập tên file cần kiểm tra
> FILE_NAME="yourfile.txt"
> 
> # Kiểm tra sự tồn tại của file bằng toán tử -f
> if [ -f "$FILE_NAME" ]; then
>     echo "File '$FILE_NAME' tồn tại."
>     echo "--- NỘI DUNG FILE ---"
>     cat "$FILE_NAME"
> else
>     echo "File '$FILE_NAME' không tồn tại."
> fi
> ```

---

## 🌐 PHẦN 3: CÂU HỎI LÝ THUYẾT MẠNG & GIAO THỨC DHCP

### **Câu 9:** DHCP là viết tắt của từ gì và nhiệm vụ chính của DHCP là gì?

> 💡 **Trả lời:**
> - **Viết tắt:** **DHCP** = **D**ynamic **H**ost **C**onfiguration **P**rotocol (Giao thức cấu hình động máy chủ).
> - **Nhiệm vụ:** Tự động cấp phát và quản lý địa chỉ IP, Subnet Mask, Default Gateway, DNS Server cho các thiết bị máy tính/điện thoại khi kết nối vào mạng.

---

### **Câu 10:** Một hệ thống mạng có **bắt buộc** phải cần dịch vụ DHCP không? Tại sao?

> 💡 **Trả lời:**
> - **Không bắt buộc.** 
> - **Giải thích:** Quản trị viên hoàn toàn có thể tự gán địa chỉ IP tĩnh (Static IP) thủ công cho từng máy tính/thiết bị trong mạng. Dịch vụ DHCP được sử dụng để tự động hóa việc gán IP, giúp tiết kiệm thời gian, công sức quản trị và tránh trùng lặp IP trong mạng lớn.

---

### **Câu 11:** Trường hợp nào người quản trị cần/nên sử dụng dịch vụ DHCP?
- A. Máy tính cá nhân có nhu cầu truy cập internet
- B. Muốn thay đổi địa chỉ IP cho một mạng nhất định
- C. Muốn thay đổi địa chỉ IP vài máy tính trong hệ thống
- D. Muốn thay đổi địa chỉ IP 1 nhánh mạng trong hệ thống

> 💡 **Đáp án chọn:** **A. Máy tính cá nhân có nhu cầu truy cập internet**  
> 🔍 **Giải thích:** Các thiết bị người dùng cá nhân (laptop, smartphone, PC) truy cập wifi/mạng LAN công cộng hoặc văn phòng cần được tự động cấp IP để vào mạng nhanh chóng mà người dùng không cần tự cấu hình thủ công.
