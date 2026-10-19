# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)
- **Họ và tên:** Đinh Quốc Đạt
- **MSSV:** 125001643
- **Tên đề tài Website:** DQPorsche - Trang quản lý bán xe Porsche
- **Công cụ AI đã sử dụng:** Claude

## 1. Yêu cầu ban đầu (System/Initial Prompt)
> Đọc kỹ tài liệu đề kiểm tra giữa kỳ (đính kèm file PDF).
> Quy định: chỉ sử dụng HTML và CSS, không sử dụng cái khác.
> Thông tin cần thiết: họ tên SV Đinh Quốc Đạt, MSSV 125001643, tên đề tài "trang quản lý bán xe Porsche", công cụ AI đã sử dụng là Claude, tên trang web là DQPorsche.
> Sử dụng hình ảnh thật cho xe, không sử dụng những hình ảnh tượng trưng.

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung website (Semantic HTML, CSS Variables, Animate.css, AOS)
- **Prompt đã dùng:** Như prompt ban đầu ở mục 1 (kèm file PDF đề bài).
- **Kết quả AI tạo ra:**
  - `index.html` dùng `<header>`, `<nav>`, `<main>`, 4 `<section>`, `<article>` cho từng xe, `<dl>` cho số liệu, `<table>` cho đơn hàng, `<form>` đặt cọc và `<footer>`.
  - `style.css` khai báo màu, font, spacing, bo góc trong `:root`; dùng Grid và Flexbox để responsive.
  - Animate.css cho tiêu đề và nút CTA ở hero; AOS (`data-aos`) cho các section và thẻ xe; hiệu ứng `:hover`, `:focus-visible` tự viết cho menu, nút, thẻ xe, ô nhập liệu.
  - 6 mẫu xe dùng ảnh thật: 911 Carrera S, 911 GT3 Touring, Taycan 4S, 718 Cayman, 911 Carrera 4S, 911 Carrera RSR 1974.
- **Nhận xét & Tinh chỉnh của SV:**
  - Trang cần thể hiện đúng chủ đề "quản lý bán xe", nên ngoài danh sách xe còn có phần tổng quan số liệu, trạng thái từng xe (còn hàng, đặt cọc, đã bán, đang về), bảng đơn hàng gần đây và phiếu đặt cọc.
  - Hình ảnh phải là ảnh thật của xe, nên đã dùng ảnh từ Wikimedia Commons và ghi nguồn, giấy phép ảnh ở chân trang.
- **Thách thức gặp phải:**
  - Quy định "chỉ dùng HTML và CSS" mâu thuẫn với yêu cầu tích hợp AOS, vì AOS cần một dòng khởi tạo `AOS.init()`.
  - Môi trường làm việc của AI không tải được ảnh về máy nên không thể lưu ảnh vào thư mục `assets/`.
- **Cách sửa prompt (Debug prompt) / Cách xử lý:**
  - Chấp nhận đúng một thẻ `<script>` nhỏ để khởi tạo AOS (thư viện bắt buộc theo đề), không viết thêm JavaScript nào khác.
  - AI tìm đúng tên tệp ảnh trên Wikimedia Commons và nhúng trực tiếp bằng đường dẫn; thư mục `assets/` để trống.

### Lần 2: Đổi màu hiện đại, đổi font, thêm thống kê doanh thu
- **Prompt đã dùng:** "Chỉnh lại màu sắc cho hiện đại hơn, sử dụng phông chữ phù hợp hơn với web, thêm phần thống kê doanh thu của tháng."
- **Kết quả AI tạo ra:**
  - Bảng màu mới: xanh đen slate cho chữ và chân trang, nền xám nhạt xen kẽ trắng, đỏ Porsche chỉ làm điểm nhấn; nút bo tròn, thẻ bo góc lớn hơn.
  - Font đổi từ Barlow Condensed và IBM Plex Sans sang Plus Jakarta Sans (tiêu đề) và Inter (nội dung), đều hỗ trợ tiếng Việt.
  - Section mới `#doanh-thu` gồm biểu đồ cột theo tuần và biểu đồ thanh theo dòng xe, vẽ hoàn toàn bằng HTML/CSS (biến `--v` điều khiển độ dài).
- **Nhận xét & Tinh chỉnh của SV:**
  - Các biểu đồ chỉ dùng dữ liệu mẫu nhưng phải khớp với nhau: 9,6 + 15,2 + 12,4 + 16,8 = 17,8 + 14,5 + 11,6 + 5,2 + 4,9 = 54,0 tỷ ₫ từ 7 xe, tăng 12% so với tháng 9 (48,2 tỷ ₫).
  - Số doanh thu ở phần Tổng quan ban đầu là 62,4 tỷ ₫, không khớp với phần mới, nên đã sửa thành 54,0 tỷ ₫.
- **Thách thức gặp phải:** Không dùng thư viện biểu đồ (vì chỉ được dùng HTML và CSS).
- **Cách sửa prompt (Debug prompt) / Cách xử lý:** Dựng biểu đồ bằng danh sách `<ul>` và CSS (chiều cao, độ rộng tính từ biến `--v`), giữ nguyên số liệu hiển thị bằng chữ để dễ đọc và dễ truy cập.

### Lần 3: Nâng cấp animation (scroll, hover, parallax, loading, navbar, micro-interaction)
- **Prompt đã dùng:** Yêu cầu nâng cấp giao diện bằng animation hiện đại, mượt mà, gồm: scroll animation, hover, page transition, parallax, micro-interaction, navbar khi cuộn, loading, background effect. Quy tắc kèm theo: giữ nguyên cấu trúc, nội dung và phong cách; không viết lại toàn bộ; ưu tiên `transform` và `opacity`; thời lượng 200-700ms; responsive; hỗ trợ `prefers-reduced-motion`; phân tích cấu trúc trước rồi mới triển khai và kiểm tra lỗi.
- **Kết quả AI tạo ra (chỉ bằng HTML/CSS):**
  - Màn hình loading ngắn, hero chờ loader xong mới xuất hiện chữ.
  - Navbar nền mờ kính, đổ bóng hiện dần và thanh tiến trình đỏ chạy theo vị trí cuộn.
  - Parallax ảnh hero, quầng sáng đỏ trôi nhẹ ở hero.
  - Ảnh xe "mở" dần khi cuộn; các cột và thanh doanh thu mọc lên khi cuộn tới.
  - Hover nâng thẻ xe, vệt sáng quét qua nút chính, gạch chân menu trượt ra; hiệu ứng lún khi bấm nút.
  - Menu hamburger trên mobile, tab lọc xe theo trạng thái (CSS-only), form báo viền xanh hoặc đỏ khi nhập hợp lệ hoặc sai.
  - `@view-transition` cho chuyển trang, và tắt toàn bộ chuyển động khi `prefers-reduced-motion`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Hiệu ứng cuộn nâng cao (scroll-driven animation) chỉ chạy trên Chrome, Edge, Safari mới; trình duyệt khác bỏ qua và trang vẫn hiển thị đầy đủ nội dung.
  - Không thêm hiệu ứng hạt (particles) vì cần JavaScript hoặc canvas, và để tránh rối mắt.
- **Thách thức gặp phải:**
  - Hiệu ứng nâng thẻ xe khi hover (dùng `transform`) bị xung đột với `transform` mà AOS gán cho cùng phần tử.
  - Khi bật `prefers-reduced-motion`, nếu tắt animation mà không xử lý thì màn hình loading sẽ che kín trang.
  - Không dùng JavaScript nên menu mobile không tự đóng sau khi chọn mục.
- **Cách sửa prompt (Debug prompt) / Cách xử lý:**
  - Chuyển hiệu ứng nâng thẻ sang thuộc tính `translate` riêng, không đụng đến `transform` của AOS.
  - Thêm quy tắc ẩn hẳn loader (`display: none`) khi người dùng bật giảm chuyển động.
  - Chấp nhận menu mobile đóng bằng cách bấm lại nút hamburger.

## 3. Đánh giá cá nhân về quá trình Vibe Coding
*(Bản nháp dựa trên quá trình làm bài, bạn nên đọc lại và sửa bằng lời của mình.)*
- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?** Dựng nhanh toàn bộ khung HTML ngữ nghĩa, CSS Variables, bố cục Grid/Flexbox, và tìm đúng ảnh xe thật có giấy phép sử dụng. Các biểu đồ doanh thu và hiệu ứng nâng cao cũng được viết bằng CSS thuần mà không cần thư viện.
- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**
  - Nêu rõ ràng buộc ngay từ đầu (chỉ HTML và CSS, ảnh thật, tên trang) giúp kết quả đúng hướng ngay lần đầu.
  - Prompt càng có quy tắc cụ thể (giữ nguyên cấu trúc, thời lượng animation, hỗ trợ giảm chuyển động) thì AI càng ít phải sửa lại.
  - Nên yêu cầu AI kiểm tra lại số liệu và xung đột giữa các hiệu ứng, vì lỗi thường nằm ở những chỗ này (số liệu không khớp, hai hiệu ứng cùng dùng `transform`).

---
*Nguồn ảnh xe: Wikimedia Commons (Alexander Migl, CC BY-SA 4.0; 多多123, CC BY 4.0; các tác giả khác theo trang tệp gốc).*
