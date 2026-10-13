# User Persona — EduPlan (Student Course Planner)

Tài liệu xác định chân dung người dùng mục tiêu, bối cảnh sử dụng và các rào cản hành vi làm căn cứ cho toàn bộ quyết định thiết kế UI/UX của EduPlan, tuân thủ Persona Guideline V1.0 (chuẩn 12 trường lõi).

---

## BẢNG TỔNG QUAN PHÂN KHÚC (PERSONA COVERAGE MATRIX)

| Mã | Tên đại diện | Archetype (Nhóm hành vi) | Vai trò hệ thống | Tác vụ trọng tâm | Khác biệt thiết kế cốt lõi |
| --- | --- | --- | --- | --- | --- |
| **P01** | **Trần Hoàng Long** (20t) | Sinh viên cơ động, tự chủ xếp lịch | **Primary Persona** | Xếp lịch nhanh, phát hiện & gỡ trùng ca học trong ≤15s | Thao tác 1 tay, nút bấm ≥48dp, cảnh báo màu + icon đa phương thức, Offline-first |
| **P02** | **Nguyễn Phương Linh** (19t) | Sinh viên cẩn trọng, kiểm soát lộ trình | **Secondary Persona** | Rà soát chỉ số tín chỉ, học phí & xuất file in PDF A4 | Thẻ KPI trực quan, preview bản in A4 (1:1.414), đồng bộ Google Calendar |

---

## P01 (PRIMARY PERSONA): TRẦN HOÀNG LONG

> *"Tôi muốn xem nhanh phòng học hôm nay trong 2 giây và tự xếp lịch mà không bao giờ bị trùng ca, không phải loay hoay làm đơn hủy môn phức tạp."*

### 12 Trường cốt lõi (Core Fields)

* **01. Identity & Archetype:** Trần Hoàng Long — *Sinh viên Kỹ thuật Phần mềm cơ động, tự chủ lập thời khóa biểu.*
* **02. Persona Priority:** **Primary Persona** (Định hình 100% kiến trúc điều hướng chính, ma trận lịch tuần 5×5 và luồng xử lý xung đột thời khóa biểu).
* **03. Usage Context:** Đứng đợi thang máy giảng đường, trên xe buýt, hành lang đổi phòng học; mạng 4G chập chờn; sự chú ý bị phân tán liên tục bởi tiếng ồn và việc di chuyển.
* **04. Goals:**
  * Tra cứu phòng học và ca học kế tiếp trong ngày trong vòng ≤2 giây chỉ với 1 lần mở app.
  * Tự do chọn và thử nghiệm các lớp học phần trước kỳ mới mà không bị xung đột giờ học.
  * Giải quyết ngay lập tức các xung đột lịch học ngay tại chỗ mà không cần thao tác lại từ đầu.
* **05. Job to Be Done (JTBD):** *"Khi chuẩn bị bước vào kỳ học mới hoặc trước giờ vào lớp, tôi muốn tra cứu ca học và tự động phát hiện trùng lịch ngay trên điện thoại, để tôi có thể lên lớp đúng giờ và không phải làm đơn hủy môn phiền toái."*
* **06. Current Behaviors:** Đăng nhập cổng web trường trên trình duyệt mobile (phải zoom to rất bất tiện), vẽ lại lịch ra Excel hoặc ghi chú Google Keep; chụp màn hình thời khóa biểu gửi vào nhóm chat Messenger.
* **07. Pain Points:**
  * **Xung đột ca học (Schedule Collision):** Đăng ký xong mới phát hiện 2 môn bị trùng Ca 2 sáng Thứ Ba, cổng trường không cảnh báo kịp thời.
  * **Cổng trường nghẽn mạng:** Web trường thường bị sập hoặc tải rất chậm vào giờ cao điểm điểm danh đầu ca.
  * **Lệch tuần học:** Các môn bắt đầu vào các tuần khác nhau (môn 10 tuần, môn 5 tuần) gây nhầm lẫn ngày bắt đầu môn mới.
* **08. Motivations:** Tốc độ phản hồi cực nhanh, độ chính xác tuyệt đối (0 trùng lịch), sự chủ động kiểm soát thời gian học và tính tiện lợi khi dùng một tay.
* **09. Constraints:** Kết nối mạng 4G không ổn định (hay mất sóng trong tầng hầm/thang máy); thiết bị tầm trung; thao tác bằng ngón cái khi đang đi lại.
* **10. Key Scenarios:**
  * *Scenario 1 (Tra cứu gấp):* Long bước ra khỏi bãi xe tầng hầm, mở app xem ngay thẻ Hero màn hình Home để biết mình học phòng BE-302 lúc 09:30 mà không cần mạng.
  * *Scenario 2 (Xử lý trùng ca):* Long chọn thêm môn IAE201 vào lịch, app rung cảnh báo đỏ ô Ca 2 T3 trên lưới. Long chạm nút `[Đổi ca khác]`, chuyển sang lớp Ca 4 và lưu thành công trong 12 giây.
* **11. Success Criteria:** Người dùng phát hiện và giải quyết xong 1 môn trùng ca học trong thời gian **dưới 15 giây**.
* **12. Evidence & Status:** **Proto-Persona** (Tổng hợp từ quan sát hành vi thực tế của 8 sinh viên K18 ĐH FPT trong đợt đăng ký môn Fall 2024; phỏng vấn nhanh 2 sinh viên chuyên ngành SE).

### Thông tin bắt buộc theo Lab 2 (Demographics & Accessibility)
* **Độ tuổi & Vai trò:** 20 tuổi • Sinh viên năm 3, ngành Kỹ thuật Phần mềm (SE).
* **Thiết bị:** Xiaomi Redmi Note 12 (Android 13, màn hình 6.67", phân giải 1080×2400 px, chuẩn viewport app 390×800 dp).
* **Nhu cầu Accessibility & Ergonomics:**
  * Vùng chạm tối thiểu **48×48 dp** cho mọi nút tương tác chính ở nửa dưới màn hình (phù hợp tầm với ngón cái).
  * Độ tương phản màu chữ/nền tối thiểu **4.5:1** (WCAG 2.1 AA) trên nền giấy kem Warm Paper chống lóa ngoài trời nắng.
  * Cơ chế lưu bộ nhớ đệm ngoại tuyến (Offline-first Cache) khi mất sóng.

---

## P02 (SECONDARY PERSONA): NGUYỄN PHƯƠNG LINH

> *"Tôi cần một bản tổng kết kế hoạch học tập rõ ràng để kiểm tra xem mình có học thiếu tín chỉ không và xuất file PDF in ra bàn học để đối chiếu học phí."*

### 12 Trường cốt lõi (Core Fields)

* **01. Identity & Archetype:** Nguyễn Phương Linh — *Sinh viên cẩn trọng, kiểm soát lộ trình đào tạo và học phí.*
* **02. Persona Priority:** **Secondary Persona** (Định hình thiết kế màn hình Tổng kết học kỳ SCR-07, cơ chế tính toán học phí, thẻ thống kê tiến độ SCR-08 và tính năng xuất file PDF A4).
* **03. Usage Context:** Tại bàn học phòng trọ vào buổi tối, kết nối Wi-Fi ổn định; tâm trạng tập trung, cần sự yên tĩnh và đọc kỹ từng thông số học tập.
* **04. Goals:**
  * Rà soát chính xác tổng số tín chỉ đăng ký (15 tín chỉ) để đảm bảo điều kiện xét học bổng và ra trường đúng hạn.
  * Xem dự toán học phí học kỳ chính xác trước khi nộp tiền.
  * Xuất bản in thời khóa biểu dạng PDF A4 chuẩn đẹp để dán góc học tập hoặc gửi cho phụ huynh và cố vấn học tập.
* **05. Job to Be Done (JTBD):** *"Khi đã hoàn tất việc sắp xếp các môn học trong kỳ, tôi muốn xem bảng tổng kết tín chỉ, học phí và xuất bản in PDF A4 chuẩn xác, để tôi an tâm về kế hoạch học tập của mình và lưu trữ tài liệu đối chiếu."*
* **06. Current Behaviors:** Dùng máy tính bỏ túi cộng thủ công từng môn; chụp màn hình nhiều đoạn trên web trường rồi ghép ảnh lại bằng ứng dụng bên thứ ba để gửi phụ huynh.
* **07. Pain Points:**
  * Web trường chỉ hiển thị danh sách dạng văn bản thô, không tính tổng học phí tạm tính.
  * Ảnh chụp màn hình điện thoại bị mờ, vỡ hạt khi in ra giấy A4 hoặc gửi qua Zalo.
  * Dễ bỏ sót các môn điều kiện tiên quyết nếu không có bảng tổng hợp đối chiếu.
* **08. Motivations:** Sự an tâm, tính minh bạch, sự chỉn chu trong học tập, giao diện dịu mắt khi sử dụng ban đêm.
* **09. Constraints:** Không quen với các biểu đồ kỹ thuật phức tạp; cần giao diện rõ ràng, phân cấp thị giác mạch lạc, xuất file nhanh chỉ với 1 click.
* **10. Key Scenarios:**
  * *Scenario 1 (Tổng kết kỳ):* Sau khi xếp xong 5 môn, Linh vào màn hình Tổng kết kế hoạch (SCR-07), nhìn thấy ngay thẻ xác nhận xanh "15 Tín chỉ • Kế hoạch hợp lệ ✅" và số tiền "14.250.000 đ".
  * *Scenario 2 (Xuất bản in):* Linh nhấn nút `[📄 Xuất file PDF (A4)]`, xem trước trang A4 thu nhỏ sắc nét và tải về máy trong 4 giây.
* **11. Success Criteria:** Người dùng hoàn tất việc xem lại chỉ số học kỳ và xuất thành công file PDF thời khóa biểu trong thời gian **dưới 10 giây**.
* **12. Evidence & Status:** **Proto-Persona** (Quan sát nhu cầu chia sẻ TKB và hỏi học phí trên diễn đàn sinh viên FPT; phỏng vấn nhanh 1 sinh viên nữ năm 2).

### Thông tin bắt buộc theo Lab 2 (Demographics & Accessibility)
* **Độ tuổi & Vai trò:** 19 tuổi • Sinh viên năm 2, chuyên ngành Kinh doanh quốc tế (học tín chỉ song ngành).
* **Thiết bị:** Samsung Galaxy A54 (Android 13, màn hình 6.4", chuẩn viewport 390×800 dp).
* **Nhu cầu Accessibility & Ergonomics:**
  * Bảng màu tone kem dịu mắt **Warm Paper Academic** (`#FBF6EB` / `#FFFDF7`) giúp giảm mỏi mắt và ức chế melatonin khi lập kế hoạch vào ban đêm.
  * Typography chuẩn chữ in ấn: Font Inter với Tabular Numbers giúp các con số học phí và mã phòng gióng thẳng hàng dọc dễ kiểm tra.

---

## TỪ PERSONA ĐẾN QUYẾT ĐỊNH THIẾT KẾ UI (MAPPING TABLE)

Bảng đối chiếu chứng minh mọi thành phần giao diện trên Figma đều bắt nguồn trực tiếp từ nhu cầu của 2 Persona (đáp ứng mục 04 Guideline):

| Persona | Vấn đề / Nhu cầu người dùng | Quyết định thiết kế trên Figma (UI Solution) | Phương pháp kiểm chứng (Validation) |
| --- | --- | --- | --- |
| **P01 - Long** | Cần xem phòng học trong 2 giây trước giờ vào lớp | Thẻ Hero Card nổi bật tại `SCR-02 (Home)` hiển thị ngay môn tiếp theo, phòng học, ca học và nút "Vào lớp" 48dp. | Đo thời gian hoàn thành tác vụ tra cứu trên màn hình Home (đạt ≤2s). |
| **P01 - Long** | Hay bị trùng ca học khi tự xếp lịch học phần | Ma trận tuần 5×5 tại `SCR-06A` tô đỏ sọc chéo ô Ca 2 T3 + Banner cảnh báo đa phương thức (WCAG 1.4.1). | Test kịch bản Flow 3: Người dùng phát hiện ngay ô xung đột. |
| **P01 - Long** | Nút lưu lịch bị bấm nhầm khi vẫn còn lỗi | Nút chân trang tại `SCR-06B` bị **VÔ HIỆU HÓA (Disabled)** màu xám; bổ sung nút `[⇄ Đổi ca khác]` để sửa lỗi tại chỗ. | Kiểm tra Heuristic #5 (Phòng ngừa lỗi): Không thể lưu lịch khi số lỗi > 0. |
| **P01 - Long** | Đi vào thang máy/tầng hầm mất mạng 4G | Banner thông báo chế độ ngoại tuyến tại `SCR-03` kết hợp cơ chế nạp dữ liệu từ Local Cache. | Test kịch bản bật Airplane Mode trên máy ảo Android. |
| **P02 - Linh** | Cần đối chiếu tổng tín chỉ và học phí dự kiến | Thẻ Hero KPI tại `SCR-07` gom cụm thông tin: 15 Tín chỉ, badge xanh "Kế hoạch hợp lệ ✅", học phí "14.250.000 đ". | Phỏng vấn người dùng về mức độ an tâm khi nhìn thấy thẻ tổng kết. |
| **P02 - Linh** | Cần in thời khóa biểu dán bàn học không bị mờ | Nút `[📄 Xuất file PDF (A4)]` tại `SCR-07` mở modal xem trước bản in khổ A4 (tỷ lệ 1:1.414). | Xuất thử file PDF và kiểm tra độ sắc nét trên thiết bị in thực tế. |
| **P02 - Linh** | Hay lên kế hoạch học tập vào ban đêm, dễ mỏi mắt | Hệ thống màu **Warm Paper Academic** (nền kem `#FBF6EB`, thẻ `#FFFDF7`, viền `#EAE1D0`) thay vì nền trắng tinh chói mắt. | Kiểm tra độ tương phản WCAG AAA (>12:1 cho chữ chính). |

---

## CÂU PHÁT BIỂU VẤN ĐỀ (PROBLEM STATEMENT)

> *"Sinh viên đại học học theo hệ tín chỉ cần một công cụ di động trực quan để vừa lập kế hoạch chọn môn không bị trùng lịch khi di chuyển, vừa theo dõi tổng quan tiến độ tín chỉ và xuất bản in thời khóa biểu chính quy, bởi vì việc quản lý thủ công và cổng thông tin web trường hiện tại thường xuyên gây xung đột ca học, quá tải máy chủ và thiếu các định dạng tài liệu lưu trữ tiện lợi."*

## TIÊU CHÍ THÀNH CÔNG ĐO ĐƯỢC (MEASURABLE SUCCESS METRICS)

1. **Hiệu suất chọn môn & sửa lỗi (P01):** Người dùng có thể thêm môn học mới và hoàn tất xử lý hoán đổi ca học trùng lịch trong thời gian **dưới 15 giây**.
2. **Hiệu suất xuất báo cáo học kỳ (P02):** Người dùng có thể rà soát toàn bộ 15 tín chỉ và xuất thành công file PDF thời khóa biểu A4 trong thời gian **dưới 10 giây**.