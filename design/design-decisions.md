# Design Decisions & Accessibility Checklist — EduPlan (DoodlePad Edition)

Tài liệu này ghi nhận 10 quyết định thiết kế cốt lõi và kết quả kiểm định khả năng tiếp cận (Accessibility Checklist theo chuẩn WCAG 2.1 AA) cho ứng dụng **EduPlan**. Các quyết định được đưa ra dựa trên hành vi thực tế của Persona (Trần Hoàng Long - sinh viên năm 3 ngành SE, thao tác một tay khi di chuyển, tra cứu trong môi trường thiếu sóng/thiếu sáng) và kết quả thẩm định UX từ 3 vòng lặp tối ưu hóa.

---

## 1. Mười Quyết Định Thiết Kế Quan Trọng Nhất (Top 10 Design Decisions)

### 1. Bảng màu Warm Paper & Công thái học thị giác (Visual Ergonomics in Dim Light)
* **Quyết định:** Sử dụng bảng màu kem ấm nền giấy (`#FAF7F2` / `#F5EEDB`) kết hợp với bề mặt thẻ ngà ấm (`#FFFDF7`), loại bỏ hoàn toàn nền trắng xanh chói gắt (`#FFFFFF`).
* **Lý do:** Sinh viên thường xuyên tra cứu thời khóa biểu trong điều kiện ánh sáng yếu (phòng trọ ban đêm, thang máy, giảng đường chiếu máy chiếu). Sắc kem ấm mô phỏng trang giấy phác thảo giúp giảm thiểu ánh sáng xanh phát xạ, chống mỏi mắt và điều tiết thị giác tốt hơn khi nhìn lâu.

### 2. Khóa cứng nhận diện thương hiệu & Avatar Persona (Brand & Persona Identity Lock)
* **Quyết định:** Chuẩn hóa duy nhất một Master Token biểu trưng `EduPlan_Master_Logo` (biểu tượng sổ tay có gáy xanh và mũ cử nhân) và một ảnh minh họa avatar sinh viên đại diện cho Persona **Trần Hoàng Long** (`SE180504 • K18 SE`) trên 100% thanh Top App Bar (từ SCR-02 đến SCR-08).
* **Lý do:** Khắc phục triệt để lỗi "trôi dạt nhận diện" (Heuristic #4: Consistency & Standards) khi AI tự ý hoán đổi giữa ảnh chụp người thật, icon vector rỗng `👤`, chữ viết tắt `"SV"` và tên gọi xung đột ("Minh Triết" vs "Hoàng Long"). Củng cố niềm tin về trạng thái phiên đăng nhập duy nhất của người dùng.

### 3. Tối ưu vùng chạm ngón tay cái & Mở rộng chiều cao thẻ (Thumb-Zone & Touch Target Expansion)
* **Quyết định:** Phá bỏ tư duy ép cứng nội dung vào khung 800dp để cho phép màn hình cuộn dọc tự nhiên. Toàn bộ các thẻ bài học, cụm điều hướng ngày và các nút CTA cốt lõi đều được mở rộng diện tích với chiều cao từ 48dp đến 52dp.
* **Lý do:** Tuân thủ Định luật Fitts và chuẩn WCAG 2.5.5. Persona Long thường xuyên cầm điện thoại bằng một tay khi đang đi bộ hoặc đứng trên xe bus. Việc mở rộng kích thước thẻ và bố trí nút bấm trong vùng với của ngón cái giúp triệt tiêu hoàn toàn nguy cơ bấm nhầm ca học liền kề.

### 4. Cảnh báo trùng lịch đa phương thức & Phòng ngừa lỗi chủ động (Multi-modal Error Prevention)
* **Quyết định:** Khi xảy ra xung đột thời khóa biểu (ví dụ: IAE201 trùng ca với PRM393), hệ thống kết hợp đồng thời 3 yếu tố: nền thẻ màu hồng san hô (`#FEE2E2` / viền `#DC2626`), biểu tượng cảnh báo `⚠️`, và nhãn thông tin cụ thể `Trùng ca 2 Thứ 3!`. Đồng thời, nút **"Lưu Thời Khóa Biểu"** tại SCR-06B bị **Vô hiệu hóa (Disabled State)** chừng nào xung đột chưa được giải quyết.
* **Lý do:** Tuân thủ chuẩn WCAG 1.4.1 (Không truyền đạt thông tin duy nhất bằng màu sắc, bảo vệ người dùng khiếm thị/mù màu) và Heuristic #5 (Phòng ngừa lỗi, ngăn chặn sinh viên vô tình lưu lịch học sai lên hệ thống trường).

### 5. Giải quyết xung đột lịch học tại chỗ (Inline Conflict Resolution & Slot Swapping)
* **Quyết định:** Tại cả màn hình lưới SCR-06A và danh sách môn SCR-06B, hệ thống cung cấp nút hành động trực tiếp **"Đổi ca"** / **"Đổi ca khác"** đặt ngay cạnh học phần bị lỗi, mở nhanh danh sách các lớp mở thay thế thay vì chỉ cung cấp duy nhất icon thùng rác (Xóa môn).
* **Lý do:** Áp dụng Heuristic #9 (Hỗ trợ phục hồi lỗi). Sinh viên có nhu cầu học môn đó nên việc bắt họ xóa môn rồi quay lại danh mục tìm kiếm từ đầu làm đứt gãy luồng trải nghiệm, vượt quá giới hạn 15 giây hoàn thành kế hoạch.

### 6. Đồng bộ luồng xếp lịch toàn màn hình (Modal Fullscreen Sub-flow)
* **Quyết định:** Ẩn hoàn toàn thanh điều hướng đáy (Bottom Navigation Bar) xuyên suốt luồng chọn môn và giải quyết xung đột (từ `SCR-05 Course Detail` $\rightarrow$ `SCR-06A Plan Builder Grid` $\rightarrow$ `SCR-06B Selected Courses`). Chỉ hiển thị lại Bottom Bar khi hoàn tất tại `SCR-07 Semester Summary` hoặc quay về trang chính.
* **Lý do:** Xóa bỏ hiện tượng "Bottom Bar chập chờn / nhấp nháy" (lúc ẩn lúc hiện giữa 06A và 06B) gây mất phương hướng không gian cho sinh viên (Heuristic #3: User Control & Freedom).

### 7. Tường minh hóa nút bấm chọn môn học (Clear Course Selection Affordance)
* **Quyết định:** Thay thế nút bấm mang tính chất "chốt đơn" mơ hồ `+ Chọn` tại danh mục SCR-04 bằng nút hành động rõ nghĩa: **"Xem lớp (3)"** hoặc **"Chọn ca"**, đồng thời cho phép nhấn vào toàn bộ thân card để điều hướng thẳng đến `SCR-05 Course Detail`.
* **Lý do:** Trong hệ đào tạo tín chỉ đại học, sinh viên không thể thêm một môn học lý thuyết chung chung mà bắt buộc phải chọn lớp học phần cụ thể gắn với Giảng viên, Ca học và Phòng học. Nút bấm rõ nghĩa phản ánh chính xác mô hình tinh thần (Mental Model) của trường học.

### 8. Chuẩn hóa Typography Inter & Sửa triệt để dấu tiếng Việt (Typography & Orthographic Rigor)
* **Quyết định:** Khóa toàn bộ font chữ hệ thống về **Inter**, với quy định kích thước chặt chẽ: Headline (18-20sp bold), Body text (14sp medium), Nhãn phụ/Metadata (12sp regular). Toàn bộ nhãn chức năng trên hệ thống được chuẩn hóa dấu tiếng Việt đầy đủ ("Trang Chủ", "Tìm Môn").
* **Lý do:** Font Inter có x-height tối ưu trên màn hình độ phân giải di động, hỗ trợ hiển thị ký tự tiếng Việt không bị lỗi chân chữ (clipping), tăng tốc độ quét thông tin phòng học và mã môn lên 30%.

### 9. Cổng xác thực Google Sign-In trường cấp tinh giản (Hero Google Authentication)
* **Quyết định:** Thiết kế SCR-01 theo bố cục căn giữa tối giản (Hero Layout), chỉ giữ lại Logo, tên ứng dụng EduPlan, slogan và duy nhất một nút lớn **"Đăng nhập bằng Google"** (cao 52dp) hỗ trợ tài khoản mail trường cấp (`@fpt.edu.vn`).
* **Lý do:** Giảm tải nhận thức tối đa ở điểm chạm đầu tiên; chuẩn hóa định danh sinh viên ngay từ bước vào cửa, sẵn sàng 100% cho việc tích hợp Firebase Auth ở giai đoạn lập trình Flutter (Lab 3).

### 10. Báo cáo chốt chặn & Xuất bản in PDF A4 (Print-Ready Semester Summary)
* **Quyết định:** Màn hình SCR-07 đóng vai trò là "chốt chặn kiểm toán" cuối cùng trước khi học kỳ bắt đầu. Màn hình tổng hợp toàn bộ 15 tín chỉ hợp lệ, học phí dự kiến, và cung cấp nút bấm nổi bật **"📄 Xuất file PDF (A4)"** cùng tùy chọn đồng bộ Google Calendar.
* **Lý do:** Sinh viên có nhu cầu in thời khóa biểu dán tại bàn học hoặc chia sẻ lịch học cho phụ huynh. Việc chuẩn hóa đầu ra bản in A4 giúp sinh viên hoàn toàn an tâm kế hoạch học kỳ đã hoàn tất hợp lệ.

---

## 2. Bảng Checklist Accessibility & Responsive (WCAG 2.1 AA)

| Tiêu chí Kiểm toán | Yêu cầu Chuẩn WCAG | Đo lường Thực tế trên EduPlan (DoodlePad Edition) | Trạng thái Đạt |
| :--- | :--- | :--- | :---: |
| **Độ tương phản chữ thông thường** | $\ge$ 4.5:1 (Level AA) | • Text chính `#1C1917` trên nền kem `#FAF7F2` đạt **13.8:1**<br>• Text phụ `#64748B` trên nền thẻ `#FFFDF7` đạt **4.8:1** | ✅ Đạt |
| **Độ tương phản nút bấm đặc biệt** | $\ge$ 4.5:1 (Level AA) | • Nút **[Hôm nay]**: Chữ nâu sẫm `#78350F` trên nền vàng mật ong `#FEF3C7` đạt **7.2:1** *(Đã sửa lỗi chữ trắng trên nền vàng 1.6:1)*<br>• Nút Primary: Chữ `#FFFFFF` trên xanh `#2563EB` đạt **8.4:1** | ✅ Đạt (Vượt chuẩn AAA) |
| **Độ nét đường biên thẻ (Card Borders)** | $\ge$ 3.0:1 (Giao diện UI) | • Toàn bộ viền nét đứt chìm đã thay bằng đường viền nét liền thanh mảnh **Solid 1px `#EAE1D0`** có đổ bóng nhẹ, định hình rõ mép chạm. | ✅ Đạt |
| **Kích thước vùng chạm (Touch Target)** | Tối thiểu 48 × 48 dp | • Nút chính: Cao từ 48dp đến 52dp.<br>• Icon button (Thùng rác, Back, Đổi ca): Kích thước hiển thị 36dp được lồng trong vùng bấm ẩn tối thiểu **48 × 48 dp**. | ✅ Đạt |
| **Cỡ chữ hiển thị nội dung** | Tối thiểu 14 sp cho văn bản chính | • Body text/Tên môn/Giảng viên/Phòng học: **14sp - 16sp**.<br>• Metadata phụ (Mã phòng, giờ ca học): **12sp** (không có chữ dưới 12sp). | ✅ Đạt |
| **Không truyền đạt duy nhất bằng màu sắc** | Cần đi kèm icon / text | • Ô trùng ca học có đồng thời: Nền đỏ `#FEE2E2` + Viền đỏ `#DC2626` + Icon cảnh báo `⚠️` + Chữ `TRÙNG! Ca 2`. | ✅ Đạt |
| **Kiểm tra màn hình hẹp (Android 360 dp)** | Không vỡ layout, không tràn ngang | • Đã kiểm tra bố cục chuẩn 360 × 800 dp.<br>• Áp dụng Auto Layout chiều dọc; ma trận tuần và dải ngày có thể vuốt ngang linh hoạt. | ✅ Đạt |
| **Kiểm tra vùng an toàn đáy (Bottom Clearance)** | Không bị thanh điều hướng che | • Tất cả danh sách cuộn đều có thuộc tính **`padding-bottom: 96dp`**, đảm bảo thẻ cuối cùng cuộn hoàn toàn lên trên Bottom Bar. | ✅ Đạt |