# Agent Templates & Skills Architecture

Kho chứa cấu hình AI Agent chuyên nghiệp (cho Antigravity, Kiro, Cursor, Windsurf...). Hệ thống này biến AI thành các kỹ sư thực thụ có kỷ luật, tuân thủ chặt chẽ các workflows (quy trình) và rules (quy chuẩn) của công ty thay vì code tự do.

## 🏗 Cấu trúc Monorepo

Dự án này sử dụng kiến trúc Agent 2 lớp, cực kỳ phù hợp cho cả dự án đơn (Single Stack) và Monorepo (Multi Stack):

```text
Class-AI-Agent/
├── .agents/                                ← TẦNG GLOBAL (Dành cho mọi dự án)
│   ├── mcp.json                            ← Cấu hình Model Context Protocol (Figma, DB...)
│   ├── workflows/                          ← Các Slash Commands Dùng Chung (/deploy, /review)
│   └── skills/                             ← Các Rule / Skill chung (Database, Kiến trúc hệ thống)
│
└── apps/
    └── mobile-app/                         ← TẦNG DỰ ÁN (Project Specific)
        └── .agents/                        ← Tương đương "Plugin" cho React Native Developer
            ├── FIGMA_MCP_SETUP.md          ← HDSD Figma cho AI
            ├── SKILL.md                    ← Phác thảo tính cách, stack của AI Agent
            ├── rules/                      ← 17 Quy chuẩn bắt buộc (Clean code, i18n, caching...)
            └── workflows/                  ← 15 Lệnh nghiệp vụ (Slash commands đặc thù)
                ├── commit-push.md          ← Tự động check test, gõ commit
                ├── analyze-spec.md         ← Phân tích spec, bẻ task
                └── do-task.md              ← Thực thi task end-to-end có check design
```

## 🚀 Các Gói Kỹ Năng Hiện Có

### 1. Mobile Developer Agent (`apps/mobile-app/.agents/`)
Một Senior React Native Developer ảo với bộ kỷ luật thép:
- **17 Mandatory Rules**: Code style, Offline Caching, State Management (Zustand), Navigation, Security, Animation...
- **15 Workflows**: `/analyze-spec`, `/do-task`, `/new-screen`, `/new-service`, `/commit-push`, `/write-tests`...
- **Figma MCP Integration**: Tự động đọc link Figma để tạo mã nguồn Pixel-perfect (Auto Map Design Tokens).

### 2. Các Kỹ Năng Đang Phát Triển (`.agents/skills/`)
- API Conventions
- Database Architecture 
- Project Structure
- Systems Architect

## 🎯 Cách Cài Đặt (Cho Dự Án Mới)

Sử dụng hệ thống này cho dự án thực tế của bạn bằng cách cực kỳ đơn giản: **Copy-Paste thư mục `.agents` mạnh nhất vào gốc dự án của bạn!**

### Kịch bản 1: Cài đặt Agent cho dự án Mobile (React Native)
Chỉ cần copy thư mục `apps/mobile-app/.agents` vào thư mục dự án React Native của bạn.

```bash
# Đứng tại thư mục React Native của bạn
cp -R /path/to/Class-AI-Agent/apps/mobile-app/.agents .
```
> Khi mở AI Editor lên, bạn gõ lệnh `/do-task` hoặc `/new-screen` — AI sẽ tự động load toàn bộ kiến thức của Senior Mobile Dev.

### Kịch bản 2: Cài đặt cho hệ thống Global / Monorepo lớn
Nếu dự án của bạn có đủ combo Web, App, Backend:
1. Copy gốc `.agents/` chung vào Root của Monorepo.
2. Copy `apps/mobile-app/.agents/` vào thẳng thư mục App của thiết bị di động trong repo đó.

## 🧠 Tiêu Chuẩn Nâng Cao
- **Write-Tests Enforced**: Hệ thống tự chặn quá trình `git commit` nếu AI nhận ra đang làm tính năng mới hoặc fix bug mà chưa có file Unit Test (`/write-tests`).
- **Tối ưu Prompt / Model**: Có rule chỉ định loại AI cho task (`/analyze-spec` dùng Opus/Pro, Test đơn giản dùng Flash) để cân đối chi phí và tốc độ.
- **Figma Native**: Không cần screenshot, chỉ cần cung cấp link Figma design node.

---
*Created and Maintained for AI Agents Ecosystem.*
