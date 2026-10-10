# Handoff 2 — EduPlan Mobile (Flutter) — DoodlePad Edition

Đặc tả kỹ thuật giao diện dành cho lập trình viên Flutter, chuyển giao trực tiếp từ thiết kế Figma & Google Stitch.

| Thông số | Giá trị chuẩn |
| --- | --- |
| Màn hình chuẩn | 360 × 800 dp (Android Mobile) |
| Design System | Material Design 3 (Custom DoodlePad Academic System) |
| Theme Mode | Warm Paper / Cozy Cream (Tối ưu chống mỏi mắt thiếu sáng) |
| Typography | Inter (Hỗ trợ 100% dấu tiếng Việt, không lỗi chân chữ) |
| Quy chuẩn màn hình | 9 màn hình (SCR-01 đến SCR-08, bao gồm SCR-06A & SCR-06B) |

## Mục lục

- Phần 1 — Bảng ánh xạ Design Tokens sang Flutter
- Phần 2 — Đặc tả chi tiết 9 màn hình
- Phần 3 — Responsive (width ≥ 600 dp) & Checklist UI

## Phần 1 — Bảng ánh xạ Design Tokens sang Flutter

### 1.1. Bảng màu (ColorScheme)

```dart
// lib/theme/app_colors.dart
class AppColors {
  // Nền canvas giấy kem ấm & thẻ ngà ấm
  static const Color warmCreamBg       = Color(0xFFFAF7F2); // Nền tổng thể Scaffold
  static const Color softIvorySurface   = Color(0xFFFFFDF7); // Bề mặt Card, Sheet, App Bar
  static const Color solidBorder        = Color(0xFFEAE1D0); // Viền 1px nét liền quanh Card
  
  // Màu thương hiệu & Hành động chính
  static const Color primaryBlue        = Color(0xFF2563EB); // Nút CTA chính, Tab active
  static const Color primaryBlueTonal   = Color(0xFFEFF6FF); // Nền nút phụ, chip chọn lớp
  static const Color onPrimaryWhite     = Color(0xFFFFFFFF);
  
  // Màu văn bản (Độ tương phản cao trên nền kem)
  static const Color textPrimary        = Color(0xFF1C1917); // Deep Espresso (Tiêu đề, tên môn)
  static const Color textSecondary      = Color(0xFF64748B); // Slate Muted (Giảng viên, ca học)
  static const Color textDisabled       = Color(0xFF94A3B8);
  
  // Trạng thái & Tiếp cận (WCAG AAA)
  static const Color badgeAmberSurface  = Color(0xFFFEF3C7); // Nền nút "Hôm nay"
  static const Color badgeAmberBorder   = Color(0xFFF59E0B);
  static const Color badgeAmberText     = Color(0xFF78350F); // Chữ nâu đậm (Tương phản 7.2:1)
  
  // Cảnh báo trùng ca & Lỗi
  static const Color errorRedSurface    = Color(0xFFFEE2E2); // Nền banner cảnh báo trùng
  static const Color errorRedBorder     = Color(0xFFDC2626); // Viền đỏ, icon ⚠️
  static const Color errorRedText       = Color(0xFFB91C1C);
  
  // Thành công & Hoàn thành
  static const Color successGreen       = Color(0xFF16A34A);
  static const Color successGreenBg     = Color(0xFFDCFCE7);
}
```

**Ánh xạ vào `ThemeData.colorScheme`:**

| `colorScheme` token | Ánh xạ |
| --- | --- |
| `colorScheme.surface` | `AppColors.warmCreamBg` |
| `colorScheme.surfaceContainer` | `AppColors.softIvorySurface` |
| `colorScheme.outlineVariant` | `AppColors.solidBorder` |
| `colorScheme.primary` | `AppColors.primaryBlue` |
| `colorScheme.onSurface` | `AppColors.textPrimary` |
| `colorScheme.onSurfaceVariant` | `AppColors.textSecondary` |
| `colorScheme.error` | `AppColors.errorRedBorder` |

### 1.2. Kiểu chữ (TextTheme - Font Inter)

```dart
// lib/theme/app_typography.dart
final TextTheme appTextTheme = TextTheme(
  displaySmall: TextStyle(fontFamily: 'Inter', fontSize: 28, fontWeight: FontWeight.bold, height: 1.2, color: AppColors.textPrimary),
  headlineMedium: TextStyle(fontFamily: 'Inter', fontSize: 20, fontWeight: FontWeight.w600, height: 1.3, color: AppColors.textPrimary),
  headlineSmall: TextStyle(fontFamily: 'Inter', fontSize: 18, fontWeight: FontWeight.w600, height: 1.3, color: AppColors.textPrimary),
  titleMedium: TextStyle(fontFamily: 'Inter', fontSize: 16, fontWeight: FontWeight.w600, height: 1.4, color: AppColors.textPrimary),
  bodyMedium: TextStyle(fontFamily: 'Inter', fontSize: 14, fontWeight: FontWeight.normal, height: 1.4, color: AppColors.textPrimary),
  labelLarge: TextStyle(fontFamily: 'Inter', fontSize: 14, fontWeight: FontWeight.w600, height: 1.4, color: AppColors.onPrimaryWhite),
  labelMedium: TextStyle(fontFamily: 'Inter', fontSize: 12, fontWeight: FontWeight.w600, height: 1.3, color: AppColors.textSecondary),
  labelSmall: TextStyle(fontFamily: 'Inter', fontSize: 11, fontWeight: FontWeight.w500, height: 1.4, color: AppColors.textSecondary),
);
```

### 1.3. Spacing & Border Radius

```dart
class AppSpacing {
  static const double xs = 4.0;
  static const double sm = 8.0;
  static const double md = 12.0;
  static const double lg = 16.0;
  static const double xl = 24.0;
  static const double xxl = 32.0;
  static const double bottomClearance = 96.0; // Khoảng đệm tránh bị Bottom Bar đè
}

class AppRadius {
  static const double sm = 8.0;     // Input search, tag con
  static const double md = 12.0;    // Nút bấm, filter chips
  static const double lg = 16.0;    // Card môn học, banner, dialog
  static const double pill = 999.0;  // Avatar, badge trạng thái
}
```

### 1.4. Thành phần tái sử dụng (Shared Components)

| Tên Component | Widget Flutter | Thông số bắt buộc |
| --- | --- | --- |
| EduPlan Master Logo | Widget `EduPlanLogoHeader()` | Hiển thị icon sổ tay gáy xanh + chữ "EduPlan" (Inter Bold) |
| Master Avatar | `CircleAvatar` | Bán kính 16dp (kích thước 32×32 dp), ảnh minh họa sinh viên Long, viền 1px #EAE1D0 |
| Primary Button | `FilledButton` | Cao tối thiểu 48–52 dp, bo góc 12dp, nền #2563EB |
| Tonal Button | `OutlinedButton` | Cao 40 dp (touch target 48 dp), nền #EFF6FF, viền #BFDBFE, chữ #1D4ED8 |
| Navigation Bar | `NavigationBar` | 4 tab: [Trang chủ, Lịch học, Tìm môn, Cá nhân], cao 64 dp, nền #FFFDF7 |

## Phần 2 — Đặc tả chi tiết 9 màn hình

### Tổng quan luồng điều hướng

| Mã màn hình | Tên màn hình | Phân cấp | Hiển thị Bottom Bar |
| --- | --- | --- | --- |
| SCR-01 | Login Screen | Root (Xác thực tài khoản) | ❌ Không |
| SCR-02 | Home Dashboard | Cấp 1 (Trang chủ) | ✅ Tab Trang chủ |
| SCR-03 | Weekly Schedule | Cấp 1 (Lịch học) | ✅ Tab Lịch học |
| SCR-04 | Course Catalog | Cấp 1 (Tìm môn) | ✅ Tab Tìm môn |
| SCR-05 | Course Detail | Cấp 2 (Chi tiết môn & chọn lớp) | ❌ Ẩn (Dùng Docked Action Footer) |
| SCR-06A | Plan Builder Grid | Cấp 2 (Lưới xếp lịch thử) | ❌ Ẩn (Luồng Modal Task Flow) |
| SCR-06B | Selected Courses | Cấp 2 (Quản lý môn đã chọn & sửa lỗi) | ❌ Ẩn (Luồng Modal Task Flow) |
| SCR-07 | Semester Summary | Cấp 2 (Tổng kết & Xuất PDF) | ✅ Tab Tìm môn (Khôi phục) |
| SCR-08 | Profile & Settings | Cấp 1 (Cá nhân & Cài đặt) | ✅ Tab Cá nhân |

```text
[ SCR-01 Login ]
                              │ (Đăng nhập Google thành công)
                              ▼
                       [ SCR-02 Home ]
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
 [ SCR-03 Lịch học ]   [ SCR-04 Tìm môn ]    [ SCR-08 Cá nhân ]
                              │ (Chạm thẻ môn học)
                              ▼
                       [ SCR-05 Chi tiết môn ] (Ẩn Bottom Bar)
                              │ (Bấm "Thêm vào lịch học")
                              ▼
                       [ SCR-06A Lưới xếp lịch ] (Ẩn Bottom Bar)
                              │ (Bấm "Xem danh sách môn ➔")
                              ▼
                       [ SCR-06B Môn đã chọn ] (Ẩn Bottom Bar, Đổi ca/Khóa Lưu)
                              │ (Hết trùng ca + Bấm "Lưu Thời Khóa Biểu")
                              ▼
                       [ SCR-07 Tổng kết & Xuất PDF ] (Hiện lại Bottom Bar)
```

### SCR-01 — Login Screen (Đăng nhập)

- **Layout:** `Scaffold → SafeArea → Padding(16) → Column(mainAxisAlignment: MainAxisAlignment.spaceBetween)` (Không cuộn).
- **Khối giữa (Hero Centered):** Logo sổ tay DoodlePad (64×64 dp) → Tiêu đề EduPlan (28sp bold) → Slogan "Lên lịch học thật dễ!".
- **Hộp thông tin đăng nhập:** Nền #FFFDF7, viền nét liền 1px #EAE1D0, bo góc 16dp.
- **Nút GoogleSignInButton:** Chiều cao 52 dp, nền #FFFFFF, viền #EAE1D0, logo Google SVG + dòng chữ "Đăng nhập bằng Google".
- **Tương tác:** Nhấn nút → Kích hoạt Firebase Auth SDK → Điều hướng `pushReplacementNamed('/home')` sang SCR-02.

### SCR-02 — Home Dashboard (Trang chủ)

- **Layout:** `Scaffold → AppBar cố định → RefreshIndicator → SingleChildScrollView(padding: EdgeInsets.fromLTRB(16, 12, 16, 96)) → Column(spacing: 16)`.
- **Top App Bar:** Logo Master EduPlan + Subtitle "Trang Chủ", chuông thông báo, avatar sinh viên Long (32×32 dp).
- **Nội dung hiển thị:**
  - **Banner ngoại tuyến** (chỉ hiện khi mất mạng): Nền #FFFDF7, icon mây offline cam, text "Dữ liệu ngoại tuyến • Đã lưu lúc 09:15", nút refresh 48dp.
  - **Lời chào:** "Chào buổi sáng ✨ Hoàng Long" kèm chip ngày "Thứ Năm, 24/10".
  - **Hero Card "Lớp tiếp theo":** Tag xanh "Lớp tiếp theo", thời gian đếm ngược "Bắt đầu trong 25p", môn Lập trình Di động (3 TC), phòng BE-302, nút bấm lớn "Vào lớp" (48dp).
  - **Lịch học sắp tới:** Danh sách thẻ môn tiếp theo kèm 2 nút xem nhanh: "Điểm danh" và "Sơ đồ phòng".
- **Tương tác:** Kéo để làm mới (Pull-to-refresh); chạm Hero Card → Mở SCR-05; chạm tab Bottom Bar để chuyển màn hình.

### SCR-03 — Weekly Schedule (Thời khóa biểu tuần)

- **Layout:** `Scaffold → AppBar("Lịch Học") cố định → Header cố định (Thanh tuần + Strip 7 ngày) → Expanded → ListView.builder(padding: EdgeInsets.only(bottom: 96))` (Danh sách Slot cuộn dọc).
- **Thành phần quan trọng:**
  - **Cụm chọn tuần:** Thanh `< Tháng 10, 2024 (Tuần 8) >` + Nút [Hôm nay] chuẩn WCAG: Nền #FEF3C7, viền #F59E0B, chữ #78350F (tuyệt đối không dùng chữ trắng trên nền vàng).
  - **Dải ngày (7-day Strip):** Vuốt ngang được; ngày đang chọn (T4, 23) tô nền xanh #2563EB chữ trắng.
  - **Thẻ Slot học:** Nền #FFFDF7, viền nét liền 1px #EAE1D0. Ca đang học có vạch chỉ báo 4dp màu xanh dương ở mép trái.

### SCR-04 — Course Catalog (Tìm & Danh mục môn học)

- **Layout:** `Scaffold → AppBar("Tìm Môn") → Khối tìm kiếm & Filter Chips (cố định) → Expanded → ListView.separated(padding: EdgeInsets.only(bottom: 96))`.
- **Thành phần quan trọng:**
  - **SearchBar:** Cao 48 dp, bo góc 12 dp, placeholder "Tìm mã môn hoặc tên môn...".
  - **Thẻ môn học (Course Card):**
    - Toàn bộ thân thẻ bọc trong `InkWell` → Chạm vào bất kỳ vị trí nào trên thẻ đều mở SCR-05 Course Detail.
    - Nút hành động bên phải: Tonal Button nhãn `Xem lớp (3)` (Cao 40 dp, touch target 48 dp) → Mở thẳng SCR-05.

### SCR-05 — Course Detail (Chi tiết môn & Chọn lớp)

- **Layout:** `Scaffold → AppBar (Nút quay lại ←, logo EduPlan, nút ghim) → SingleChildScrollView(padding: EdgeInsets.only(bottom: 110)) → DockedActionBar (Ghim đáy cố định)`.
- **Quy tắc điều hướng:** ẨN HOÀN TOÀN Bottom Navigation Bar.
- **Nội dung hiển thị:**
  - **Thông tin môn:** Lập trình Di động (PRM393), badge "3 Tín chỉ", tag xanh lá "Tiên quyết: Đạt ✅".
  - **Danh sách Radio chọn lớp mở** (SE1801, SE1802, SE1803): Thẻ đang chọn có viền xanh #2563EB.
  - **Docked Action Footer:**
    - Chứa nút yêu thích (Icon Button 48dp) + Nút chính "Thêm vào lịch học" (FilledButton cao 52dp).
    - Bọc trong `SafeArea(bottom: true)` với padding đáy 16dp.
- **Tương tác:** Chọn radio SE1801 → Nhấn "Thêm vào lịch học" → `Navigator.pushNamed('/plan-builder-grid')` sang SCR-06A.

### SCR-06A — Plan Builder Grid (Xếp lịch học thử - Lưới tuần)

- **Layout:** `Scaffold → AppBar("Xếp Lịch Học Thử", Back Button) → SingleChildScrollView(padding: EdgeInsets.only(bottom: 110)) → DockedBottomButton`.
- **Quy tắc điều hướng:** ẨN HOÀN TOÀN Bottom Navigation Bar.
- **Thành phần quan trọng:**
  - **Banner cảnh báo trùng (Conflict Alert):** Nền #FEE2E2, viền #DC2626, icon ⚠️, tiêu đề đỏ "Trùng ca 2 Thứ 3! IAE201 trùng ca với PRM393" kèm nút bấm Đổi ca (FilledButton xanh).
  - **Lưới ma trận tuần (Simulation Grid 5×5):**
    - Các ca bình thường hiển thị mã môn trên nền trắng ngà.
    - Ô xung đột (Ca 2 Thứ 3): Nền đỏ #FEE2E2, viền đỏ #DC2626, icon ⚠️ + chữ đậm TRÙNG! Ca 2.
  - **Nút chuyển trang đáy:** Nút ghim đáy "Xem danh sách môn (4 môn • 12 TC) ➔" (Cao 52dp) → Chuyển sang SCR-06B.

### SCR-06B — Selected Courses Management (Quản lý môn đã chọn & Khắc phục lỗi)

- **Layout:** `Scaffold → AppBar("Môn Đã Chọn", Back Button) → ListView(padding: EdgeInsets.only(bottom: 110)) → DockedBottomButton`.
- **Quy tắc điều hướng:** ẨN HOÀN TOÀN Bottom Navigation Bar.
- **Khắc phục xung đột & Phòng ngừa lỗi (Crucial UX):**
  - **Môn bị xung đột (An toàn Thông tin - IAE201):** Hiển thị khung viền đỏ, tag "Trùng lịch Ca 2 T3".
  - Bên cạnh icon thùng rác 🗑️, BẮT BUỘC có nút **[Đổi ca khác]** (OutlinedButton đỏ, cao 40dp, touch target 48dp) để mở Modal Bottom Sheet đổi lớp tức thì.
  - **Nút chân trang "Lưu Thời Khóa Biểu":**
    - Khi còn trùng ca: Bị VÔ HIỆU HÓA (Disabled), nền #CBD5E1, text #64748B, nhãn: "Giải quyết 1 môn trùng để lưu".
    - Khi hết trùng ca (0 xung đột): Kích hoạt màu xanh #2563EB, nhãn: "Lưu Thời Khóa Biểu".
- **Tương tác:** Giải quyết xong trùng lịch → Nhấn "Lưu Thời Khóa Biểu" → Chuyển sang SCR-07.

### SCR-07 — Semester Summary & Export PDF (Tổng kết & Xuất báo cáo)

- **Layout:** `Scaffold → AppBar("Tổng Kết Kế Hoạch") → SingleChildScrollView(padding: EdgeInsets.only(bottom: 96)) → NavigationBar (Khôi phục Bottom Bar, tab Tìm môn active)`.
- **Nội dung hiển thị:**
  - **Thẻ Hero KPI:** 5 Môn học • 15 Tín chỉ, badge xanh "Kế hoạch hợp lệ ✅", học phí dự kiến "14.250.000 đ".
  - **Danh sách xác nhận (5 môn):** Hiển thị mã môn, giờ học, giảng viên và dấu tích xanh.
  - **Cụm hành động xuất file (In-flow Content):** Nút lớn "📄 Xuất file PDF (A4)" (Cao 52dp), nút "Đồng bộ Google Lịch" và "Chia sẻ ảnh TKB".
- **Tương tác:** Nhấn "Xuất file PDF (A4)" → Mở ModalBottomSheet xem trước bản in theo chuẩn tỷ lệ trang giấy A4 (1 : 1.414).

### SCR-08 — Profile & Settings (Cá nhân & Cài đặt)

- **Layout:** `Scaffold → AppBar("Cá Nhân") → SingleChildScrollView(padding: EdgeInsets.only(bottom: 96)) → NavigationBar (Tab Cá nhân active)`.
- **Nội dung hiển thị:**
  - **Thông tin sinh viên:** Avatar minh họa tròn, họ tên Trần Hoàng Long, MSSV SE180504 • K18 SE, email trường.
  - **Thống kê:** Thẻ 15 Tín chỉ (HK 2) và GPA 3.42 (Giỏi).
  - **Danh mục SwitchListTile (Cao 56dp):** Bật/tắt "Nhắc giờ học trước 15 phút", "Tự động báo trùng lịch".
  - **Nút nguy hiểm:** "Đăng xuất tài khoản" (Nền #FEE2E2, viền #FCA5A5, chữ đỏ #DC2626).
- **Tương tác:** Bấm Đăng xuất → Mở AlertDialog xác nhận → Xóa token phiên → `pushNamedAndRemoveUntil('/login')` về SCR-01.

## Phần 3 — Responsive (width ≥ 600 dp) & Checklist UI

### 3.1. Quy tắc Responsive Tablet / Landscape (Width ≥ 600 dp)

- **Navigation Transition:** `NavigationBar` ở đáy màn hình tự động chuyển đổi thành `NavigationRail` cố định ở cạnh trái màn hình.
- **Content Max-Width Constraint:** Toàn bộ nội dung đọc chính (Hero card, Course catalog, Profile settings) bọc trong:

  ```dart
  Center(child: ConstrainedBox(constraints: BoxConstraints(maxWidth: 540), child: content))
  ```

- **Lưới thời khóa biểu (SCR-06A):** Màn hình ≥ 600 dp hiển thị cố định toàn bộ 5 cột ngày (T2–T6), không cần kích hoạt tính năng cuộn ngang.

### 3.2. Checklist nghiệm thu UI (Flutter Dev QA Checklist)

- **Màu sắc & Chống chói:** Nền toàn bộ Scaffold đạt mã #FAF7F2; thẻ đạt mã #FFFDF7; viền thẻ nét liền 1px solid #EAE1D0. Không có bất kỳ thành phần nào dùng nền trắng xanh #FFFFFF gây chói mắt.
- **Độ tương phản nút [Hôm nay] (SCR-03):** Chữ nâu đậm #78350F trên nền vàng #FEF3C7 (Đạt WCAG AAA ≥ 7:1).
- **Nhận diện thương hiệu & Avatar:** 100% Top App Bar sử dụng chung Master Logo EduPlan và avatar minh họa của Trần Hoàng Long.
- **Bottom Navigation Bar:**
  - Hiển thị cố định trên: SCR-02, SCR-03, SCR-04, SCR-07, SCR-08.
  - ẨN HOÀN TOÀN trên: SCR-01, SCR-05, SCR-06A, SCR-06B.
- **Vùng an toàn cuộn (Bottom Clearance):**
  - Màn hình có Bottom Bar: padding-bottom: 96dp.
  - Màn hình có Docked Footer Button (SCR-05, 06A, 06B): padding-bottom: 110dp đến 160dp.
- **Phòng ngừa lỗi (SCR-06B):** Nút "Lưu Thời Khóa Biểu" bị khóa disabled khi còn môn báo trùng ca; có nút "Đổi ca khác" cạnh icon thùng rác.
- **Kích thước vùng chạm:** Tất cả các nút bấm, icon button, switch tile có diện tích chạm tối thiểu 48×48 dp.
