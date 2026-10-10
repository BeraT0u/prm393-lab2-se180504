# Information Architecture & User Flows — EduPlan (DoodlePad Edition)

Tài liệu này đặc tả Kiến trúc thông tin (Information Architecture - IA) và 3 Luồng người dùng cốt lõi (User Flows) của ứng dụng EduPlan. Cấu trúc được tối ưu hóa cho Persona Trần Hoàng Long (sinh viên năm 3 ngành SE) với các mục tiêu: tra cứu ca học trong 2 giây, lên kế hoạch và giải quyết xung đột lịch học trong dưới 15 giây bằng thao tác ngón cái trên một tay.

## 1. Information Architecture (Kiến trúc thông tin)

Hệ thống được thiết kế theo cấu trúc điều hướng phân cấp (Hierarchical Structure) kết hợp tiến trình làm việc toàn màn hình (Modal Task Flow). Thanh điều hướng đáy (Bottom Navigation Bar) làm trục chính cho 4 màn hình chức năng cấp 1:

```text
App Root (Authentication Guard)
│
├── [SCR-01] Login Screen (Google Sign-In trường cấp)
│
└── Main App Shell (Bottom Navigation Bar — 4 Destinations)
    │
    ├── [Tab 1] Trang Chủ ──────────────────────────────────────┐
    │     └── [SCR-02] Home Dashboard                           │
    │           ├── Thẻ Hero: Ca học tiếp theo (vào lớp nhanh)   │
    │           ├── Tiến độ tín chỉ & GPA tích lũy              │
    │           └── Danh sách 3 ca học sắp tới                  │
    │                                                           │
    ├── [Tab 2] Lịch Học                                        │
    │     └── [SCR-03] Weekly Schedule (Timeline dòng thời gian) │
    │           ├── Cụm điều hướng tuần & Nút [Hôm nay]         │
    │           ├── Dải 7 ngày (Horizontal swipe)               │
    │           └── Vạch chỉ báo thời gian thực (Now Indicator)  │
    │                                                           │
    ├── [Tab 3] Tìm Môn                                         │
    │     └── [SCR-04] Course Catalog                           │
    │           ├── Thanh tìm kiếm & Filter Chips chuyên ngành  │
    │           └── Danh sách môn học mở trong kỳ                │
    │                                                           │
    │     ┌─────────────────────────────────────────────────────┘
    │     │ [TIẾN TRÌNH CON — MODAL TASK FLOW: ẨN BOTTOM BAR]
    │     │
    │     ├──▶ [SCR-05] Course Detail (Chi tiết môn & Chọn lớp mở)
    │     │      ├── Tiên quyết, tín chỉ, giảng viên
    │     │      └── Danh sách Radio chọn lớp (SE1801, SE1802...)
    │     │
    │     ├──▶ [SCR-06A] Plan Builder Grid (Lưới tuần mô phỏng)
    │     │      ├── Banner cảnh báo trùng lịch ⚠️
    │     │      └── Ma trận thời khóa biểu 5x5 (Ô trùng tô đỏ)
    │     │
    │     └──▶ [SCR-06B] Selected Courses Management (Quản lý môn dự thảo)
    │            ├── Danh sách 4 môn đã chọn + Icon thùng rác
    │            ├── Nút hành động trực tiếp [Đổi ca khác]
    │            └── Nút chân trang [Lưu Thời Khóa Biểu] (Bị khóa nếu có lỗi)
    │
    ├── [Điểm kết thúc quy trình xếp lịch]
    │     └── [SCR-07] Semester Summary & Export PDF (Khôi phục Bottom Bar)
    │           ├── Thẻ KPI xác nhận: 15 Tín chỉ • Kế hoạch hợp lệ ✅
    │           ├── Hành động chính: [📄 Xuất file PDF (A4)]
    │           └── Tùy chọn: Đồng bộ Google Calendar, Chia sẻ ảnh TKB
    │
    └── [Tab 4] Cá Nhân
          └── [SCR-08] Profile & Settings
                ├── Hồ sơ sinh viên Trần Hoàng Long (SE180504)
                ├── Cài đặt: Nhắc ca học 15p, Tự động báo trùng lịch
                └── Nút hành động nguy hiểm: [Đăng xuất tài khoản]
```

### Bảng phân loại cấp bậc màn hình & Quy tắc Bottom Bar

| Cấp bậc | Màn hình | Định danh | Trạng thái Bottom Navigation Bar |
| --- | --- | --- | --- |
| Root | Đăng nhập tài khoản | SCR-01 | ❌ Ẩn hoàn toàn |
| Cấp 1 | Trang chủ Dashboard | SCR-02 | ✅ Hiển thị (Tab Trang chủ Active) |
| Cấp 1 | Thời khóa biểu tuần | SCR-03 | ✅ Hiển thị (Tab Lịch học Active) |
| Cấp 1 | Tìm & Danh mục môn | SCR-04 | ✅ Hiển thị (Tab Tìm môn Active) |
| Cấp 2 | Chi tiết môn & Chọn lớp | SCR-05 | ❌ Ẩn (Ưu tiên Docked Footer "Thêm vào lịch") |
| Cấp 2 | Lưới tuần xếp lịch thử | SCR-06A | ❌ Ẩn (Ưu tiên diện tích lưới ma trận) |
| Cấp 2 | Quản lý môn & Đổi ca | SCR-06B | ❌ Ẩn (Ưu tiên nút Sticky "Lưu TKB") |
| Cấp 2 | Tổng kết kỳ & Xuất PDF | SCR-07 | ✅ Khôi phục (Tab Tìm môn Active) |
| Cấp 1 | Hồ sơ & Cài đặt | SCR-08 | ✅ Hiển thị (Tab Cá nhân Active) |

## 2. Đặc tả 3 Luồng người dùng chính (Core User Flows)

### 🟢 Flow 1: Tra cứu môn học & Lập kế hoạch đăng ký lớp mở (Course Exploration & Planning)

- **Mục tiêu:** Sinh viên tìm kiếm môn học chuyên ngành SE, kiểm tra môn tiên quyết và đưa lớp học phần mong muốn vào lưới xếp lịch dự thảo.
- **Thời gian kỳ vọng:** Hoàn thành trong ≤15 giây.

```text
[BẮT ĐẦU]
   │
[SCR-01: Đăng nhập] ──(Google Sign-In)──▶ [SCR-02: Home]
                                                 │
                                        (Chạm Tab "Tìm Môn")
                                                 ▼
                                     [SCR-04: Course Catalog]
                                                 │
                  ┌──────────────────────────────┴──────────────────────────────┐
                  ▼                                                             ▼
      (Gõ tìm "PRM393" / Filter SE)                                  (Chạm thân thẻ PRM393)
                  │                                                             │
                  └──────────────────────────────┬──────────────────────────────┘
                                                 ▼
                                     [SCR-05: Course Detail]
                                                 │
                                     (Kiểm tra: Tiên quyết Đạt ✅)
                                     (Chọn Radio: Lớp SE1801 - Ca 2 T3, T6)
                                                 │
                                  (Bấm "Thêm vào lịch học" - 52dp)
                                                 ▼
                                 [SCR-06A: Plan Builder Grid]
                                                 │
                                [KẾT THÚC FLOW 1 / CHUYỂN TIẾP FLOW 3]
```

### 🔵 Flow 2: Tra cứu lịch học tức thì & Xuất thời khóa biểu PDF A4 (Schedule Tracking & PDF Export)

- **Mục tiêu:** Sinh viên kiểm tra ca học hôm nay trong 2 giây trước khi vào thang máy, hoặc xuất bản in thời khóa biểu A4 hoàn chỉnh để dán góc học tập.
- **Thời gian kỳ vọng:** Tra cứu ca học: ≤2 giây; Xuất bản PDF: ≤5 giây.

```text
[KỊCH BẢN A: Tra cứu nhanh trước giờ vào lớp]
[Mở App] ──▶ [SCR-02: Home Dashboard]
                    │
                    ├─(Liếc nhìn 2 giây)─▶ Thấy ngay: "Lập trình Di động - 09:30 - BE-302"
                    │
           (Muốn xem cả tuần)
                    ▼
        [SCR-03: Weekly Schedule] ──(Bấm [Hôm nay] / Vuốt ngày)──▶ Xem Slot 1 -> Slot 5

────────────────────────────────────────────────────────────────────────────────────────

[KỊCH BẢN B: Xuất file in PDF khi đã chốt học kỳ]
[SCR-07: Semester Summary]
           │
           ├─▶ Xem tổng quan: 5 Môn học • 15 Tín chỉ • Kế hoạch hợp lệ ✅
           │
   (Chạm [📄 Xuất file PDF (A4)])
           │
           ▼
[Modal Preview: Trang A4 thu nhỏ (Tỷ lệ 1:1.414)]
           │
           ├─(Xác nhận tải file)──▶ Tải xuống "EduPlan_TKB_Fall2024.pdf"
           │
           └─(Bấm "Đồng bộ")──────▶ Bắn toàn bộ ca học sang Google Calendar
```

### 🔴 Flow 3: Phát hiện xung đột trùng ca & Hoán đổi lịch học tại chỗ (Conflict Detection & Inline Resolution)

- **Mục tiêu:** Tự động phát hiện khi 2 môn bị trùng giờ học, ngăn chặn việc lưu lịch lỗi và cung cấp lối tắt đổi sang lớp khác chỉ với 1 lần chạm.
- **Quy tắc nghiệp vụ then chốt (Business Logic):**
  - **Đa phương thức (WCAG 1.4.1):** Ô xung đột trên lưới bắt buộc có nền đỏ #FEE2E2 + viền #DC2626 + icon ⚠️ + chữ TRÙNG! Ca 2.
  - **Phòng ngừa lỗi chủ động (Heuristic #5):** Nút "Lưu Thời Khóa Biểu" bị VÔ HIỆU HÓA (Disabled) chừng nào xung đột còn tồn tại.
  - **Không ép xóa môn (Heuristic #9):** Cung cấp nút [Đổi ca khác] để chọn lớp thay thế ngay tại chỗ mà không cần xóa đi tìm lại.

```text
[BẮT ĐẦU: Tại SCR-06A sau khi vừa thêm môn mới]
   │
[Hệ thống quét xung đột Real-time]
   │
   ├──▶ Phát hiện: Môn IAE201 bị TRÙNG CA 2 THỨ 3 với PRM393!
   │
[SCR-06A: Plan Builder Grid]
   │  ├── Banner đỏ: "⚠️ Trùng ca 2 Thứ 3! IAE201 trùng với PRM393"
   │  └── Ô Ca 2 Thứ 3 trên ma trận bị tô đỏ sọc chéo [⚠️ TRÙNG! Ca 2]
   │
 (Chạm nút: "Xem danh sách môn (4 môn • 12 TC) ➔")
   │
   ▼
[SCR-06B: Selected Courses Management]
   │
   ├── Thẻ môn IAE201 viền đỏ: Tag [Trùng lịch Ca 2 T3]
   │
   ├── Nút chân trang [Lưu Thời Khóa Biểu] ──▶ TRẠNG THÁI: DISABLED (Màu xám)
   │                                          (Nhãn: "Cần xử lý 1 môn trùng để lưu")
   │
   ▼
(Sinh viên chạm nút: [Đổi ca khác] cạnh môn IAE201)
   │
   ▼
[Bottom Sheet: Danh sách lớp mở thay thế của IAE201]
   │
 (Chọn: Lớp Ca 4 Thứ 2, Thứ 5 • Phòng BE-204 còn 6 chỗ)
   │
   ▼
[Hệ thống cập nhật thời khóa biểu]
   │
   ├── Ô Ca 2 Thứ 3 trên lưới chuyển xanh hợp lệ
   ├── Số lượng xung đột: 0 Trùng lịch
   └── Nút chân trang [Lưu Thời Khóa Biểu] ──▶ KÍCH HOẠT: ACTIVE (Màu xanh #2563EB)
   │
 (Bấm: "Lưu Thời Khóa Biểu")
   │
   ▼
[SCR-07: Semester Summary & Export PDF]
   │  └── Hiển thị thông báo: "Kế hoạch hợp lệ (0 Trùng lịch) ✅"
   │
[KẾT THÚC THÀNH CÔNG]
```

## 3. Ma trận đối chiếu Màn hình và Luồng người dùng (Traceability Matrix)

| Mã màn hình | Tên màn hình | Flow 1 (Chọn môn) | Flow 2 (Lịch & Xuất PDF) | Flow 3 (Xử lý trùng ca) |
| --- | --- | --- | --- | --- |
| SCR-01 | Login Screen | 🟢 Điểm khởi đầu | | |
| SCR-02 | Home Dashboard | 🟢 Chuyển tiếp | 🔵 Điểm bắt đầu (Tra cứu) | |
| SCR-03 | Weekly Schedule | | 🔵 Tra cứu chi tiết | |
| SCR-04 | Course Catalog | 🟢 Tìm kiếm môn | | 🔴 Tìm môn bổ sung |
| SCR-05 | Course Detail | 🟢 Chọn lớp & ca | | 🔴 Xem chi tiết lớp thay thế |
| SCR-06A | Plan Builder Grid | 🟢 Điểm kết thúc | | 🔴 Phát hiện trùng ca |
| SCR-06B | Selected Courses | | | 🔴 Đổi ca & Khắc phục lỗi |
| SCR-07 | Semester Summary | | 🔵 Xuất file PDF A4 | 🔴 Điểm kết thúc hợp lệ |
| SCR-08 | Profile & Settings | | 🔵 Quản lý đồng bộ | |

## 4. Quy tắc điều hướng & Trạng thái ngoại tuyến (Navigation & Offline Rules)

### 4.1. Quy tắc quản lý Stack điều hướng (Navigation Stack Rules)

- **Xác thực (SCR-01 → SCR-02):** Sử dụng `pushReplacementNamed('/home')` để xóa màn hình đăng nhập khỏi ngăn xếp, ngăn người dùng bấm Back quay lại màn hình Login sau khi đã xác thực.
- **Luồng Modal Sub-Flow (SCR-05 → SCR-06A → SCR-06B):**
  - Duy trì nút Back [←] ở góc trên bên trái thanh App Bar để cho phép lùi từng bước.
  - Khi hoàn tất ở SCR-06B và bấm "Lưu Thời Khóa Biểu", thực hiện `pushNamedAndRemoveUntil('/summary', ModalRoute.withName('/home'))` để đóng toàn bộ tiến trình chọn môn và đưa người dùng đến màn hình tổng kết SCR-07.
- **Đăng xuất (SCR-08 → SCR-01):** Bật Dialog xác nhận → Xóa sạch Local Cache / Session → Gọi `pushNamedAndRemoveUntil('/login', (route) => false)`.

### 4.2. Khả năng chịu lỗi ngoại tuyến (Offline-First Affordance)

Khi mất mạng 4G (Persona Long đi vào thang máy/tầng hầm), ứng dụng không chặn màn hình mà kích hoạt chế độ Offline Cache:

- Tại SCR-02 Home và SCR-03 Lịch học, hiển thị dải micro-banner: "Dữ liệu ngoại tuyến • Đã lưu lúc 09:15".
- Lịch học trong ngày vẫn hiển thị đầy đủ từ SQLite/Hive nội bộ.
- Khi có mạng trở lại, tính năng Pull-to-refresh cho phép sinh viên kéo xuống để đồng bộ tức thì ca học và phòng học mới nhất từ máy chủ.
