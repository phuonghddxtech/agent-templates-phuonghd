# Agent Templates & Skills Architecture

Kho chứa cấu hình AI Agent chuyên nghiệp (cho Antigravity, Kiro, Cursor, Windsurf...). Hệ thống này biến AI thành các kỹ sư thực thụ có kỷ luật, tuân thủ chặt chẽ các workflows (quy trình) và rules (quy chuẩn) của công ty thay vì code tự do.

## 🏗 Cấu trúc Monorepo

Dự án này sử dụng kiến trúc Agent 2 lớp, cực kỳ phù hợp cho cả dự án đơn (Single Stack) và Monorepo (Multi Stack). Các Agent được phân loại khép kín theo hệ sinh thái tương ứng của chúng:

```text
Class-AI-Agent/
├── .agents/                                ← TẦNG GLOBAL (Dành cho mọi dự án)
│   ├── mcp.json                            ← Cấu hình Model Context Protocol (Figma, DB...)
│   ├── workflows/                          ← Các Slash Commands Dùng Chung (/deploy, /review)
│   └── skills/                             ← Các Rule / Skill chung (Database, Kiến trúc hệ thống)
│
└── apps/
    ├── mobile-app/                         ← TẦNG DỰ ÁN (React Native Developer)
    │   └── .agents/                        
    │
    ├── laravel-vue/                        ← TẦNG DỰ ÁN (Laravel + Vue Fullstack)
    │   └── .agents/                        
    │
    └── python-api/                         ← TẦNG DỰ ÁN (Python Django Developer)
        └── .agents/                        
```

## 🚀 Các Gói Kỹ Năng Hiện Có

### 1. Mobile Developer Agent (`apps/mobile-app/.agents/`)
Một Senior React Native Developer ảo với bộ kỷ luật thép:
- **17 Mandatory Rules**: Code style, Offline Caching, State Management (Zustand), Navigation, Security, Animation...
- **15 Workflows**: `/analyze-spec`, `/do-task`, `/new-screen`, `/new-service`, `/commit-push`, `/write-tests`...
- **Figma MCP Integration**: Tự động đọc link Figma để tạo mã nguồn Pixel-perfect.

### 2. Fullstack Laravel + Vue Agent (`apps/laravel-vue/.agents/`)
Trợ lý Code Monolith nguyên khối chuẩn MVC hiện đại (không xài Headless API):
- **Core Rules**: Ép dùng Inertia.js renders, Vue 3 Composition API `<script setup lang="ts">`, bắt buộc tạo `FormRequest` và dùng `Action/Service` classes thay vì nhồi nhét logic vào Controller.
- **Workflows**: Viết sẵn `/new-page` (tạo luôn Controller, Route và Vue Interface cực nhanh), bắt test kỹ thuật với Pest/PHPUnit.

### 3. Python Backend Agent (`apps/python-api/.agents/`)
Trợ lý API công nghiệp (Django + DRF + Celery):
- **Core Rules**: PEP-8, Type Hints bắt buộc. Cấm truy vấn ORM lặp nhờ ép dùng `select_related`/`prefetch_related`. Ép quy chuẩn Celery Tasks Idempotency vững chãi.
- **Workflows**: `/new-api`, `/new-model`, ép viết Pytest/FactoryBoy trước khi git commit.

## 🎯 Cách Cài Đặt (Cho Dự Án Mới)

Sử dụng hệ thống này cho dự án thực tế của bạn bằng cách cực kỳ đơn giản: **Copy-Paste thư mục `.agents` mạnh nhất vào gốc dự án của bạn!**

### Kịch bản 1: Cài đặt Agent cho dự án độc lập (VD: Laravel-Vue)
Chỉ cần copy thư mục `apps/laravel-vue/.agents` vào thư mục dự án Laravel của bạn.

```bash
# Đứng tại thư mục Laravel của bạn
cp -R /path/to/Class-AI-Agent/apps/laravel-vue/.agents .
```
> Khi mở AI Editor lên, bạn gõ lệnh `/do-task` hoặc `/new-page` — AI sẽ tự động kích hoạt Agent Fullstack tương ứng.

### Kịch bản 2: Cài đặt cho hệ thống Monorepo khổng lồ
Nếu dự án của bạn có đủ combo App, Backend:
1. Copy gốc `.agents/` chung vào Root của Monorepo.
2. Copy `apps/mobile-app/.agents/` vào thẳng thư mục App của thiết bị di động trong repo đó.
3. Y hệt với Python/Laravel. Quá trình làm việc, gõ slash commands ở phân vùng nào thì Agent tương ứng mới được gọi lên làm việc! Tránh "đá chân" nhau hoàn hảo.

## 🧠 Tiêu Chuẩn Nâng Cao
- **Write-Tests Enforced**: Hệ thống tự chặn quá trình `git commit` nếu AI nhận ra đang làm tính năng mới hoặc fix bug mà chưa có file Unit Test (`/write-tests`).
- **Tối ưu Prompt / Model**: Có rule chỉ định loại AI cho task (`/analyze-spec` dùng Opus/Pro, Test đơn giản dùng Flash) để cân đối chi phí và tốc độ.
- **Figma Native**: Bắt cầu thẳng API Figma, tạo ứng dụng hoàn hảo mà không cần chụp screenshot màn hình.

---
*Created and Maintained for AI Agents Ecosystem.*
