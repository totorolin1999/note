# 常用Git指令

## 設定配置

```bash
# 設定用戶名稱
git config --global user.name "你的名字"

# 設定郵箱
git config --global user.email "你的郵箱@example.com"

# 查看配置
git config --list
```

## 基礎指令

```bash
# 初始化Git倉庫
git init

# 查看當前狀態
git status

# 將檔案加入暫存區
git add <檔案名稱>
git add .  # 加入所有修改的檔案

# 提交變更
git commit -m "提交說明"

# 查看提交歷史
git log
git log --oneline  # 簡潔模式
```

## 分支操作

```bash
# 查看分支
git branch

# 創建分支
git branch <分支名稱>

# 切換分支
git checkout <分支名稱>
git switch <分支名稱>  # Git 2.23版本後的新指令

# 創建並切換分支
git checkout -b <分支名稱>
git switch -c <分支名稱>  # Git 2.23版本後的新指令

# 合併分支
git merge <分支名稱>

# 刪除分支
git branch -d <分支名稱>  # 安全刪除
git branch -D <分支名稱>  # 強制刪除
```

## 遠端操作

```bash
# 複製遠端倉庫
git clone <倉庫URL>

# 查看遠端倉庫
git remote -v

# 添加遠端倉庫
git remote add <遠端名稱> <倉庫URL>

# 從遠端倉庫獲取更新
git fetch <遠端名稱>

# 從遠端倉庫獲取更新並清除已刪除的遠端分支
git fetch --prune
git fetch -p  # 簡短版本

# 從遠端倉庫拉取更新並合併
git pull <遠端名稱> <分支名稱>

# 推送到遠端倉庫
git push <遠端名稱> <分支名稱>

# 刪除遠端分支
git push <遠端名稱> --delete <分支名稱>
```

## 修改與回退

```bash
# 查看修改的內容
git diff

# 撤銷暫存區的修改
git restore --staged <檔案名稱>
git reset HEAD <檔案名稱>  # 舊版指令

# 撤銷工作區的修改
git restore <檔案名稱>
git checkout -- <檔案名稱>  # 舊版指令

# 回退到某個提交
git reset --soft <commit-id>  # 只撤銷提交，保留修改在暫存區
git reset --mixed <commit-id>  # 撤銷提交和暫存，保留修改在工作區
git reset --hard <commit-id>  # 撤銷提交、暫存和工作區修改

# 撤銷已推送的提交
git revert <commit-id>
```

## 儲藏與標籤

```bash
# 儲藏當前修改
git stash

# 查看儲藏列表
git stash list

# 應用儲藏
git stash apply  # 保留儲藏記錄
git stash pop  # 應用後刪除儲藏記錄

# 創建標籤
git tag <標籤名稱>
git tag -a <標籤名稱> -m "標籤說明"

# 查看標籤
git tag

# 查看標籤詳情
git show <標籤名稱>

# 推送標籤到遠端
git push <遠端名稱> <標籤名稱>
git push <遠端名稱> --tags  # 推送所有標籤
```

## 高級操作

```bash
# 合併多個提交
git rebase -i <commit-id>

# 暫存部分修改
git add -p <檔案名稱>

# 修改最後一次提交
git commit --amend

# 尋找引入Bug的提交
git bisect start
git bisect bad  # 標記當前版本有問題
git bisect good <commit-id>  # 標記某個版本正常

# 清理無用檔案
git clean -f  # 刪除未追蹤的檔案
git clean -fd  # 刪除未追蹤的檔案和目錄
```

## 刪除 GitHub 上的 Commit

在 GitHub 上刪除已推送的 commit 需要謹慎操作，因為這會改變歷史記錄。以下是幾種方法：

### 方法一：使用 git reset 和強制推送

```bash
# 重置到指定的 commit (保留本地檔案變更)
git reset --soft <要回退到的commit-id>
# 或
git reset --mixed <要回退到的commit-id>

# 重置到指定的 commit (不保留本地檔案變更，謹慎使用)
git reset --hard <要回退到的commit-id>

# 強制推送到遠端倉庫，覆蓋遠端記錄
git push --force origin <分支名稱>
# 或使用稍微安全的方式
git push --force-with-lease origin <分支名稱>
```

### 方法二：使用 git revert 創建新的撤銷提交

```bash
# 撤銷指定的 commit，會創建一個新的提交
git revert <commit-id>

# 撤銷一系列的 commits
git revert <較早的commit-id>..<較新的commit-id>

# 推送到遠端
git push origin <分支名稱>
```

### 方法三：使用交互式 rebase 移除或修改 commit

```bash
# 進入交互式 rebase 模式
git rebase -i <要修改commit之前的commit-id>

# 在編輯器中：
# - 刪除要移除的 commit 所在行
# - 或將 pick 改為 drop
# - 或將 pick 改為 edit 來修改 commit

# 完成 rebase 後強制推送
git push --force origin <分支名稱>
```

### 注意事項

- 使用 `--force` 會覆蓋遠端倉庫，可能會影響其他協作者的工作
- 在共享分支上修改歷史應當提前通知所有協作者
- 在重要的生產環境分支上應避免使用這些操作
- 部分團隊或倉庫可能設置了分支保護規則，禁止強制推送

## 常見工作流

### 功能分支工作流

```bash
# 創建並切換到功能分支
git checkout -b feature-x

# 開發完成後，提交變更
git add .
git commit -m "完成功能x開發"

# 切換到主分支並更新
git checkout main
git pull origin main

# 合併功能分支
git merge feature-x

# 推送到遠端
git push origin main

# 刪除功能分支
git branch -d feature-x
```

### Git Flow工作流

```bash
# 創建功能分支
git checkout -b feature/x develop

# 完成功能開發後合併到develop
git checkout develop
git merge --no-ff feature/x

# 創建發布分支
git checkout -b release/1.0 develop

# 發布完成後合併到main和develop
git checkout main
git merge --no-ff release/1.0
git tag -a v1.0 -m "Version 1.0"

git checkout develop
git merge --no-ff release/1.0

# 刪除發布分支
git branch -d release/1.0
```

## 技巧與最佳實踐

- 經常提交小的、邏輯完整的變更
- 寫清晰的提交信息
- 使用 .gitignore 忽略不需要版本控制的檔案
- 定期從上游拉取更新
- 使用分支進行功能開發
- 在合併前進行程式碼審核
- 善用 Git Hooks 進行自動化檢查
