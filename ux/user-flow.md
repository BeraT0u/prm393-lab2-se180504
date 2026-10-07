# Information Architecture & User Flows

## 1. Information Architecture (Kiến trúc thông tin)

Hệ thống được thiết kế theo cấu trúc điều hướng phân cấp (Hierarchical Structure), lấy thanh điều hướng đáy (Bottom Navigation Bar) làm trục chính cho các màn hình cấp 1:

```text
App Root (Auth Check)
├── [Screen 1] Login Screen (Google Sign-In)
│
└── Main App Shell (Bottom Navigation)
    ├── [Screen 2] Home / Dashboard (Lịch học hôm nay & KPI tín chỉ)
    │     └── [Screen 6] Course Detail Screen (Xem chi tiết môn, phòng, GV)
    │
    ├── [Screen 3] Weekly Schedule Screen (Thời khóa biểu dạng lưới tuần)
    │     └── [Screen 6] Course Detail Screen
    │
    ├── [Screen 4] Course Catalog Screen (Tra cứu & tìm kiếm môn học mở trong kỳ)
    │     └── [Screen 5] Plan Builder Screen (Xếp lịch & Kiểm tra trùng ca)
    │
    ├── [Screen 7] Semester Summary & Export Screen (Tổng kết & Xuất PDF)
    │
    └── [Screen 8] Profile & Settings Screen (Thông tin sinh viên, Đăng xuất)