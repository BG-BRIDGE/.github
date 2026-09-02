<p align="center">
  <img src="https://bg-bridge.com/favicon.png" alt="BG-Bridge logo" width="112" />
</p>

<h1 align="center">BG-Bridge</h1>

<p align="center">
  连接校园、学习与成长。<br />
  Connecting campuses, learning, and everyday student life.
</p>

<p align="center">
  <a href="https://bg-bridge.com">访问 BG-Bridge / Visit BG-Bridge</a>
  ·
  <a href="#中文">中文</a>
  ·
  <a href="#english">English</a>
</p>

---

## 中文

BG-Bridge 是面向中国贝赛思国际学校和双语学校校园成员的跨校区社区平台。它把公开校园交流、学习资料共享和个人效率工具整合进一个响应式的中英双语应用。界面默认使用英文，登录后可在 Account 中切换中文。

### 核心功能

- **社区交流**：按频道浏览和搜索帖子，支持发帖、评论、点赞、收藏、投票、按需翻译与举报。
- **专注与任务**：提供沉浸式 Focus 计时器，以及简洁的个人 Todo 清单。
- **学习资料**：按课程查找和分享图片、文档、演示文稿、表格与视频资料。
- **校园墙**：通过有时间范围和主题的照片墙、留言墙记录校园活动。
- **账号资料**：使用已验证的学校邮箱登录，维护用户名、校区、年级、简介、头像、语言和可选密码。
- **社区治理**：提供内容举报、账号治理、公告、违禁词、内容下架与永久安全审计能力。

### 设计与安全原则

- 不提供私信或私聊，交流发生在可治理的公开社区中。
- 学校邮箱使用六位数字验证码登录；密码是可选入口，不是唯一恢复方式。
- 纯文字内容可直接发布；附件、资料和照片必须先通过可信的类型、大小与恶意内容检查。
- 文件保存在私有 Storage 中，通过短时授权链接访问。
- 已登录成员发布公开内容时，用户名和完整学校邮箱会随内容显示，发布界面会明确提示。
- 权限由数据库 RLS、RPC 和服务端 Function 强制执行，前端隐藏按钮不构成授权。
- 管理员不能读取成员的私有 Todo 或 Focus 数据。

### 当前状态

BG-Bridge 正在持续开发和分阶段部署。请按下面的状态理解功能，而不是把仓库中的所有代码都视为已经上线。

| 范围 | 状态 |
| --- | --- |
| 公开主页与 React 应用 | 已部署至 [bg-bridge.com](https://bg-bridge.com) |
| 六位验证码、核心资料、社区、Focus 与 Todo 基座 | 已在生产环境部署；仍持续做真实设备和权限回归 |
| 论坛附件、头像、学习资料与照片墙的可信文件流程 | 已在仓库实现；Storage、Function 和 Worker 仍需完成分阶段部署与验证 |
| 管理系统 v2、完整账号治理与永久审计 | 已本地实现并进入 staging 验证；尚未作为生产能力承诺 |
| 白名单富文本 | 已本地实现；后端迁移与生产验证尚未完成 |

### 技术栈

| 层级 | 技术 |
| --- | --- |
| Web | React 19、React Router 7、TypeScript 5、Vite 8、Tailwind CSS 4 |
| 数据与认证 | Supabase Auth、Postgres、RLS、Realtime、私有 Storage |
| 服务端 | Supabase Edge Functions、可信 Node.js 文件 Worker |
| 托管与安全 | Cloudflare Pages、Cloudflare Turnstile、Resend |
| 质量保障 | Vitest、ESLint、TypeScript、GitHub Actions |

### 本地开发

环境要求：Node.js 22、pnpm 11。

```bash
git clone https://github.com/BG-BRIDGE/bg-bridge.git
cd bg-bridge
corepack enable
pnpm install --frozen-lockfile
```

复制 `.env.example` 为 `.env`，至少填写浏览器可公开的 Supabase URL 和 publishable key。不要把 `service_role`、邮件密钥、翻译密钥或其他服务端 Secret 写入 `VITE_*` 变量或提交到仓库。

```bash
pnpm dev
```

本地 loopback 地址的开发构建在登录页提供只读式界面预览入口；它不会创建真实 Supabase 会话，也不会绕过 RLS、上传或管理权限。

常用质量命令：

```bash
pnpm typecheck
pnpm lint
pnpm test
pnpm build
pnpm --dir workers/trusted-file-worker test
pnpm worker:build
```

### 项目结构

```text
app/                         React 应用、路由、组件与前端 API
supabase/migrations/         数据库结构、RLS、RPC 与安全约束
supabase/functions/          认证、文件访问、翻译与账号治理 Function
workers/trusted-file-worker/ 文件扫描、预览、租约与清理 Worker
public/                      Cloudflare 路由、搜索元数据与品牌资源
.github/workflows/           持续集成质量门
```

### 参与贡献

提交较大改动前请先创建 Issue 说明问题和范围。Pull Request 应保持改动聚焦，并通过类型检查、Lint、测试和生产构建。安全问题不要公开披露，请通过仓库维护者提供的私密渠道报告。

仓库当前未包含开源许可证。除非维护者另行授权，公开可见不代表授予复制、修改或再分发权利。

---

## English

BG-Bridge is a cross-campus community platform for members of BASIS China international and bilingual school campuses. It brings public campus discussion, learning-resource sharing, and personal productivity tools into one responsive bilingual application. English is the default interface language, and Chinese can be selected from Account after sign-in.

### Core features

- **Community**: browse and search channel-based posts, then post, comment, like, save, vote, translate on demand, or report content.
- **Focus and tasks**: use an immersive Focus timer and a streamlined private Todo list.
- **Learning resources**: find and share images, documents, presentations, spreadsheets, and videos by course.
- **Campus walls**: capture campus activities through time-bound, themed photo and message walls.
- **Account profile**: sign in with a verified school email and manage a username, campus, grade, bio, avatar, language, and optional password.
- **Governance**: support reporting, account governance, announcements, prohibited terms, content takedowns, and permanent security auditing.

### Design and safety principles

- There are no direct messages or private chats; discussion stays in a governable public community.
- School email sign-in uses a six-digit code. A password is optional and is not the only account-recovery path.
- Text-only content can be published immediately. Attachments, resources, and photos must pass trusted type, size, and malware checks first.
- Files remain in private Storage and are accessed through short-lived authorized URLs.
- When signed-in members publish public content, their username and full school email are shown with it; the publishing flow states this clearly.
- Authorization is enforced by database RLS, RPCs, and server-side Functions. Hiding a frontend control is never treated as access control.
- Administrators cannot access members' private Todo or Focus data.

### Current status

BG-Bridge is under active development and staged rollout. The status below distinguishes code present in the repository from capabilities verified in production.

| Area | Status |
| --- | --- |
| Public landing page and React application | Deployed at [bg-bridge.com](https://bg-bridge.com) |
| Six-digit sign-in, core profiles, community, Focus, and Todo foundation | Deployed in production; real-device and permission regression testing continues |
| Trusted file flows for forum attachments, avatars, resources, and photo walls | Implemented in the repository; phased Storage, Function, and Worker deployment and verification remain |
| Management v2, complete account governance, and permanent auditing | Implemented locally and undergoing staging verification; not yet a production capability commitment |
| Allowlisted rich text | Implemented locally; backend migration and production verification remain |

### Technology

| Layer | Technology |
| --- | --- |
| Web | React 19, React Router 7, TypeScript 5, Vite 8, Tailwind CSS 4 |
| Data and identity | Supabase Auth, Postgres, RLS, Realtime, private Storage |
| Server-side | Supabase Edge Functions, trusted Node.js file worker |
| Hosting and protection | Cloudflare Pages, Cloudflare Turnstile, Resend |
| Quality | Vitest, ESLint, TypeScript, GitHub Actions |

### Local development

Requirements: Node.js 22 and pnpm 11.

```bash
git clone https://github.com/BG-BRIDGE/bg-bridge.git
cd bg-bridge
corepack enable
pnpm install --frozen-lockfile
```

Copy `.env.example` to `.env` and provide at least the browser-safe Supabase URL and publishable key. Never place a `service_role` key, email credential, translation credential, or other server-side secret in a `VITE_*` variable or commit it to the repository.

```bash
pnpm dev
```

Development builds on a loopback address expose a read-only-style UI preview from the sign-in page. It does not create a real Supabase session or bypass RLS, uploads, or management authorization.

Common quality checks:

```bash
pnpm typecheck
pnpm lint
pnpm test
pnpm build
pnpm --dir workers/trusted-file-worker test
pnpm worker:build
```

### Repository structure

```text
app/                         React application, routes, components, and frontend APIs
supabase/migrations/         Database schema, RLS, RPCs, and security constraints
supabase/functions/          Identity, file access, translation, and governance Functions
workers/trusted-file-worker/ File scanning, preview, lease, and cleanup worker
public/                      Cloudflare routing, search metadata, and brand assets
.github/workflows/           Continuous-integration quality gate
```

### Contributing

For substantial changes, open an Issue first to describe the problem and scope. Pull Requests should stay focused and pass type checking, linting, tests, and the production build. Do not disclose security vulnerabilities publicly; report them through a private channel provided by the repository maintainers.

This repository currently has no open-source license. Unless the maintainers grant separate permission, public visibility does not grant permission to copy, modify, or redistribute the code.

