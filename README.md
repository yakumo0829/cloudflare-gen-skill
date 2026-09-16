# Cloudflare Gen - AI Agent Skill

[English](#english) | [中文](#中文)

---

## 中文

### 簡介

這是一個適用於任何支援 skills 的 AI Agent 的圖片生成工具，使用 Cloudflare Workers AI 的 FLUX.1 Schnell 模型生成高品質圖片（如 [Opencode](https://opencode.ai)、其他兼容平台）。

- 免費額度：每天約 230 張
- 無需信用卡
- 零安裝需求（僅需 curl）

### 安裝方式

1. 將 `SKILL.md` 放入你的 agent 的 skills 目錄中：
   - **Opencode：** `~/.config/opencode/skills/cloudflare-gen/SKILL.md`
   - **其他 Agent：** 參考你的 agent 文件，找到 skills 目錄位置
2. 重新啟動你的 AI Agent

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

This is an image generation tool for any AI Agent that supports skills, using Cloudflare Workers AI's FLUX.1 Schnell model to generate high-quality images (such as [Opencode](https://opencode.ai) and other compatible platforms).

- Free quota: ~230 images per day
- No credit card required
- Zero installation (curl only)

### Installation

1. Place the `SKILL.md` file into your agent's skills directory:
   - **Opencode:** `~/.config/opencode/skills/cloudflare-gen/SKILL.md`
   - **Other Agents:** Refer to your agent's documentation to find the skills directory location
2. Restart your AI Agent

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
