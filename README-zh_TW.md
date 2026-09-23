<p align="center">
  <img src="LanLanLu_Profile.webp" alt="LanLanLu Discord Bot Icon" width="128">
</p>

# 攔藍錄 Discord 機器人

[English](README.md) | [臺灣正體中文](README-zh_TW.md)

> **注意事項**  
> 本專案使用 **Gemini 氛圍編碼 (Vibe Coding)** 撰寫，由 AI 魔法與過量的數位薯條驅動。**使用請注意**！如果您發現 UI 開始跳舞或程式碼看起來像某種神秘咒語，別擔心——那只是「氛圍」到位了。

「你的每一句話我全都要！！」

## 這是什麼瘋狂的傑作？

來自蘭蘭露宇宙的⸺**攔藍錄**，是個專門綁架對話紀錄的瘋狂機器人！

## 超狂魔法指令

**注意**：僅限擁有 Discord 原生 **伺服器管理員** 權限，或被加入授權清單的身分組操作。

* **`/record`**：開始錄製頻道對話。未指定結束點時會持續監聽新訊息，直到輸入 `/stop` 結束；若指定了結束時間或訊息 ID 則直接批次匯出該區間紀錄。支援以時間、訊息 ID 或則數篩選，並可選擇輸出為 `txt`（預設）、`md` 或 `both` 雙格式，以及是否產生 AI 摘要。
* **`/summary`**：直接抓取指定範圍的歷史訊息並產生 AI 摘要，不輸出完整紀錄檔。支援指定時間、訊息 ID 或則數範圍，並可選擇輸出 `txt`、`md` 或 `both` 格式。
* **`/stop`**：停止目前的錄製工作，將對話紀錄與 AI 摘要檔案輸出至當前頻道；可選填 `target_channel` 將檔案傳送至指定頻道。
* **`/models`**：查看機器人當前的 Gemini 模型優先順序與 API 金鑰啟用狀態。
* **`/say`**：讓機器人代表發言並傳送指定訊息，隱藏指令呼叫者的痕跡（自動阻擋 `@everyone` 與 `@here` 廣播提及）。
* **`/add_role` 與 `/remove_role`**：將指定身分組加入或移出允許使用指令的授權清單（僅限伺服器管理員操作）。

## Gemini AI 摘要與模型設定

本機器人整合 Google Gemini 官方 `google-genai` SDK，具備自動容錯與多層備援機制。

### 預設模型順序與備援機制

預設優先使用 `gemini-3.8-flash` 產生摘要；若遇到 API 配額上限或連線異常，系統會依序向後降級嘗試備援模型：

1. `gemini-3.8-flash`（主力首選）
2. `gemini-3.7-flash`（第二順位備援）
3. `gemini-3.6-flash`（第三順位備援）

### 自訂模型清單

若需調整欲使用的模型或優先順序，可直接編輯 [`main.py`](main.py) 中的 `GEMINI_MODELS` 清單：

```python
GEMINI_MODELS = [
    'gemini-3.8-flash',
    'gemini-3.7-flash',
    'gemini-3.6-flash'
]
```

## 安裝與啟動

### 方法一：使用 Docker 部署（推薦）
適合放置於 24 小時運作的 Linux 伺服器，內建自動重啟機制。
1. **設定環境變數**：建立 `.env` 檔案並寫入您的 Token：
   ```env
   DISCORD_TOKEN=您的_Discord_Token
   GEMINI_API_KEY=您的_Gemini_API_Key
   ```
2. **初始化設定檔**：在專案目錄下建立一個空白檔案以防 Docker 掛載錯誤：`touch config.json`
3. **啟動機器人**：執行指令 `docker compose up -d`

### 方法二：本機直接啟動
1. **設定環境變數**：在 `.env` 檔案中填入您的 Token。
2. **安裝套件**：`pip install -r requirements.txt`
3. **啟動機器人**：`python main.py`

### 權限設定
伺服器管理員預設擁有所有權限。若要開放給其他身分組，請管理員直接在 Discord 頻道中輸入 `/add_role` 指令進行動態授權（設定會自動儲存於 `config.json`）。

**授權與著作權**  
版權所有 © 2026 flandretw | 本專案採用 [MIT License](LICENSE) 授權
