# QUY TRÌNH TROUBLESHOOTING NỘI BỘ & BUG REPORT TEMPLATE

## I. QUY TRÌNH 3 BƯỚC TRA CỨU BẮT BUỘC (SELF-TROUBLESHOOTING)
*Mục tiêu: Đảm bảo 80% các lỗi phổ biến về môi trường (Docker, Port conflict, Env...) được tự giải quyết trước khi gửi yêu cầu hỗ trợ lên kênh chat chung.*

```
[Bắt đầu gặp lỗi]
       │
       ▼
 ┌───────────┐      Thành công
 │  Bước 1   │ ───────────────────► [Đã giải quyết bug]
 │ Googling  │
 └─────┬─────┘
       │ Thất bại
       ▼
 ┌───────────┐      Thành công
 │  Bước 2   │ ───────────────────► [Đã giải quyết bug]
 │ Community │
 └─────┬─────┘
       │ Thất bại
       ▼
 ┌───────────┐      Thành công
 │  Bước 3   │ ───────────────────► [Đã giải quyết bug]
 │    AI     │
 └─────┬─────┘
       │ Thất bại
       ▼
 [Điền Bug Report Form & Gửi vào nhóm]
```

---

### Bước 1: Googling (Tra cứu bằng từ khóa chuẩn)
* **Quy tắc search:** Bỏ các từ vô nghĩa (như *"how to fix"*, *"help me"*). Chỉ giữ lại **[Tên công cụ/Thư viện] + [Mã lỗi hoặc Thông báo lỗi chính] + [Hệ điều hành/Phiên bản]**.
* **Công thức tìm kiếm nâng cao (Search Operators):**
  * Tìm kiếm chính xác cụm từ lỗi: `"port is already allocated"`
  * Giới hạn trang tìm kiếm: `site:stackoverflow.com "docker-compose up"`
  * Loại trừ thông tin nhiễu: `docker port conflict -kubernetes`
* **Thời gian tối đa:** 5 - 10 phút.

---

### Bước 2: Community Search (Tra cứu trên GitHub Issues & Forums)
* **Kênh tìm kiếm:** Tìm trực tiếp trên trang **GitHub Issues** của kho mã nguồn (Repository) đang dùng hoặc StackOverflow.
* **Bộ lọc ưu tiên:**
  1. Đọc các issue có nhãn `closed` (đã sửa xong) hoặc `OPEN` có nhiều reaction (👍, ❤️).
  2. Ưu tiên giải phát có bình luận gần đây (đặc biệt với Windows 11 / macOS Apple Silicon).
* **Quy tắc tìm Workaround:** Tìm giải pháp tạm thời (workaround) nếu issue chưa có bản vá chính thức.

---

### Bước 3: AI Translation & Analysis (Dịch & Phân tích bằng AI)
* **Đưa ngữ cảnh cho AI:** Không hỏi chung chung. Cung cấp log lỗi + đoạn mã hiện tại.
* **Sử dụng Prompt chuẩn phân tích lỗi:**
  > *"Tôi đang gặp lỗi sau khi chạy lệnh [Tên lệnh] trên môi trường [Hệ điều hành/Docker version]. Đây là log lỗi chi tiết: [Dán Log]. Hãy: 1. Dịch thông báo lỗi sang tiếng Việt dễ hiểu. 2. Nguyên nhân gốc rễ (Root cause) gây ra lỗi này là gì? 3. Cho tôi 2-3 hướng khắc phục kèm lệnh cụ thể."*
* **Cảnh báo an toàn (Anti-Hallucination):** Trước khi chạy các lệnh can thiệp hệ thống nguy hiểm (`rm -rf`, `sudo`, `setx PATH`), bắt buộc áp dụng Prompt kiểm chứng an toàn.

---

## II. BUG REPORT TEMPLATE (MẪU BÁO CÁO LỖI NỘI BỘ)

> **Quy định chung:** Thành viên **bắt buộc** điền đầy đủ mẫu sau vào kênh support (ví dụ: `#dev-help` trên Slack/Discord) khi cả 3 bước tra cứu tự động không thành công. Bài đăng không tuân thủ mẫu sẽ bị từ chối hỗ trợ.

```markdown
### 🐛 BUG REPORT: [Tóm tắt lỗi ngắn gọn]

#### 1. Context (Ngữ cảnh môi trường)
- **Hệ điều hành:** [Ví dụ: Windows 11 / macOS Sonoma M2 / Ubuntu 22.04]
- **Công cụ/Môi trường:** [Ví dụ: Docker v24.0.5 / Node.js v18 / Python 3.11]
- **Nhánh Git / Service bị ảnh hưởng:** [Ví dụ: branch `feature/auth` - Service `backend-api`]
- **Hành động dẫn đến lỗi:** [Ví dụ: Chạy lệnh `docker-compose up` sau khi pull code mới về]

#### 2. Expected (Kết quả kỳ vọng)
- [Mô tả chi tiết những gì đáng lẽ phải xảy ra. Ví dụ: Container `backend` khởi chạy thành công ở port 8080 và kết nối tới DB].

#### 3. Actual (Kết quả thực tế xảy ra)
- [Mô tả hành vi lỗi xảy ra. Ví dụ: Container báo lỗi gán port và tự động thoát (exit status 1)].

#### 4. Log & Visuals (Nhật ký lỗi & Hình ảnh)
- **Terminal Log (Dạng Text Code Block):**
```text
[Dán toàn bộ đoạn log lỗi chi tiết vào đây - KHÔNG CHỤP ẢNH MÀN HÌNH ĐỐI VỚI TEXT LOG]
```
- **Ảnh màn hình (nếu có lỗi trên giao diện GUI):**
[Chèn ảnh chụp tại đây]

---

#### 🔍 Kết quả sau 3 bước tự tra cứu (Bắt buộc điền)
- [x] **Googling:** Đã thử tìm cụm từ `...` nhưng chỉ thấy hướng dẫn cho Mac, máy hiện tại dùng Windows.
- [x] **Community:** Đã xem GitHub Issue #1234, thử cách đổi port `8080:8080` thành `8081:8080` nhưng vẫn báo bận.
- [x] **AI Analysis:** AI báo lỗi do tiến trình PID `4123` chiếm port, đã thử `kill` nhưng báo `Permission Denied`.
```

---

## III. QUY TẮC VẬN HÀNH TRÁNH TRÔI THÔNG TIN (CHAT OPS RULES)

1. **Một chủ đề = Một Thread:** Mọi thảo luận, hỏi đáp giải quyết lỗi bắt buộc phải nằm trong **Thread (Luồng)** của bài Bug Report đó. Không nhắn tin rời rạc vào channel chung.
2. **Đánh dấu trạng thái:**
   * 🟡 `[IN PROGRESS]`: Đang có người tiếp nhận hỗ trợ.
   * ✅ `[RESOLVED]`: Đã sửa xong. Người gửi lỗi phải reply lại vào Thread đáp án/cách xử lý thành công để lưu làm tài liệu cho người sau.
3. **Knowledge Base (Kho tri thức nội bộ):** Các lỗi lặp lại từ 2 lần trở lên sẽ được tổng hợp lại thành 1 trang *FAQ/Troubleshooting* trên Notion hoặc Wiki của nhóm.
