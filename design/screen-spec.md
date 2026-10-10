# Screen Specifications — EduPlan (DoodlePad Edition)

Tài liệu này đặc tả chi tiết ý đồ thiết kế, nội dung hiển thị và luồng tương tác của toàn bộ 9 màn hình trong ứng dụng **EduPlan**, bám sát hệ thống thiết kế **DoodlePad** (nền kem ấm `#F5EEDB`, thẻ trắng viền nét đứt `#D8CFBF`, typography Inter tối giản thông tin).

---

### SCR-01: Login Screen (Đăng Nhập)
* **Thuộc Flow:** Khởi động ứng dụng / Xác thực tài khoản.
* **Ý đồ thiết kế:** Bố cục căn giữa (Hero Centered Layout) tối giản tuyệt đối, loại bỏ toàn bộ dữ liệu giả và chữ thừa để tập trung duy nhất vào hành động đăng nhập bằng Google Mail trường cấp.
* **Nội dung hiển thị:**
  * Logo nhận diện: Biểu tượng sổ tay học tập (Study Notebook) có chấm tròn xanh ở góc phải.
  * Tên thương hiệu: **EduPlan** kèm slogan ngắn gọn *"Lên lịch học thật dễ!"*.
  * Nút hành động chính: Nút nền trắng có viền nét đứt (chiều cao 52dp) mang logo Google đa màu và dòng chữ **"Đăng nhập bằng Google"**.
  * Chú thích chân trang: Dòng chữ tối giản *"Dành cho sinh viên hệ tín chỉ"*.
* **Tương tác chính:** Nhấn nút Google Sign-In $\rightarrow$ Chuyển sang `SCR-02 Home`.

---

### SCR-02: Home Dashboard (Trang Chủ)
* **Thuộc Flow:** Flow 1 (Điểm bắt đầu).
* **Ý đồ thiết kế:** Màn hình tổng quan thông tin đầu ngày, cung cấp ngay phòng học và thời gian ca học kế tiếp trong 2 giây mà không cần thao tác cuộn phức tạp.
* **Nội dung hiển thị:**
  * Top App Bar: Logo EduPlan + Tiêu đề phụ *"Trang Chủ"*, chuông thông báo, avatar sinh viên Long.
  * Lời chào cá nhân hóa: *"Chào buổi sáng ✨ Hoàng Long"* kèm ngày học hiện tại.
  * Thẻ Hero "Lớp tiếp theo" (Nổi bật nhất): Tag xanh *"Lớp tiếp theo"*, tên môn **Lập trình Di động (3 TC)**, giờ học và phòng **09:30 - 11:50 • Phòng BE-302**, nút hành động nhanh **"Vào lớp"**.
  * Danh mục Lịch học sắp tới: Thẻ rút gọn các môn kế tiếp (Kiến trúc Phần mềm, Hệ quản trị CSDL) kèm nút xem nhanh *"Điểm danh"* và *"Sơ đồ phòng"*.
  * Thanh điều hướng đáy: Bottom Navigation Bar 4 tab (Tab *Trang chủ* kích hoạt).
* **Tương tác chính:** Chạm vào thẻ Lập trình Di động $\rightarrow$ Chuyển đến `SCR-05 Course Detail`.

---

### SCR-03: Weekly Schedule (Thời Khóa Biểu Tuần)
* **Thuộc Flow:** Flow 2 (Điểm bắt đầu tra cứu lịch tuần).
* **Ý đồ thiết kế:** Thời khóa biểu trực quan theo dòng thời gian (Timeline). Đồng bộ toàn bộ thẻ ca học bằng màu trắng viền nét đứt trung tính, chỉ nhấn viền xanh cho ca học đang diễn ra để tránh rối mắt.
* **Nội dung hiển thị:**
  * Top App Bar: Logo EduPlan + Tiêu đề phụ *"Lịch Học"*, chuông thông báo, avatar sinh viên.
  * Thanh chọn tuần: Cụm điều hướng `< Tháng 10, 2024 (Tuần 8) >` kèm nút badge vàng *"Hôm nay"*.
  * Dải chọn ngày (7-day Strip): Các pill từ Thứ Hai (21) đến Chủ Nhật (27), ngày Thứ Tư (23) đang chọn được tô nền xanh `#60A5FA`.
  * Danh sách ca học theo dòng thời gian:
    * Ca 1 (07:30 - 09:50): **Toán Rời Rạc** (Phòng BE-201 • Thầy Nam) kèm nhãn xanh *"Đang học"*.
    * Ca 2 (09:30 - 11:50): **Lập trình Di động** (Phòng BE-302 • Cô Linh) kèm nhãn *"Ca tiếp"*.
    * Ca trống: Khung nét đứt *"Tự học (12:30 - 14:50)"*.
    * Ca 4 (15:00 - 17:20): **Mạng Máy Tính** (Phòng LAB-04 • Thầy Tuấn).
  * Thanh điều hướng đáy: 4 tab (Tab *Lịch học* kích hoạt).
* **Tương tác chính:** Vuốt ngang đổi ngày; bấm nút "Hôm nay" để quay về ca học tức thì.

---

### SCR-04: Course Catalog (Tìm & Danh Mục Môn Học)
* **Thuộc Flow:** Flow 1 (Tìm kiếm môn học).
* **Ý đồ thiết kế:** Không gian tra cứu môn học mở trong kỳ với thanh tìm kiếm bo tròn và danh sách thẻ môn tối giản, loại bỏ các đoạn mô tả dài dòng.
* **Nội dung hiển thị:**
  * Top App Bar: Logo EduPlan + Tiêu đề phụ *"Tìm Môn"*, chuông thông báo, avatar sinh viên.
  * Thanh tìm kiếm: Ô nhập liệu bo góc viền nét đứt *"Tìm mã môn hoặc tên môn..."*.
  * Bộ lọc danh mục (Filter Chips): 3 chip nhỏ *"Tất cả"* (đang chọn), *"Chuyên ngành"*, *"Cơ sở"*.
  * Danh sách thẻ môn học (PRM393, SWP391, OSG209, CSD201, PRN211, MAS291): Mỗi thẻ chỉ gồm Mã môn/Tín chỉ, Tên môn học, và nút bấm kích thước lớn **"Xem lớp (4)"** hoặc **"+ Chọn"**.
  * Thanh điều hướng đáy: 4 tab (Tab *Tìm môn* kích hoạt).
* **Tương tác chính:** Nhập tìm kiếm môn $\rightarrow$ Danh sách lọc thời gian thực; Chạm vào môn PRM393 $\rightarrow$ Chuyển sang `SCR-05 Course Detail`.

---

### SCR-05: Course Detail (Chi Tiết Môn Học)
* **Thuộc Flow:** Flow 1 (Xem lớp mở và chọn ca học).
* **Ý đồ thiết kế:** Màn hình cấp 2 tập trung hỗ trợ sinh viên đối chiếu thông tin giảng viên, giờ học và chọn lớp học phần phù hợp mà không bị phân tâm bởi thanh Bottom Bar.
* **Nội dung hiển thị:**
  * Top App Bar: Nút quay lại `←`, Logo EduPlan + Tiêu đề *"Chi Tiết Môn"*, nút ghim bookmark và avatar.
  * Khối thông tin môn: Tiêu đề **Lập trình Di động (PRM393)**, badge *"3 Tín chỉ"*, tag xanh lá *"Tiên quyết: Đạt ✅"*, mô tả ngắn gọn 2 dòng về kiến thức cốt lõi.
  * Danh sách lớp học phần đang mở (Chọn lớp mở 3 lớp):
    * Lớp SE1801 (Ca 2 T3, T6 • 09:15 - 11:45 • Phòng BE-302 • GV: ThS. Nguyễn Văn A) - *Trạng thái đã chọn (Radio checked)*.
    * Lớp SE1802 (Ca 4 T2, T5 • 15:00 - 17:30 • Phòng BE-305 • GV: TS. Lê Văn C).
    * Lớp SE1803 (Ca 1 T3, T6 • 07:00 - 09:15 • Phòng AL-102 • GV: ThS. Trần D).
  * Chân trang cố định (Sticky Bottom Bar): Nút icon yêu thích + Nút chính **"Thêm vào lịch học"** (Nền xanh Sky Blue, chiều cao 52dp).
* **Tương tác chính:** Chọn radio lớp SE1801 $\rightarrow$ Bấm "Thêm vào lịch học" $\rightarrow$ Chuyển hướng sang `SCR-06A Plan Builder Grid`.

---

### SCR-06A: Plan Builder - Timetable Grid (Xếp Lịch Học Thử - Lưới Tuần)
* **Thuộc Flow:** Flow 3 (Phát hiện xung đột trùng lịch học).
* **Ý đồ thiết kế:** Màn hình xếp lịch chuyên biệt, dành tối đa diện tích hiển thị lưới ma trận thời khóa biểu to rõ để mắt người nhìn thấy ngay ca học bị trùng trong 1 giây.
* **Nội dung hiển thị:**
  * Top App Bar: Nút quay lại `←`, Logo EduPlan + Tiêu đề *"Xếp Lịch Học Thử"*, chuông thông báo, avatar.
  * Banner cảnh báo trùng lịch (Màu đỏ nổi bật): Icon ⚠️ + Tiêu đề đỏ *"Trùng ca 2 Thứ 3! IAE201 trùng ca với PRM393"* kèm nút bấm nhanh **"Đổi ca"**.
  * Ma trận thời khóa biểu tuần phóng to (Lưới 5 ngày T2 -> T6, 5 ca học):
    * Các ca bình thường hiển thị mã môn màu xanh/vàng (AIE411, SWE302, PRM393).
    * Ô Ca 2 Thứ 3 được tô màu đỏ sẫm cảnh báo nổi bật: **"TRÙNG! Ca 2"**.
  * Nút chuyển trang ở đáy: Nút lớn màu xanh Sky Blue **"Xem danh sách môn (4 môn • 12 TC) ➔"** dẫn sang màn hình quản lý chi tiết.
  * Thanh điều hướng đáy: 4 tab (Tab *Tìm môn* kích hoạt).
* **Tương tác chính:** Nhấn nút "Xem danh sách môn" $\rightarrow$ Chuyển sang `SCR-06B Selected Courses`.

---

### SCR-06B: Selected Courses Management (Quản Lý Môn Đã Chọn & Xóa Môn)
* **Thuộc Flow:** Flow 3 (Khắc phục và giải quyết xung đột lịch).
* **Ý đồ thiết kế:** Màn hình chuyên trách để sinh viên rà soát toàn bộ các môn dự thảo, đối chiếu tín chỉ và xóa môn gây xung đột bằng vùng chạm thùng rác kích thước lớn (48x48dp).
* **Nội dung hiển thị:**
  * Top App Bar: Nút quay lại `←`, Tiêu đề *"Môn Đã Chọn"*, nút text phụ *"+ Thêm môn"*, avatar.
  * Thẻ tổng quan học kỳ: Hiển thị nổi bật **4 Môn • 12 Tín chỉ** kèm cảnh báo đỏ *"⚠️ 1 môn bị trùng ca học"*.
  * Danh sách 4 học phần đã chọn:
    * Môn PRM393 (3 TC • Ca 2 T2, T5) kèm icon thùng rác đỏ `🗑️`.
    * Môn AIE411 (3 TC • Ca 1 T4) kèm icon thùng rác đỏ `🗑️`.
    * Môn SWE302 (3 TC • Ca 1 T6) kèm icon thùng rác đỏ `🗑️`.
    * Môn **An toàn Thông tin (IAE201)**: Khung viền đỏ cảnh báo, tag *"Trùng lịch Ca 2 T3"*, nút phụ *"Đổi ca khác"* và icon thùng rác `🗑️`.
  * Nút chân trang cố định: Nút lớn **"Lưu Thời Khóa Biểu"** (kích hoạt sau khi giải quyết xong trùng lịch).
* **Tương tác chính:** Nhấn nút thùng rác tại IAE201 hoặc đổi ca $\rightarrow$ Giải quyết xong xung đột $\rightarrow$ Bấm "Lưu Thời Khóa Biểu" $\rightarrow$ Chuyển sang `SCR-07 Semester Summary`.

---

### SCR-07: Semester Summary & Export PDF (Tổng Kết & Xuất Báo Cáo)
* **Thuộc Flow:** Flow 2 (Điểm kết thúc xuất file PDF).
* **Ý đồ thiết kế:** Báo cáo xác nhận chính thức toàn bộ kế hoạch học kỳ đã chốt ca học, cung cấp tùy chọn xuất bản in PDF A4 chuẩn mực.
* **Nội dung hiển thị:**
  * Top App Bar: Nút quay lại `←`, Logo EduPlan + Tiêu đề *"Tổng Kết Kế Hoạch"*, chuông thông báo, avatar.
  * Thẻ KPI khối lượng tích lũy: Tiêu đề to **5 Môn học • 15 Tín chỉ**, tag xanh lá *"Kế hoạch hợp lệ ✅"*, học phí dự kiến *"14.250.000 đ"*.
  * Danh sách môn học đã xác nhận (5 môn): PRM393, AIE411, SWE302, SWP391, OSG209; mỗi môn hiển thị mã lớp, giờ học và icon tích xanh `check`.
  * Khung hành động xuất bản in: Nút lớn màu xanh Sky Blue **"📄 Xuất file PDF (A4)"** kèm 2 nút phụ *"Đồng bộ Google Lịch"* và *"Chia sẻ ảnh TKB"*.
  * Thanh điều hướng đáy: 4 tab (Tab *Tìm môn* kích hoạt).
* **Tương tác chính:** Chạm vào "Xuất file PDF (A4)" $\rightarrow$ Mở hộp thoại xem trước và tải file PDF về điện thoại.

---

### SCR-08: Profile & Settings (Cá Nhân & Cài Đặt Ứng Dụng)
* **Thuộc Flow:** Quản lý tài khoản & Cài đặt hệ thống.
* **Ý đồ thiết kế:** Màn hình quản lý hồ sơ sinh viên, thông tin tín chỉ tích lũy toàn khóa và các tùy chọn bật/tắt thông báo phục vụ tích hợp Firebase ở Lab 3.
* **Nội dung hiển thị:**
  * Top App Bar: Logo EduPlan + Tiêu đề *"Cá Nhân"*, chuông thông báo, avatar sinh viên.
  * Thẻ hồ sơ sinh viên: Avatar chibi tròn, họ tên **Trần Hoàng Long**, mã số sinh viên `SE180504 • K18 SE`, email trường.
  * Thống kê học tập nhanh: 2 pill con *"15 Tín chỉ (HK 2)"* và *"⭐ GPA: 3.42 (Giỏi)"*.
  * Danh mục Cài đặt ứng dụng (Các công tắc Switch bo tròn màu xanh):
    * Công tắc 1: *"Nhắc giờ học trước 15 phút"* (ON).
    * Công tắc 2: *"Tự động báo trùng lịch"* (ON).
    * Mục liên kết: *"Đồng bộ Google Calendar"*, *"Trợ giúp & FAQ"*, *"Về EduPlan (v2.4.1)"*.
  * Nút hành động nguy hiểm: Nút viền đỏ sẫm **"Đăng xuất tài khoản"** ở cuối màn hình.
  * Thanh điều hướng đáy: 4 tab (Tab *Cá nhân* kích hoạt).
* **Tương tác chính:** Nhấn "Đăng xuất tài khoản" $\rightarrow$ Bật Dialog xác nhận $\rightarrow$ Quay về `SCR-01 Login`.

---

## Bảng Đối Chiếu Ma Trận 3 User Flows Sang 9 Màn Hình

| Mã màn hình | Tên màn hình | Flow 1 (Chọn môn học) | Flow 2 (Lịch & Xuất PDF) | Flow 3 (Giải quyết trùng ca) |
| :---: | :--- | :---: | :---: | :---: |
| **SCR-01** | Login Screen | [x] Bắt đầu | | |
| **SCR-02** | Home Dashboard | [x] | | |
| **SCR-03** | Weekly Schedule | | [x] Bắt đầu | |
| **SCR-04** | Course Catalog | [x] | | [x] |
| **SCR-05** | Course Detail | [x] | | |
| **SCR-06A** | Plan Builder Grid | [x] Kết thúc | | [x] Bắt đầu |
| **SCR-06B** | Selected Courses | | | [x] Khắc phục |
| **SCR-07** | Semester Summary | | [x] Kết thúc | [x] Kết thúc |
| **SCR-08** | Profile & Settings | | | |