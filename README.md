# PRM323 — Lab 2: Thiết Kế UI/UX Có Hỗ Trợ AI (EduPlan)

* **Môn học:** PRM323 — Cross-Platform Application Development
* **Sinh viên:** Nguyễn Trọng Hiếu
* **MSSV:** SE180504
* **Đề tài:** Student Course Planner — Ứng dụng lập kế hoạch chọn môn học và thời khóa biểu cho sinh viên hệ tín chỉ.
* **Persona:** Sinh viên năm 3 ngành Kỹ thuật Phần mềm, thao tác một tay khi di chuyển, cần tra cứu lịch nhanh và tự động phát hiện trùng ca học.

---

## 🔗 Liên Kết Sản Phẩm

* **Link Figma chính thức:** https://www.figma.com/design/p43KeBybC7w5tNvRGnYj0G/PRM393_Lab2_SE180504?m=auto&t=O9vQsxHv7CW7vW6e-1


---

## 🛠️ Công Cụ AI Đã Sử Dụng

1. **Google Stitch:** Hỗ trợ tạo bố cục UI ban đầu và thực hiện 3 vòng lặp tinh chỉnh giao diện.
2. **Gemini 3.8 Flash:** Đóng vai trò chuyên gia UX Audit, phản biện giao diện theo 10 Heuristics của Jakob Nielsen và tiêu chuẩn WCAG 2.1 AA.

---

## 🗺️ Bản Đồ Cấu Trúc Dự Án (Repository Map)

* **`ux/`**:
  * `persona.md`: Chân dung người dùng chi tiết, bài toán thực tế và tiêu chí thành công đo được.
  * `user-flow.md`: Kiến trúc thông tin (IA) và 3 luồng người dùng hoàn chỉnh (vẽ bằng Mermaid).
* **`design/`**:
  * `DESIGN.md`: Hệ thống Design Tokens (Màu sắc Academic Matte Dark, Typography Inter, Spacing 8dp).
  * `screen-spec.md`: Đặc tả ý đồ thiết kế và nội dung cho toàn bộ 8 màn hình.
  * `design-decisions.md`: 10 quyết định thiết kế then chốt và bảng kiểm tra tiếp cận (WCAG 2.1 AA).
* **`ai/`**:
  * `ai-design-log.md`: Nhật ký sử dụng AI đầy đủ gồm prompt nguyên văn, 3 vòng lặp tinh chỉnh (Before/After) và bảng quyết định xử lý 5 phát hiện phản biện.
* **`assets/`**:
  * `stitch/`: Chứa ảnh chụp các phiên bản thử nghiệm ban đầu và các vòng lặp từ Google Stitch.
  * `figma/`: Chứa ảnh PNG trích xuất từ 8 màn hình cuối cùng trên Figma.
* **`handoff/`**:
  * `flutter-handoff.md`: Tài liệu đặc tả kỹ thuật chuyển giao cho lập trình viên Flutter (chuẩn bị cho Lab 3).