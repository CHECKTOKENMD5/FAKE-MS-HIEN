# Security Policy

## 🛡️ Supported Versions

Dự án **English with Ms Hien — Vocab 12 Pro** là ứng dụng học từ vựng chạy hoàn toàn phía client (client-side only), được triển khai trên GitHub Pages. Chúng tôi chỉ hỗ trợ các phiên bản mới nhất.

| Version | Supported          | Notes                          |
| ------- | ------------------ | ------------------------------ |
| 12.x    | :white_check_mark: | Phiên bản hiện tại (Pro)       |
| 11.x    | :x:                | Đã ngừng hỗ trợ                |
| < 11.0  | :x:                | Không còn được bảo trì         |

---

## 📢 Reporting a Vulnerability

Nếu bạn phát hiện lỗ hổng bảo mật trong dự án này, **vui lòng KHÔNG tạo Issue công khai** trên GitHub. Thay vào đó, hãy báo cáo riêng tư để chúng tôi có thời gian khắc phục trước khi công bố.

### 📧 Cách báo cáo

Gửi email đến: **[your-email@example.com]**  
Tiêu đề: `[SECURITY] Vocab 12 Pro — <mô tả ngắn>`

Hoặc sử dụng tính năng **Private vulnerability reporting** của GitHub:
1. Vào tab **Security** của repository
2. Bấm **"Report a vulnerability"**
3. Điền form mô tả chi tiết

### 📋 Thông tin cần cung cấp

Để giúp chúng tôi xử lý nhanh chóng, vui lòng bao gồm:

- **Loại lỗ hổng** (XSS, injection, data leak, v.v.)
- **Mức độ nghiêm trọng** (Low / Medium / High / Critical)
- **Các bước tái hiện** (step-by-step reproduction)
- **Ảnh chụp màn hình / video** (nếu có)
- **Trình duyệt & phiên bản** đã test (Chrome 120, Safari iOS 17, v.v.)
- **Thiết bị** (điện thoại, tablet, desktop)
- **Ảnh hưởng tiềm năng** (impact)

---

## ⏱️ Response Timeline

Chúng tôi cam kết phản hồi theo khung thời gian sau:

| Bước                          | Thời gian cam kết      |
| ----------------------------- | ---------------------- |
| Xác nhận đã nhận báo cáo      | Trong vòng **48 giờ**  |
| Đánh giá sơ bộ ban đầu        | Trong vòng **5 ngày**  |
| Cập nhật tiến độ              | Mỗi **7 ngày**         |
| Vá lỗ hổng (nếu được chấp nhận)| Trong vòng **30 ngày** |
| Công bố công khai             | Sau khi đã vá xong     |

---

## 🏗️ Security Model & Scope

### Kiến trúc bảo mật

Ứng dụng này là **static HTML + JavaScript thuần**, chạy hoàn toàn trong trình duyệt của người dùng:

- ❌ **Không có backend server**
- ❌ **Không có database**
- ❌ **Không thu thập dữ liệu người dùng lên server**
- ❌ **Không sử dụng API bên thứ ba**
- ✅ **Toàn bộ dữ liệu lưu tại `localStorage` của trình duyệt**
- ✅ **Không có cookie, không có tracking, không có analytics**

### Dữ liệu được lưu trữ

Ứng dụng chỉ lưu **cục bộ trên thiết bị người dùng** (localStorage) các thông tin sau:

| Key                            | Nội dung                                     |
| ------------------------------ | -------------------------------------------- |
| `v12_profile`                  | Tên học sinh + mã số (MSSV)                  |
| `v12_progress_<MSSV>`          | Tiến độ học tập (từ đã biết, điểm quiz, v.v.)|
| `v12_theme`                    | Chế độ sáng/tối                              |
| `v12_pomo`                     | Trạng thái Pomodoro timer                    |
| `v12_tts_rate`                 | Tốc độ đọc giọng nói                         |

**⚠️ Lưu ý:** Dữ liệu này **KHÔNG** được gửi đi đâu cả. Xóa cache trình duyệt sẽ xóa toàn bộ dữ liệu học tập.

### Trong phạm vi (In Scope)

Các vấn đề sau **được coi là lỗ hổng** và sẽ được xử lý:

- ✅ **Cross-Site Scripting (XSS)** — chèn script độc hại qua dữ liệu từ vựng, tên học sinh, ghi chú
- ✅ **HTML Injection** — chèn HTML không mong muốn qua input của người dùng
- ✅ **Prototype Pollution** — tấn công vào các object JavaScript
- ✅ **Data leakage** — rò rỉ dữ liệu `localStorage` giữa các user khác nhau trên cùng thiết bị
- ✅ **Dependency vulnerabilities** — lỗ hổng từ thư viện bên ngoài (nếu có)
- ✅ **Denial of Service** — payload làm treo trình duyệt / vô hiệu hóa ứng dụng
- ✅ **Clickjacking** — nhúng iframe lừa đảo người dùng
- ✅ **CSRF** — mặc dù không có server, vẫn xem xét các luồng liên quan

### Ngoài phạm vi (Out of Scope)

Các vấn đề sau **KHÔNG** được coi là lỗ hổng của dự án này:

- ❌ Lỗ hổng của chính **trình duyệt** (Chrome, Safari, Firefox...)
- ❌ Lỗ hổng của **GitHub Pages** hoặc hạ tầng GitHub
- ❌ Lỗ hổng của **Google Fonts** hoặc CDN bên ngoài
- ❌ Tấn công vật lý (ai đó cầm máy tính của bạn)
- ❌ Dữ liệu bị mất do người dùng **xóa cache trình duyệt**
- ❌ Vấn đề về **nội dung từ vựng** (sai chính tả, dịch sai...) — vui lòng báo qua Issue thường
- ❌ Spam, lạm dụng báo cáo
- ❌ Social engineering vào giáo viên/học sinh

---

## 🔒 Security Best Practices cho người dùng

Vì đây là ứng dụng lưu dữ liệu **cục bộ trên thiết bị**, người dùng cần lưu ý:

### Đối với giáo viên

- 🔐 **Không** chia sẻ MSSV của học sinh với người lạ
- 💾 Nhắc học sinh **export tiến độ** (tính năng Profile → Export Data) định kỳ để backup
- 🚫 **Không** cài đặt extension trình duyệt không rõ nguồn gốc khi dùng máy chung
- 👥 Nếu dùng máy tính chung, nhớ **xóa cache** hoặc **sign out** sau mỗi buổi học

### Đối với học sinh

- 🔒 Không dùng MSSV của bạn bè để "học hộ"
- 🚪 **Sign out** khi dùng máy tính ở trường/thư viện
- 📱 Trên điện thoại cá nhân — dữ liệu an toàn, không cần lo lắng
- 📤 Export dữ liệu định kỳ để không mất tiến độ khi đổi máy

### Đối với developer

- 🔍 Review code trước khi merge PR
- ⚠️ Không dùng `innerHTML` với dữ liệu người dùng chưa escape
- ✅ Sử dụng `textContent` hoặc `escapeHtml()` cho mọi input của user
- 🧪 Test kỹ tính năng **ghi chú (Notes)** vì đây là điểm có thể bị XSS
- 📦 Kiểm tra dependency định kỳ: `npm audit` (nếu có build pipeline)

---

## 🛠️ Biện pháp bảo mật đã triển khai

Ứng dụng đã được thiết kế với các biện pháp bảo mật sau:

- ✅ **Escape dữ liệu đầu vào** — mọi dữ liệu từ user (notes, name, ID) đều được escape trước khi hiển thị
- ✅ **Không eval / new Function** — không sử dụng eval hoặc Function constructor
- ✅ **Không inline event handlers** trong dữ liệu động — tất cả event đều qua `addEventListener`
- ✅ **Content Security Policy** (khuyến nghị) — có thể bật qua meta tag khi deploy
- ✅ **Subresource Integrity** — Google Fonts được load với cross-origin an toàn
- ✅ **HTTPS only** — GitHub Pages tự động cung cấp HTTPS
- ✅ **Same-Origin Policy** — dữ liệu localStorage bị cô lập theo domain
- ✅ **Không lưu thông tin nhạy cảm** — không có mật khẩu, không có token, không có PII nhạy cảm

---

## 🌐 Third-Party Services

Ứng dụng sử dụng **tối thiểu** các dịch vụ bên ngoài:

| Service              | Mục đích               | Rủi ro                  | Mitigation                     |
| -------------------- | ---------------------- | ----------------------- | ------------------------------ |
| Google Fonts         | Hiển thị font đẹp      | Tracking (minor)        | Có thể self-host font nếu lo   |
| GitHub Pages         | Hosting                | Không đáng kể           | HTTPS tự động                  |
| Web Speech API       | Text-to-speech         | Chạy local (browser)    | Không gửi dữ liệu lên cloud    |

**Không sử dụng:**
- ❌ Google Analytics
- ❌ Facebook Pixel
- ❌ bất kỳ tracker / analytics nào
- ❌ bất kỳ backend / API tự dựng nào

---

## 📜 Responsible Disclosure

Chúng tôi áp dụng nguyên tắc **Coordinated Vulnerability Disclosure (CVD)**:

1. Bạn báo cáo riêng tư → chúng tôi xác nhận
2. Chúng tôi điều tra và vá lỗ hổng
3. Cả hai bên thống nhất thời điểm công bố công khai
4. Sau khi vá xong ≥ 30 ngày → bạn có thể công bố nghiên cứu của mình

Chúng tôi sẽ **ghi nhận đóng góp của bạn** trong mục `Acknowledgements` (nếu bạn đồng ý) và có thể tặng 1 phần quà nhỏ (sách, voucher...) tùy mức độ nghiêm trọng.

---

## 🙏 Acknowledgements

Xin chân thành cảm ơn những người đã đóng góp cho bảo mật của dự án:

<!--
  Danh sách các security researcher đã báo cáo lỗ hổng.
  Format: - [@username](https://github.com/username) — Mô tả ngắn lỗ hổng — Năm
-->

*Chưa có báo cáo nào. Bạn có thể là người đầu tiên!*

---

## 📚 Tham khảo

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [GitHub Security Best Practices](https://docs.github.com/en/code-security)
- [MDN Web Security](https://developer.mozilla.org/en-US/docs/Web/Security)
- [Content Security Policy Reference](https://content-security-policy.com/)

---

## 📞 Liên hệ

- **Email bảo mật:** [zaazvn44@gmail.com]

---

<div align="center">

**Cảm ơn bạn đã giúp cộng đồng học tiếng Anh an toàn hơn! 🛡️**

*Last updated: 2026*

</div>
