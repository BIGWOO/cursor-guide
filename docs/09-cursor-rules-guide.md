# Cursor Rules 完整使用指南

## 🎯 什麼是 Cursor Rules？

Cursor Rules 是 Cursor 的進階 AI 指導系統，比基本的 `.cursorrules` 檔案更強大。它允許你創建結構化的規則，讓 AI 更好地理解專案架構、編碼規範和團隊標準。

## 🆚 .cursorrules vs Cursor Rules

| 特性 | .cursorrules | Cursor Rules |
|------|-------------|-------------|
| 檔案格式 | 純文字 | Markdown + 特殊語法 |
| 檔案引用 | ❌ 不支援 | ✅ `[file.ext](mdc:file.ext)` |
| 多檔案組織 | ❌ 單一檔案 | ✅ 多檔案結構化 |
| 上下文感知 | ❌ 靜態 | ✅ 動態檔案連結 |
| 複雜度 | 簡單 | 進階 |

## 📁 建立 Cursor Rules

### 1. 目錄結構設定

```powershell
# 在專案根目錄建立結構
mkdir .cursor
mkdir .cursor\rules

# 建立規則檔案（必須是 .mdc 副檔名）
New-Item .cursor\rules\architecture.mdc
New-Item .cursor\rules\coding-standards.mdc
New-Item .cursor\rules\testing-guidelines.mdc
New-Item .cursor\rules\api-guidelines.mdc
```

### 2. 基本語法

#### 檔案引用語法
```markdown
# 引用特定檔案
[檔案名稱](mdc:相對路徑)

# 範例
[主要設定](mdc:package.json)
[元件範例](mdc:src/components/Button/Button.tsx)
[型別定義](mdc:src/types/index.ts)
```

#### 資料夾引用
```markdown
# 引用整個資料夾
[元件資料夾](mdc:src/components/)
[工具函數](mdc:src/utils/)
[測試檔案](mdc:tests/)
```

## 📋 實用範例

### 1. 專案架構規則

**檔案：`.cursor/rules/architecture.mdc`**

```markdown
# 專案架構指南

## 應用程式入口點
- 主要入口：[src/main.tsx](mdc:src/main.tsx)
- HTML 模板：[index.html](mdc:index.html)
- 環境設定：[.env.example](mdc:.env.example)

## 核心配置檔案
- Vite 設定：[vite.config.ts](mdc:vite.config.ts)
- TypeScript：[tsconfig.json](mdc:tsconfig.json)
- 套件管理：[package.json](mdc:package.json)

## 資料夾結構

### 元件架構
所有 UI 元件放在 [src/components/](mdc:src/components/) 資料夾中。
每個元件應遵循以下結構：

src/components/ComponentName/
├── ComponentName.tsx     ← 主要元件
├── ComponentName.test.tsx ← 測試檔案
├── ComponentName.module.css ← 樣式檔案
└── index.ts             ← 匯出檔案

參考範例：[src/components/Button/](mdc:src/components/Button/)

### 頁面元件
頁面級元件放在 [src/pages/](mdc:src/pages/) 資料夾中。
每個頁面對應一個路由，參考：[src/router/index.tsx](mdc:src/router/index.tsx)

### 狀態管理
- 全域狀態：[src/store/](mdc:src/store/)
- 本地狀態：使用 React hooks
- 表單狀態：使用 React Hook Form

### 工具函數
- 通用工具：[src/utils/](mdc:src/utils/)
- API 呼叫：[src/services/](mdc:src/services/)
- 常數定義：[src/constants/](mdc:src/constants/)

## 資料流架構

### API 層
所有 API 呼叫通過 [src/services/](mdc:src/services/) 進行。
參考 API 設定：[src/services/api.ts](mdc:src/services/api.ts)

### 錯誤處理
統一錯誤處理邏輯在：[src/utils/errorHandler.ts](mdc:src/utils/errorHandler.ts)
```

### 2. 編碼規範規則

**檔案：`.cursor/rules/coding-standards.mdc`**

```markdown
# 編碼規範

## TypeScript 設定
嚴格遵循 [tsconfig.json](mdc:tsconfig.json) 中的配置：
- 啟用嚴格模式
- 禁用 any 類型
- 要求明確回傳類型

## 程式碼格式化
- Prettier 設定：[.prettierrc](mdc:.prettierrc)
- ESLint 設定：[.eslintrc.json](mdc:.eslintrc.json)
- EditorConfig：[.editorconfig](mdc:.editorconfig)

## 命名規範

### 檔案命名
- 元件：PascalCase（UserProfile.tsx）
- 工具函數：camelCase（formatDate.ts）
- 常數：UPPER_SNAKE_CASE（API_ENDPOINTS.ts）
- 類型定義：PascalCase（UserType.ts）

### 變數命名
// 好的範例
const userName = 'john_doe';
const isUserLoggedIn = true;
const userProfileData = {...};

// 避免的範例
const u = 'john_doe';
const flag = true;
const data = {...};

## 元件規範

### React 元件
參考標準元件範例：[src/components/Button/Button.tsx](mdc:src/components/Button/Button.tsx)

#### 元件結構
interface ComponentProps {
  // 明確定義 props 類型
}

export const ComponentName: React.FC<ComponentProps> = ({ 
  // 解構 props
}) => {
  // 元件邏輯
  
  return (
    // JSX 結構
  );
};

#### PropTypes 和 TypeScript
- 優先使用 TypeScript 界面
- 為複雜 props 提供預設值
- 使用泛型提高重用性

### 自訂 Hooks
自訂 hooks 放在 [src/hooks/](mdc:src/hooks/) 資料夾中。
參考範例：[src/hooks/useLocalStorage.ts](mdc:src/hooks/useLocalStorage.ts)

## 樣式規範

### CSS Modules
使用 CSS Modules 進行樣式隔離。
檔案命名：Component.module.css

### 設計令牌
全域設計令牌定義在：[src/styles/tokens.css](mdc:src/styles/tokens.css)

## 測試規範
測試檔案參考：[src/components/Button/Button.test.tsx](mdc:src/components/Button/Button.test.tsx)

### 測試檔案位置
- 單元測試：與被測試檔案同目錄
- 整合測試：[tests/integration/](mdc:tests/integration/)
- E2E 測試：[tests/e2e/](mdc:tests/e2e/)
```

## 🎯 最佳實踐

### 1. 規則組織
- **模組化**：將規則分成邏輯相關的檔案
- **具體性**：提供具體的檔案引用而不是抽象描述
- **即時性**：保持規則與實際專案狀態同步

### 2. 檔案引用策略
- **頻繁引用重要檔案**：package.json、配置檔案等
- **提供範例**：引用具體的實作範例
- **保持路徑正確**：確保所有引用路徑都存在

### 3. 團隊協作
- **統一規則**：確保所有團隊成員使用相同的規則
- **版本控制**：將 `.cursor/rules/` 目錄納入版本控制
- **定期更新**：隨專案演進更新規則

## 🚀 實際應用場景

### 場景 1：新專案設定
```markdown
問題：「根據我們的架構規則建立一個新的使用者管理功能」

Cursor 會自動：
1. 讀取 architecture.mdc 規則
2. 參考現有元件結構
3. 遵循編碼規範
4. 建立符合專案標準的程式碼
```

### 場景 2：程式碼重構
```markdown
問題：「重構這個元件，使其符合我們的編碼規範」

Cursor 會：
1. 檢查 coding-standards.mdc
2. 參考現有最佳實踐範例
3. 應用一致的命名和結構
4. 確保符合 TypeScript 規範
```

## 📊 效果比較

| 情況 | 沒有 Cursor Rules | 有 Cursor Rules |
|------|------------------|----------------|
| AI 理解專案結構 | 需要每次解釋 | 自動理解 |
| 程式碼一致性 | 需要手動檢查 | 自動遵循 |
| 新人上手 | 需要大量說明 | 快速適應 |
| 重構效率 | 容易偏離標準 | 保持一致性 |

---

**相關指南：**
- [新手入門指南](./01-getting-started.md)
- [團隊設定指南](./02-team-setup.md)
- [Cursor 獨有功能詳解](./08-cursor-unique-features.md) 
- [Agent Rules 大全](https://github.com/steipete/agent-rules)