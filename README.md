# git-examples
A demo of git exmples

---

# ken7667 fork

這份筆記記錄我用 **Fork（分岔）** 的方式參與別人專案的完整流程。
母專案是別人的 `git-examples`，子專案則是我自己帳號底下的副本。整個概念一句話總結：

> **個人子專案是草稿本，Pull Request 是交作業給母專案的作者。**

---

## 1. 我的專案連結

* **母專案（原作者）**：`https://github.com/se-dd5/git-examples`
* **子專案（我的 Fork）**：`https://github.com/ken7667/git-examples`
* **Remote 名稱**：`origin`（指向我的子專案）

---

## 2. 建立 GitHub 子專案（Fork）🍴

1. 開啟母專案頁面：`https://github.com/se-dd5/git-examples`
2. 點擊右上角的 **Fork** 按鈕。
3. 成功後在我的帳號下產生一份副本 `ken7667/git-examples`。

> 💡 **為什麼要 Fork？**
> 這樣我就可以直接在自己的一份副本上改東西、送 PR，完全不需要母專案作者的額外權限。

---

## 3. 把專案抓回本機（Clone）📥

```bash
# 使用 SSH 安全連線，將自己的子專案 Clone 到本機
git clone git@github.com:ken7667/git-examples.git

# 切換進入專案資料夾
cd git-examples
```

> 🔑 **為什麼用 `git@github.com:` 而不是 `https://github.com/`？**
> 兩種都能下載，但 SSH 不用每次都輸入帳密，之後 `git push` 也比較方便。

---

## 4. 【觀念】分支（Branch）的控制指令 🌿

```bash
# 檢視目前所有分支
git branch

# 創造新分支，並直接切換過去（合體快捷指令）
git checkout -b developGitBranch
```

> 💡 `-b` 就是 **branch** 的意思，代表「建立新分支後順便 checkout 過去」，
> 等同於 `git branch developGitBranch` + `git checkout developGitBranch` 兩步驟。

---

## 5. 修改檔案與本地提交（Commit & Merge）✍️

在本地對專案進行實際修改，並把變更記錄到 Git 歷史中。

### 新增檔案並提交

```bash
# 將工作區所有新增、修改的檔案（包含 ken7667Fork.md）加入暫存區
git add .

# 提交變更並記錄說明訊息
git commit -m "add ken7667Fork.md"
```

### 【觀念】如何進行本地合併（Merge）

如果今天在 `developGitBranch` 分支寫好功能，要將其合併回 `main` 分支：

```bash
git checkout main              # 先切換回接收變更的主分支
git merge developGitBranch     # 【本地合併】將開發分支的內容融合進來
```

---

## 6. 申請合併回母專案（Pull Request）🔀

> 注意：這一步**不是在 GitHub 網頁外**，而是在自己的子專案頁面上發起。

1. 開啟我的子專案網頁：`https://github.com/ken7667/git-examples`
2. 點擊畫面上方自動跳出來的黃綠色提示鈕 **「Compare & pull request」**。
3. 設定正確的對比方向（左邊選母專案，右邊選自己的子專案）：

   | 欄位 | 專案 | 分支 |
   | --- | --- | --- |
   | **base repository** | `se-dd5/git-examples` | `main` |
   | **head repository** | `ken7667/git-examples` | `developGitBranch` |

4. 填寫標題與說明後，點擊 **「Create pull request」**，正式遞交合併申請！

---

## 7. 整份流程一次看完 🔄

```
Fork（GitHub 網頁）
   ↓
git clone（抓回本機）
   ↓
git checkout -b developGitBranch（開新分支）
   ↓
修改檔案 → git add . → git commit -m "..."（本地提交）
   ↓
git checkout main → git merge developGitBranch（本地合併）
   ↓
git push（把變動推上我的子專案）
   ↓
Compare & pull request → Create pull request（申請合併回母專案）
```

---

## 8. 小提醒 ⚠️

* `git add .` 會把**整個資料夾**所有變更都加入暫存區，包含 `.git` 以外的雜項檔案；
  如果只想加單一檔案，用 `git add 檔名` 會更安全。
* 在合併（`merge`）之前，先 `git status` 確認工作區是乾淨的，
  有未提交的變更時 Git 會 refuse 讓你合併。
* `main` 分支是「隨時都能跑的穩定版本」，所以實務上不直接在 `main` 上寫 code，
  而是開一條分支開發，確定沒問題了再合併回去。