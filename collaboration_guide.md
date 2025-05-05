# React Next.js 專案協作指南

歡迎加入我們的 React Next.js 專案！本文檔旨在幫助所有貢獻者了解專案協作流程和最佳實踐，確保團隊能順暢地協同工作。

## 目錄

- [環境設置](#環境設置)
- [分支管理](#分支管理)
- [提交規範](#提交規範)
- [開發流程](#開發流程)
- [程式碼審查](#程式碼審查)
- [發布流程](#發布流程)
- [專案結構](#專案結構)
- [開發規範](#開發規範)
- [常見問題](#常見問題)

## 環境設置

### 必備條件

- Node.js (版本 18.x 或以上)
- npm (版本 8.x 或以上) 或 yarn (版本 1.22.x 或以上)
- Git (版本 2.x 或以上)

### 本地開發環境設置

1. **複製儲存庫**

   ```bash
   git clone https://github.com/[組織名稱]/[專案名稱].git
   cd [專案名稱]
   ```

2. **安裝依賴**

   ```bash
   npm install
   # 或使用 yarn
   yarn install
   ```

3. **設置環境變數**

   複製 `.env.example` 檔案為 `.env.local`，並填入必要的環境變數：

   ```bash
   cp .env.example .env.local
   ```

4. **啟動開發伺服器**

   ```bash
   npm run dev
   # 或使用 yarn
   yarn dev
   ```

   開發伺服器將在 [http://localhost:3000](http://localhost:3000) 啟動。

## 分支管理

我們使用 [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/) 作為分支管理策略：

- `main`: 生產環境分支，僅包含已發布的程式碼
- `develop`: 開發主分支，包含最新的開發功能
- `feature/*`: 新功能分支
- `bugfix/*`: 錯誤修復分支
- `hotfix/*`: 緊急修復分支
- `release/*`: 釋出準備分支

### 創建新分支

開發新功能時，請從 `develop` 分支創建新的功能分支：

```bash
git checkout develop
git pull
git checkout -b feature/your-feature-name
```

## 提交規範

我們遵循 [Conventional Commits](https://www.conventionalcommits.org/) 規範進行提交：

```
<類型>[可選作用域]: <描述>

[可選正文]

[可選頁腳]
```

### 提交類型

- `feat`: 新功能
- `fix`: 錯誤修復
- `docs`: 文檔更新
- `style`: 樣式變更
- `refactor`: 程式碼重構
- `perf`: 效能優化
- `test`: 添加或修改測試
- `build`: 構建系統或外部依賴變更
- `ci`: 持續整合配置變更
- `chore`: 其他變更

### 提交範例

```
feat(auth): 實現使用者登入功能

- 添加登入表單組件
- 實現 JWT 驗證
- 創建使用者狀態管理

Closes #123
```

## 開發流程

1. **選擇任務**
   - 從專案看板或問題跟蹤系統選擇一個任務
   - 將任務標記為「進行中」

2. **建立分支**
   - 從 `develop` 分支創建新的功能或錯誤修復分支

3. **開發**
   - 遵循程式碼風格指南進行開發
   - 確保寫入適當的註釋
   - 添加必要的測試

4. **本地測試**
   - 運行單元測試：`npm test`
   - 運行整合測試：`npm run test:integration`
   - 確保所有測試通過

5. **提交更改**
   - 按照提交規範提交更改
   - 保持提交簡潔明確

6. **提交合併請求 (Pull Request)**
   - 將分支推送到遠端儲存庫
   - 創建合併請求到 `develop` 分支
   - 填寫合併請求模板

## 程式碼審查

所有程式碼變更必須經過審查才能合併到主要分支：

1. **審查者分配**
   - 每個合併請求至少需要一位審查者
   - 專案維護者將分配適當的審查者

2. **審查標準**
   - 程式碼是否符合專案風格指南
   - 功能是否按預期工作
   - 是否有足夠的測試覆蓋率
   - 是否有性能或安全問題

3. **處理反饋**
   - 及時回應審查意見
   - 根據需要進行修改並更新合併請求

## 發布流程

1. **創建發布分支**
   ```bash
   git checkout develop
   git pull
   git checkout -b release/vX.Y.Z
   ```

2. **版本號更新**
   - 更新 `package.json` 中的版本號
   - 更新 CHANGELOG.md

3. **最終測試**
   - 確保所有測試通過
   - 進行必要的手動測試

4. **合併到主分支**
   - 創建從 `release/vX.Y.Z` 到 `main` 的合併請求
   - 審查通過後合併

5. **標記版本**
   ```bash
   git checkout main
   git pull
   git tag -a vX.Y.Z -m "版本 X.Y.Z"
   git push origin vX.Y.Z
   ```

6. **更新開發分支**
   - 將發布更改合併回 `develop` 分支

## 專案結構

```
├── components/       # 可重用的 React 組件
├── pages/            # Next.js 頁面
├── public/           # 靜態資源
├── styles/           # 全局樣式
├── lib/              # 工具函數和服務
├── context/          # React Context
├── hooks/            # 自定義 React Hooks
├── models/           # 數據模型
├── api/              # API 路由處理
├── tests/            # 測試文件
├── .env.example      # 環境變數範例
├── .eslintrc.js      # ESLint 配置
├── .prettierrc       # Prettier 配置
├── next.config.js    # Next.js 配置
└── package.json      # 專案依賴
```

## 開發規範

### JavaScript/TypeScript 規範

- 使用 TypeScript 進行類型安全
- 遵循 ESLint 和 Prettier 配置
- 採用函數式編程風格
- 使用 ES6+ 特性

### React 組件規範

- 優先使用函數組件和 Hooks
- 保持組件小且專注於單一職責
- 使用 PropTypes 或 TypeScript 進行屬性類型檢查
- 命名規範：
  - 組件文件使用 PascalCase
  - React 組件使用 PascalCase
  - 變數和函數使用 camelCase

### 樣式規範

- 使用 CSS Modules 或 styled-components
- 遵循 BEM 命名約定
- 使用相對單位 (rem, em, %) 而非絕對單位 (px)

### 測試規範

- 為所有關鍵功能編寫單元測試
- 對重要用戶流程進行整合測試
- 使用 Jest 和 React Testing Library
- 保持測試簡潔明了

## 常見問題

### 如何處理合併衝突？

1. 將最新的目標分支合併到您的分支：
   ```bash
   git checkout develop
   git pull
   git checkout your-branch
   git merge develop
   ```

2. 解決衝突後，提交更改：
   ```bash
   git add .
   git commit -m "解決合併衝突"
   ```

### 如何回滾錯誤提交？

回滾特定提交：
```bash
git revert <commit-hash>
```

### 如何更新我的分支？

```bash
git checkout develop
git pull
git checkout your-branch
git merge develop
```

---

歡迎所有建議和改進！如有任何問題，請隨時在問題跟蹤系統中提出，或聯繫專案維護者。

最後更新日期: 2025年5月5日
