# Cursor 團隊設定指南

## 🎯 目標

建立團隊統一的 Cursor 配置，確保所有成員有一致的開發體驗。

## 📋 團隊設定標準

### 1. 統一設定檔

建立 `.vscode/settings.json` 作為專案設定：

```json
{
  // 編輯器設定
  "editor.fontSize": 14,
  "editor.fontFamily": "Cascadia Code, Fira Code, Consolas",
  "editor.fontLigatures": true,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.detectIndentation": false,
  
  // 格式化設定
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": true
  },
  
  // AI 設定
  "cursor.chat.openAiApiKey": "",
  "cursor.general.enableAIFeatures": true,
  
  // 檔案設定
  "files.encoding": "utf8",
  "files.eol": "\n",
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  
  // 終端機設定
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  "terminal.integrated.fontSize": 14
}
```

### 2. 必要擴充功能清單

建立 `.vscode/extensions.json`：

```json
{
  "recommendations": [
    // 語言支援
    "ms-vscode.vscode-json",
    "ms-vscode.powershell",
    
    // 程式碼品質
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    
    // Git 工具
    "eamodio.gitlens",
    "mhutchie.git-graph",
    
    // 協作工具
    "ms-vsliveshare.vsliveshare",
    
    // 實用工具
    "rangav.vscode-thunder-client",
    "ms-vscode.vscode-yaml",
    "redhat.vscode-xml"
  ]
}
```

### 3. 程式碼格式化配置

#### Prettier 設定 (`.prettierrc`)：

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "bracketSpacing": true,
  "arrowParens": "avoid"
}
```

#### ESLint 設定 (`.eslintrc.json`)：

```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended"
  ],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "rules": {
    "indent": ["error", 2],
    "quotes": ["error", "single"],
    "semi": ["error", "always"]
  }
}
```

### 4. Cursor 專用配置

#### 啟用 Cursor 1.1+ 進階功能
團隊應該統一啟用 Cursor 的最新功能：

**1. Memories（AI 記憶）**
```powershell
# 每位成員都應啟用
# Settings → Rules → 啟用 Memories
```

**2. BugBot（自動程式碼審查）**
```markdown
管理員設定步驟：
1. 前往 GitHub 專案設定
2. 整合 Cursor BugBot
3. 配置自動審查規則
4. 測試 PR 自動審查功能
```

**3. MCP 整合（Model Context Protocol）**
```json
// 建議啟用的 MCP 工具
{
  "mcpServers": {
    "filesystem": "enabled",    // 檔案系統整合
    "git-advanced": "enabled",  // Git 進階操作
    "database": "enabled",      // 資料庫連接
    "web-search": "enabled"     // 網路搜尋功能
  }
}
```

**4. Background Agent 預設設定**
```json
// 團隊統一的 Background Agent 設定
{
  "backgroundAgent": {
    "defaultModel": "claude-3.5-sonnet",
    "maxParallelTasks": 3,
    "autoCreatePR": true
  }
}
```

**5. Slack 整合（可選）**
如果團隊使用 Slack，可設定 @Cursor 機器人：
```markdown
管理員設定步驟：
1. 前往 Cursor Dashboard → Integrations
2. 連接 Slack 工作區
3. 配置預設模型和代碼庫
4. 設定團隊權限
```

#### .cursorrules 檔案
在專案根目錄建立 `.cursorrules` 檔案，定義 AI 行為規範：

```
You are an expert in React, TypeScript, and modern web development.

Code Style Guidelines:
- Use functional components with hooks
- Prefer TypeScript over JavaScript
- Use meaningful variable and function names
- Add JSDoc comments for complex functions
- Follow the existing code structure and patterns

Project Structure:
- Components go in src/components/
- Utilities go in src/utils/
- Types go in src/types/
- Tests go alongside the code they test

Best Practices:
- Write tests for all new features
- Use proper error handling
- Follow accessibility guidelines
- Optimize for performance when needed
```

#### Cursor Rules 目錄結構（進階）
建立進階規則系統，適用於大型專案：

```powershell
# 建立 Cursor Rules 目錄
mkdir .cursor
mkdir .cursor\rules

# 建立規則檔案
New-Item .cursor\rules\architecture.mdc
New-Item .cursor\rules\coding-standards.mdc
New-Item .cursor\rules\testing-guidelines.mdc
```

**架構規則範例（.cursor/rules/architecture.mdc）：**
```markdown
# 專案架構指南

## 主要檔案結構
- 應用程式入口：[src/main.tsx](mdc:src/main.tsx)
- 路由定義：[src/App.tsx](mdc:src/App.tsx)
- 全域樣式：[src/index.css](mdc:src/index.css)

## 元件架構
所有可重用元件放在 [src/components/](mdc:src/components/) 目錄下。
每個元件應包含：
- 主要元件檔案
- 樣式檔案（如果需要）
- 測試檔案
- 型別定義檔案

範例元件結構：[src/components/Button/](mdc:src/components/Button/)
```

**編碼規範範例（.cursor/rules/coding-standards.mdc）：**
```markdown
# 編碼規範

## TypeScript 配置
嚴格遵循 [tsconfig.json](mdc:tsconfig.json) 中的設定

## 檔案命名規範
- 元件檔案：PascalCase（如 Button.tsx）
- 工具檔案：camelCase（如 formatDate.ts）
- 常數檔案：UPPER_SNAKE_CASE（如 API_ENDPOINTS.ts）

## 程式碼風格
參考 [.eslintrc.json](mdc:.eslintrc.json) 和 [.prettierrc](mdc:.prettierrc) 設定
```

## 🔧 團隊導入流程

### Phase 1：準備階段（1週）

1. **團隊會議討論**
   - 介紹 Cursor 功能和優勢
   - 討論團隊需求和期望
   - 制定導入時程表

2. **環境準備**
   - 準備統一設定檔案
   - 測試 AI 功能設定
   - 準備教學資源

### Phase 2：安裝與設定（1週）

1. **個人安裝**
   - 每位成員安裝 Cursor
   - 導入團隊統一設定
   - 安裝必要擴充功能

2. **設定驗證**
   - 檢查 AI 功能運作
   - 測試格式化設定
   - 確認終端機設定

### Phase 3：團隊測試（2週）

1. **小型專案練習**
   - 建立測試專案
   - 練習 AI 協作功能
   - 熟悉快捷鍵操作

2. **協作流程測試**
   - 測試即時協作功能（CodeTogether 等）
   - 練習程式碼審查流程
   - 建立協作規範

### Phase 4：正式導入（持續）

1. **實際專案應用**
   - 在真實專案中使用
   - 收集使用回饋
   - 調整設定和流程

## 👥 角色分工

### 團隊負責人
- 制定團隊標準
- 協調導入進度
- 解決技術問題

### 資深工程師
- 協助新手上手
- 分享使用技巧
- 建立最佳實踐

### 所有成員
- 積極學習新工具
- 提供使用回饋
- 分享經驗心得

## 📊 導入成效評估

### 評估指標

1. **效率提升**
   - 程式碼撰寫速度
   - Bug 修復時間
   - 功能開發週期

2. **品質改善**
   - 程式碼審查效率
   - 測試覆蓋率
   - 技術債務減少

3. **團隊協作**
   - 知識分享頻率
   - 協作滿意度
   - 學習曲線縮短

### 評估時程

- **第1週**：基本功能使用率
- **第1個月**：工作效率變化
- **第3個月**：整體團隊效能

## 🔄 持續改進

### 定期檢討

- **週會討論**：分享使用心得
- **月度回顧**：評估效果並調整
- **季度規劃**：制定進階目標

### 設定更新

- 根據專案需求調整設定
- 更新擴充功能清單
- 優化 AI 使用策略

## 📞 支援資源

### 內部資源

- 團隊 Slack/Teams 頻道
- 內部知識庫
- 定期分享會議

### 外部資源

- [Cursor 官方文件](https://docs.cursor.com/)
- [社群論壇](https://forum.cursor.com/)
- [GitHub 討論區](https://github.com/getcursor/cursor)

---

**下一步：** 學習 [AI 協作技巧](./03-ai-collaboration.md) 提升開發效率。 