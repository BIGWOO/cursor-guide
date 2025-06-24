# Cursor 程式碼協作流程

## 🤝 團隊協作概述

有效的程式碼協作是團隊成功的關鍵。Cursor 提供多種協作工具，幫助團隊建立高效的開發流程。

## 🚀 即時協作功能

### 1. 即時協作解決方案

**Cursor 協作選項：**

> ⚠️ **注意**：Cursor 目前不支援 Microsoft Live Share 擴充功能

**推薦替代方案：**

1. **CodeTogether**（推薦）
   ```powershell
   # 透過擴充功能市集安裝 CodeTogether
   # 搜尋 "CodeTogether" 並安裝
   ```

2. **其他協作方式：**
   - Git 頻繁提交協作
   - Teams/Zoom 螢幕分享
   - 遠端桌面協作

**CodeTogether 使用：**

```powershell
# 啟動協作會話
# 按 Ctrl+Shift+P，搜尋 "CodeTogether: Start Hosting Session"
```

**協作功能：**
- 即時程式碼編輯
- 多人游標顯示
- 語音通話支援
- 瀏覽器端協作

### 2. 協作最佳實踐

**主持人（Host）責任：**
- 確保專案環境正確
- 設定適當的權限
- 引導協作流程
- 管理協作會話

**參與者（Guest）責任：**
- 主動溝通意圖
- 遵循團隊規範
- 適時詢問問題
- 尊重主持人決定

## 📋 程式碼審查流程

### 1. Pull Request 工作流程

**步驟 1：建立功能分支**

```powershell
# 從主分支建立新分支
git checkout -b feature/user-authentication

# 或者使用更描述性的命名
git checkout -b feature/JIRA-123-user-login
```

**步驟 2：開發與提交**

```powershell
# 頻繁的小提交
git add .
git commit -m "feat: 新增使用者登入表單驗證"

# 推送到遠端
git push origin feature/user-authentication
```

**步驟 3：建立 Pull Request**

```markdown
## Pull Request 模板

### 變更摘要
簡潔描述這次變更的內容

### 變更類型
- [ ] 新功能
- [ ] Bug 修復
- [ ] 重構
- [ ] 文件更新
- [ ] 效能改善

### 測試
- [ ] 單元測試通過
- [ ] 整合測試通過
- [ ] 手動測試完成

### 檢查清單
- [ ] 程式碼符合團隊規範
- [ ] 無 lint 錯誤
- [ ] 已更新相關文件
- [ ] 已處理所有 TODO 註解
```

### 2. 程式碼審查標準

**審查重點：**

1. **功能正確性**
   - 邏輯是否正確
   - 邊界條件處理
   - 錯誤處理機制

2. **程式碼品質**
   - 可讀性和可維護性
   - 命名規範
   - 程式碼結構

3. **效能考量**
   - 時間複雜度
   - 空間複雜度
   - 資源使用效率

4. **安全性**
   - 輸入驗證
   - 授權檢查
   - 敏感資料處理

**審查方法：**

```markdown
## 審查評論範例

### 建議改進
```javascript
// 建議：使用更描述性的變數名稱
// 原本：const d = new Date();
// 建議：const currentDate = new Date();
```

### 讚賞好的做法
```javascript
// 👍 很好的錯誤處理方式
try {
  await userService.createUser(userData);
} catch (error) {
  logger.error('使用者建立失敗', error);
  throw new UserCreationError(error.message);
}
```
```

## 🔧 Git 工作流程最佳實踐

### 1. 分支策略

**Git Flow 模型：**

```
main (主分支)
├── develop (開發分支)
│   ├── feature/user-auth (功能分支)
│   ├── feature/payment-system (功能分支)
│   └── bugfix/login-error (修復分支)
└── release/v1.2.0 (發布分支)
```

**分支命名規範：**

```powershell
# 功能開發
git checkout -b feature/JIRA-123-user-authentication

# Bug 修復
git checkout -b bugfix/JIRA-456-fix-login-error

# 熱修復
git checkout -b hotfix/JIRA-789-critical-security-fix

# 發布準備
git checkout -b release/v1.2.0
```

### 2. 提交訊息規範

**Conventional Commits 格式：**

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**範例：**

```powershell
# 功能新增
git commit -m "feat(auth): 新增 JWT 身份驗證功能"

# Bug 修復
git commit -m "fix(login): 修復密碼驗證邏輯錯誤"

# 文件更新
git commit -m "docs(api): 更新 API 文件範例"

# 重構
git commit -m "refactor(user): 重構使用者服務層程式碼"

# 效能改善
git commit -m "perf(database): 優化使用者查詢效能"
```

### 3. 合併策略

**Squash and Merge（推薦）：**

```powershell
# 將功能分支的多個提交合併為一個
git checkout main
git merge --squash feature/user-auth
git commit -m "feat: 完整實作使用者身份驗證功能"
```

**好處：**
- 保持主分支歷史清潔
- 每個功能一個提交
- 容易回滾變更

## 👥 團隊協作規範

### 1. 日常協作流程

**晨會同步（Daily Standup）：**
```markdown
1. 昨天完成了什麼？
2. 今天計劃做什麼？
3. 遇到什麼阻礙？
4. 需要什麼協助？
```

**程式碼配對（Pair Programming）：**
- 使用 CodeTogether 或螢幕分享進行遠端配對
- 定期輪換 Driver 和 Navigator 角色
- 專注於複雜邏輯和關鍵功能

### 2. 衝突解決

**合併衝突處理：**

```powershell
# 1. 更新本地分支
git checkout feature/my-feature
git pull origin main

# 2. 解決衝突
# 在 Cursor 中使用內建的合併工具

# 3. 完成合併
git add .
git commit -m "resolve: 解決與主分支的合併衝突"
```

**衝突預防：**
- 頻繁同步主分支
- 保持功能分支短小
- 及時溝通變更計劃

### 3. 程式碼所有權

**集體所有制原則：**
- 任何人都可以修改任何程式碼
- 修改前要理解程式碼邏輯
- 重大修改需要通知原作者

**責任分區：**
```markdown
- Frontend: 前端團隊負責
- Backend API: 後端團隊負責
- Database: 資料庫專家負責
- DevOps: 維運團隊負責
```

## 🛠️ 協作工具整合

### 1. 專案管理工具

**JIRA 整合：**
```powershell
# 分支命名包含 JIRA 票號
git checkout -b feature/PROJ-123-user-dashboard

# 提交訊息包含票號
git commit -m "feat: PROJ-123 實作使用者儀表板"
```

**Trello/Asana 整合：**
- PR 描述中包含卡片連結
- 完成後自動移動卡片狀態

### 2. 通訊工具整合

**Slack/Teams 通知：**
```markdown
# GitHub/GitLab Webhook 設定
- PR 建立/更新通知
- 程式碼審查狀態
- 部署結果通知
```

### 3. CI/CD 整合

**GitHub Actions 範例：**

```yaml
name: Code Review Automation

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm ci
      - name: Run linting
        run: npm run lint
      - name: Run tests
        run: npm test
```

## 📊 協作效率評估

### 1. 評估指標

**開發速度：**
- 功能交付週期
- 程式碼審查時間
- 部署頻率

**品質指標：**
- Bug 發現率
- 程式碼重工率
- 客戶滿意度

**團隊協作：**
- 知識分享頻率
- 協作工具使用率
- 團隊滿意度調查

### 2. 持續改進

**定期回顧：**
```markdown
## Sprint 回顧議題
1. 這個週期什麼進行得很順利？
2. 遇到了哪些挑戰？
3. 下個週期如何改進？
4. 需要調整哪些流程？
```

**流程優化：**
- 簡化不必要的流程
- 自動化重複性工作
- 提升工具整合度

## ⚠️ 常見協作問題

### 問題 1：程式碼衝突頻繁

**原因：**
- 分支過大或存在時間過長
- 多人修改同一文件
- 缺乏溝通協調

**解決方案：**
- 保持小而頻繁的提交
- 提前溝通變更計劃
- 及時同步主分支

### 問題 2：審查效率低下

**原因：**
- PR 過大難以審查
- 缺乏審查標準
- 審查者負擔過重

**解決方案：**
- 限制 PR 大小（建議 <400 行）
- 建立審查檢查清單
- 輪流分配審查任務

### 問題 3：知識孤島

**原因：**
- 程式碼缺乏文件
- 知識集中在少數人
- 缺乏知識分享機制

**解決方案：**
- 要求程式碼文件化
- 定期技術分享會
- 實施程式碼配對

---

**下一步：** 學習 [最佳實踐](./05-best-practices.md) 提升團隊開發品質。 