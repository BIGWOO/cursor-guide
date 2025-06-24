# Cursor 進階技巧

## 🚀 高效快捷鍵組合

### 1. 核心快捷鍵進階應用

**多重選取與編輯：**
```markdown
Ctrl+D          - 選取下一個相同文字
Ctrl+Shift+L    - 選取所有相同文字
Alt+Click       - 新增游標位置
Ctrl+Alt+Up/Down - 垂直多游標選取
```

**程式碼導航進階：**
```markdown
Ctrl+P          - 快速開啟檔案
Ctrl+Shift+P    - 指令面板
Ctrl+T          - 前往符號
Ctrl+Shift+O    - 前往檔案中的符號
F12             - 前往定義
Alt+F12         - 查看定義（不離開目前檔案）
Shift+F12       - 查看所有參考
```

**視窗管理進階：**
```markdown
Ctrl+\          - 分割編輯器
Ctrl+1/2/3      - 切換編輯器群組
Ctrl+Shift+E    - 顯示檔案總管
Ctrl+Shift+F    - 全域搜尋
Ctrl+Shift+G    - 顯示版本控制
Ctrl+Shift+D    - 顯示除錯面板
```

### 2. 自訂快捷鍵

**keybindings.json 進階配置：**
```json
[
  {
    "key": "ctrl+alt+f",
    "command": "editor.action.formatDocument",
    "when": "editorTextFocus"
  },
  {
    "key": "ctrl+alt+i",
    "command": "editor.action.organizeImports",
    "when": "editorTextFocus"
  },
  {
    "key": "ctrl+alt+r",
    "command": "workbench.action.reloadWindow"
  },
  {
    "key": "ctrl+alt+t",
    "command": "workbench.action.terminal.toggleTerminal"
  },
  {
    "key": "ctrl+k ctrl+c",
    "command": "editor.action.addCommentLine",
    "when": "editorTextFocus"
  }
]
```

## 🤖 AI 功能進階運用

### 1. 複雜提示詞技巧

**情境感知提示詞：**
```markdown
**角色設定** + **專案上下文** + **具體需求** + **品質標準**

範例：
"你是一位資深的 React 架構師，
在這個電商專案中（使用 TypeScript + Next.js），
我需要設計一個可重用的產品卡片元件，
要支援不同尺寸、載入狀態和錯誤處理，
請遵循 SOLID 原則和團隊程式碼規範。"
```

**多輪對話策略：**
```markdown
輪次 1：基本架構設計
"設計一個購物車系統的基本架構"

輪次 2：具體實作
"實作 CartItem 介面和基本方法"

輪次 3：進階功能
"加入優惠券計算和庫存檢查功能"

輪次 4：錯誤處理
"為所有方法加入完整的錯誤處理"

輪次 5：測試撰寫
"撰寫對應的單元測試和整合測試"
```

### 2. 程式碼生成範本

**API 端點生成範本：**
```javascript
// 提示詞範本
"根據以下規格生成 Express.js API 端點：
- 路徑：{route_path}
- HTTP 方法：{http_method}
- 輸入驗證：{validation_schema}
- 業務邏輯：{business_logic}
- 錯誤處理：{error_handling}
- 回應格式：{response_format}
- 授權需求：{auth_requirements}

請包含 JSDoc 註解和 TypeScript 型別定義。"
```

**React 元件生成範本：**
```javascript
// 提示詞範本
"建立一個 React 功能元件：
- 元件名稱：{component_name}
- Props 介面：{props_interface}
- 狀態管理：{state_management}
- 副作用：{side_effects}
- 樣式方案：{styling_approach}
- 無障礙支援：{accessibility_features}

使用 TypeScript 和 React Hooks，
遵循函數式程式設計原則。"
```

### 3. 程式碼重構策略

**大型重構工作流程：**
```markdown
階段 1：分析現有程式碼
"分析這個類別的職責，找出違反單一職責原則的地方"

階段 2：制定重構計劃
"制定分離關注點的重構計劃，不改變外部介面"

階段 3：逐步重構
"將驗證邏輯提取到獨立的驗證器類別"

階段 4：測試驗證
"為重構後的程式碼撰寫測試，確保功能一致性"
```

## 🔧 自訂化配置進階

### 1. 工作區自動化

**tasks.json 進階配置：**
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Build and Test",
      "type": "shell",
      "command": "npm",
      "args": ["run", "build"],
      "group": "build",
      "presentation": {
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "shared"
      },
      "problemMatcher": "$tsc",
      "dependsOn": "Install Dependencies"
    },
    {
      "label": "Install Dependencies",
      "type": "shell",
      "command": "npm",
      "args": ["install"],
      "group": "build",
      "presentation": {
        "echo": true,
        "reveal": "silent"
      }
    },
    {
      "label": "Run Development Server",
      "type": "shell",
      "command": "npm",
      "args": ["run", "dev"],
      "group": "build",
      "isBackground": true,
      "presentation": {
        "echo": true,
        "reveal": "always",
        "panel": "new"
      },
      "problemMatcher": {
        "pattern": {
          "regexp": ".",
          "file": 1,
          "location": 2,
          "message": 3
        },
        "background": {
          "activeOnStart": true,
          "beginsPattern": "^.*starting.*",
          "endsPattern": "^.*ready.*"
        }
      }
    }
  ]
}
```

**launch.json 多環境除錯：**
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Node.js (Development)",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/src/app.js",
      "env": {
        "NODE_ENV": "development",
        "DEBUG": "*"
      },
      "console": "integratedTerminal",
      "restart": true,
      "runtimeArgs": ["--nolazy"]
    },
    {
      "name": "Debug Node.js (Production)",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/dist/app.js",
      "env": {
        "NODE_ENV": "production"
      },
      "console": "integratedTerminal"
    },
    {
      "name": "Debug Jest Tests",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": [
        "--runInBand",
        "--no-cache",
        "--watchAll=false"
      ],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}
```

## 📈 生產力提升技巧

### 1. 批次操作技巧

**批次檔案處理：**
```powershell
# 批次重新命名檔案
Get-ChildItem -Filter "*.component.js" | 
    Rename-Item -NewName { $_.Name -replace "\.component\.js$", ".tsx" }

# 批次更新導入語句
Get-ChildItem -Recurse -Filter "*.ts" | 
    ForEach-Object {
        (Get-Content $_.FullName) -replace 
            "import \* as React from 'react'", 
            "import React from 'react'" | 
        Set-Content $_.FullName
    }
```

### 2. 智慧搜尋與替換

**正規表示式搜尋：**
```regex
// 搜尋所有 console.log 語句
console\.log\(.*?\)

// 搜尋函數定義
function\s+(\w+)\s*\([^)]*\)\s*\{

// 搜尋 React 元件
const\s+(\w+):\s*React\.FC

// 搜尋 TODO 註解
\/\/\s*TODO:.*
```

### 3. 自動化工作流程

**環境設定腳本：**
```powershell
# setup-dev-environment.ps1

param(
    [string]$ProjectName = "my-project",
    [string]$Template = "react-typescript"
)

Write-Host "正在設定開發環境..." -ForegroundColor Green

# 建立專案目錄
New-Item -ItemType Directory -Force -Path $ProjectName
Set-Location $ProjectName

# 初始化 Git
git init
git config core.autocrlf false

# 建立基本檔案結構
@"
node_modules/
dist/
build/
.env.local
.DS_Store
*.log
"@ | Out-File -FilePath ".gitignore" -Encoding UTF8

Write-Host "環境設定完成！" -ForegroundColor Green
Write-Host "請執行 'cursor .' 開啟專案" -ForegroundColor Yellow
```

## 🛠️ 進階設定技巧

### 1. 效能最佳化

**記憶體使用最佳化：**
```json
{
  "typescript.preferences.maxTsServerMemory": 4096,
  "files.watcherExclude": {
    "**/node_modules/**": true,
    "**/.git/objects/**": true,
    "**/dist/**": true,
    "**/build/**": true
  },
  "search.useGlobalIgnoreFiles": true,
  "editor.largeFileOptimizations": true,
  "editor.maxTokenizationLineLength": 20000
}
```

### 2. 專案範本

**全端專案結構：**
```
my-fullstack-app/
├── packages/
│   ├── frontend/          # React + TypeScript
│   ├── backend/           # Node.js + Express
│   └── shared/            # 共用型別和工具
├── docs/                  # 專案文件
├── scripts/               # 建置腳本
├── .vscode/              # VS Code 設定
└── README.md
```

### 3. 團隊協作工具

**程式碼審查範本：**
```markdown
## 變更描述
<!-- 簡潔描述這次變更的內容 -->

## 變更類型
- [ ] 🎉 新功能 (feature)
- [ ] 🐛 Bug 修復 (fix)
- [ ] 📚 文件更新 (docs)
- [ ] ♻️ 重構 (refactor)

## 測試
- [ ] 單元測試通過
- [ ] 整合測試通過
- [ ] 手動測試完成

## 檢查清單
- [ ] 程式碼符合團隊規範
- [ ] 無除錯程式碼
- [ ] 已更新相關文件
```

---

**恭喜！** 您已完成 Cursor 團隊協作導入指南的學習。現在可以開始將這些技巧應用到實際專案中，提升團隊的開發效率和協作品質。

記住：**持續學習、實踐和改進**是掌握 Cursor 的關鍵！ 