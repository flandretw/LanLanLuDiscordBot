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

* `/record`：**錄製對話**。可即時監聽直到 `/stop`，或指定結束時間／訊息 ID 進行區間批次匯出。支援時間與則數過濾、格式切換（`txt`、`md`、`both`）與摘要開關。
* `/summary`：**即時摘要**。直接擷取歷史對話並生成重點摘要，不輸出完整對話紀錄檔。
* `/stop`：**停止錄製**。即刻結案並輸出檔案至當前頻道，可選填 `target_channel` 轉送至指定頻道。
* `/models`：**模型狀態**。檢視目前 Gemini 備援鏈的調度清單與 API 啟用狀態。
* `/say`：**匿名發言**。以機器人身分送出訊息，內建 `@everyone` 與 `@here` 廣播防護。
* `/add_role` / `/remove_role`：**身分組授權**。動態增刪允許操控機器人的身分組（管理員限定）。

## Gemini 摘要容錯架構

我們絕不允許摘要任務中途暴斃。機器人內建多層模型容錯鏈：首選 `gemini-3.8-flash` 快速消化海量廢話；若遇到 API 配額緊縮或連線異常，系統會自動無縫接力換上 3.7 與 3.6 繼續總結，不讓任何對話漏接。

### 備援調度鏈

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
1. **設定環境變數**：建立 `.env` 檔案並填入你的 Token：
   ```env
   DISCORD_TOKEN=你的_Discord_Token
   GEMINI_API_KEY=你的_Gemini_API_Key
   ```
2. **初始化設定檔**：在專案目錄下建立空白檔案以防掛載錯誤：`touch config.json`
3. **啟動機器人**：執行指令 `docker compose up -d`

### 方法二：本機直接啟動
1. **設定環境變數**：在 `.env` 檔案中填入你的 Token。
2. **安裝套件**：`pip install -r requirements.txt`
3. **啟動機器人**：`python main.py`

### 權限設定
伺服器管理員預設擁有所有權限。若要開放給其他身分組，請管理員直接在 Discord 頻道中輸入 `/add_role` 指令進行動態授權（設定會自動儲存於 `config.json`）。

**授權與著作權**  
版權所有 © 2026 flandretw | 本專案採用 [MIT License](LICENSE) 授權
