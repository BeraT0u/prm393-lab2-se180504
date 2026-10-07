# User Persona — Student Course Planner

## 1. Thông tin Persona

* **Họ và tên:** Trần Hoàng Long
* **Độ tuổi:** 20 tuổi
* **Vai trò:** Sinh viên năm 3, chuyên ngành Kỹ thuật Phần mềm (Đại học FPT / hệ thống tín chỉ).
* **Thiết bị sử dụng:** Xiaomi Redmi Note 12 (Android 13, màn hình 6.67 inch, độ phân giải 1080 x 2400 px).
* **Bối cảnh hằng ngày:**
  * Mỗi kỳ phải tự đăng ký từ 4 đến 6 môn học chuyên ngành.
  * Thường xuyên phải đăng ký môn trên điện thoại khi đang di chuyển, mạng 4G không ổn định.
  * Lịch học thay đổi theo tuần (tuần học lý thuyết, tuần học thực hành lab, tuần thi).

## 2. Mục tiêu (Goals)
* Xem nhanh thời khóa biểu trong ngày (hôm nay học phòng nào, ca mấy, giảng viên nào) chỉ với 1 lần mở app.
* Lập thử kế hoạch chọn môn trước kỳ học mới để tránh bị trùng lịch học giữa các môn bắt buộc và môn tự chọn.
* Theo dõi tổng số tín chỉ đã đăng ký trong kỳ và tiến độ tín chỉ tích lũy để đảm bảo ra trường đúng hạn.
* Xuất được thời khóa biểu dạng PDF để in ra bàn học hoặc chia sẻ cho nhóm bạn.

## 3. Nỗi đau (Pain Points)
* **Xung đột lịch học (Schedule Conflict):** Đăng ký xong mới phát hiện 2 môn bị trùng ca học vào sáng Thứ Tư, phải làm đơn hủy môn phức tạp.
* **Giao diện cổng trường quá tải:** Web trường thường bị sập hoặc giao diện web mobile quá nhỏ, khó tra cứu phòng học nhanh trước giờ vào lớp 5 phút.
* **Rối loạn tuần học:** Môn học bắt đầu vào các tuần khác nhau (môn học 10 tuần, môn học 5 tuần) khiến sinh viên dễ bị nhầm lẫn ngày bắt đầu môn mới.

## 4. Thói quen sử dụng & Nhu cầu Accessibility
* **Thao tác một tay:** Thường dùng ngón tay cái thao tác khi đang đứng đợi thang máy hoặc đi bộ lên giảng đường (cần vùng chạm tối thiểu 48x48 dp và các nút quan trọng nằm ở nửa dưới màn hình).
* **Độ tương phản cao:** Thường xem lịch học ngoài trời nắng gắt khi di chuyển giữa các tòa nhà (độ tương phản màu text/background tối thiểu 4.5:1 theo chuẩn WCAG 2.1).
* **Trạng thái ngoại tuyến (Offline-first):** Cần xem được lịch học đã lưu ngay cả khi mất sóng trong tầng hầm hay thang máy.

---

## 5. Câu phát biểu vấn đề (Problem Statement)
> *"Sinh viên đại học học theo hệ tín chỉ cần một công cụ di động trực quan để lập kế hoạch chọn môn học và tự động phát hiện trùng lịch, bởi vì việc quản lý thời khóa biểu thủ công khiến họ thường xuyên bị xung đột ca học và nhầm lẫn phòng học trước giờ lên lớp."*

## 6. Tiêu chí thành công đo được (Measurable Success Metric)
> **"Người dùng có thể thêm một môn học mới vào kế hoạch và nhận cảnh báo nếu trùng lịch trong thời gian dưới 15 giây."**