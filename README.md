# Cloudflare Gen - Opencode Skill

[English](#english) | [中文](#中文)

---

## 中文

### 簡介

這是一個 [Opencode](https://opencode.ai) 的 skill，使用 Cloudflare Workers AI 的 FLUX.1 Schnell 模型生成高品質圖片。

- 免費額度：每天約 230 張
- 無需信用卡
- 零安裝需求（僅需 curl）

### 安裝方式

1. 確保你已安裝 [Opencode](https://opencode.ai)
2. 將 `SKILL.md` 複製到你的 opencode skills 目錄：
   ```
   ~/.config/opencode/skills/cloudflare-gen/SKILL.md
   ```
3. 重新啟動 opencode

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

在 Opencode 中輸入：

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

This is an [Opencode](https://opencode.ai) skill that uses Cloudflare Workers AI's FLUX.1 Schnell model to generate high-quality images.

- Free quota: ~230 images per day
- No credit card required
- Zero installation (curl only)

### Installation

1. Make sure you have [Opencode](https://opencode.ai) installed
2. Copy `SKILL.md` to your opencode skills directory:
   ```
   ~/.config/opencode/skills/cloudflare-gen/SKILL.md
   ```
3. Restart opencode

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

In Opencode, type:

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
