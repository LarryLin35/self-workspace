# Self-Workspace

## 在另一台機器設定 Git

這個 repository 使用個人 GitHub 身分，不使用公司的 Git 提交身分或已儲存的公司憑證。

### 1. Clone repository

```bash
git clone https://github.com/LarryLin35/Self-Workspace.git
cd Self-Workspace
```

如果已經 clone 過舊名稱的 repository，只需要更新 remote URL：

```bash
git remote set-url origin https://github.com/LarryLin35/Self-Workspace.git
```

### 2. 設定此 repository 專用的提交身分

以下設定只會寫入這個 repository 的 `.git/config`，不會改動其他 repository 的設定：

```bash
git config --local user.name "LarryLin35"
git config --local user.email "good.cool112233@gmail.com"
git config --local credential.helper ""
git config --local commit.gpgsign false
```

- 空白的 `credential.helper` 會清除從全域設定繼承的 credential helper，避免自動使用公司帳號所儲存的憑證。
- `commit.gpgsign=false` 會停用這個 repository 的自動 commit 簽章，不影響其他 repository。
- `user.name` 和 `user.email` 是 commit 作者資訊，不等於 push 時使用的 GitHub 登入帳號。

### 3. 第一次 push

```bash
git push
```

Git 要求驗證時，使用 `LarryLin35` 的個人 GitHub 憑證或 personal access token。IDE、AskPass 或其他外部 credential manager 提供的憑證仍會決定實際 push 帳號。不要把 token 寫進 remote URL、Git 設定或 README。

### 4. 確認設定

```bash
git config --local --get user.name
git config --local --get user.email
git config --local --get-all credential.helper
git config --local --get commit.gpgsign
git remote -v
```

預期結果：

- 使用者名稱：`LarryLin35`
- Email：`good.cool112233@gmail.com`
- Credential helper：空白
- Commit GPG signing：`false`
- Remote：`https://github.com/LarryLin35/Self-Workspace.git`
