---
name: cloudflare-gen
description: 使用 Cloudflare Workers AI (FLUX.1 Schnell) 從文字描述生成高品質圖片。免費額度 ~230 張/天，無需信用卡。當使用者說「生圖」「生成圖片」「畫一張」「generate an image」時，與 pollinations-gen 一起提供選擇。
trigger: /gen-img /生圖
---

# Cloudflare Workers AI 圖片生成

使用 Cloudflare Workers AI 的 FLUX.1 Schnell 模型生成高品質圖片，免費額度約 230 張/天。

## 與 Pollinations-gen 共用觸發指令

當使用者輸入 `/gen-img` 或 `/生圖` 時，**詢問要使用哪個引擎**：
- **Cloudflare**：品質最高，需要帳號和 API Token
- **Pollinations**：免 Key，品質不穩定

## 前置需求

### 1. 取得 API Token 和 Account ID（免費）
1. 前往 [Cloudflare 註冊](https://dash.cloudflare.com/sign-up/workers-and-pages)（無需信用卡）
2. 登入後，前往 [Workers AI 頁面](https://dash.cloudflare.com/?to=/:account/ai/workers-ai)
3. 點擊 **「Use REST API」**
4. 點擊 **「Create a Workers AI API Token」** → **「Create API Token」**
5. 複製 Token
6. 在同一頁面找到 **Account ID** 並複製

### 2. 設定環境變數
```powershell
# 永久設定（需重新開啟終端機）
setx CF_API_TOKEN "你的API_TOKEN"
setx CF_ACCOUNT_ID "你的ACCOUNT_ID"

# 目前 session 臨時設定
$env:CF_API_TOKEN = "你的API_TOKEN"
$env:CF_ACCOUNT_ID = "你的ACCOUNT_ID"
```

### 3. 驗證設定
```powershell
if ($env:CF_API_TOKEN -and $env:CF_ACCOUNT_ID) { echo "OK" } else { echo "MISSING" }
```

## API 端點

```
POST https://api.cloudflare.com/client/v4/accounts/{ACCOUNT_ID}/ai/run/@cf/black-forest-labs/flux-1-schnell
```

## 可用模型

| 模型 ID | 說明 | 適合場景 |
|---------|------|----------|
| `@cf/black-forest-labs/flux-1-schnell` | FLUX.1 快速版 | 一般用途、快速生成 |
| `@cf/black-forest-labs/flux-2-klein-4b` | FLUX.2 Klein 4B | 超快生成、即時預覽 |
| `@cf/black-forest-labs/flux-2-klein-9b` | FLUX.2 Klein 9B | 增強品質 |
| `@cf/stabilityai/stable-diffusion-xl-base-1.0` | SDXL Base | 經典穩定 |
| `@cf/stabilityai/stable-diffusion-xl-lightning` | SDXL Lightning | 超快生成 |
| `@cf/leonardo/phoenix-1.0` | Leonardo Phoenix | 高品質藝術風 |

## 使用方式

```
/gen-img <prompt>                    # 選擇 Cloudflare 後生成圖片
/生圖 <prompt>                       # 同上
```

## 執行步驟

### Step 1：確認環境變數

```powershell
if ($env:CF_API_TOKEN -and $env:CF_ACCOUNT_ID) { echo "OK" } else { echo "MISSING" }
```

若顯示 `MISSING`，停止並要求使用者設定環境變數。

### Step 2：建立 JSON 請求體

**重要：必須使用 UTF8 編碼且無 BOM，否則 API 會回傳 "Request body is not valid json" 錯誤。**

```powershell
$json = '{"prompt":"你的prompt"}'
[System.IO.File]::WriteAllText("C:\Users\user\AppData\Local\Temp\opencode\cf_request.json", $json, [System.Text.UTF8Encoding]::new($false))
```

### Step 3：呼叫 Cloudflare API

```powershell
curl.exe -s -X POST "https://api.cloudflare.com/client/v4/accounts/$env:CF_ACCOUNT_ID/ai/run/@cf/black-forest-labs/flux-1-schnell" -H "Authorization: Bearer $env:CF_API_TOKEN" -H "Content-Type: application/json" -d "@C:\Users\user\AppData\Local\Temp\opencode\cf_request.json" -o "C:\Users\user\AppData\Local\Temp\opencode\cf_response.json"
```

**注意：** 必須使用 `curl.exe`，不能用 PowerShell 的 `curl` alias。

### Step 4：解碼 base64 並儲存圖片

```powershell
$response = Get-Content "C:\Users\user\AppData\Local\Temp\opencode\cf_response.json" -Raw | ConvertFrom-Json

# 檢查是否有錯誤
if (-not $response.success) {
    Write-Output "API Error: $($response.errors | ConvertTo-Json)"
    exit 1
}

# 提取 base64 圖片資料
$imageData = $response.result.image

# 解碼並儲存
[System.IO.File]::WriteAllBytes("輸出路徑.jpg", [System.Convert]::FromBase64String($imageData))
```

### Step 5：驗證檔案

```powershell
Get-Item "輸出路徑.jpg" | Select-Object Name, Length, Extension
```

檔案大小應 > 10KB。

### Step 6：顯示圖片

使用 Read 工具讀取圖片檔案即可在聊天中顯示。

## 完整範例

### 基本用法
```powershell
$env:CF_API_TOKEN = "你的Token"
$env:CF_ACCOUNT_ID = "你的AccountID"

$json = '{"prompt":"A cute cat sitting on a windowsill at sunset"}'
[System.IO.File]::WriteAllText("C:\Users\user\AppData\Local\Temp\opencode\cf_request.json", $json, [System.Text.UTF8Encoding]::new($false))

curl.exe -s -X POST "https://api.cloudflare.com/client/v4/accounts/$env:CF_ACCOUNT_ID/ai/run/@cf/black-forest-labs/flux-1-schnell" -H "Authorization: Bearer $env:CF_API_TOKEN" -H "Content-Type: application/json" -d "@C:\Users\user\AppData\Local\Temp\opencode\cf_request.json" -o "C:\Users\user\AppData\Local\Temp\opencode\cf_response.json"

$response = Get-Content "C:\Users\user\AppData\Local\Temp\opencode\cf_response.json" -Raw | ConvertFrom-Json
[System.IO.File]::WriteAllBytes("C:\Users\user\Desktop\cat.jpg", [System.Convert]::FromBase64String($response.result.image))
```

## 與其他引擎的比較

| 比較項目 | Cloudflare Workers AI | Pollinations.ai |
|---------|----------------------|-----------------|
| 圖片品質 | ⭐⭐⭐⭐⭐ 極高 | ⭐⭐⭐ 中等 |
| 需要帳號 | ✅ 是（免費） | ❌ 否 |
| 每日額度 | ~230 張（10,000 neurons） | ~無限（每 15 秒 1 次） |
| 安裝需求 | 零（僅需 curl） | 零（僅需 curl） |
| 圖片格式 | JPEG（base64） | JPEG |
| Prompt 語言 | 英文較佳 | 英文較佳 |
| 多物件理解 | ⭐⭐⭐⭐ 較佳 | ⭐⭐ 較差 |
| 穩定性 | ⭐⭐⭐⭐⭐ 穩定 | ⭐⭐⭐ 不穩定 |

## 疑難排解

### "Request body is not valid json" 錯誤
JSON 檔案必須是 **UTF8 編碼且無 BOM**。使用：
```powershell
[System.IO.File]::WriteAllText("request.json", $json, [System.Text.UTF8Encoding]::new($false))
```

### 環境變數未生效
`setx` 設定後需**重新開啟終端機**。可在新終端機中執行 `echo $env:CF_API_TOKEN` 確認。

### 額度用完
每日 10,000 neurons 額度在 UTC 00:00 重置。可到 Cloudflare Dashboard 查看使用量。

### PowerShell curl 問題
必須使用 `curl.exe` 而非 `curl`（PowerShell alias 會報錯）。
