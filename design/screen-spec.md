# Screen Specifications — EduPlan

Tài liệu này đặc tả chi tiết ý đồ thiết kế và nội dung hiển thị cho toàn bộ 8 màn hình chính của ứng dụng.

---

### SCR-01: Login Screen (Đăng nhập)
* **Thuộc Flow:** Luồng khởi động hệ thống.
* **Mục đích:** Xác thực danh tính sinh viên bằng tài khoản Google trường cấp (phục vụ sẵn cho Lab 3).
* **Nội dung hiển thị:**
  * Logo và slogan của EduPlan ("Lập kế hoạch học tập thông minh").
  * Nút "Đăng nhập với Google" (Touch target lớn 52dp, icon Google chuẩn).
  * Điều khoản sử dụng và cam kết bảo mật dữ liệu sinh viên.

---

### SCR-02: Home Dashboard (Trang chủ)
* **Thuộc Flow:** Flow 1 (Điểm bắt đầu).
* **Mục đích:** Cung cấp thông tin quan trọng nhất trong ngày ngay khi mở app.
* **Nội dung hiển thị:**
  * Lời chào cá nhân hóa + Ngày tháng hiện tại.
  * **Card "Lớp học tiếp theo":** Đếm ngược giờ, Tên môn, Ca học (Slot), Phòng học, Giảng viên.
  * **Khối KPI tín chỉ:** Tiến độ tín chỉ kỳ này (Ví dụ: `15 / 18 Tín chỉ`), tiến độ tích lũy toàn khóa.
  * Lịch học rút gọn của 3 ngày kế tiếp.

---

### SCR-03: Weekly Schedule (Thời khóa biểu tuần)
* **Thuộc Flow:** Flow 1 (Điểm kết thúc) & Flow 2 (Điểm bắt đầu).
* **Mục đích:** Hiển thị trực quan lịch học toàn bộ 7 ngày trong tuần dạng lưới.
* **Nội dung hiển thị:**
  * Thanh chuyển tuần (Tuần 1, Tuần 2... kèm ngày bắt đầu và kết thúc).
  * Lưới thời khóa biểu chia theo ca học: Slot 1 (07:30 - 09:50) đến Slot 6 (17:40 - 20:00).
  * Mỗi ca học hiển thị mã môn, phòng học với màu phân loại theo môn.

---

### SCR-04: Course Catalog (Danh mục môn học)
* **Thuộc Flow:** Flow 1 & Flow 3.
* **Mục đích:** Tra cứu, tìm kiếm và lọc các môn học mở trong học kỳ mới.
* **Nội dung hiển thị:**
  * Thanh tìm kiếm (Search bar) có hỗ trợ tìm theo mã môn (PRM393) hoặc tên môn.
  * Bộ lọc nhanh (Filter chips): Theo khoa (Kỹ thuật phần mềm, An toàn thông tin), Số tín chỉ (3, 4 tín chỉ).
  * Danh sách các Card môn học hiển thị tóm tắt: Mã môn, tên, số tín chỉ, số lớp đang mở.

---

### SCR-05: Plan Builder & Conflict Checker (Xếp lịch & Kiểm tra trùng ca)
* **Thuộc Flow:** Flow 3 (Trọng tâm xử lý lỗi trùng ca).
* **Mục đích:** Không gian thử nghiệm xếp môn, tự động phát hiện và cảnh báo xung đột lịch.
* **Nội dung hiển thị:**
  * Lưới mô phỏng thời khóa biểu dự kiến.
  * Danh sách các môn đã chọn đưa vào kế hoạch.
  * **Conflict Alert Banner/Dialog:** Khi thêm một lớp có ca học trùng với môn đã chọn, hệ thống sẽ hiện popup màu đỏ thông báo rõ môn bị trùng và hiển thị danh sách các ca học khác còn trống để chọn thay thế.

---

### SCR-06: Course Detail (Chi tiết môn học)
* **Thuộc Flow:** Flow 1.
* **Mục đích:** Xem đầy đủ thông tin trước khi quyết định chọn ca học.
* **Nội dung hiển thị:**
  * Tên môn học, mã môn, số tín chỉ, môn tiên quyết bắt buộc.
  * Danh sách các lớp/slot đang mở: Giảng viên phụ trách, thứ trong tuần, giờ học, phòng học.
  * Nút CTA cố định ở đáy màn hình: "Thêm vào Kế hoạch học kỳ".

---

### SCR-07: Semester Summary & Export PDF (Tổng kết & Xuất báo cáo)
* **Thuộc Flow:** Flow 2 (Trọng tâm xuất PDF).
* **Mục đích:** Kiểm tra tổng kết học kỳ và xuất bản file thời khóa biểu.
* **Nội dung hiển thị:**
  * Thẻ tổng kết: Tổng số môn (5 môn), Tổng tín chỉ (15 tín chỉ), Học phí dự kiến.
  * Danh sách chi tiết các môn chính thức đã xếp xong.
  * Nút "Xuất Thời khóa biểu PDF" (Mở xem trước bản in và lưu file vào máy).

---

### SCR-08: Profile & Settings (Cá nhân & Cài đặt)
* **Thuộc Flow:** Quản lý tài khoản.
* **Mục đích:** Quản lý thông tin sinh viên, cấu hình thông báo nhắc học và chuẩn bị cho Lab 3.
* **Nội dung hiển thị:**
  * Avatar Google, Họ tên, Mã số sinh viên, Ngành học, Khóa.
  * Công tắc cài đặt: "Bật nhắc nhở trước buổi học 15 phút" (FCM cho Lab 3).
  * Thông tin phiên bản ứng dụng (Remote Config demo cho Lab 3).
  * Nút "Đăng xuất" (Sign out).