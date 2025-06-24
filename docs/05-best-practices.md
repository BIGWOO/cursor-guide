# Cursor 團隊最佳實踐

## 🎯 目標

建立 Cursor 使用最佳實踐，提升團隊開發效率和程式碼品質。

## 💻 編輯器設定最佳實踐

### 1. 工作區配置

**專案根目錄結構：**
```
project-root/
├── .vscode/
│   ├── settings.json          # 專案特定設定
│   ├── extensions.json        # 推薦擴充功能
│   ├── launch.json           # 除錯配置
│   └── tasks.json            # 任務配置
├── .cursorrules              # Cursor AI 規則
├── .prettierrc               # 程式碼格式化
├── .eslintrc.json           # 程式碼檢查
└── README.md                # 專案說明
```

**settings.json 最佳實踐：**
```json
{
  // 效能優化
  "files.watcherExclude": {
    "**/node_modules/**": true,
    "**/dist/**": true,
    "**/build/**": true,
    "**/.git/**": true
  },
  
  // 自動儲存與格式化
  "files.autoSave": "onFocusChange",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": true,
    "source.organizeImports": true
  },
  
  // AI 最佳化設定
  "cursor.chat.defaultModel": "gpt-4",
  "cursor.general.enableAIFeatures": true,
  "cursor.cpp.enableAIFeatures": true,
  
  // 開發體驗優化
  "editor.minimap.enabled": true,
  "editor.lineNumbers": "on",
  "editor.rulers": [80, 120],
  "editor.wordWrap": "bounded",
  "editor.wordWrapColumn": 120
}
```

### 2. .cursorrules 設定

**建立 .cursorrules 檔案：**
```markdown
# Cursor AI 規則設定

## 程式碼風格
- 使用 TypeScript 進行開發
- 遵循 ESLint 和 Prettier 規範
- 變數命名使用 camelCase
- 常數使用 UPPER_SNAKE_CASE
- 類別名稱使用 PascalCase

## 程式碼結構
- 每個檔案長度不超過 300 行
- 函數長度不超過 50 行
- 使用純函數優於副作用函數
- 優先使用 async/await 而非 Promise

## 註解規範
- 複雜邏輯必須加註解
- 公開 API 需要 JSDoc
- TODO 註解包含負責人和日期
- 範例：// TODO(john): 2024-01-15 優化查詢效能

## 錯誤處理
- 所有 async 函數都要有錯誤處理
- 使用具體的錯誤類型
- 記錄錯誤日誌
- 用戶友善的錯誤訊息

## 測試要求
- 新功能必須包含單元測試
- 測試覆蓋率至少 80%
- 使用描述性的測試名稱
- 遵循 AAA 模式（Arrange, Act, Assert）
```

## 🧠 AI 協作最佳實踐

### 1. 提示詞工程

**結構化提示詞模板：**
```markdown
**角色設定**
你是一位資深的 [技術棧] 工程師

**上下文**
專案類型：[Web應用/API/Mobile App]
技術棧：[React/Node.js/Python等]
目前狀況：[具體描述]

**任務描述**
需要實作：[具體功能]
輸入：[輸入參數]
輸出：[預期結果]
限制：[技術限制或需求]

**品質要求**
- 程式碼可讀性高
- 包含錯誤處理
- 遵循團隊規範
- 加入適當註解
```

**範例應用：**
```markdown
**角色設定**
你是一位資深的 Node.js 後端工程師

**上下文**
專案類型：電商 API 服務
技術棧：Node.js + Express + MongoDB
目前狀況：需要新增商品管理功能

**任務描述**
需要實作：商品建立 API 端點
輸入：商品名稱、價格、描述、分類
輸出：建立成功的商品資料
限制：需要輸入驗證和權限檢查

**品質要求**
- 使用 Express Router
- 包含 Joi 驗證
- 遵循 RESTful 設計
- 加入 JSDoc 註解
```

### 2. 程式碼生成策略

**分層漸進式開發：**

**第一層：基本結構**
```javascript
// 使用 Ctrl+K 生成基本框架
"建立一個商品管理服務的基本結構，包含 CRUD 操作的方法簽名"
```

**第二層：核心邏輯**
```javascript
// 選中每個方法，逐一實作
"實作 createProduct 方法，包含輸入驗證和資料庫操作"
```

**第三層：錯誤處理**
```javascript
// 加入錯誤處理機制
"為這個方法加入完整的錯誤處理，包含自定義錯誤類型"
```

**第四層：測試撰寫**
```javascript
// 生成對應測試
"為 createProduct 方法撰寫完整的單元測試，包含正常和異常情況"
```

### 3. 重構最佳實踐

**重構工作流程：**

1. **理解現有程式碼**
```markdown
"分析這段程式碼的功能和潛在問題"
```

2. **制定重構計劃**
```markdown
"為這段程式碼制定重構計劃，優先考慮可讀性和效能"
```

3. **逐步重構**
```markdown
"將這個大函數分解為多個小函數，保持功能不變"
```

4. **驗證重構結果**
```markdown
"檢查重構後的程式碼是否遵循 SOLID 原則"
```

## 🔧 開發流程最佳實踐

### 1. 功能開發流程

**開發前準備：**
```markdown
1. 閱讀需求文件
2. 設計 API 介面
3. 建立測試案例
4. 設定開發環境
```

**開發中實踐：**
```markdown
1. 小步驟頻繁提交
2. 及時同步主分支
3. 持續執行測試
4. 定期程式碼審查
```

**開發後檢查：**
```markdown
1. 完整測試覆蓋
2. 程式碼品質檢查
3. 效能基準測試
4. 文件更新
```

### 2. 除錯最佳實踐

**使用 Cursor 內建除錯器：**

**launch.json 設定：**
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch Node.js",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/src/app.js",
      "env": {
        "NODE_ENV": "development"
      },
      "console": "integratedTerminal",
      "skipFiles": ["<node_internals>/**"]
    },
    {
      "name": "Debug Jest Tests",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": ["--runInBand"],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}
```

**除錯技巧：**
```javascript
// 1. 使用有意義的 console.log
console.log('[DEBUG] 使用者資料:', { userId, userData });

// 2. 設定條件中斷點
if (userId === 'specific-user-id') {
  debugger; // 只對特定使用者觸發
}

// 3. 使用 AI 協助分析錯誤
// 在 Ctrl+L 中提供錯誤堆疊和上下文
```

### 3. 效能優化實踐

**程式碼效能分析：**
```javascript
// 使用 AI 協助效能分析
"分析這段程式碼的效能瓶頸，並提供優化建議"

// 範例：優化前
function findUsersByAge(users, targetAge) {
  return users.filter(user => {
    return calculateAge(user.birthDate) === targetAge;
  });
}

// AI 建議：預計算年齡，避免重複計算
function findUsersByAge(users, targetAge) {
  return users
    .map(user => ({ ...user, age: calculateAge(user.birthDate) }))
    .filter(user => user.age === targetAge);
}
```

## 📊 品質保證最佳實踐

### 1. 測試策略

**測試金字塔實作：**
```markdown
單元測試 (70%)
├── 業務邏輯測試
├── 工具函數測試
└── 元件測試

整合測試 (20%)
├── API 端點測試
├── 資料庫操作測試
└── 服務間通信測試

端到端測試 (10%)
├── 用戶流程測試
├── 關鍵功能測試
└── 回歸測試
```

**測試程式碼範例：**
```javascript
// 使用 AI 生成測試
// 提示詞："為這個使用者服務撰寫完整的 Jest 測試，包含成功和失敗情況"

describe('UserService', () => {
  describe('createUser', () => {
    it('應該成功建立新使用者', async () => {
      // Arrange
      const userData = {
        name: 'John Doe',
        email: 'john@example.com'
      };
      
      // Act
      const result = await userService.createUser(userData);
      
      // Assert
      expect(result).toHaveProperty('id');
      expect(result.name).toBe(userData.name);
      expect(result.email).toBe(userData.email);
    });
    
    it('應該拒絕無效的電子郵件格式', async () => {
      // Arrange
      const invalidUserData = {
        name: 'John Doe',
        email: 'invalid-email'
      };
      
      // Act & Assert
      await expect(userService.createUser(invalidUserData))
        .rejects.toThrow('無效的電子郵件格式');
    });
  });
});
```

### 2. 程式碼審查檢查清單

**自動化檢查：**
```markdown
□ 程式碼通過 ESLint 檢查
□ 程式碼格式符合 Prettier 規範
□ 測試覆蓋率達到 80%
□ 沒有安全漏洞警告
□ 建置過程成功
```

**人工審查：**
```markdown
□ 程式碼邏輯正確
□ 變數命名清晰
□ 函數職責單一
□ 錯誤處理完整
□ 效能考量合理
□ 註解適當且準確
□ 符合團隊架構規範
```

### 3. 文件化實踐

**API 文件範例：**
```javascript
/**
 * 建立新使用者
 * @param {Object} userData - 使用者資料
 * @param {string} userData.name - 使用者姓名
 * @param {string} userData.email - 電子郵件地址
 * @param {string} [userData.phone] - 電話號碼（可選）
 * @returns {Promise<Object>} 建立的使用者物件
 * @throws {ValidationError} 當輸入資料無效時
 * @throws {DuplicateError} 當電子郵件已存在時
 * 
 * @example
 * const user = await createUser({
 *   name: 'John Doe',
 *   email: 'john@example.com'
 * });
 */
async function createUser(userData) {
  // 實作細節...
}
```

## 🚀 部署與維運最佳實踐

### 1. 環境設定

**多環境配置：**
```javascript
// config/index.js
const configs = {
  development: {
    port: 3000,
    database: {
      host: 'localhost',
      name: 'app_dev'
    },
    logging: 'debug'
  },
  production: {
    port: process.env.PORT || 8080,
    database: {
      host: process.env.DB_HOST,
      name: process.env.DB_NAME
    },
    logging: 'error'
  }
};

module.exports = configs[process.env.NODE_ENV || 'development'];
```

### 2. 監控與日誌

**日誌最佳實踐：**
```javascript
const logger = require('./utils/logger');

// 結構化日誌
logger.info('使用者建立成功', {
  userId: user.id,
  action: 'CREATE_USER',
  timestamp: new Date().toISOString(),
  metadata: { source: 'api', version: '1.0.0' }
});

// 錯誤日誌
logger.error('資料庫連線失敗', {
  error: error.message,
  stack: error.stack,
  operation: 'DATABASE_CONNECT'
});
```

### 3. 效能監控

**關鍵指標追蹤：**
```javascript
// 使用 AI 協助建立監控指標
"為這個 API 服務建立效能監控指標，包含回應時間、錯誤率和吞吐量"

const monitoring = {
  // 回應時間監控
  responseTime: {
    p50: '<100ms',
    p95: '<500ms',
    p99: '<1000ms'
  },
  
  // 錯誤率監控
  errorRate: {
    target: '<1%',
    critical: '>5%'
  },
  
  // 系統資源監控
  resources: {
    cpu: '<70%',
    memory: '<80%',
    diskSpace: '<85%'
  }
};
```

## 📈 持續改進實踐

### 1. 技術債務管理

**債務分類與處理：**
```markdown
## 技術債務等級

### 高優先級（立即處理）
- 安全漏洞
- 效能瓶頸
- 關鍵功能缺陷

### 中優先級（下個版本）
- 程式碼重複
- 過時的依賴套件
- 缺少測試覆蓋

### 低優先級（有時間時處理）
- 程式碼風格問題
- 註解不完整
- 小型重構機會
```

### 2. 學習與分享

**知識管理：**
```markdown
## 團隊學習計劃

### 每週分享
- 新技術探索
- 問題解決案例
- 最佳實踐更新

### 每月回顧
- 工具效率評估
- 流程改進建議
- 技術趨勢討論

### 季度規劃
- 技術棧升級
- 團隊技能提升
- 工具鏈優化
```

---

**下一步：** 查看 [常見問題解決方案](./06-troubleshooting.md) 解決使用中的問題。 