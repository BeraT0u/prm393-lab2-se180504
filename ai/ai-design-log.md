# Nhật Ký Sử Dụng AI (AI Design Log) — EduPlan

Tài liệu này ghi lại toàn bộ quy trình tôi sử dụng trí tuệ nhân tạo (AI) trong giai đoạn thiết kế UI/UX theo nguyên tắc cốt lõi: **AI tạo ra; Sinh viên thẩm định và quyết định.**

---

## 1. Khai Báo Công Cụ AI Đã Sử Dụng

| Công cụ | Mục đích sử dụng |
| :--- | :--- |
| **Google Stitch** | Generative UI: Phác thảo và tạo layout giao diện mobile ban đầu (8 màn hình) từ các text prompt mô tả đặc tả yêu cầu. Dùng để thực hiện các vòng lặp tinh chỉnh giao diện. |
| **Gemini 3.8 Flash** | UX Audit: Đóng vai chuyên gia QA/UX để phản biện thiết kế giao diện dựa trên 10 Heuristics của Nielsen và tiêu chuẩn WCAG 2.1 AA. |

---

## 2. Nhật Ký 1: Tạo UI Ban Đầu Bằng Google Stitch (Initial Generation)

Tôi đã sử dụng Google Stitch để phác thảo nhanh 8 màn hình cốt lõi. Tôi thiết lập hệ thống màu nền tảng là Material Design 3, Dark Navy Theme (Background: #0F172A, Surface: #1E293B, Primary: #2563EB).

Dưới đây là các **Prompt nguyên văn (Verbatim Prompts)** tôi đã dùng cho các màn hình chính:

* **Prompt cho SCR-02 (Home Dashboard):**
  > *"Mobile app screen: "Home Dashboard" for a university course planning app named "EduPlan". Platform: Android mobile, dimensions: 360x800 dp. Style: Material Design 3, modern, clean, academic. Color palette: Primary Deep Blue (#1E40AF), background neutral light (#F8FAFC), surface cards (#FFFFFF), text primary (#0F172A), text secondary (#475569), success green (#16A34A). Layout structure (from top to bottom): 1. Top Bar: Greeting "Chào Long, 👋", subtitle "Học kỳ 1 • 2026-2027", user avatar on the right, offline sync cloud status icon. 2. Next Class Hero Card: Highlighted upcoming class today with a countdown timer "Bắt đầu sau 25 phút", subject name "Lập trình Di động (PRM393)", slot time "09:30 - 11:50 (Slot 2)", room "BE-302", lecturer name "Ths. Nguyen Van A". 3. KPI Credit Progress Card. 4. Upcoming 3-Day Schedule List. 5. Floating Action Button (FAB): Prominent circular button (56x56 dp) at the bottom right. 6. Bottom Navigation Bar (4 destinations). Ensure all touch targets are at least 48x48 dp."*

* **Prompt cho SCR-04 (Course Catalog):**
  > *"Mobile app screen: "Course Catalog" for university course planner app "EduPlan". Platform: Android mobile, dimensions: 360x800 dp. Style: Material Design 3. Primary color: Deep Blue (#1E40AF), background: #F8FAFC, card surface: #FFFFFF. Layout structure: 1. Top App Bar: Title "Danh Mục Môn Học", back arrow icon on the left, search icon. 2. Search Bar: Rounded input field (8dp radius) with search icon. 3. Filter Chips (horizontal scroll): "Tất cả", "Chuyên ngành (SE)", "Cơ sở ngành", "3 Tín chỉ", "4 Tín chỉ". Active chip highlighted. 4. Course List (vertical scroll of cards, 12dp radius, 8dp spacing): Card 1: Code badge "PRM393" (primary blue), Title "Lập trình Di động Cross-platform", Credits badge "3 TC", "4 lớp đang mở ca học", chevron right icon. 5. Bottom Navigation Bar: Course Catalog tab is active."*

*(Ghi chú: Các màn hình SCR-01, 03, 05, 06, 07, 08 cũng được tạo bằng prompt tương tự với cùng hệ màu và kiến trúc).*

**Quyết định của tôi:** 
Tôi **Chấp nhận (Accepted)** kết quả bố cục cơ bản từ Stitch vì nó thể hiện đúng kiến trúc thông tin (IA). Tuy nhiên, tôi nhận thấy có nhiều lỗi về Usability, do đó tôi tiến hành 3 vòng lặp tinh chỉnh dưới đây.
    **Hình ảnh kiểm chứng:**
    `(..\assets\stitch\StitchGenerate.png)`
---

## 3. Nhật Ký 2: Ba Vòng Lặp Tinh Chỉnh Có Ý Nghĩa (3 Meaningful Iterations)

### 🔄 Vòng lặp 1: Nhiễu thị giác và phân tán hành động trên màn hình Đăng nhập
* **Tại sao là vấn đề UX?** Người dùng chưa đăng nhập thì việc hiện một bảng thời khóa biểu giả phía sau không có ý nghĩa gì, nó làm tăng gánh nặng nhận thức (Cognitive Load - Heuristic #8 của Nielsen). Hơn nữa, nó đẩy nút "Đăng nhập bằng Google" (Primary CTA) xuống tít đáy, khiến sinh viên phải tìm kiếm.
* **Prompt nguyên văn gửi Stitch:**
  > *"Refactor the SCR-01 Login screen: Remove the fake schedule preview table completely. Center the middle card with the 'Sign in with Google' button vertically on the screen (Hero Centered Layout). Keep the screen focused solely on a single call-to-action."*
* **Hình ảnh kiểm chứng:**
  * Trước: `![Before](../assets/stitch/iter1_before_login.png)`
  * Sau: `![After](../assets/stitch/iter1_after_login.png)`
* **Quyết định (Decision):** **CHẤP NHẬN**. Màn hình mới giúp sinh viên hiểu ngay lập tức phải làm gì trong 2 giây đầu, không bị phân tâm bởi dữ liệu rác.

### 🔄 Vòng lặp 2: Mơ hồ trong tương tác và thiếu vùng chạm trên Thẻ môn học
* **Tại sao là vấn đề UX?** Thẻ môn học ban đầu chỉ có một icon mũi tên `>` nhỏ (< 24dp), không rõ bấm vào thẻ là để xem chi tiết hay thêm môn (Vi phạm Nielsen #7). Kích thước chạm vi phạm chuẩn WCAG 2.5.5 (Tối thiểu 48x48 dp).
* **Prompt nguyên văn gửi Stitch:**
  > *"Refactor the Course Catalog screen (SCR-04 'Danh Mục Môn Học'). On every course card, remove the tiny chevron arrow '>' at the bottom right. Replace it with two prominent, dedicated icon buttons aligned at the bottom-right with 8dp spacing: (1) 'View Detail' icon button (Info icon, 48x48 dp touch target, subtle container); (2) 'Add to Plan' icon button (Calendar-plus icon, filled Primary Blue #2563EB, 48x48 dp touch target). Prioritize large icon buttons over text to maximize tap target and avoid visual clutter."*
* **Hình ảnh kiểm chứng:**
  * Trước: `![Before](../assets/stitch/iter2_before_card.png)`
  * Sau: `![After](../assets/stitch/iter2_after_card.png)`
* **Quyết định (Decision):** **CHẤP NHẬN**. Việc tách làm 2 icon to (Xem chi tiết ℹ️ và Thêm 📅+) giúp rút ngắn thời gian thao tác chọn môn xuống dưới 15 giây đúng như mục tiêu của Persona.

### 🔄 Vòng lặp 3: Sự bất nhất của thanh điều hướng và phân tán điểm kích hoạt
* **Tại sao là vấn đề UX?** Stitch tạo thanh Bottom Navigation bất nhất (có màn 5 tab, có màn 4 tab) vi phạm Heuristic #4. Nút Floating Action Button (+) xuất hiện tràn lan ở màn hình Home và Lịch học làm loãng luồng thao tác.
* **Prompt nguyên văn gửi Stitch (Sửa hàng loạt):**
  > *"Refactor Screen 2 (Home Dashboard): REMOVE the Floating Action Button (FAB with '+' icon) at the bottom right completely. Course registration must only be accessible via the bottom navigation bar."*
  > *"Refactor bottom navigation bar on SCR-05 and SCR-07: Replace the current 5 tabs with exactly 4 standard tabs: 1. 'Trang chủ' (Home icon), 2. 'Lịch học' (Calendar icon), 3. 'Đăng ký môn' (Book icon) -> ACTIVE state (#2563EB), 4. 'Cá nhân' (Person icon). Ensure the sticky bottom bar with action buttons sits directly above this 4-item bottom bar. Maintain Dark Navy theme (#0F172A, #1E293B)."*
* **Hình ảnh kiểm chứng:**
  * Trước: `![Before](../assets/stitch/iter3_before_nav.png)`
  * Sau: `![After](../assets/stitch/iter3_after_nav.png)`
* **Quyết định (Decision):** **CHẤP NHẬN**. Đưa toàn bộ app về chuẩn 4 tab đồng nhất, xóa sạch nút (+) nổi. Từ chối chèn Bottom Bar vào SCR-06 (Chi tiết môn) vì đây là màn hình cấp 2 cần diện tích để đọc thông tin.

---

## 4. Nhật Ký 3: Phản Biện UX Cùng Gemini 3.8 Flash (AI UX Audit)

Sau khi hoàn thiện cơ bản trên Stitch, tôi đã đưa giao diện cho Gemini 3.8 Flash để nhờ kiểm toán (Audit).

### Prompt nguyên văn gửi Gemini 3.8 Flash:
> *"Bạn là một Chuyên gia Thẩm định UX/UI và Accessibility. Hãy phản biện giao diện cho đồ án 'EduPlan' trên Android Mobile (360x800 dp). Persona: Nam sinh viên 20 tuổi, thao tác một tay bằng ngón cái khi đi xe bus, mạng 4G chập chờn. YÊU CẦU: Dựa trên 10 Heuristics của Jakob Nielsen và tiêu chuẩn WCAG 2.1 AA, hãy chỉ ra 5 lỗ hổng UX thực tế, gắn đích danh với màn hình và đề xuất giải pháp."*

### 5 Phát hiện của AI và Quyết định của tôi:

| Màn hình | Phát hiện của AI (AI Findings) | Quyết định của tôi (My Decisions) & Lập luận |
| :--- | :--- | :--- |
| **SCR-03** | **Heuristic #6:** Nút chuyển tuần và nút `[Hôm nay]` bị neo quá cao. Người dùng cầm máy 1 tay không thể với ngón cái tới được nếu không đổi thế tay. | **CHẤP NHẬN:** Tôi quyết định đưa thanh cuộn xuống thấp hơn và thêm cử chỉ vuốt ngang màn hình (Swipe). Điều này khớp hoàn toàn với hành vi thao tác 1 tay của Persona. |
| **SCR-05** | **WCAG 2.1 (Tương phản):** Ô trùng lịch dùng chữ đỏ trên nền đen tối sẫm, độ tương phản < 4.5:1, không thể đọc rõ dưới ánh nắng ngoài trời. | **CHẤP NHẬN:** Thay vì chỉ dùng màu đỏ, tôi thêm biểu tượng ⚠️ và nhãn text "TRÙNG CA" nổi bật. Đáp ứng chuẩn WCAG 1.4.1 (Không truyền đạt thông tin chỉ bằng màu sắc). |
| **SCR-06** | **Lỗi Overlap:** Nút CTA "Thêm vào Kế hoạch" ở đáy che lấp vùng cuộn nội dung, không có Safe Area. | **CHẤP NHẬN:** Tôi sửa lại bằng cách thêm `padding-bottom` 24dp bên dưới nội dung cuộn để nội dung không bao giờ bị nút nổi che khuất. |
| **SCR-04** | **Fitts's Law:** Các nút lọc (Chips) quá nhỏ và sát nhau, thao tác đi xe rung lắc dễ bấm nhầm. | **CHẤP NHẬN:** Tôi mở rộng khoảng cách padding giữa các Filter Chips lên 8dp và nâng chiều cao tối thiểu lên 32dp để dễ chạm hơn. |
| **Toàn app**| **Heuristic #1:** Mạng chập chờn nhưng ứng dụng không có dấu hiệu thông báo đang xem dữ liệu cũ (Offline) hay dữ liệu mới (Online). | **CHẤP NHẬN:** Thêm thanh micro-banner "Đang xem dữ liệu ngoại tuyến" và tính năng Pull-to-refresh (Kéo để làm mới) giúp sinh viên luôn kiểm soát được trạng thái lịch học. |
* **Hình ảnh kiểm chứng:**
  *  `![Before](..\assets\stitch\FinalStitch.png)`
  
---

## 5. Kết Luận

Tôi đã sử dụng AI một cách có kiểm soát. Google Stitch giúp tăng tốc độ dựng Layout gấp 10 lần, nhưng tôi là người trực tiếp ra quyết định cấu trúc (ép về 4 tab) và dùng Gemini để vá các lỗ hổng khả năng tiếp cận (Accessibility) trước khi đưa thiết kế cuối cùng sang Figma.