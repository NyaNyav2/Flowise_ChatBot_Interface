# 🤖 Chatbot Hỏi Đáp Hướng Dẫn (LLM + Flowise)

## 📌 Giới thiệu

Dự án này xây dựng một **chatbot hỏi đáp thông minh** dựa trên **LLM** và **Flowise**, cho phép người dùng đặt câu hỏi liên quan đến tài liệu hướng dẫn và nhận câu trả lời chính xác, có kèm **hình ảnh minh họa** ngay trong giao diện chat.

Hệ thống bao gồm:

- **Backend**: Flowise (Agent-based workflow)
- **Frontend**: HTML / CSS / JavaScript thuần
- **Dữ liệu**: Tài liệu Markdown + ảnh Base64

---

## 🧠 Quy trình xây dựng dự án

### 1️⃣ Chuẩn bị dữ liệu

- Phân tích **2 tài liệu hướng dẫn gốc**
- Cắt gọn nội dung và **chuyển sang định dạng Markdown (.md)**  
  → giúp LLM dễ đọc và trích xuất thông tin
- Toàn bộ hình ảnh trong tài liệu:
  - Chuyển sang **Base64**
  - Gán **ID định danh** dạng `{{IMG_xxx}}`
  - Lưu trong file JSON (`images_map_v5.json`)

**Mục tiêu**:  
Giúp LLM hiểu được **nội dung văn bản + ngữ cảnh hình ảnh** mà không cần truy cập file ảnh gốc.

---

### 2️⃣ Xây dựng luồng Agent trong Flowise

- Thiết kế **luồng agent** trong Flowise để:
  - Phân loại câu hỏi
  - Điều hướng đến agent phù hợp
  - Trả lời đúng vai trò và ngữ cảnh
- Tối ưu:
  - Độ chính xác câu trả lời
  - Khả năng bao phủ nhiều trường hợp câu hỏi
  - Giảm hallucination

#### 📷 Sơ đồ luồng Agent

<img width="1075" height="681" alt="Screenshot 2026-02-03 113021" src="https://github.com/user-attachments/assets/22624c8e-3ef6-47f6-991d-307f6917e621" />

---

### 3️⃣ Xây dựng Frontend Chatbot

Frontend được xây dựng bằng **HTML + CSS + JavaScript thuần**, không sử dụng framework.

#### ✨ Tính năng chính

- 💬 Giao diện chat hiện đại, responsive
- 🔄 Kết nối trực tiếp tới Flowise API
- 🧠 Lưu lịch sử trò chuyện theo **session**
- 🔁 Tạo **phiên trò chuyện mới**
- 🖼️ Tự động hiển thị ảnh từ placeholder `{{IMG_xxx}}`
- ✍️ Hỗ trợ Markdown:
  - **In đậm**, *in nghiêng*
  - Link
  - Danh sách
- ⏳ Hiển thị typing indicator khi bot đang trả lời

---

## 🗂️ Cấu trúc dự án

```text
.
├── index.html
├── images_map_v5.json
├── images/
│   └── flowise-agent.png
└── README.md
