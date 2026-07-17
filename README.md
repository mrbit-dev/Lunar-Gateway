# Lunar Gateway — AI API Gateway

<p align="center">
  <img src="https://agent.devkit.vn/favicon.svg" width="80" alt="Lunar Gateway logo" />
</p>

<p align="center">
  <strong>Một cổng API tập trung, tương thích OpenAI, cung cấp quyền truy cập thống nhất vào nhiều mô hình AI hàng đầu.</strong>
</p>

<p align="center">
  <a href="https://agent.devkit.vn">🌐 agent.devkit.vn</a>
</p>

---

## Tổng quan

**Lunar Gateway** là một hệ thống server cung cấp cổng API (API Gateway) tập trung cho các mô hình AI, cho phép người dùng truy cập nhiều mô hình ngôn ngữ lớn (LLM) khác nhau thông qua **một endpoint API duy nhất**, tương thích chuẩn OpenAI.

Trang web **agent.devkit.vn** là giao diện người dùng của hệ thống, được xây dựng bằng React + Vite, cung cấp trải nghiệm toàn diện từ khám phá mô hình, chat thử nghiệm, đến quản lý tài khoản và API keys.

---

## Tính năng chính

### 🎯 API Gateway tập trung
- **Một endpoint, nhiều mô hình:** Chỉ cần kết nối đến một API duy nhất (`/v1`) để truy cập tất cả các mô hình AI được hỗ trợ.
- **Tương thích OpenAI:** Sử dụng định dạng API quen thuộc, dễ dàng tích hợp với các ứng dụng, thư viện và công cụ hiện có.
- **Quản lý tập trung:** Theo dõi và kiểm soát việc sử dụng API qua một dashboard thống nhất.

### 💬 Playground Chat
- Giao diện chat trực quan, thân thiện, cho phép dùng thử các mô hình AI trực tiếp trên web.
- Hỗ trợ markdown, code highlighting trong tin nhắn.
- Chuyển đổi nhanh giữa các mô hình để so sánh chất lượng phản hồi.

### 🤖 Đa dạng mô hình AI
- Truy cập nhiều mô hình ngôn ngữ lớn từ các nhà cung cấp khác nhau.
- Giao diện khám phá và tìm kiếm mô hình với thông tin chi tiết.
- Phân loại miễn phí/premium giúp người dùng dễ dàng lựa chọn.

### 🔐 Xác thực & Bảo mật
- Hệ thống đăng ký / đăng nhập tài khoản.
- Quản lý API key cá nhân để tích hợp với ứng dụng bên thứ ba.
- Phân quyền người dùng (user / admin).

### 🌙 Giao diện hiện đại
- Thiết kế tối giản, hiện đại với tùy chọn chế độ **sáng / tối**.
- Hỗ trợ đa ngôn ngữ (Tiếng Việt / English).
- Responsive, hoạt động tốt trên cả desktop và mobile.

### ⚙️ Admin Dashboard
- Thống kê sử dụng hệ thống (số lượng user, request, model, …).
- Quản lý người dùng, API keys, mô hình.
- Dashboard dành cho quản trị viên vận hành hệ thống.

---

## Kiến trúc hệ thống

```
┌─────────────────────────────────────────────────────┐
│                    Người dùng                        │
├────────────────────┬────────────────────────────────┤
│  agent.devkit.vn   │   Ứng dụng / Tool bên thứ ba   │
│  (Web App - React) │   (curl, LangChain, …)         │
└────────┬───────────┴────────┬───────────────────────┘
         │                    │
         │   REST API (HTTPS) │   OpenAI-compatible
         │                    │
         ▼                    ▼
┌─────────────────────────────────────────────────────┐
│              Lunar Gateway (API Server)              │
│         Endpoint: /v1 (OpenAI-compatible)            │
├─────────────────────────────────────────────────────┤
│  ┌─────────┐  ┌─────────┐  ┌─────────────────────┐  │
│  │ Auth &  │  │ Rate    │  │ Model Router         │  │
│  │ API Key │  │ Limiter │  │ (OpenAI, Claude,     │  │
│  │ Manager │  │         │  │  Gemini, Llama, …)   │  │
│  └─────────┘  └─────────┘  └──────────┬──────────┘  │
│                                        │             │
└────────────────────────────────────────┼─────────────┘
                                         │
                    ┌────────────────────┼────────────────────┐
                    ▼                    ▼                    ▼
              ┌──────────┐        ┌──────────┐        ┌──────────┐
              │ OpenAI   │        │  Claude  │        │  Gemini  │
              │ Models   │        │  Models  │        │  Models  │
              └──────────┘        └──────────┘        └──────────┘
```

---

## API

Hệ thống Lunar Gateway cung cấp API tương thích với chuẩn OpenAI, giúp việc tích hợp trở nên đơn giản.

**Endpoint cơ bản:**
```
https://agent.devkit.vn/v1
```

**Ví dụ gọi API (tương thích OpenAI):**

```bash
curl https://agent.devkit.vn/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {"role": "user", "content": "Hello! Xin chào!"}
    ]
  }'
```

Bạn có thể sử dụng các thư viện OpenAI SDK hiện có (Python, Node.js, …) chỉ cần thay đổi `base_url` trỏ đến Lunar Gateway.

---

## Giao diện web

Truy cập **[agent.devkit.vn](https://agent.devkit.vn)** để trải nghiệm:

| Trang         | Mô tả                                            |
|---------------|--------------------------------------------------|
| **Landing**   | Giới thiệu tổng quan về hệ thống, tính năng nổi bật |
| **Playground**| Chat trực tiếp với các mô hình AI                 |
| **Models**    | Khám phá danh sách các mô hình AI có sẵn          |
| **Docs**      | Tài liệu hướng dẫn sử dụng API                    |
| **Admin**     | Dashboard quản trị hệ thống (cho admin)           |

---

## Công nghệ sử dụng

### Frontend (agent.devkit.vn)
- **React 19** — UI framework
- **Vite** — Build tool
- **React Router** — Điều hướng SPA
- **CSS Variables** — Theme sáng/tối
- **Google Fonts (Inter, JetBrains Mono)** — Typography
- **Material Symbols** — Icon system

### Backend (Lunar Gateway Server)
- API tương thích chuẩn OpenAI
- Hỗ trợ đa dạng mô hình AI (GPT, Claude, Gemini, …)
- Xác thực qua API key
- Rate limiting & quota management

---

## Lợi ích cho người dùng

### 👨‍💻 Developer
- **Tích hợp dễ dàng:** Chỉ cần một API key duy nhất, code một lần là có thể truy cập nhiều mô hình AI khác nhau.
- **Giảm độ phức tạp:** Không cần quản lý nhiều tài khoản, nhiều API endpoint từ các nhà cung cấp khác nhau.
- **Tương thích OpenAI SDK:** Có thể dùng lại toàn bộ code hiện có.

### 🏢 Doanh nghiệp
- **Quản lý tập trung:** Một dashboard duy nhất để theo dõi chi phí và usage của toàn bộ đội nhóm.
- **Kiểm soát truy cập:** Phân quyền chi tiết, quản lý API keys cho từng thành viên.
- **Tiết kiệm chi phí:** Linh hoạt lựa chọn mô hình phù hợp với từng tác vụ.

### 🧑‍🎓 Người dùng phổ thông
- **Trải nghiệm liền mạch:** Chat trực tiếp với AI qua giao diện web đẹp, không cần cài đặt.
- **Nhiều lựa chọn:** Thoải mái so sánh và chọn mô hình phù hợp nhất với nhu cầu.
- **Hỗ trợ tiếng Việt:** Giao diện và nội dung hỗ trợ tiếng Việt.

---

## Cài đặt & Phát triển

### Yêu cầu
- Node.js 18+
- npm / yarn / pnpm

### Frontend

```bash
# Clone repository
git clone https://github.com/mrbit-dev/Lunar-Gateway.git
cd Lunar-Gateway

# Cài đặt dependencies
npm install

# Chạy môi trường phát triển
npm run dev

# Build production
npm run build
```

### Backend (API Server)
*Thông tin chi tiết về cách cài đặt và cấu hình backend sẽ được cập nhật sau.*

---

## Đường dẫn liên quan

- **Website:** [agent.devkit.vn](https://agent.devkit.vn)
- **GitHub:** [github.com/mrbit-dev/Lunar-Gateway](https://github.com/mrbit-dev/Lunar-Gateway)
- **Báo cáo lỗi & Đề xuất:** [Issues](https://github.com/mrbit-dev/Lunar-Gateway/issues)

---

## Giấy phép

Dự án được phát hành theo giấy phép [MIT](LICENSE).

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/mrbit-dev">mrbit-dev</a>
</p>
