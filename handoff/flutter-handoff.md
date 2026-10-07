# Handoff 2 — EduPlan Mobile (Flutter)

Đặc tả giao diện dành cho lập trình viên Flutter, chuyển đổi từ thiết kế Figma.

| Thông số | Giá trị |
| :--- | :--- |
| Màn hình chuẩn | 360 × 800 dp |
| Design system | Material Design 3 |
| Theme | Dark Navy |
| Font | Inter / Roboto |

**Mục lục**

1. [Phần 1 — Bảng ánh xạ chung](#phần-1--bảng-ánh-xạ-chung)
2. [Phần 2 — Đặc tả 8 màn hình](#phần-2--đặc-tả-8-màn-hình)
3. [Phần 3 — Responsive (width ≥ 600 dp)](#phần-3--responsive-width--600-dp)

---

# Phần 1 — Bảng ánh xạ chung

## 1.1. Design Tokens → Flutter

### 1.1.1. Bảng màu (ColorScheme)

| Token Figma | Biến Flutter (`colorScheme.*`) | Hex | Mục đích |
| :--- | :--- | :---: | :--- |
| `color/bg-main` | `surface` | `0xFF0B0F17` | Nền tổng thể của Scaffold |
| `color/surface` | `surfaceContainer` | `0xFF161F30` | Nền Card môn học, Bottom Bar, App Bar |
| `color/surface-subtle` | `surfaceContainerLow` | `0xFF0F172A` | Nền hộp thông tin con (slot, phòng học) |
| `color/surface-high` | `surfaceContainerHigh` | `0xFF1E293B` | Nền banner offline, thẻ dialog nổi bật |
| `color/primary` | `primary` | `0xFF2563EB` | Nút CTA chính, tab active, viền lớp đang chọn |
| `color/on-primary` | `onPrimary` | `0xFFFFFFFF` | Chữ/icon trên nền Primary |
| `color/secondary` | `secondary` | `0xFF10B981` | Nhãn xanh lá: "Đang mở", "Có mặt", thanh tiến độ |
| `color/secondary-container` | `secondaryContainer` | `0xFF064E3B` | Nền sẫm cho nhãn trạng thái xanh lá |
| `color/warning` | `tertiary` | `0xFFF59E0B` | Cam: icon đám mây offline, sao GPA |
| `color/error` | `error` | `0xFFDC2626` | Đỏ: cảnh báo trùng lịch, nút Đăng xuất |
| `color/text-primary` | `onSurface` | `0xFFF8FAFC` | Tiêu đề chính, tên môn, giờ học (trắng) |
| `color/text-secondary` | `onSurfaceVariant` | `0xFF94A3B8` | Giảng viên, phòng học, mã môn, chú thích (xám) |
| `color/border` | `outlineVariant` | `0xFF26334D` | Viền 1px quanh Card và Bottom Bar |

### 1.1.2. Kiểu chữ (TextTheme)

| Token Figma | Biến Flutter (`textTheme.*`) | Style | Ứng dụng |
| :--- | :--- | :--- | :--- |
| `type/display-sm` | `displaySmall` | 30 / bold / h 1.2 | Logo, KPI tín chỉ lớn |
| `type/headline-md` | `headlineMedium` | 20 / w600 / h 1.3 | Lời chào Home, tên môn chi tiết |
| `type/headline-sm` | `headlineSmall` | 18 / w600 / h 1.3 | Tiêu đề App Bar, tiêu đề Section |
| `type/title-md` | `titleMedium` | 16 / w600 / h 1.4 | Tên môn trên Card, tiêu đề Dialog |
| `type/body-md` | `bodyMedium` | 14 / normal / h 1.4 | Mô tả môn, input text, chú thích |
| `type/label-lg` | `labelLarge` | 14 / w600 / h 1.4 | Chữ trên nút bấm |
| `type/label-md` | `labelMedium` | 12 / w600 / h 1.3 | Giờ học, phòng học, filter chips |
| `type/label-sm` | `labelSmall` | 11 / w500 / h 1.4 | Nhãn phụ, mã môn, tag ca học |

### 1.1.3. Spacing & Border Radius

```dart
class AppSpacing {
  static const double xs = 4.0;
  static const double sm = 8.0;
  static const double md = 12.0;
  static const double lg = 16.0;
  static const double xl = 24.0;
  static const double xxl = 32.0;
  static const double bottomClearance = 96.0; // Đệm tránh Bottom Bar đè
}

class AppRadius {
  static const double sm = 8.0;    // Controls, input, chip
  static const double md = 12.0;   // Button, slot blocks
  static const double lg = 16.0;   // Cards, dialogs
  static const double pill = 999.0; // Tags, badges tròn
}
```

## 1.2. Component → Widget Flutter

| Component (Figma) | Widget Flutter | Cấu hình quan trọng |
| :--- | :--- | :--- |
| Button | `FilledButton` / `ElevatedButton` | `minimumSize: Size(double.infinity, 52)`, `borderRadius: 12` |
| Secondary Button | `OutlinedButton` | `side: BorderSide(color: Color(0xFF26334D))`, `borderRadius: 12` |
| Text field | `TextFormField` | `filled: true`, `fillColor: Color(0xFF161F30)`, viền `OutlineInputBorder` |
| Card | `Container` / `Card` | `color: Color(0xFF161F30)`, `border: Border.all(color: Color(0xFF26334D))` |
| Navigation Bar | `NavigationBar` | 4 `NavigationDestination`, `height: 64`, ghim cố định đáy |
| App Bar | `AppBar` | `backgroundColor: Color(0xFF0B0F17)`, `elevation: 0`, `centerTitle: false` |
| Dialog | `AlertDialog` | `backgroundColor: Color(0xFF161F30)`, `shape: RoundedRectangleBorder(16)` |
| Loading state | Shimmer / Skeleton card | Container màu `#1E293B`, bo góc 12dp |
| Empty state | `Column` | `Icon(Icons.inbox)` + Text + `ElevatedButton` hành động |
| Error state | `Container` / Banner | Nền `#1E293B`, icon `cloud_off` cam + nút "Đồng bộ lại" |

---

# Phần 2 — Đặc tả 8 màn hình

## Tổng quan nhanh

| Màn hình | Tên | Loại | Tab Bottom Bar |
| :--- | :--- | :--- | :---: |
| SCR-01 | Login | Root (chặn truy cập khi chưa đăng nhập) | — |
| SCR-02 | Home Dashboard | Cấp 1 | Home |
| SCR-03 | Weekly Schedule | Cấp 1 | Lịch học |
| SCR-04 | Course Catalog | Cấp 1 | Đăng ký môn |
| SCR-05 | Plan Builder | Cấp 2 (Flow 3) | Đăng ký môn |
| SCR-06 | Course Detail | Cấp 2 | — |
| SCR-07 | Semester Summary | Cấp 2 (điểm kết thúc Flow 2) | Đăng ký môn |
| SCR-08 | Profile & Settings | Cấp 1 | Cá nhân |

**Luồng điều hướng chính**

```
SCR-01 Login ──(đăng nhập thành công)──▶ SCR-02 Home
                                           │
        ┌──────────────┬───────────────────┼──────────────┐
        ▼              ▼                   ▼              ▼
   SCR-03 Lịch    SCR-04 Danh mục     (Hero card)    SCR-08 Cá nhân
                   │        │              │
                   │        └──(+)──▶ SCR-05 Plan Builder ──(xác nhận)──▶ SCR-07 Tổng kết
                   └──(thân thẻ)──▶ SCR-06 Course Detail ──(thêm kế hoạch)──▶ SCR-05
```

---

## SCR-01 — Login (Đăng nhập)

### Layout

```
Scaffold → SafeArea → Padding(16) → Column(mainAxisAlignment: spaceBetween)  [không cuộn]
```

- **Khối giữa:** Logo (`Image.asset` 64×64) → `SizedBox(12)` → Tiêu đề "EduPlan" → Slogan → `SizedBox(24)` → WelcomeCard → `SizedBox(20)` → GoogleSignInButton → `SizedBox(8)` → Helper text
- **Khối đáy:** FooterTermsAndPrivacy (cách mép dưới 16dp)

### Thành phần chính

- **GoogleSignInButton** — cao 52dp, nền trắng hoặc `#1E293B`, icon Google SVG
- **WelcomeCard** — nền `#161F30`, viền `#26334D`, chip email `@fpt.edu.vn`

### Trạng thái

| Trạng thái | Mô tả |
| :--- | :--- |
| Default | Màn hình chào mừng, sẵn sàng đăng nhập |
| Loading | Bấm Google → disable click, hiện `CircularProgressIndicator(strokeWidth: 2)` trong nút |
| Error | Hiện SnackBar đỏ: "Đăng nhập thất bại. Vui lòng thử lại bằng email trường cấp." |

### Tương tác

- Chạm "Đăng nhập bằng Google" → kích hoạt Firebase Auth SDK
- Chạm "Điều khoản dịch vụ" → mở WebView điều khoản

### Điều hướng

- Màn hình gốc; chưa đăng nhập không vào được
- Đăng nhập thành công → `pushReplacement` sang **SCR-02** (xóa stack cũ)

### Ràng buộc UI

- [ ] Nút đăng nhập cao tối thiểu **52dp**
- [ ] `resizeToAvoidBottomInset: false` (không có bàn phím)
- [ ] Chữ không bị cắt; tablet ≥600dp: `maxWidth: 400dp`, căn giữa

---

## SCR-02 — Home Dashboard (Trang chủ)

### Layout

```
Scaffold → TopAppBar (cố định) → RefreshIndicator
        → SingleChildScrollView(padding: LTRB(16, 12, 16, 96))
        → Column(spacing: 16)
```

**Thứ tự nội dung:** OfflineStatusBanner → Lời chào "Chào Long, 👋" → NextClassHeroCard → KpiCreditCard → UpcomingScheduleSection → NavigationBar (ghim đáy, 64dp)

**Vùng cuộn:** toàn bộ nội dung giữa Header và Bottom Bar (cuộn dọc).

### Thành phần chính

- **NextClassHeroCard** — tag "Bắt đầu sau 25 phút", môn PRM393, phòng BE-302, GV ThS. Nguyễn Văn A
- **KpiCreditCard** — ProgressBar 83%, GPA 3.42
- **NavigationBar** — variant Home active (icon `#2563EB`)

### Trạng thái

| Trạng thái | Mô tả |
| :--- | :--- |
| Populated | Đầy đủ thông tin ca học hôm nay + tiến độ tín chỉ |
| Loading | Shimmer 2 thẻ xám mờ giả lập HeroCard (nạp Firestore) |
| Offline | Banner `#1E293B` dưới Header: "Dữ liệu ngoại tuyến • Đã lưu lúc 09:15" + nút "Đồng bộ lại" |
| Empty | Hero đổi thành "Hôm nay không có ca học. Chúc bạn một ngày tốt lành!" |

### Tương tác

- Pull-to-refresh → gọi API đồng bộ lịch học
- Chạm NextClassHeroCard → mở **SCR-06** (môn PRM393)
- Chạm "Xem tất cả" → sang tab **SCR-03**

### Điều hướng

| Hành động | Màn hình đến |
| :--- | :--- |
| Tab "Lịch học" | SCR-03 |
| Tab "Đăng ký môn" | SCR-04 |
| Tab "Cá nhân" | SCR-08 |

### Ràng buộc UI

- [ ] `padding-bottom: 96dp` — thẻ cuối không bị Bottom Bar che
- [ ] Vùng chạm icon (chuông, avatar, xem tất cả) ≥ **48 × 48 dp**
- [ ] Chữ dài cắt `TextOverflow.ellipsis`

---

## SCR-03 — Weekly Schedule (Thời khóa biểu tuần)

### Layout

```
Scaffold → AppBar("Lịch Học") (cố định)
        → Column cố định: WeekNavigator + DaySelectorStrip
        → Expanded → ListView.builder (slot học theo dòng thời gian)
        → NavigationBar (ghim đáy)
```

**Vùng cuộn:** chỉ danh sách Slot (Slot 1–5); thanh tuần + thanh 7 ngày ghim cố định trên.

### Thành phần chính

- **DayChip** — Active (Thứ Ba, `#2563EB`) / Default (các thứ khác)
- **TimelineSlotCard** — Occupied (viền trái xanh/cam phân loại) / Empty (viền nét đứt + nút "+ Đặt phòng tự học")
- **NavigationBar** — variant Schedule active

### Trạng thái

| Trạng thái | Mô tả |
| :--- | :--- |
| Populated | Ca học trong ngày đã chọn |
| Empty | Ngày nghỉ → khung "Ca tự học / Nghỉ ngơi - Không có ca học" viền nét đứt |
| Now Indicator | Ngày = hôm nay → vạch ngang phát sáng cyan `#38BDF8` tại giờ hiện tại (10:15) |

### Tương tác

- Chạm "Hôm nay" → cuộn/focus về ngày hiện tại
- Vuốt ngang → chuyển nhanh giữa các ngày trong tuần
- Mũi tên `<` `>` → chuyển tuần trước/sau
- Chạm ca học → BottomSheet tóm tắt tài liệu môn học

### Điều hướng

- Tab chính cấp 1; các tab Bottom Bar chuyển màn hình tương ứng

### Ràng buộc UI

- [ ] DayChip ≥ **48 × 58 dp**
- [ ] Danh sách Slot có `padding-bottom: 96dp`

---

## SCR-04 — Course Catalog (Danh mục môn học)

### Layout

```
Scaffold → AppBar("Danh Mục Môn Học")
        → Column: SemesterBanner → StickySearchBar → FilterChipsRow (cuộn ngang)
        → Expanded → ListView.separated (PRM393, SWP391, OSG209, CSD201...)
        → NavigationBar (ghim đáy)
```

**Vùng cuộn:** danh sách môn học cuộn dọc tự do.

### Thành phần chính

- **SearchBar** — cao 48dp, bo góc 12dp, nền `#161F30`, viền `#26334D`
- **FilterChip** — Selected nền `#2563EB` / Unselected nền xám viền `#334155`
- **CourseCard** — mã môn, tên môn, môn tiên quyết, nhãn số lớp mở, nút "+ Thêm vào lịch"
- **NavigationBar** — variant Catalog active

### Trạng thái

| Trạng thái | Mô tả |
| :--- | :--- |
| Populated | 28 môn học mở trong kỳ |
| Empty/Filtering | Không khớp → EmptyState: icon kính lúp + "Không tìm thấy môn học phù hợp" |
| Loading | 4 khung xương Skeleton card nhấp nháy mờ |

### Tương tác

- Nhập SearchBar → lọc real-time theo mã/tên môn
- Chạm thân thẻ → mở **SCR-06**
- Chạm "+ Thêm vào lịch" → thêm vào dự thảo, chuyển **SCR-05**

### Điều hướng

| Hành động | Màn hình đến |
| :--- | :--- |
| Thẻ môn | SCR-06 |
| Nút "+ Thêm vào lịch" | SCR-05 |

### Ràng buộc UI

- [ ] Nút "+ Thêm vào lịch" ≥ **40dp cao × 100dp rộng**, tách biệt thân thẻ (tránh bấm nhầm)
- [ ] `resizeToAvoidBottomInset: true` khi mở bàn phím tìm kiếm

---

## SCR-05 — Plan Builder & Conflict Checker (Xếp lịch học thử)

### Layout

```
Scaffold → AppBar("Xếp Lịch Học Thử")
        → SingleChildScrollView(padding-bottom: 160dp)
        → Column(spacing: 16): SimulationGrid → ConflictAlertBanner → SelectedCoursesList

Chân trang cố định:
  - StickyBottomSummaryBar (bottom: 64dp — tổng 12/18 TC + nút Xác nhận)
  - NavigationBar (bottom: 0 — tab Đăng ký môn active)
```

### Thành phần chính

- **SimulationGrid** — lưới ma trận tuần 6 ca × 5 ngày thu nhỏ; ô trùng vẽ sọc chéo đỏ + icon ⚠️ + chữ "TRÙNG!"
- **ConflictAlertBanner** — nền `#331515`, viền `#DC2626`, nút xanh "Đổi ca này" + nút xám "Chọn ca"
- **CourseCard** — có icon thùng rác xóa môn
- **FilledButton** — "Xác nhận lịch"

### Trạng thái (Error Recovery)

| Trạng thái | Mô tả |
| :--- | :--- |
| Conflict | PRM393 trùng Ca 2 Thứ 3 với SWP391 → ô lưới đỏ + banner cảnh báo; nút "Xác nhận lịch" disable/cảnh báo |
| Resolved | Bấm "Đổi ca này" → PRM393 chuyển Ca 4 Thứ 6 → ô lưới xanh, banner biến mất, đạt 12/18 TC hợp lệ |

### Tương tác

- "Đổi ca này" → giải quyết xung đột chỉ với 1 chạm
- Icon thùng rác → xóa môn, hiện SnackBar **Undo trong 5 giây**
- "Xác nhận lịch" → lưu kế hoạch, chuyển **SCR-07**

### Điều hướng

- Thuộc Flow 3; xác nhận → SCR-07; Back → SCR-04

### Ràng buộc UI

- [ ] Lưới 6×5 cuộn ngang nhẹ nếu màn hình < 360dp (tránh chữ đè)
- [ ] `padding-bottom: 160dp` bắt buộc — StickyBottomSummaryBar không che môn cuối

---

## SCR-06 — Course Detail (Chi tiết môn học)

### Layout

```
Scaffold → AppBar("Chi Tiết Môn Học": Back, Bookmark, Share)
        → SingleChildScrollView(padding-bottom: 110dp)
        → Column(spacing: 16):
             CourseHeaderCard → QuickSpecsRow → TechBanner
             → CourseDescriptionCard → OpenClassSlotsSection
        → DockedActionBar (ghim đáy: học phí 3.200.000đ + nút "Thêm vào Kế hoạch học kỳ")
```

> **Lưu ý:** KHÔNG có Bottom Navigation Bar trên màn hình này.

### Thành phần chính

- **CourseHeaderCard** — badge PRM393, tiêu đề lớn, banner "Môn tiên quyết đã đạt"
- **QuickSpecsRow** — 3 cột: 3 TC / 30 Slots / Lý thuyết & Lab
- **TechBanner** — ảnh Flutter & React Native
- **OpenClassSlotsSection** — 4 lớp SE1801, SE1802, SE1803, SE1804
- **ClassRadioCard** — Selected viền `#2563EB` / Unselected viền `#26334D` / Full gạch ngang tên lớp
- **FilledButton** — cao 52dp, "Thêm vào Kế hoạch học kỳ"

### Trạng thái

| Lớp | Trạng thái |
| :--- | :--- |
| SE1801, SE1802 | Còn chỗ → bấm chọn được, hiện số chỗ còn lại màu xanh/xám |
| SE1804 | Hết chỗ → Disabled (Opacity 0.5), icon khóa, không chọn được |

### Tương tác

- Chạm Card lớp → đổi Radio, cập nhật học phí ở chân trang
- "Thêm vào Kế hoạch học kỳ" → hiện thông báo thành công, chuyển **SCR-05**
- Back ← → quay **SCR-04**

### Điều hướng

- Màn hình con cấp 2: quay về SCR-04 hoặc tiến tới SCR-05

### Ràng buộc UI

- [ ] Nút đáy bọc `SafeArea(bottom: true)` — không bị thanhgesture bar đè
- [ ] `padding-bottom: 110dp` — cuộn qua hết SE1804 không bị footer che

---

## SCR-07 — Semester Summary & Export PDF (Tổng kết & xuất báo cáo)

### Layout

```
Scaffold → AppBar("Tổng Kết Học Kỳ": Back, Share)
        → SingleChildScrollView(padding-bottom: 96dp)
        → Column(spacing: 16):
             HeroKpiCard → TimetableRhythmCard → ConfirmedCourseList → PdfExportActionCard
        → NavigationBar (ghim đáy — tab Đăng ký môn active)
```

### Thành phần chính

- **HeroKpiCard** — gradient `#161F30 → #1A253A`, "5 Môn học • 15 Tín chỉ", thanh tiến độ 83%, học phí 14.250.000đ
- **TimetableRhythmCard** — "5 buổi sáng/chiều • Không có ca tối"
- **ConfirmedCourseList** — 5 thẻ môn đã chốt ca (viền trái xanh dương phân loại)
- **PdfExportActionCard** — 340 KB, nút "Tải xuống Thời khóa biểu A4" + nút "Bản in"

### Trạng thái

| Trạng thái | Mô tả |
| :--- | :--- |
| Default | Bản tóm tắt 5 môn hoàn chỉnh |
| Exporting | Bấm "Tải xuống" → icon xoay + Toast: "Đang tạo bản PDF A4... Thời khóa biểu HK1_2026_EduPlan.pdf" |
| Preview | Bấm "Bản in" → ModalBottomSheet xem trước A4 thu nhỏ |

### Tương tác

- "Tải xuống Thời khóa biểu (A4)" → sinh PDF, lưu bộ nhớ máy / mở dialog lưu file
- "Bản in" → mở khung xem trước in ấn
- Back ← → quay màn hình trước

### Điều hướng

- Điểm kết thúc của **Flow 2**

### Ràng buộc UI

- [ ] Khung xem trước đúng tỷ lệ A4 (**1 : 1.414**)
- [ ] `padding-bottom: 96dp` — khung xuất PDF không bị Bottom Bar che

---

## SCR-08 — Profile & Settings (Cá nhân & cài đặt)

### Layout

```
Scaffold → AppBar("Cá Nhân": icon Chuông, Avatar)
        → SingleChildScrollView(padding-bottom: 96dp)
        → Column(spacing: 20):
             StudentProfileHero → AcademicStatsGrid
             → PreferencesCardGroup → LegalLinksGroup → LogoutSection
        → NavigationBar (ghim đáy — tab Cá nhân active)
```

### Thành phần chính

- **StudentProfileHero** — avatar tròn 96dp, Trần Hoàng Long, MSSV SE180504, badge K18 FPTU, email trường
- **AcademicStatsGrid** — 2 thẻ: Tích lũy 92/145 TC, GPA 3.42 (Hạng Giỏi)
- **PreferencesCardGroup** — Switch: nhắc nhở ca học 15p, cảnh báo trùng lịch, đồng bộ đám mây, phiên bản v1.0.0 Stable
- **SwitchListTile** — công tắc xanh `#2563EB`
- **DestructiveButton** — viền đỏ, chữ `#DC2626`
- **ConfirmationDialog** — popup xác nhận đăng xuất

### Trạng thái

| Hành động | Mô tả |
| :--- | :--- |
| Đăng xuất | AlertDialog: "Bạn có chắc chắn muốn đăng xuất khỏi tài khoản EduPlan?" → 2 nút: Hủy / Đăng xuất |
| Đồng bộ | Bấm refresh cạnh "Đồng bộ lịch" → icon quay, text đổi thành "Đã đồng bộ vừa xong" |

### Tương tác

- Bật/tắt Switch "Nhắc nhở ca học" → lưu vào local storage / Firebase Remote Config
- Xác nhận Đăng xuất → xóa session, chuyển **SCR-01**

### Điều hướng

- Tab chính cấp 1; xác nhận đăng xuất → SCR-01

### Ràng buộc UI

- [ ] Dòng Switch/Link cao tối thiểu **56dp**; vùng chạm công tắc **48 × 48 dp**
- [ ] Nút Đăng xuất đặt xa các mục cài đặt thường dùng (tránh bấm nhầm)

---

# Phần 3 — Responsive (width ≥ 600 dp)

Áp dụng khi chạy trên máy tính bảng hoặc màn hình ngang (chuẩn thiết kế vẫn là 360 × 800 dp):

| # | Hành vi | Mô tả |
| :---: | :--- | :--- |
| 1 | **Navigation Transition** | `NavigationBar` ngang ở đáy → tự chuyển thành `NavigationRail` cố định cạnh trái |
| 2 | **Max-Width Constraint** | Nội dung đọc chính (Hero card, Course list, Profile) bọc trong `Center` + `BoxConstraints(maxWidth: 600)` |
| 3 | **Lưới thời khóa biểu (SCR-03 & SCR-05)** | Mobile: cuộn ngang từng ngày · ≥600dp: hiện đồng thời toàn bộ 7 cột, không cuộn ngang |

---

## Checklist tổng hợp ràng buộc UI

- [ ] SCR-01 — nút đăng nhập ≥52dp; `resizeToAvoidBottomInset: false`; tablet maxWidth 400dp
- [ ] SCR-02 — padding-bottom 96dp; touch target 48×48dp; ellipsis cho chữ dài
- [ ] SCR-03 — DayChip ≥48×58dp; padding-bottom 96dp
- [ ] SCR-04 — nút "+ Thêm" ≥40×100dp; `resizeToAvoidBottomInset: true`
- [ ] SCR-05 — padding-bottom 160dp; lưới cuộn ngang khi <360dp
- [ ] SCR-06 — không có NavigationBar; `SafeArea(bottom: true)`; padding-bottom 110dp
- [ ] SCR-07 — tỷ lệ A4 1:1.414; padding-bottom 96dp
- [ ] SCR-08 — dòng ≥56dp; touch 48×48dp; Đăng xuất xa mục thường dùng
- [ ] ≥600dp — NavigationRail + maxWidth 600 + lưới 7 cột
