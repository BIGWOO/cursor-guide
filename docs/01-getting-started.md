# Cursor 新手入門指南

## 什麼是 Cursor？

Cursor 是一個基於 VS Code 的 AI 驅動程式碼編輯器，提供強大的 AI 輔助程式設計功能。

## 🔽 安裝 Cursor

### Windows 11 安裝步驟

1. 前往 [Cursor 官網](https://www.cursor.com/)
2. 點擊 "Download for Windows"
3. 執行下載的 `.exe` 安裝檔
4. 依照安裝精靈完成安裝

### 首次啟動設定

1. 啟動 Cursor
2. 選擇主題（建議：Dark+ 或 Light+）
3. 導入現有 VS Code 設定（可選）
4. 設定 AI 功能

## ⚡ AI 功能設定

### 1. 註冊 AI 服務

**選項 A：使用 Cursor Pro**
- 前往 Settings > Cursor Pro
- 註冊並訂閱服務
- 獲得最佳 AI 體驗

**選項 B：使用自己的 API 金鑰**
- 設定 > AI Provider
- 輸入 OpenAI/Anthropic API 金鑰
- 配置模型偏好

### 2. Cursor 獨有 AI 功能

#### 🔥 核心 AI 功能

| 功能 | 快捷鍵 | 說明 |
|------|--------|------|
| **Ctrl+K** | `Ctrl+K` | 內聯程式碼生成與編輯 |
| **Ctrl+L** | `Ctrl+L` | AI 聊天視窗（專案上下文感知） |
| **Tab 補全** | `Tab` | 智慧程式碼補全 |
| **Background Agent** | `Ctrl+E` | 背景 AI 代理（遠端執行任務） |

#### 🚀 Cursor 獨特功能

**1. Codebase-wide Understanding（程式碼庫理解）**
- AI 可以理解整個專案結構
- 跨檔案程式碼建議和重構
- 智慧導入和依賴管理

**2. @-mentions（程式碼引用）**
```
@filename.js - 引用特定檔案
@foldername/ - 引用整個資料夾
@docs/ - 引用文件資料夾
@git - 引用 Git 變更
```

**3. Background Agent（背景代理）**
- 遠端執行複雜任務
- 平行處理多個任務
- 自動化程式碼生成和重構

**4. 智慧 Terminal 整合**
- AI 可以建議終端指令
- 自動偵錯錯誤訊息
- 專案設定自動化

**5. 上下文感知聊天**
- 聊天視窗自動載入相關檔案
- 理解專案架構和設計模式
- 技術選型建議

## 🛠️ 基本設定

### PowerShell 整合設定

1. 開啟 Cursor
2. 按 `Ctrl+Shift+P` 開啟指令面板
3. 搜尋 "Terminal: Select Default Profile"
4. 選擇 "PowerShell"

### 字體設定（建議）

```json
{
  "editor.fontFamily": "Cascadia Code, Fira Code, Consolas",
  "editor.fontSize": 14,
  "editor.fontLigatures": true
}
```

### 必要擴充功能

推薦安裝以下擴充功能：

- **Chinese (Traditional) Language Pack** - 繁體中文介面
- **GitLens** - Git 增強功能
- **Git Graph** - Git 圖形化管理
- **Prettier** - 程式碼格式化
- **Project Manager** - 專案管理
- **Thunder Client** - API 測試工具
- **CodeTogether** - 即時協作（Cursor 相容的替代方案）

## ⚠️ 重要注意事項

### Cursor 與 VS Code 的差異
- **Live Share 不可用**：Cursor 無法安裝 Microsoft Live Share 擴充功能
- **替代協作方案**：建議使用 CodeTogether 或其他協作工具
- **相容性**：大部分 VS Code 擴充功能都可正常使用
- **AI 功能**：這是 Cursor 的主要優勢，VS Code 無法直接獲得
- **BugBot**：自動程式碼審查功能，可在 GitHub PR 中自動偵測問題
- **Memories**：AI 記憶功能，可記住專案開發模式和偏好
- **MCP 整合**：支援外部工具和服務的深度整合
- **Cursor Rules**：進階規則系統，可創建 `.cursor/rules/*.mdc` 檔案定義專案規範

## 🎯 第一次使用

### 建立測試專案

1. 建立新資料夾：
```powershell
mkdir cursor-test
cd cursor-test
```

2. 用 Cursor 開啟：
```powershell
cursor .
```

3. 建立 `hello.js` 檔案
4. 使用 `Ctrl+K` 請求 AI 協助寫一個 Hello World

### 測試 Cursor 獨有功能

#### 1. 測試 Ctrl+L 聊天功能
1. 在空白檔案中按 `Ctrl+L`
2. 詢問：「幫我建立一個待辦事項清單應用程式，可以新增、刪除和標記完成項目」
3. 觀察 AI 如何生成程式碼

#### 2. 測試 @-mentions 功能
1. 建立 `package.json` 檔案
2. 在聊天中輸入：「根據 @package.json 建議適合的資料夾結構」
3. 觀察 AI 如何引用檔案內容

#### 3. 測試 Background Agent
1. 按 `Ctrl+E` 開啟 Background Agent
2. 要求：「建立一個完整的待辦事項應用程式，包含前端和後端」
3. 觀察代理在背景執行任務

#### 4. 測試程式碼庫理解
1. 建立幾個相關檔案
2. 在聊天中詢問：「分析這個專案的架構並提出改進建議」
3. 體驗跨檔案理解能力

## ✅ 檢查清單

完成以下項目確保設定正確：

### 基本設定
- [ ] Cursor 成功安裝並啟動
- [ ] AI 功能正常運作（可生成程式碼）
- [ ] PowerShell 設定為預設終端機
- [ ] 基本擴充功能已安裝
- [ ] 字體和主題設定完成

### Cursor 獨有功能測試
- [ ] `Ctrl+K` 內聯編輯功能正常
- [ ] `Ctrl+L` 聊天視窗可以使用
- [ ] `Ctrl+E` Background Agent 可以啟動
- [ ] @-mentions 功能可以引用檔案
- [ ] AI 可以理解專案結構
- [ ] Tab 補全提供智慧建議

## 🆘 常見安裝問題

### 問題：AI 功能無法使用
**解決方案：**
- 檢查網路連線
- 確認 AI 服務設定正確
- 重新啟動 Cursor

### 問題：PowerShell 無法使用
**解決方案：**
```powershell
# 檢查 PowerShell 路徑
Get-Command pwsh
```
- 在 Cursor 設定中手動指定 PowerShell 路徑

### 問題：中文顯示異常
**解決方案：**
- 安裝 Chinese (Traditional) Language Pack
- 重新啟動 Cursor
- 檢查系統語言設定

---

**下一步：** 閱讀 [團隊設定指南](./02-team-setup.md) 了解如何設定團隊統一配置。 