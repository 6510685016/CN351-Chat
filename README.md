# Chat

Real-time chat application intentionally built with security vulnerabilities for educational and testing purposes.

---

## Tech Stack
- React.js (Frontend)
- Node.js + Express + WebSocket (Backend)
- MongoDB (Database)
- Docker + Docker Compose

---

## Starting App

### 1. Clone and Setup
```bash
git clone https://github.com/6510685016/CN351-Chat.git chat
cd chat
docker-compose up --build
```

- Web App: http://localhost:3000
- API Server: http://localhost:3001

---

## 🛡 Known Vulnerabilities (Intentional)

- Passwords stored in **plain text**.
- No limit on failed login attempts (brute force possible).
- **Hardcoded session ID** for all users.
- **Directory listing** enabled at `/uploads`.
- Debug mode enabled (logs printed directly).
- No HTTPS (all traffic is unencrypted).
- **Client-side controls** (e.g., hide buttons using JavaScript only).

---

## How to Test Vulnerabilities

| Category | How to Test |
|:---|:---|
| Client-side control | Change `localStorage.role` to `admin` to see hidden buttons |
| Plaintext Passwords | Check MongoDB content, passwords are not encrypted |
| Brute Force Attack | Send massive login requests without block |
| Hardcoded Session ID | All users share the same session token |
| Directory Listing | Access http://localhost:3001/uploads to see files |
| Debug Mode | View server logs for sensitive information |
| No HTTPS | Capture network traffic to see sensitive data |

---

**DISCLAIMER:** This app is for testing purposes only. Do not deploy it in production environments.

---