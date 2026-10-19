# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Trương Hoàng Bảo Trân
- **MSSV:** 125001209
- **Tên đề tài Website:** Landing Page Giới Thiệu Phim Điện Ảnh Anime — *One Piece Film: Red (Kỷ Nguyên Mới)*
- **Công cụ AI đã sử dụng:** Antigravity AI / Gemini 3.8 Flash (kết hợp Vibe Coding IDE)

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> **Prompt tổng quan ban đầu:**
> *"Bạn là một Senior Frontend Developer có 10 năm kinh nghiệm trong thiết kế giao diện web UI/UX. Hãy viết mã nguồn hoàn chỉnh cho một Landing Page giới thiệu phim điện ảnh / Anime (One Piece Film: Red) bao gồm 2 file riêng biệt: index.html và style.css.*
> 
> *1. Yêu cầu cấu trúc Semantic HTML5 (Tối thiểu 5 thành phần chuẩn):*
> *- `<header>`: Chứa logo thương hiệu phim và menu điều hướng.*
> *- `<nav>`: Thanh điều hướng trang (Trang chủ, Cốt truyện, Nhân vật, Trailer, Liên hệ).*
> *- `<main>`: Khu vực nội dung chính chứa các section.*
> *- `<section>` & `<article>`: Chia khối rõ ràng. Phần danh sách nhân vật và nội dung cốt truyện bắt buộc sử dụng thẻ `<article>` để bọc từng bài viết/card nhân vật.*
> *- `<footer>`: Chân trang chứa thông tin bản quyền, thông tin sinh viên thực hiện và liên hệ.*
> *- Lưu ý: Tuyệt đối không lạm dụng thẻ `<div>` vô nghĩa khi đã có thẻ ngữ nghĩa HTML5 tương ứng.*
> 
> *2. Kỹ thuật CSS & CSS Variables:*
> *- Khai báo hệ thống biến ở `:root` trong style.css quản lý: màu sắc Cinema (`--primary-color`, `--bg-dark`, `--bg-card`), font chữ (`--font-main`), khoảng cách (`--spacing-sm`, `--spacing-md`, `--spacing-lg`), bán kính bo góc (`--radius-md`).*
> *- Sử dụng CSS Flexbox cho Layout của `<header>`, `<nav>`, và `<footer>`.*
> *- Sử dụng CSS Grid (`grid-template-columns: repeat(auto-fit, minmax(...))`) cho danh sách nhân vật và nội dung cốt truyện để tự động responsive.*
> 
> *3. Tương tác & Hiệu ứng Thư viện:*
> *- Tích hợp CDN Animate.css cho tiêu đề H1 và nút CTA ở Hero Section.*
> *- Tích hợp CDN AOS (Animate On Scroll) với các thuộc tính `data-aos` (fade-up, flip-left, zoom-in) cho từng `<section>` và `<article>`. Khởi tạo `AOS.init()` ở cuối file HTML.*
> *- Tự viết hiệu ứng `:hover` và `:focus` bằng CSS thuần cho các nút bấm (`.btn`) và thẻ (`.card`) với hiệu ứng nổi `transform: translateY(...)`, đổ bóng mượt mà, hỗ trợ phím Tab cho tính truy cập (Accessibility).*
> *- Yêu cầu: Tách riêng HTML và CSS, không sử dụng file Javascript tự viết."*

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & Hệ thống CSS Variables

- **Prompt đã dùng:**
  > *"Hãy xây dựng cấu trúc Semantic HTML5 chuẩn xác với đầy đủ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`. Tuyệt đối thay thế các thẻ `<div>` bọc không cần thiết bằng các thẻ ngữ nghĩa tương ứng (`<figure>`, `<figcaption>`, `<time>`, `<aside>`, `<address>`). Trong style.css, thiết lập toàn bộ biến tại `:root` theo chuẩn Cinema Palette (đỏ thẫm điện ảnh, đen rạp chiếu, hiệu ứng kính mờ glassmorphism), bố cục Flexbox cho Header/Nav/Footer và CSS Grid cho các thẻ `<article>`."*

- **Kết quả AI tạo ra:**
  - File `index.html` có đầy đủ các thẻ ngữ nghĩa chuẩn SEO và accessibility. Các card nhân vật và các hồi cốt truyện đều sử dụng `<article>`.
  - File `style.css` xây dựng một bảng biến `:root` khoa học: màu sắc, typography (`Outfit`, `Cinzel`), tỷ lệ spacing, radius và các bóng đổ neon/cinema.
  - Sử dụng layout CSS Grid `repeat(auto-fit, minmax(280px, 1fr))` giúp giao diện tự động co giãn đa màn hình mà không cần media queries phức tạp.

- **Nhận xét & Tinh chỉnh của SV:**
  - AI ban đầu có xu hướng dùng thẻ `<div>` để bọc ảnh và thông tin sinh viên. Tôi đã yêu cầu chuyển ảnh nhân vật vào thẻ `<figure>`, chuyển thông tin sinh viên ở `<footer>` vào thẻ `<address>` để đạt điểm tối đa tiêu chí chuẩn Semantic HTML5 (2.0 điểm).

---

### Lần 2: Tích hợp thư viện Animate.css, AOS và tối ưu tương tác thuần CSS

- **Prompt đã dùng:**
  > *"Tích hợp CDN Animate.css cho thẻ `<h1>` tiêu đề chính với hiệu ứng `animate__fadeInDown` và nút CTA với `animate__pulse animate__infinite`. Thêm thư viện AOS với các thuộc tính `data-aos='fade-up'`, `data-aos='flip-left'`, `data-aos='zoom-in'` vào các thẻ `<article>` và `<section>`. Viết hiệu ứng `:hover`, `:focus` và `:focus-visible` bằng CSS thuần cho nút bấm và thẻ card, đảm bảo khi người dùng nhấn phím Tab vẫn hiển thị viền sáng rõ ràng."*

- **Thách thức gặp phải:**
  - Yêu cầu đề bài ghi "không sử dụng JS", nhưng thư viện AOS bắt buộc phải có câu lệnh `AOS.init()` thì các hiệu ứng cuộn trang mới kích hoạt được.
  - Một số hiệu ứng `:hover` làm giật nhẹ layout nếu thay đổi thuộc tính `border` trực tiếp thay vì dùng `box-shadow` hoặc `transform`.

- **Cách sửa prompt (Debug prompt):**
  > *"Chỉ giữ lại duy nhất 1 đoạn mã inline script `<script>AOS.init({...})</script>` ở cuối `index.html` để khởi tạo thư viện theo yêu cầu, không tạo thêm bất kỳ file script.js tùy biến nào. Thay thế thay đổi border bằng thuộc tính `box-shadow` và `transform: translateY(-8px)` kết hợp `transition` mượt mà để chống giật khung hình."*

---

### Lần 3: Khởi tạo và đồng bộ thư mục tài nguyên hình ảnh (`assets/`)

- **Prompt đã dùng:**
  > *"Hãy tạo cho tôi 1 thư mục assets đã được sử dụng trong dự án, bao gồm logo thương hiệu, ảnh nền Hero Section và các ảnh đại diện nhân vật tương ứng."*

- **Kết quả AI tạo ra:**
  - Khởi tạo thư mục `assets/` gồm 7 tệp tài nguyên thực tế:
    1. `logo.svg`: Logo vector One Piece Film Red sắc nét chuẩn Cinema.
    2. `hero-bg.jpg`: Ảnh nền đại cảnh concert Utopia sân khấu điện ảnh (1376x768).
    3. `luffy.jpg`: Ảnh chân dung Monkey D. Luffy.
    4. `uta.jpg`: Ảnh chân dung ca sĩ Diva Uta.
    5. `shanks.jpg`: Ảnh chân dung Tứ Hoàng Shanks Tóc Đỏ.
    6. `poster.jpg`: Poster chính thức của bộ phim.
    7. `luffy.png`: Ảnh render trong suốt của nhân vật Luffy.
  - Đồng bộ liên kết ảnh vào các thẻ `<figure><img src="assets/..." class="character-img"></figure>` trong `index.html` và `background-image: url('assets/hero-bg.jpg')` trong `style.css`.

- **Nhận xét & Tinh chỉnh của SV:**
  - Bổ sung thuộc tính `loading="lazy"` cho tất cả các thẻ `<img>` để tối ưu tốc độ tải trang.
  - Thêm hiệu ứng phóng to ảnh nhẹ `.character-img { transition: ... }` khi rê chuột `:hover` vào `<article>`.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

### AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?
1. **Thiết lập hệ thống CSS Variables & Cinema Theme:** Thay vì phải tự tra cứu mã màu, tính toán từng thông số `rem`/`px` và viết thủ công hàng chục class màu sắc, AI tạo ngay một bảng biến toàn cục `:root` đồng bộ, chuẩn xác và mang đậm chất điện ảnh.
2. **Xây dựng bố cục Responsive Grid:** Kỹ thuật `grid-template-columns: repeat(auto-fit, minmax(...))` được AI áp dụng chính xác, giúp website hiển thị mượt mà trên cả Mobile, Tablet và Desktop mà không tốn hàng giờ viết Media Queries lẻ tẻ.
3. **Soạn thảo nội dung ngữ nghĩa & SVG:** AI hỗ trợ viết toàn bộ nội dung tiếng Việt chuẩn xác theo cốt truyện One Piece Film: Red và tạo sẵn file vector SVG cho logo giúp trang web hoàn thiện nhanh chóng.

### Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?
- **Đặt ra vai trò và ngữ cảnh rõ ràng:** Bắt đầu bằng việc chỉ định vai trò (*"Senior Frontend Developer có 10 năm kinh nghiệm UI/UX"*) giúp chất lượng code đầu ra chuyên nghiệp và tuân thủ các quy chuẩn thiết kế hiện đại hơn.
- **Quy định ràng buộc phủ định cụ thể:** Những câu lệnh như *"Tuyệt đối không lạm dụng thẻ `<div>`"*, *"Tách riêng HTML và CSS"*, *"Không tạo file script.js tùy biến"* là chìa khóa để AI không tự ý thêm các cấu trúc thừa thãi làm lệch yêu cầu chấm điểm.
- **Phát triển theo từng vòng lặp (Iterative Prompting):** Không nên nhồi nhét tất cả vào một lần sinh mã duy nhất; việc chia làm các bước: **Dựng khung Semantic -> Áp dụng CSS Styling -> Tích hợp Thư viện/Tương tác -> Hoàn thiện Assets & Debug** giúp kiểm soát mã nguồn 100% và dễ dàng phát hiện lỗi sai.
