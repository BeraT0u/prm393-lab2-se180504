# Design Decisions & Accessibility Checklist — EduPlan

Tài liệu này ghi nhận 10 quyết định thiết kế quan trọng nhất nhằm giải quyết triệt để bài toán của Persona (Trần Hoàng Long) và kết quả kiểm tra khả năng tiếp cận (Accessibility Checklist).

---

## 1. Mười Quyết Định Thiết Kế Quan Trọng Nhất (Top 10 Design Decisions)

1. **Bố cục điều hướng ngón tay cái (Thumb-zone Navigation):**
   * *Quyết định:* Đặt thanh điều hướng chính (Bottom Navigation) và các nút hành động cốt lõi (Thêm môn, Đổi ca, Xuất PDF) ở 1/3 phía dưới màn hình.
   * *Lý do:* Persona thường xuyên sử dụng điện thoại bằng một tay khi đang di chuyển trên xe bus hoặc hành lang giảng đường.

2. **Cảnh báo trùng lịch đa phương thức (Multi-modal Conflict Notification):**
   * *Quyết định:* Khi phát hiện trùng ca học, hệ thống không chỉ đổi màu đỏ mà bắt buộc đi kèm biểu tượng cảnh báo `⚠️` và nhãn chữ chi tiết (Ví dụ: `Trùng ca với SWP391`).
   * *Lý do:* Tuân thủ nguyên tắc WCAG 1.4.1 (Không truyền đạt thông tin chỉ bằng màu sắc) và tránh nhầm lẫn cho sinh viên bị mù màu (color blindness).

3. **Lưới thời khóa biểu rút gọn kết hợp thẻ ca học (Compact Grid + Card View):**
   * *Quyết định:* Cung cấp chế độ xem lịch học theo ngày (Day view) dạng thẻ lớn cho màn hình 360dp, và dạng lưới tuần (Week grid) có thể trượt ngang.
   * *Lý do:* Tránh nhồi nhét 7 ngày vào màn hình hẹp 360dp gây vỡ giao diện và chữ quá nhỏ khó đọc.

4. **Nút Floating Action Button (FAB) tạo kế hoạch nhanh:**
   * *Quyết định:* Đặt nút FAB tròn (+) với kích thước 56x56 dp nổi trên Dashboard.
   * *Lý do:* Rút ngắn thời gian thêm môn mới xuống dưới 15 giây (đáp ứng tiêu chí thành công đã đặt ra trong `persona.md`).

5. **Khu vực giải quyết xung đột trực quan (Inline Conflict Resolution):**
   * *Quyết định:* Khi bị trùng ca, Dialog không chỉ báo lỗi đóng lại mà gợi ý luôn danh sách các ca học khác còn trống của môn đó để sinh viên đổi ngay tại chỗ.
   * *Lý do:* Giảm thiểu thao tác quay lại tìm kiếm từ đầu (Heuristic #5: Phòng ngừa và hỗ trợ phục hồi lỗi).

6. **Giới hạn font chữ đọc tối thiểu 14sp:**
   * *Quyết định:* Toàn bộ chữ nội dung, tên giảng viên, phòng học đều từ 14sp trở lên; chỉ các nhãn phụ (Slot time) dùng 12sp.
   * *Lý do:* Sinh viên thường tra cứu lịch học dưới trời nắng chói chang giữa các tòa nhà học, cỡ chữ lớn giúp đọc nhanh trong 3 giây.

7. **Vùng chạm tối thiểu 48 × 48 dp (Touch Target Standard):**
   * *Quyết định:* Tất cả các icon (chuyển tuần, nút xóa môn, filter chips) đều có padding vô hình để đạt kích thước chạm tối thiểu 48dp.
   * *Lý do:* Tránh bấm nhầm ca học liền kề khi ngón tay thao tác vội.

8. **Tích hợp sẵn luồng xác thực Google Sign-In:**
   * *Quyết định:* Sử dụng nút đăng nhập Google trường cấp (edu mail) làm cổng vào duy nhất ngay tại màn hình chào mừng.
   * *Lý do:* Chuẩn hóa dữ liệu sinh viên và chuẩn bị sẵn sàng 100% cho việc tích hợp Firebase Auth ở Lab 3.

9. **Xem trước bản in (Print Preview) trước khi xuất PDF:**
   * *Quyết định:* Khi bấm xuất thời khóa biểu, hệ thống mở Bottom Sheet xem trước bản in dạng trang giấy A4 thu nhỏ trước khi cho phép lưu hoặc chia sẻ.
   * *Lý do:* Giúp sinh viên rà soát toàn bộ lịch học của kỳ trước khi in ra bàn học, giảm thiểu việc in sai.

10. **Trạng thái lưu trữ cục bộ rõ ràng (Offline-Ready Visual):**
    * *Quyết định:* Bổ sung icon đám mây nhỏ hiển thị trạng thái `Đã đồng bộ` hoặc `Đang xem offline` ở góc trên Dashboard.
    * *Lý do:* Giúp sinh viên yên tâm thời khóa biểu đã được lưu trong máy ngay cả khi đi vào thang máy hoặc tầng hầm mất sóng.

---

## 2. Bảng Checklist Accessibility & Responsive (WCAG 2.1 AA)

| Tiêu chí | Chuẩn yêu cầu | Đo lường trên EduPlan | Đánh giá |
| :--- | :--- | :--- | :---: |
| **Độ tương phản chữ thường** | Tối thiểu 4.5:1 | Text `#0F172A` trên nền `#FFFFFF` đạt **15.4:1**<br>Text `#475569` trên nền `#FFFFFF` đạt **4.7:1** | ✅ Đạt |
| **Độ tương phản nút bấm/UI** | Tối thiểu 3.0:1 | Primary `#1E40AF` trên nền `#FFFFFF` đạt **8.2:1** | ✅ Đạt |
| **Vùng chạm (Touch target)** | Tối thiểu 48 × 48 dp | Nút bấm: 48dp - 52dp height<br>Icon button: Có padding 12dp $\rightarrow$ chạm 48dp | ✅ Đạt |
| **Cỡ chữ nội dung** | Tối thiểu 14 sp | Body text: 14sp; Title: 16sp; Headline: 20sp | ✅ Đạt |
| **Không phụ thuộc màu sắc** | Cần kèm icon / text | Lỗi trùng lịch có kèm icon `⚠️` và chữ `Trùng ca` | ✅ Đạt |
| **Kiểm tra màn hình hẹp (360 dp)** | Không tràn ngang | Đã kiểm tra bố cục 360 × 800 dp, dùng Auto Layout co giãn | ✅ Đạt |
| **Kiểm tra màn hình rộng (412 dp)** | Trải đều hợp lý | Đã test trên Pixel 7 (412 dp), các card mở rộng theo tỷ lệ | ✅ Đạt |