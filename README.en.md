# Lunar Gateway — AI API Gateway

<p align="center">
  <img src="https://agent.devkit.vn/favicon.svg" width="80" alt="Lunar Gateway logo" />
</p>

<p align="center">
  <strong>A unified API gateway with OpenAI-compatible endpoints, providing seamless access to multiple top-tier AI models.</strong>
</p>

<p align="center">
  <a href="https://agent.devkit.vn">🌐 agent.devkit.vn</a>
</p>

---

## Overview

**Lunar Gateway** is a server system that provides a centralized API Gateway for AI models, allowing users to access various Large Language Models (LLMs) through **a single API endpoint** compatible with the OpenAI standard.

The web application at **agent.devkit.vn** serves as the user interface, built with React + Vite. It offers a comprehensive experience including model discovery, interactive chat playground, account management, and API key administration.

---

## Key Features

### 🎯 Centralized API Gateway
- **One endpoint, many models:** Connect to a single API (`/v1`) to access all supported AI models.
- **OpenAI-compatible:** Uses the familiar OpenAI API format, making integration with existing applications, libraries, and tools straightforward.
- **Centralized management:** Monitor and control API usage through a unified dashboard.

### 💬 Playground Chat
- Intuitive chat interface for trying AI models directly in the browser.
- Markdown rendering with syntax highlighting.
- Quick model switching to compare response quality.

### 🤖 Diverse AI Models
- Access multiple LLMs from various providers.
- Browse and search models with detailed information.
- Free / premium model classification for easy selection.

### 🔐 Authentication & Security
- Account registration and login system.
- Personal API key management for third-party integrations.
- Role-based access control (user / admin).

### 🌙 Modern UI
- Minimal, modern design with **light / dark** mode support.
- Multi-language support (Vietnamese / English).
- Responsive layout — works great on desktop and mobile.

### ⚙️ Admin Dashboard
- System usage statistics (users, requests, models, …).
- Manage users, API keys, and models.
- Administrative dashboard for system operations.

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│                      Users                           │
├────────────────────┬────────────────────────────────┤
│  agent.devkit.vn   │   Third-party Apps / Tools     │
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

Lunar Gateway provides an API compatible with the OpenAI standard, making integration simple.

**Base endpoint:**
```
https://agent.devkit.vn/v1
```

**API call example (OpenAI-compatible):**

```bash
curl https://agent.devkit.vn/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {"role": "user", "content": "Hello!"}
    ]
  }'
```

You can use existing OpenAI SDKs (Python, Node.js, …) — just point the `base_url` to Lunar Gateway.

---

## Web Interface

Visit **[agent.devkit.vn](https://agent.devkit.vn)** to explore:

| Page          | Description                                        |
|---------------|----------------------------------------------------|
| **Landing**   | Overview of the system and key features            |
| **Playground**| Chat directly with AI models                       |
| **Models**    | Browse the list of available AI models             |
| **Docs**      | API documentation and usage guides                 |
| **Admin**     | System administration dashboard (admin only)       |

---

## Technology Stack

### Frontend (agent.devkit.vn)
- **React 19** — UI framework
- **Vite** — Build tool
- **React Router** — SPA navigation
- **CSS Variables** — Light/dark theming
- **Google Fonts (Inter, JetBrains Mono)** — Typography
- **Material Symbols** — Icon system

### Backend (Lunar Gateway Server)
- OpenAI-compatible API
- Multi-model support (GPT, Claude, Gemini, …)
- API key authentication
- Rate limiting & quota management

---

## User Benefits

### 👨‍💻 Developers
- **Easy integration:** One API key, one integration — access multiple AI models.
- **Reduced complexity:** No need to manage multiple accounts and API endpoints from different providers.
- **OpenAI SDK compatible:** Reuse your existing codebase with a simple `base_url` change.

### 🏢 Enterprises
- **Centralized management:** A single dashboard to track usage and costs across your entire team.
- **Access control:** Granular permissions and API key management for each member.
- **Cost efficiency:** Flexibly choose the right model for each task.

### 🧑‍🎓 General Users
- **Seamless experience:** Chat with AI directly through a beautiful web interface — no setup required.
- **Many choices:** Compare and pick the model that best fits your needs.
- **Vietnamese support:** Interface and content available in Vietnamese.

---

## Related Links

- **Website:** [agent.devkit.vn](https://agent.devkit.vn)
- **GitHub:** [github.com/mrbit-dev/Lunar-Gateway](https://github.com/mrbit-dev/Lunar-Gateway)
- **Report issues & Suggestions:** [Issues](https://github.com/mrbit-dev/Lunar-Gateway/issues)

---

## License

This project is licensed under the [MIT](LICENSE) license.

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/mrbit-dev">mrbit-dev</a>
</p>
