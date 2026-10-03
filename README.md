# Cloudflare Gen - AI Agent Skill

[English](#english) | [中文](#中文)

---

## 中文

### 簡介

這是一個適用於任何支援 skills 的 AI Agent 的圖片生成工具，使用 Cloudflare Workers AI 的 FLUX.1 Schnell 模型生成高品質圖片（如 [Opencode](https://opencode.ai)、[Claude Code](https://code.claude.com)、[Codex](https://developers.openai.com/codex)、[Cursor](https://cursor.com)、[GitHub Copilot](https://github.com/features/copilot)、[Gemini CLI / Antigravity](https://developers.googleblog.com/en/introducing-antigravity)）。

### 支援的 AI Agent

| AI Agent | 專案路徑 | 全域路徑 |
|----------|----------|----------|
| [Opencode](https://opencode.ai/docs/skills/) | `.opencode/skills/cloudflare-gen/SKILL.md` | `~/.config/opencode/skills/cloudflare-gen/SKILL.md` |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/cloudflare-gen/SKILL.md` | `~/.claude/skills/cloudflare-gen/SKILL.md` |
| [Codex](https://developers.openai.com/codex/skills) | `.codex/skills/cloudflare-gen/SKILL.md` | `~/.codex/skills/cloudflare-gen/SKILL.md` |
| [Cursor](https://cursor.com/docs/context/skills) | `.cursor/skills/cloudflare-gen/SKILL.md` | `~/.cursor/skills/cloudflare-gen/SKILL.md` |
| [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/skills) | `.github/skills/cloudflare-gen/SKILL.md` | `~/.copilot/skills/cloudflare-gen/SKILL.md` |
| [Gemini CLI / Antigravity](https://developers.googleblog.com/en/introducing-antigravity) | `.gemini/skills/cloudflare-gen/SKILL.md` | `~/.gemini/skills/cloudflare-gen/SKILL.md` |

- 免費額度：每天約 230 張
- 無需信用卡
- 零安裝需求（僅需 curl）

### 安裝方式

1. 將 `SKILL.md` 放入你的 agent 的 skills 目錄中（見上表，例如 **Opencode：** `~/.config/opencode/skills/cloudflare-gen/SKILL.md`，**Claude Code：** `~/.claude/skills/cloudflare-gen/SKILL.md`）：
2. 重新啟動你的 AI Agent

> 本 skill 遵循 Agent Skills 開放標準，僅使用 `curl` 呼叫 API、無廠商專屬 hook，上述 6 家 agent 皆可直接使用。

### 前置需求：取得 Cloudflare 憑證（免費）

1. 前往 [Cloudflare 註冊](https://dash.cloudflare.com/sign-up/workers-and-pages)（無需信用卡）
2. 登入後，前往 [Workers AI 頁面](https://dash.cloudflare.com/?to=/:account/ai/workers-ai)
3. 點擊 **「Use REST API」**
4. 點擊 **「Create a Workers AI API Token」** → **「Create API Token」**
5. 複製 Token
6. 在同一頁面找到 **Account ID** 並複製

### 設定環境變數

```powershell
# 永久設定（需重新開啟終端機）
setx CF_API_TOKEN "你的API_TOKEN"
setx CF_ACCOUNT_ID "你的ACCOUNT_ID"

# 目前 session 臨時設定
$env:CF_API_TOKEN = "你的API_TOKEN"
$env:CF_ACCOUNT_ID = "你的ACCOUNT_ID"
```

### 使用方式

在你的 AI Agent 中輸入：

```
/gen-img 一隻可愛的貓咪坐在窗台上
/生圖 一隻可愛的貓咪坐在窗台上
```

### 支援模型

| 模型 ID | 說明 |
|---------|------|
| `@cf/black-forest-labs/flux-1-schnell` | FLUX.1 快速版（預設） |
| `@cf/black-forest-labs/flux-2-klein-4b` | FLUX.2 Klein 4B |
| `@cf/black-forest-labs/flux-2-klein-9b` | FLUX.2 Klein 9B |
| `@cf/stabilityai/stable-diffusion-xl-base-1.0` | SDXL Base |
| `@cf/stabilityai/stable-diffusion-xl-lightning` | SDXL Lightning |
| `@cf/leonardo/phoenix-1.0` | Leonardo Phoenix |

### 免責聲明

- 本 skill 僅供學習與個人使用
- 請遵守 Cloudflare 的使用條款
- 生成的圖片版權歸使用者所有

---

## English

### Introduction

This is an image generation tool for any AI Agent that supports skills, using Cloudflare Workers AI's FLUX.1 Schnell model to generate high-quality images (such as [Opencode](https://opencode.ai), [Claude Code](https://code.claude.com), [Codex](https://developers.openai.com/codex), [Cursor](https://cursor.com), [GitHub Copilot](https://github.com/features/copilot), [Gemini CLI / Antigravity](https://developers.googleblog.com/en/introducing-antigravity)).

### Supported AI Agents

| AI Agent | Project path | Global path |
|----------|--------------|-------------|
| [Opencode](https://opencode.ai/docs/skills/) | `.opencode/skills/cloudflare-gen/SKILL.md` | `~/.config/opencode/skills/cloudflare-gen/SKILL.md` |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/cloudflare-gen/SKILL.md` | `~/.claude/skills/cloudflare-gen/SKILL.md` |
| [Codex](https://developers.openai.com/codex/skills) | `.codex/skills/cloudflare-gen/SKILL.md` | `~/.codex/skills/cloudflare-gen/SKILL.md` |
| [Cursor](https://cursor.com/docs/context/skills) | `.cursor/skills/cloudflare-gen/SKILL.md` | `~/.cursor/skills/cloudflare-gen/SKILL.md` |
| [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/skills) | `.github/skills/cloudflare-gen/SKILL.md` | `~/.copilot/skills/cloudflare-gen/SKILL.md` |
| [Gemini CLI / Antigravity](https://developers.googleblog.com/en/introducing-antigravity) | `.gemini/skills/cloudflare-gen/SKILL.md` | `~/.gemini/skills/cloudflare-gen/SKILL.md` |

- Free quota: ~230 images per day
- No credit card required
- Zero installation (curl only)

### Installation

1. Place the `SKILL.md` file into your agent's skills directory (see table above, e.g. **Opencode:** `~/.config/opencode/skills/cloudflare-gen/SKILL.md`, **Claude Code:** `~/.claude/skills/cloudflare-gen/SKILL.md`):
2. Restart your AI Agent

> This skill follows the Agent Skills open standard and only uses `curl` to call the API with no vendor-specific hooks, so all 6 agents above work directly.

### Prerequisites: Get Cloudflare Credentials (Free)

1. Sign up at [Cloudflare](https://dash.cloudflare.com/sign-up/workers-and-pages) (no credit card needed)
2. Go to the [Workers AI page](https://dash.cloudflare.com/?to=/:account/ai/workers-ai)
3. Click **"Use REST API"**
4. Click **"Create a Workers AI API Token"** → **"Create API Token"**
5. Copy the Token
6. Find and copy your **Account ID** on the same page

### Set Environment Variables

```powershell
# Permanent (restart terminal required)
setx CF_API_TOKEN "YOUR_API_TOKEN"
setx CF_ACCOUNT_ID "YOUR_ACCOUNT_ID"

# Temporary for current session
$env:CF_API_TOKEN = "YOUR_API_TOKEN"
$env:CF_ACCOUNT_ID = "YOUR_ACCOUNT_ID"
```

### Usage

In your AI Agent, type:

```
/gen-img a cute cat sitting on a windowsill
/生圖 a cute cat sitting on a windowsill
```

### Supported Models

| Model ID | Description |
|----------|-------------|
| `@cf/black-forest-labs/flux-1-schnell` | FLUX.1 Schnell (default) |
| `@cf/black-forest-labs/flux-2-klein-4b` | FLUX.2 Klein 4B |
| `@cf/black-forest-labs/flux-2-klein-9b` | FLUX.2 Klein 9B |
| `@cf/stabilityai/stable-diffusion-xl-base-1.0` | SDXL Base |
| `@cf/stabilityai/stable-diffusion-xl-lightning` | SDXL Lightning |
| `@cf/leonardo/phoenix-1.0` | Leonardo Phoenix |

### Disclaimer

- This skill is for learning and personal use only
- Please comply with Cloudflare's terms of service
- Generated images' copyright belongs to the user
