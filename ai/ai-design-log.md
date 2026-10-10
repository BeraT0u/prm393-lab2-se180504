# Nhật Ký Sử Dụng AI (AI Design Log) — EduPlan

Tài liệu này ghi lại toàn bộ quy trình tôi sử dụng trí tuệ nhân tạo (AI) trong giai đoạn thiết kế UI/UX theo nguyên tắc cốt lõi: AI tạo ra; Sinh viên thẩm định và quyết định.

## 1. Khai Báo Công Cụ AI Đã Sử Dụng

| Công cụ | Mục đích sử dụng |
| --- | --- |
| Google Stitch | Generative UI: Phác thảo và sinh layout giao diện mobile ban đầu (8-9 màn hình) từ các text prompt mô tả đặc tả yêu cầu; thực thi các prompt tinh chỉnh trực tiếp trên canvas. |
| Gemini (UX Specialist) | UX Audit & Accessibility Review: Đóng vai chuyên gia QA/UX để phản biện thiết kế giao diện dựa trên 10 Heuristics của Jakob Nielsen và tiêu chuẩn WCAG 2.1 AA. |

## 2. Nhật Ký 1: Tạo UI Ban Đầu Bằng Google Stitch (Initial Generation)

Tôi đã sử dụng Google Stitch để phác thảo nhanh các màn hình cốt lõi của ứng dụng EduPlan theo kích thước chuẩn Android (360 × 800 dp). Ban đầu, tôi thử nghiệm phong cách Material Design 3 kết hợp Dark/Light theme để định hình Kiến trúc Thông tin (Information Architecture).

Dưới đây là các Prompt nguyên văn (Verbatim Prompts) tôi đã dùng cho các màn hình chính:

### Prompt cho SCR-02 (Home Dashboard)

> "Mobile app screen: 'Home Dashboard' for a university course planning app named 'EduPlan'. Platform: Android mobile, dimensions: 360x800 dp. Style: Material Design 3, modern, clean, academic. Color palette: Primary Deep Blue (#1E40AF), background neutral light (#F8FAFC), surface cards (#FFFFFF), text primary (#0F172A), text secondary (#475569), success green (#16A34A). Layout structure (from top to bottom): 1. Top Bar: Greeting 'Chào Long, 👋', subtitle 'Học kỳ 1 • 2026-2027', user avatar on the right, offline sync cloud status icon. 2. Next Class Hero Card: Highlighted upcoming class today with a countdown timer 'Bắt đầu sau 25 phút', subject name 'Lập trình Di động (PRM393)', slot time '09:30 - 11:50 (Slot 2)', room 'BE-302', lecturer name 'Ths. Nguyen Van A'. 3. KPI Credit Progress Card. 4. Upcoming 3-Day Schedule List. 5. Floating Action Button (FAB): Prominent circular button (56x56 dp) at the bottom right. 6. Bottom Navigation Bar (4 destinations). Ensure all touch targets are at least 48x48 dp."

### Prompt cho SCR-04 (Course Catalog)

> "Mobile app screen: 'Course Catalog' for university course planner app 'EduPlan'. Platform: Android mobile, dimensions: 360x800 dp. Style: Material Design 3. Primary color: Deep Blue (#1E40AF), background: #F8FAFC, card surface: #FFFFFF. Layout structure: 1. Top App Bar: Title 'Danh Mục Môn Học', back arrow icon on the left, search icon. 2. Search Bar: Rounded input field (8dp radius) with search icon. 3. Filter Chips (horizontal scroll): 'Tất cả', 'Chuyên ngành (SE)', 'Cơ sở ngành', '3 Tín chỉ', '4 Tín chỉ'. Active chip highlighted. 4. Course List (vertical scroll of cards, 12dp radius, 8dp spacing): Card 1: Code badge 'PRM393' (primary blue), Title 'Lập trình Di động Cross-platform', Credits badge '3 TC', '4 lớp đang mở ca học', chevron right icon. 5. Bottom Navigation Bar: Course Catalog tab is active."

### Quyết định của tôi

Tôi Chấp nhận (Accepted) kết quả bố cục cơ bản từ Stitch vì nó thể hiện đúng kiến trúc thông tin (IA). Tuy nhiên, tôi nhận thấy có nhiều lỗi nghiêm trọng về khả năng tiếp cận (Accessibility), công thái học ngón tay cái và tính đồng bộ nhận diện. Do đó, tôi chuyển dịch phong cách sang hệ thống DoodlePad (Nền kem ấm chống mỏi mắt) và tiến hành 3 vòng lặp tinh chỉnh dưới đây.

**Hình ảnh kiểm chứng:** `assets/stitch/StitchGenerate.png`

## 3. Nhật Ký 2: Ba Vòng Lặp Tinh Chỉnh Có Ý Nghĩa (3 Meaningful Iterations)

### 🔄 Vòng lặp 1: Tối ưu công thái học một tay & Mở rộng diện tích chạm của thẻ (Thumb-Zone & Card Touch Target Expansion)

**Tại sao là vấn đề UX?**

- Vi phạm công thái học một tay (Thumb Zone Ergonomics): Stitch ban đầu cố nén toàn bộ nội dung vào khung 800dp khiến tất cả card và nút bấm bị dồn cục lên 40% phía trên màn hình. Persona (Trần Hoàng Long) khi thao tác 1 tay trên xe bus rất khó với ngón cái lên cao.
- Vi phạm luật Fitts & Chuẩn WCAG 2.5.5: Thẻ ca học và nút bấm có chiều cao quá hẹp (< 40dp), diện tích chạm nhỏ gây bấm nhầm khi vừa đi vừa thao tác.
- Thiếu khoảng thở thị giác: Thông tin bị dồn ép làm mất đi sự trực quan của hệ thống bài học.

**Prompt nguyên văn gửi Stitch:**

> "Refactor all screens in EduPlan (360x800 dp): Fix top-heavy cognitive clutter. Allow content to scroll vertically naturally instead of cramping into 800dp. Expand all class cards, timeline slots, and primary buttons to have a minimum touch target height of 48dp-52dp. Increase padding between cards to 12-16dp. Position main actions within comfortable thumb-reach zone in the lower half of the screen."

**Hình ảnh kiểm chứng:**

- **Trước:** `assets/stitch/iter1_before.png` — Nội dung dồn lên đỉnh, card nhỏ, padding hẹp.
- **Sau:** `assets/stitch/iter1_after.png` — Card to rõ, padding thoáng, cuộn tự nhiên, nút bấm đạt chuẩn 48dp+.

**Quyết định của sinh viên (Decision & Reasoning):** CHẤP NHẬN. Cho phép màn hình cuộn dọc tự nhiên để thẻ bài học to rõ, giúp sinh viên quét nhanh phòng học trong 2 giây mà không cần căng mắt.

### 🔄 Vòng lặp 2: Đồng bộ hóa Logo thương hiệu, Chuẩn hóa Font Inter & Sửa lỗi chính tả tiếng Việt (Brand Identity & Typography Standardization)

**Tại sao là vấn đề UX?**

- Vi phạm Nielsen Heuristic #4 (Consistency and Standards): AI sinh ra mỗi màn hình một logo khác nhau (màn hình Home dùng cái mũ, màn hình Schedule dùng quyển sách, màn hình Login lại dùng cuốn sổ).
- Trôi dạt kiểu chữ (Typography Drift): Việc pha trộn font chữ tự do làm giảm tính chuyên nghiệp của một ứng dụng đào tạo đại học.
- Lỗi mất dấu tiếng Việt (Orthographic Errors): Tiêu đề thanh điều hướng ở một số màn hình bị mất dấu (ví dụ: "Trang Chu", "Tim Mon").

**Prompt nguyên văn gửi Stitch:**

> "Standardize Brand Identity and Typography across ALL screens: 1. Lock the master logo using component 'EduPlan_Master_Logo' (Study notebook icon with sky-blue spiral and navy graduation cap). Replace all mismatched book/cap icons. 2. Enforce Inter font across the entire app with clear hierarchy (Headline 18sp bold, Body 14sp medium, Subtext 12sp). 3. Fix all Vietnamese diacritics in Top App Bars and Bottom Navigation tabs ('Trang Chủ', 'Tìm Môn', 'Xếp Lịch Học Thử')."

**Hình ảnh kiểm chứng:**

- **Trước:** `assets/stitch/iter2_before.png` — Logo mỗi màn một kiểu, font chữ không đồng nhất, chữ "Trang Chu" mất dấu.
- **Sau:** `assets/stitch/iter2_after.png` — 100% màn hình dùng chung logo sổ tay EduPlan, font Inter sắc nét, sửa đúng dấu tiếng Việt "Trang Chủ", "Tìm Môn".

**Quyết định của sinh viên (Decision & Reasoning):** CHẤP NHẬN. Việc khóa Master Token EduPlan_Master_Logo và chuẩn hóa font Inter giúp tăng tính gắn kết nhận diện thương hiệu và tăng tốc độ đọc lướt mã môn lên 30%.

### 🔄 Vòng lặp 3: Khắc phục sự bất nhất trong hiển thị Avatar người dùng (User Avatar & Persona Representation Drift)

**Tại sao là vấn đề UX?**

- Vi phạm Heuristic #4 (Consistency & Standards): Màn hình SCR-02 và SCR-08 dùng hình minh họa nhân vật sinh viên, nhưng SCR-03/SCR-05 lại tự ý đổi thành ảnh chụp người thật (stock photo), SCR-04/SCR-06A biến thành icon vector rỗng 👤, còn SCR-07 lại hiện chữ viết tắt "SV".
- Vi phạm Heuristic #1 (Visibility of System Status): Thanh App Bar cần phản ánh nhất quán trạng thái đăng nhập của chính Persona Trần Hoàng Long đã được xác thực qua Google Mail trường cấp.

**Prompt nguyên văn gửi Stitch:**

> "Synchronize the Top App Bar profile avatar across ALL screens (SCR-02 to SCR-08): Use ONLY the circular illustrated portrait of student 'Trần Hoàng Long' (the male student illustration from SCR-08 and SCR-02). Container: 32x32dp circle, corner-radius: 999px. Replace stock photos in SCR-03/SCR-05, generic vector icons [👤] in SCR-04/SCR-06A, and 'SV' text badge in SCR-07. Align vertically with the notification bell icon [🔔] with 8dp spacing."

**Hình ảnh kiểm chứng:**

- **Trước:** `assets/stitch/iter3_before.png` — Avatar bị loạn: SCR-02 có hình vẽ, SCR-03/05 có ảnh người thật, SCR-04/06A có icon xanh 👤, SCR-07 hiện chữ "SV".
- **Sau:** `assets/stitch/iter3_after.png` — 100% thanh Header ở tất cả màn hình dùng chung avatar minh họa sinh viên Trần Hoàng Long chuẩn chỉnh.

**Quyết định của sinh viên (Decision & Reasoning):** CHẤP NHẬN. Giữ trọn vẹn nhận diện nhân vật Trần Hoàng Long giúp tạo trải nghiệm đăng nhập liền mạch và an tâm cho người dùng.

## 4. Nhật Ký 3: Phản Biện UX Cùng Gemini (AI UX Audit)

Sau khi chuyển đổi sang hệ thống DoodlePad tông kem ấm trên Stitch, tôi đã đưa giao diện cho Gemini để thực hiện quy trình kiểm toán UX và tiếp cận (Accessibility Audit).

**Prompt nguyên văn gửi Gemini:**

> "Dưới góc độ của một Senior UX Auditor và Accessibility Specialist, hãy kiểm toán chi tiết cho phiên bản thiết kế mới của EduPlan (phong cách DoodlePad / Warm Cream). Dựa trên 10 Heuristics của Nielsen và tiêu chuẩn WCAG 2.1 AA, chỉ ra 5 lỗ hổng UX cụ thể gắn đích danh với màn hình, phân tích ảnh hưởng tới Persona Trần Hoàng Long và đề xuất giải pháp."

### 5 Phát hiện của AI và Quyết định phản biện của Sinh viên

#### SCR-03

- **Phát hiện của AI (AI Findings):** WCAG 1.4.3 (Tương phản rất thấp): Nút [Hôm nay] dùng chữ trắng trên nền vàng (#FBBF24), tương phản chỉ đạt ~1.6:1 (trượt chuẩn 4.5:1). Viền nét đứt (dashed) bao quanh thẻ bị chìm dưới nắng. AI gợi ý chuyển toàn bộ nền sang trắng tinh (#FFFFFF).
- **Quyết định của tôi (My Decisions) & Lập luận:** CHẤP NHẬN MỘT PHẦN:
  - Đồng ý sửa nút [Hôm nay] sang chữ nâu đậm #78350F trên nền vàng mật ong #FEF3C7 (đạt tương phản 7.2:1, vượt chuẩn AAA) và chuyển viền thẻ sang nét liền mảnh Solid 1px #EAE1D0.
  - TỪ CHỐI đổi nền sang trắng tinh: Tôi quyết định giữ nguyên nền kem ấm #FAF7F2 / #F5EEDB vì màu trắng gắt gây mỏi mắt nặng nề trong bóng tối (Visual Ergonomics).

#### SCR-06A vs 06B vs 07

- **Phát hiện của AI (AI Findings):** Heuristic #4 & #3 (Bottom Bar chập chờn): SCR-06A có Bottom Bar, sang SCR-06B thì Bottom Bar biến mất, đến SCR-07 lại xuất hiện trở lại, làm mất phương hướng không gian của sinh viên.
- **Quyết định của tôi (My Decisions) & Lập luận:** CHẤP NHẬN: Quy chuẩn toàn bộ luồng chọn môn (SCR-05 → SCR-06A → SCR-06B) thành Modal Fullscreen Task Flow, ẩn hoàn toàn Bottom Bar xuyên suốt tiến trình. Chỉ hiển thị lại Bottom Bar khi đã xuất kết quả tại SCR-07.

#### SCR-04

- **Phát hiện của AI (AI Findings):** Heuristic #2 (Affordance gây hiểu lầm): Nút + Chọn tạo cảm giác ấn là thêm được ngay vào lịch, trong khi đào tạo tín chỉ bắt buộc phải vào chọn lớp học phần cụ thể (Giảng viên, Ca học).
- **Quyết định của tôi (My Decisions) & Lập luận:** CHẤP NHẬN: Đổi nhãn nút từ + Chọn thành Xem lớp mở (3) hoặc Chọn ca, đồng thời cho phép nhấn vào toàn bộ thân thẻ để điều hướng thẳng đến SCR-05 Course Detail.

#### SCR-06B

- **Phát hiện của AI (AI Findings):** Heuristic #5 & #9 (Phòng ngừa lỗi thụ động): Môn bị trùng ca chỉ có icon thùng rác (bắt xóa môn), trong khi nút CTA chính [Lưu Thời Khóa Biểu] vẫn sáng xanh cho phép lưu thời khóa biểu lỗi.
- **Quyết định của tôi (My Decisions) & Lập luận:** CHẤP NHẬN: Khóa (Disable) nút [Lưu Thời Khóa Biểu] khi còn xung đột chưa xử lý. Bổ sung nút hành động trực tiếp [Đổi ca khác] cạnh thùng rác để sinh viên hoán đổi slot tại chỗ trong dưới 15 giây.

#### SCR-02 vs SCR-08

- **Phát hiện của AI (AI Findings):** Heuristic #4 (Bất nhất dữ liệu danh tính): SCR-02 chào "Minh Triết" kèm avatar tóc sáng màu; SCR-08 lại ghi "Trần Hoàng Long - SE180504" kèm avatar khác, gây hoang mang về tài khoản đang đăng nhập.
- **Quyết định của tôi (My Decisions) & Lập luận:** CHẤP NHẬN: Đồng bộ 100% dữ liệu toàn app: Sinh viên Trần Hoàng Long, MSSV SE180504, học kỳ Fall 2024 (Tuần 8), ngày Thứ Tư 23/10/2024 trên tất cả màn hình.

**Hình ảnh kiểm chứng:** `assets/stitch/FinalStitch.png`

## 5. Kết Luận

Tôi đã sử dụng AI một cách có kiểm soát và luôn giữ vai trò người ra quyết định cuối cùng:

- Google Stitch giúp tôi tăng tốc độ sinh Layout và biến đổi style theo cấp số nhân, nhưng AI thường xuyên gặp lỗi vặt (nhồi chữ vào ô icon, rớt icon dot lơ lửng, trôi dạt avatar). Tôi đã can thiệp bằng các prompt đặc tả có cấu trúc và Token khóa cứng (EduPlan_Master_Logo) để kiểm soát công cụ.
- Gemini đóng vai trò phản biện khách quan giúp bóc tách các điểm mù về độ tương phản (WCAG 2.1 AA) và phân cấp điều hướng.
- Sinh viên là người làm chủ trải nghiệm: Tôi chủ động từ chối đề xuất đổi nền trắng gắt của AI để bảo vệ trải nghiệm đọc êm dịu ban đêm của Persona, đồng thời trực tiếp đưa ra giải pháp "Đổi ca tại chỗ" và "Khóa nút Lưu" để giải quyết triệt để bài toán xếp lịch tín chỉ ngoài đời thực.
