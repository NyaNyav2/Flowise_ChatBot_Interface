🤖 Chatbot Hỏi Đáp Hướng Dẫn (LLM + Flowise)
📌 Giới thiệu

Dự án này xây dựng một chatbot hỏi đáp thông minh dựa trên LLM và Flowise, cho phép người dùng đặt câu hỏi liên quan đến tài liệu hướng dẫn và nhận câu trả lời chính xác, có kèm hình ảnh minh họa ngay trong giao diện chat.

Hệ thống bao gồm:

Backend: Flowise với luồng agent được thiết kế tối ưu

Frontend: Giao diện chat HTML/CSS/JS thuần

Dữ liệu: Tài liệu hướng dẫn được chuẩn hóa + ảnh base64

🧠 Quy trình xây dựng dự án
1️⃣ Chuẩn bị dữ liệu (Data Preparation)

Phân tích 2 tài liệu hướng dẫn gốc

Cắt gọn, chuẩn hóa nội dung và chuyển sang định dạng Markdown (.md)
→ giúp LLM dễ đọc, dễ trích xuất thông tin

Toàn bộ hình ảnh trong tài liệu:

Chuyển sang Base64

Gán ID định danh dạng {{IMG_xxx}}

Lưu vào file JSON (images_map_v5.json)

📌 Mục tiêu:

Giúp LLM hiểu nội dung + ngữ cảnh hình ảnh mà không cần truy cập file ảnh gốc.

2️⃣ Xây dựng luồng Agent trong Flowise (Backend)

Thiết kế luồng agent trong Flowise để:

Phân loại câu hỏi

Điều hướng đến agent phù hợp

Trả lời đúng vai trò/ngữ cảnh

Tối ưu:

Độ chính xác

Phủ nhiều trường hợp câu hỏi

Hạn chế hallucination

📷 Sơ đồ luồng agent trong Flowise:
<img width="1075" height="681" alt="Screenshot 2026-02-03 113021" src="https://github.com/user-attachments/assets/22624c8e-3ef6-47f6-991d-307f6917e621" />

3️⃣ Xây dựng Frontend Chatbot

Frontend được xây dựng bằng HTML + CSS + JavaScript thuần, không phụ thuộc framework.

✨ Tính năng chính

💬 Giao diện chat hiện đại, responsive

🔄 Kết nối trực tiếp tới Flowise API

🧠 Lưu lịch sử chat theo session

🔁 Tạo phiên trò chuyện mới

🖼️ Hiển thị ảnh từ placeholder {{IMG_xxx}}

✍️ Hỗ trợ Markdown:

Bold / Italic

Link

Danh sách

⏳ Typing indicator khi bot đang trả lời

🗂️ Cấu trúc & logic chính
🔹 API kết nối Flowise
const API_URL = "https://flowisetenant.demozone.vn/api/v1/prediction/xxxx";

🔹 Quản lý session

Mỗi phiên chat có SESSION_ID

Lưu trong sessionStorage

Lịch sử chat tách biệt theo từng phiên

🔹 Quản lý ảnh Base64

File JSON chứa map:

{
  "IMG_001": "data:image/png;base64,..."
}


Trong câu trả lời của LLM:

Xem hình minh họa {{IMG_001}}


Frontend tự động render thành <img />

🚀 Cách sử dụng

Clone repo

Đặt file images_map_v5.json cùng thư mục HTML

Mở trực tiếp file .html trên trình duyệt
(hoặc deploy lên server tĩnh)

Bắt đầu chat 🎉

⚠️ Lưu ý quan trọng
Cache busting cho ảnh

Mỗi lần cập nhật ảnh bắt buộc tăng version:

const IMAGES_VERSION = 2;


Điều này giúp:

Tránh cache cũ

Đảm bảo ảnh mới được load đúng

🎯 Kết quả đạt được

Chatbot trả lời đúng ngữ cảnh tài liệu

Hiển thị hình ảnh minh họa trực tiếp trong hội thoại

Frontend gọn nhẹ, dễ mở rộng

Backend linh hoạt nhờ Flowise Agent

📌 Hướng phát triển tiếp theo (Optional)

Thêm streaming response

Đăng nhập người dùng

Lưu lịch sử chat vào database

Phân quyền agent theo vai trò
