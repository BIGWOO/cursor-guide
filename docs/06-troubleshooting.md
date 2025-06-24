# Cursor 常見問題與解決方案

## 🆕 Cursor 1.1+ 新功能問題

### 問題：Background Agent 無法啟動
**症狀：** 按 `Ctrl+E` 沒有反應或出現錯誤

**解決方案：**
```powershell
# 檢查 Cursor 版本
cursor --version

# 確保版本 >= 1.0
# 如果版本過舊，請更新 Cursor
```

**其他檢查項目：**
- 確認網路連線正常
- 檢查是否啟用 Privacy Mode（可能影響 Background Agent）
- 前往 Settings → Beta → 確認 Background Agent 已啟用
- 重新啟動 Cursor

### 問題：BugBot 未在 PR 中出現
**症狀：** GitHub Pull Request 中沒有 BugBot 的自動審查評論

**解決方案：**
1. **檢查 BugBot 設定**
   - 確認 GitHub 專案已啟用 Cursor BugBot 整合
   - 檢查專案權限設定

2. **確認觸發條件**
   - PR 必須包含實際的程式碼變更
   - 檔案類型必須是 BugBot 支援的格式

3. **檢查網路連線**
   ```powershell
   # 測試 GitHub API 連線
   Test-NetConnection -ComputerName "api.github.com" -Port 443
   ```

### 問題：Memories 功能無效
**症狀：** AI 無法記住之前的專案偏好和開發模式

**解決方案：**
1. **啟用 Memories 功能**
   ```json
   // Settings → Rules → 啟用 Memories
   "cursor.memories.enabled": true
   ```

2. **等待學習週期**
   - AI 需要時間建立專案記憶
   - 至少需要 10-20 次互動才能建立有效記憶

3. **檢查專案活動**
   - 確保有足夠的程式碼互動記錄
   - 使用多種 AI 功能讓 AI 學習專案模式

### 問題：MCP 工具無法使用
**症狀：** 外部工具整合失敗，無法使用 Database 或其他 MCP 服務

**解決方案：**
1. **檢查 MCP 設定**
   ```powershell
   # 查看 MCP 狀態
   # Settings → Tools → MCP
   ```

2. **重新安裝 MCP 工具**
   - 移除有問題的 MCP 伺服器
   - 重新進行一鍵安裝
   - 確認 OAuth 認證成功

3. **網路連線問題**
   ```powershell
   # 檢查防火牆設定
   # 確認 MCP 伺服器可以連線
   ```

### 問題：Slack 整合無效
**症狀：** 在 Slack 中 @Cursor 無反應

**解決方案：**
1. **檢查整合設定**
   - Dashboard → Integrations → Slack
   - 確認已正確連接工作區

2. **權限檢查**
   - 確認 Slack 機器人有適當權限
   - 檢查頻道設定

3. **使用方式檢查**
   ```markdown
   正確用法：@Cursor 請幫我建立一個登入功能
   錯誤用法：@cursor 或 cursor（大小寫敏感）
   ```

### 問題：聊天分頁功能異常
**症狀：** `Ctrl+T` 無法建立新分頁或分頁切換有問題

**解決方案：**
1. **檢查快捷鍵衝突**
   ```json
   // 確認快捷鍵設定
   "keyboard.dispatch": "keyCode"
   ```

2. **重設聊天設定**
   - Settings → Features → Chat
   - 重設為預設值

## 🚨 安裝與設定問題

### 問題 1：Cursor 無法啟動

**症狀：**
- 雙擊 Cursor 圖示沒有反應
- 啟動時立即崩潰
- 顯示錯誤訊息後關閉

**可能原因與解決方案：**

**原因 A：系統權限不足**
```powershell
# 以管理員身份執行 PowerShell
# 右鍵 PowerShell → 以系統管理員身分執行
Start-Process "cursor" -Verb RunAs
```

**原因 B：防毒軟體干擾**
- 將 Cursor 加入防毒軟體白名單
- 暫時關閉即時防護測試

**原因 C：系統檔案損壞**
```powershell
# 修復系統檔案
sfc /scannow

# 檢查系統完整性
Dism /Online /Cleanup-Image /CheckHealth
```

**原因 D：版本衝突**
```powershell
# 完全移除舊版本
# 到控制台 → 程式和功能 → 解除安裝 Cursor

# 清理殘留檔案
Remove-Item -Path "$env:APPDATA\Cursor" -Recurse -Force
Remove-Item -Path "$env:LOCALAPPDATA\Programs\Cursor" -Recurse -Force
```

### 問題 2：AI 功能無法使用

**症狀：**
- Ctrl+K 沒有反應
- Ctrl+L 聊天視窗無法開啟
- 顯示 "AI 服務不可用"

**診斷步驟：**

**步驟 1：檢查網路連線**
```powershell
# 測試網路連線
Test-NetConnection -ComputerName "api.openai.com" -Port 443
ping google.com
```

**步驟 2：檢查 AI 服務設定**
```json
// 檢查 settings.json 中的 AI 設定
{
  "cursor.general.enableAIFeatures": true,
  "cursor.chat.openAiApiKey": "your-api-key-here"
}
```

**步驟 3：重新設定 AI 服務**
1. 開啟 Cursor 設定 (Ctrl+,)
2. 搜尋 "AI"
3. 重新輸入 API 金鑰
4. 重新啟動 Cursor

**步驟 4：檢查 API 額度**
- 登入 OpenAI/Anthropic 後台
- 檢查 API 使用額度
- 確認帳單狀態

### 問題 3：擴充功能安裝失敗

**症狀：**
- 擴充功能商店無法載入
- 安裝時顯示錯誤
- 已安裝的擴充功能無法運作

**解決方案：**

**方法 A：清理擴充功能快取**
```powershell
# 關閉 Cursor
taskkill /f /im cursor.exe

# 清理擴充功能快取
Remove-Item -Path "$env:USERPROFILE\.vscode\extensions" -Recurse -Force
```

**方法 B：手動安裝擴充功能**
```powershell
# 下載 .vsix 檔案後手動安裝
# 在 Cursor 中：Ctrl+Shift+P → "Extensions: Install from VSIX"
```

**方法 C：重設擴充功能設定**
```json
// 在 settings.json 中重設擴充功能設定
{
  "extensions.autoUpdate": true,
  "extensions.autoCheckUpdates": true
}
```

## 🔧 效能問題

### 問題 4：Cursor 運行緩慢

**症狀：**
- 啟動時間過長
- 檔案開啟緩慢
- AI 回應延遲
- 介面卡頓

**診斷與優化：**

**步驟 1：檢查系統資源**
```powershell
# 檢查 CPU 和記憶體使用率
Get-Counter "\Processor(_Total)\% Processor Time"
Get-Counter "\Memory\Available MBytes"

# 檢查磁碟使用率
Get-Counter "\PhysicalDisk(_Total)\% Disk Time"
```

**步驟 2：優化 Cursor 設定**
```json
{
  // 減少檔案監視
  "files.watcherExclude": {
    "**/node_modules/**": true,
    "**/dist/**": true,
    "**/build/**": true,
    "**/.git/**": true,
    "**/coverage/**": true
  },
  
  // 關閉不必要的功能
  "editor.minimap.enabled": false,
  "editor.codeLens": false,
  "editor.hover.enabled": false,
  
  // 優化搜尋設定
  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/dist": true
  }
}
```

**步驟 3：清理工作區**
```powershell
# 清理暫存檔案
Remove-Item -Path "$env:TEMP\*" -Recurse -Force

# 清理 Cursor 快取
Remove-Item -Path "$env:APPDATA\Cursor\CachedData" -Recurse -Force
```

**步驟 4：升級硬體**
```markdown
建議硬體需求：
- RAM: 8GB+ (推薦 16GB)
- CPU: 4 核心以上
- 儲存: SSD 硬碟
- 網路: 穩定的寬頻連線
```

### 問題 5：記憶體使用過高

**症狀：**
- Cursor 佔用大量 RAM
- 系統變慢
- 其他程式無法正常運行

**解決方案：**

**方法 A：調整記憶體設定**
```json
{
  "typescript.preferences.maxTsServerMemory": 4096,
  "files.maxMemoryForLargeFilesMB": 4096,
  "editor.maxTokenizationLineLength": 20000
}
```

**方法 B：關閉大型檔案**
```powershell
# 檢查開啟的大型檔案
# 關閉不必要的分頁
# 使用 "File: Close All Editors"
```

**方法 C：重新啟動 Cursor**
```powershell
# 定期重新啟動 Cursor
# 設定自動重新啟動排程（可選）
```

## 🤖 AI 協作問題

### 問題 6：AI 回應品質不佳

**症狀：**
- AI 生成的程式碼有錯誤
- 回應不符合需求
- 建議不實用

**改善策略：**

**策略 A：優化提示詞**
```markdown
❌ 不佳的提示詞：
"寫一個函數"

✅ 良好的提示詞：
"寫一個 JavaScript 函數，接收使用者陣列，
回傳年齡大於 18 歲的成年使用者，
包含輸入驗證和錯誤處理"
```

**策略 B：提供上下文**
```javascript
// 在詢問前開啟相關檔案
// 讓 AI 了解專案結構和程式碼風格

// 範例：同時開啟
// - models/User.js
// - utils/validation.js
// - config/constants.js
```

**策略 C：分步驟請求**
```markdown
步驟 1：建立基本結構
步驟 2：實作核心邏輯
步驟 3：加入錯誤處理
步驟 4：撰寫測試案例
```

### 問題 7：AI 服務中斷

**症狀：**
- AI 功能突然無法使用
- 顯示連線錯誤
- 請求超時

**處理步驟：**

**步驟 1：檢查服務狀態**
```powershell
# 檢查 OpenAI 服務狀態
# 訪問 https://status.openai.com/

# 檢查網路連線
Test-NetConnection -ComputerName "api.openai.com" -Port 443
```

**步驟 2：切換 AI 提供者**
```json
{
  "cursor.chat.provider": "anthropic",  // 或 "openai"
  "cursor.chat.anthropicApiKey": "your-key"
}
```

**步驟 3：調整超時設定**
```json
{
  "cursor.chat.timeout": 30000,  // 30 秒
  "cursor.general.requestTimeout": 60000
}
```

## 🔀 Git 整合問題

### 問題 8：Git 功能無法正常運作

**症狀：**
- 無法看到 Git 狀態
- 提交按鈕無反應
- 分支切換失敗

**診斷與修復：**

**步驟 1：檢查 Git 安裝**
```powershell
# 檢查 Git 是否已安裝
git --version

# 如果未安裝，下載並安裝 Git for Windows
# https://git-scm.com/download/win
```

**步驟 2：設定 Git 路徑**
```json
{
  "git.path": "C:\\Program Files\\Git\\bin\\git.exe"
}
```

**步驟 3：檢查 Git 配置**
```powershell
# 設定使用者資訊
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 檢查目前配置
git config --list
```

**步驟 4：重新初始化儲存庫**
```powershell
# 如果 Git 儲存庫損壞
cd your-project-directory
Remove-Item -Path ".git" -Recurse -Force
git init
git remote add origin your-repo-url
```

### 問題 9：合併衝突處理困難

**症狀：**
- 無法解決合併衝突
- 衝突標記顯示異常
- 合併工具無法使用

**解決方案：**

**方法 A：使用內建合併工具**
```powershell
# 在 Cursor 中開啟有衝突的檔案
# 使用內建的三方合併工具
# 點擊 "Accept Current Change" 或 "Accept Incoming Change"
```

**方法 B：手動解決衝突**
```javascript
// 尋找衝突標記
<<<<<<< HEAD
// 你的變更
const myCode = "current version";
=======
// 其他人的變更
const myCode = "incoming version";
>>>>>>> branch-name

// 手動選擇保留的版本
const myCode = "final version";
```

**方法 C：使用外部工具**
```powershell
# 設定外部合併工具
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```

## 📦 專案相關問題

### 問題 10：大型專案載入緩慢

**症狀：**
- 開啟大型專案時間過長
- IntelliSense 反應遲緩
- 檔案搜尋很慢

**優化方案：**

**方案 A：排除不必要的資料夾**
```json
{
  "files.exclude": {
    "**/node_modules": true,
    "**/dist": true,
    "**/build": true,
    "**/.next": true,
    "**/coverage": true,
    "**/.nyc_output": true
  },
  "search.exclude": {
    "**/node_modules": true,
    "**/dist": true,
    "**/build": true
  }
}
```

**方案 B：使用工作區**
```json
// multi-root.code-workspace
{
  "folders": [
    {
      "name": "Frontend",
      "path": "./packages/frontend"
    },
    {
      "name": "Backend",
      "path": "./packages/backend"
    }
  ],
  "settings": {
    "typescript.preferences.includePackageJsonAutoImports": "off"
  }
}
```

**方案 C：調整 TypeScript 設定**
```json
// tsconfig.json
{
  "compilerOptions": {
    "skipLibCheck": true,
    "incremental": true,
    "tsBuildInfoFile": ".tsbuildinfo"
  },
  "exclude": [
    "node_modules",
    "dist",
    "build"
  ]
}
```

### 問題 11：套件管理問題

**症狀：**
- npm/yarn 命令執行失敗
- 依賴套件安裝錯誤
- 版本衝突

**解決策略：**

**策略 A：清理套件快取**
```powershell
# 清理 npm 快取
npm cache clean --force

# 清理 yarn 快取
yarn cache clean

# 刪除 node_modules 重新安裝
Remove-Item -Path "node_modules" -Recurse -Force
Remove-Item -Path "package-lock.json" -Force
npm install
```

**策略 B：使用 package.json 鎖定版本**
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "express": "~4.18.0"
  },
  "engines": {
    "node": ">=16.0.0",
    "npm": ">=8.0.0"
  }
}
```

**策略 C：檢查套件相容性**
```powershell
# 檢查過時的套件
npm outdated

# 檢查安全漏洞
npm audit
npm audit fix
```

## 🛠️ 故障排除工具

### 自動診斷腳本

**系統健康檢查腳本：**
```powershell
# cursor-health-check.ps1

Write-Host "=== Cursor 健康檢查 ===" -ForegroundColor Green

# 檢查 Cursor 是否運行
$cursorProcess = Get-Process "cursor" -ErrorAction SilentlyContinue
if ($cursorProcess) {
    Write-Host "✓ Cursor 正在運行" -ForegroundColor Green
    Write-Host "  PID: $($cursorProcess.Id)" -ForegroundColor Gray
    Write-Host "  記憶體使用: $([math]::Round($cursorProcess.WorkingSet64/1MB, 2)) MB" -ForegroundColor Gray
} else {
    Write-Host "✗ Cursor 未運行" -ForegroundColor Red
}

# 檢查 Git 安裝
try {
    $gitVersion = git --version
    Write-Host "✓ Git 已安裝: $gitVersion" -ForegroundColor Green
} catch {
    Write-Host "✗ Git 未安裝或未加入 PATH" -ForegroundColor Red
}

# 檢查 Node.js 安裝
try {
    $nodeVersion = node --version
    Write-Host "✓ Node.js 已安裝: $nodeVersion" -ForegroundColor Green
} catch {
    Write-Host "✗ Node.js 未安裝" -ForegroundColor Red
}

# 檢查網路連線
try {
    Test-NetConnection -ComputerName "api.openai.com" -Port 443 -WarningAction SilentlyContinue | Out-Null
    Write-Host "✓ OpenAI API 連線正常" -ForegroundColor Green
} catch {
    Write-Host "✗ 無法連線到 OpenAI API" -ForegroundColor Red
}

# 檢查磁碟空間
$disk = Get-WmiObject -Class Win32_LogicalDisk -Filter "DeviceID='C:'"
$freeSpaceGB = [math]::Round($disk.FreeSpace/1GB, 2)
if ($freeSpaceGB -gt 5) {
    Write-Host "✓ 磁碟空間充足: $freeSpaceGB GB" -ForegroundColor Green
} else {
    Write-Host "⚠ 磁碟空間不足: $freeSpaceGB GB" -ForegroundColor Yellow
}

Write-Host "=== 檢查完成 ===" -ForegroundColor Green
```

### 效能監控腳本

```powershell
# cursor-performance-monitor.ps1

Write-Host "=== Cursor 效能監控 ===" -ForegroundColor Blue

while ($true) {
    $cursorProcess = Get-Process "cursor" -ErrorAction SilentlyContinue
    
    if ($cursorProcess) {
        $cpuUsage = $cursorProcess.CPU
        $memoryMB = [math]::Round($cursorProcess.WorkingSet64/1MB, 2)
        $timestamp = Get-Date -Format "HH:mm:ss"
        
        Write-Host "[$timestamp] CPU: $cpuUsage% | 記憶體: $memoryMB MB" -ForegroundColor Cyan
        
        # 如果記憶體使用超過 2GB，發出警告
        if ($memoryMB -gt 2048) {
            Write-Host "⚠ 記憶體使用過高！" -ForegroundColor Yellow
        }
    } else {
        Write-Host "Cursor 未運行" -ForegroundColor Red
    }
    
    Start-Sleep -Seconds 5
}
```

## 🆘 緊急處理程序

### 當 Cursor 完全無法使用時

**步驟 1：備份重要資料**
```powershell
# 備份設定檔
Copy-Item -Path "$env:APPDATA\Cursor\User\settings.json" -Destination ".\cursor-settings-backup.json"

# 備份擴充功能清單
code --list-extensions > extensions-backup.txt
```

**步驟 2：完全重新安裝**
```powershell
# 1. 解除安裝 Cursor
# 2. 清理殘留檔案
Remove-Item -Path "$env:APPDATA\Cursor" -Recurse -Force
Remove-Item -Path "$env:LOCALAPPDATA\Programs\Cursor" -Recurse -Force

# 3. 重新下載並安裝最新版本
# 4. 恢復設定檔
```

**步驟 3：聯繫支援**
```markdown
準備以下資訊：
- 作業系統版本
- Cursor 版本
- 錯誤訊息截圖
- 重現步驟
- 已嘗試的解決方案
```

---

**下一步：** 探索 [進階技巧](./07-advanced-tips.md) 提升使用效率。 