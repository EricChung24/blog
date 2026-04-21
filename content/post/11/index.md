---
title: "新手第十一步：Git 入門　工程師的時光機，讓你的程式碼永遠有後悔藥！"
date: 2026-04-17
weight: 11
draft: false
description: "每個工程師都必備的技能。Git 讓你隨時回到過去的版本、和別人一起協作、把作品放上 GitHub 讓全世界看見——這篇從安裝到實戰，一次學完！"
image: "https://git-scm.com/images/logos/downloads/Git-Logo-2Color.png"
tags: ["Git", "GitHub", "版本控制", "新手入門"]
categories: ["版本控制", "Git"]
---

你有沒有遇過這種情況：改了一堆程式碼，結果改壞了，想回到之前的版本，卻發現根本回不去？

或者，和同學一起做專案，兩個人同時改同一個檔案，最後合併的時候整個亂掉？

**Git** 就是解決這兩個問題的神器，也是全球每一位工程師每天都在用的工具。

---

## 1. Git 是什麼？

Git 是一個**版本控制系統（Version Control System）**，它會追蹤你的程式碼每一次的變動，讓你可以：

* **隨時回到任何一個過去的版本**（像時光機）
* **多人同時開發同一個專案**（不會互相覆蓋）
* **實驗新功能而不影響主線程式碼**（用「分支」隔離）
* **知道誰改了什麼、什麼時候改的**（完整歷史紀錄）

**Git 和 GitHub 的差別：**
* **Git** — 在你電腦上運行的版本控制工具（本地端）
* **GitHub** — 一個存放 Git 儲存庫的雲端平台（遠端）

就像 Word 和 Google Drive 的關係：Word 是編輯工具，Google Drive 是儲存分享的地方。

---

## 2. 安裝 Git

### Windows
前往 [https://git-scm.com](https://git-scm.com) 下載安裝，安裝過程全部使用預設選項即可。

### Mac
打開終端機輸入：
```bash
git --version
```
如果尚未安裝，Mac 會自動提示你安裝 Xcode Command Line Tools。

### 確認安裝成功
```bash
git --version
# 出現版本號代表成功，例如：git version 2.43.0
```

---

## 3. 第一次使用 Git：設定身份

在開始用 Git 之前，要先告訴它你是誰（這些資訊會附在每一次的提交紀錄上）：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的Email"
```

**只需要設定一次**，之後所有專案都會使用這個身份。

確認設定是否成功：
```bash
git config --global --list
```

---

## 4. Git 的核心概念：三個區域

要理解 Git，最重要的是搞清楚這三個區域：

```
工作目錄               暫存區              本地儲存庫
(Working Directory)  (Staging Area)    (Local Repository)

  你寫程式碼的地方   →  準備要提交的區域  →  正式儲存版本的地方
       git add              git commit
```

* **工作目錄**：你平時寫程式的地方，Git 會追蹤這裡的變動
* **暫存區（Index）**：你決定「這些改動要放進下一個版本」就先放這裡
* **本地儲存庫**：正式存下來的版本紀錄，永遠不會消失

---

## 5. 最常用的 Git 指令

### 初始化儲存庫

```bash
# 在目前資料夾建立 Git 儲存庫
git init
```

這個指令會在你的資料夾裡建立一個隱藏的 `.git` 資料夾，Git 的所有版本資訊都存在裡面。

---

### 查看狀態

```bash
git status
```

這是你最常用的指令，它會告訴你：
* 哪些檔案被修改了（`modified`）
* 哪些檔案是新加的還沒被追蹤（`untracked`）
* 哪些改動已經在暫存區了（`staged`）

---

### 加入暫存區

```bash
# 加入指定檔案
git add index.html

# 加入多個檔案
git add index.html style.css

# 加入目前資料夾所有變動的檔案
git add .
```

---

### 提交（Commit）：正式儲存版本

```bash
git commit -m "新增導覽列元件"
```

`-m` 後面的字串是**提交訊息（Commit Message）**，用來描述這次改了什麼。

**好的 Commit Message 應該要：**
* 用動詞開頭，描述「做了什麼」
* 讓任何人一看就知道這次改動的目的

```bash
# 好的範例
git commit -m "新增登入頁面"
git commit -m "修正首頁版面在手機上跑版的問題"
git commit -m "更新 README 安裝說明"

# 不好的範例
git commit -m "update"       # 太模糊
git commit -m "fix bug"      # 什麼 bug？
git commit -m "asdfghjk"     # ???
```

---

### 查看提交歷史

```bash
# 完整歷史
git log

# 精簡版（每筆 commit 只顯示一行）
git log --oneline

# 圖形化顯示分支
git log --oneline --graph --all
```

每一筆 commit 都有一個獨一無二的 **Hash ID**（例如 `a3f5b2c`），你可以用這個 ID 回到任何一個版本。

---

### 查看改動內容

```bash
# 查看工作目錄和暫存區的差異（尚未 git add 的改動）
git diff

# 查看暫存區和上一次 commit 的差異
git diff --staged
```

---

### 回到過去的版本

```bash
# 查看歷史，找到想回去的 commit hash
git log --oneline

# 回到指定的 commit（只是「看看」，不影響現在的分支）
git checkout a3f5b2c

# 回到最新版本
git checkout main
```

**如果真的要「撤銷」最近的提交：**
```bash
# 撤銷最近一次 commit，但保留改動（改動回到工作目錄）
git reset HEAD~1

# 撤銷最近一次 commit，連改動也一起丟掉（危險！謹慎使用）
git reset --hard HEAD~1
```

---

## 6. 分支（Branch）：安全實驗新功能

分支是 Git 最強大的功能之一。想像一下：你的網站已經上線了，突然想加一個新功能，但又怕改壞原本的程式碼。

**分支讓你在「平行宇宙」裡開發，不影響主線。**

```
main (主線，已上線的穩定版本)
│
├── feature/login (你在這條分支上開發登入功能)
│
└── feature/dark-mode (另一個人在這條分支上開發深色模式)
```

### 常用分支指令

```bash
# 查看所有分支（* 號代表目前在哪條分支）
git branch

# 建立新分支
git branch feature/login

# 切換到指定分支
git checkout feature/login

# 建立並立刻切換（上面兩個指令的合體）
git checkout -b feature/login

# 刪除分支（合併完才能刪）
git branch -d feature/login
```

### 合併分支（Merge）

當你的新功能開發完畢，要把它合回主線：

```bash
# 先切回主線
git checkout main

# 把 feature/login 分支的改動合進來
git merge feature/login
```

---

## 7. 解決合併衝突（Merge Conflict）

兩個人同時改了同一個地方，Git 無法自動決定要用哪個版本，就會出現「合併衝突」。

衝突的檔案裡，Git 會自動插入標記：

```
<<<<<<< HEAD
這是你這條分支的版本
=======
這是要合併進來的另一條分支的版本
>>>>>>> feature/login
```

解決方法：
1. 打開有衝突的檔案
2. 找到 `<<<<<<<`、`=======`、`>>>>>>>` 這些標記
3. **手動決定要保留哪個版本**（或兩個都要的話，手動合併內容）
4. 刪除標記符號
5. 再次 `git add` 和 `git commit`

---

## 8. 連接到 GitHub：把程式碼放上雲端

### 第一步：在 GitHub 建立新儲存庫

1. 登入 [https://github.com](https://github.com)
2. 點擊右上角的 **「+」**，選 **「New repository」**
3. 輸入儲存庫名稱，點 **「Create repository」**

### 第二步：把本地儲存庫連接到 GitHub

GitHub 建立完後，會顯示一組指令，複製貼上執行：

```bash
# 設定遠端來源（只需要做一次）
git remote add origin https://github.com/你的帳號/你的專案.git

# 把本地的 main 分支推上去
git push -u origin main
```

以後只要用 `git push` 就能同步上去。

### 第三步：常用的遠端同步指令

```bash
# 把本地的 commit 推送到 GitHub
git push

# 把 GitHub 上的最新版本拉回來（別人改了你要同步）
git pull

# 複製別人的 GitHub 專案到本地
git clone https://github.com/帳號/專案名.git
```

---

## 9. `.gitignore`：告訴 Git 哪些檔案不要追蹤

有些檔案不應該上傳到 GitHub，例如：
* `node_modules/`（npm 套件資料夾，幾百 MB，每個人自己裝就好）
* `.env`（環境變數，裡面可能有 API 金鑰等機密資訊）
* 系統產生的暫存檔（`.DS_Store`、`Thumbs.db`）

在專案根目錄建立 `.gitignore` 檔案：

```
# .gitignore
node_modules/
dist/
.env
.env.local
.DS_Store
Thumbs.db
```

Git 會自動忽略這些檔案，不追蹤、不上傳。

---

## 10. 完整工作流程：每天的 Git 使用習慣

以下是一個健康的 Git 工作流程：

```bash
# 1. 開始工作前，先把遠端最新版本拉下來
git pull

# 2. 建立新功能分支
git checkout -b feature/新功能名稱

# 3. 開始寫程式碼...

# 4. 隨時查看改動狀態
git status

# 5. 把確定要的改動加入暫存區
git add .

# 6. 提交，寫清楚做了什麼
git commit -m "完成登入表單的驗證功能"

# 7. 繼續開發 → 繼續 git add / git commit...

# 8. 功能完成後，切回主線並合併
git checkout main
git merge feature/新功能名稱

# 9. 推上 GitHub
git push

# 10. 刪除已完成的分支（保持乾淨）
git branch -d feature/新功能名稱
```

---

## 11. 常見情境與解法

### 「不小心把不需要的檔案 add 進去了！」
```bash
# 把指定檔案從暫存區移出（改動還在，只是取消 add）
git restore --staged index.html

# 把全部檔案從暫存區移出
git restore --staged .
```

### 「想撤銷工作目錄的改動，回到上一次 commit 的樣子」
```bash
# 丟棄指定檔案的改動（危險！改動會消失）
git restore index.html
```

### 「commit 訊息打錯了，還沒 push 出去」
```bash
# 修改最近一次的 commit 訊息
git commit --amend -m "正確的 commit 訊息"
```

### 「想暫時把目前的改動藏起來，去做別的事」
```bash
# 把目前未提交的改動暫存起來
git stash

# 去做其他事...

# 把剛才藏起來的改動取回來
git stash pop
```

---

## 12. 給新手的實戰練習：把你的作品集放上 GitHub

1. **初始化你的作品集專案**
    ```bash
    cd my-portfolio
    git init
    ```

2. **建立 `.gitignore`**
    ```
    node_modules/
    dist/
    .DS_Store
    ```

3. **第一次提交**
    ```bash
    git add .
    git commit -m "初始化作品集專案"
    ```

4. **在 GitHub 建立新 repo，連接並推上去**
    ```bash
    git remote add origin https://github.com/你的帳號/portfolio.git
    git push -u origin main
    ```

5. **以後每次修改，重複這個流程**
    ```bash
    git add .
    git commit -m "更新作品集：新增 Vite 練習專案"
    git push
    ```

現在打開你的 GitHub 頁面，你的作品就在上面，有完整的歷史紀錄，全世界的工程師都能看到！

---

## 結語：版本控制，是工程師的基本素養

Git 的指令雖然多，但日常用到的其實不超過 10 個：

| 指令 | 用途 |
|------|------|
| `git init` | 初始化儲存庫 |
| `git status` | 查看目前狀態 |
| `git add .` | 加入暫存區 |
| `git commit -m ""` | 提交版本 |
| `git log --oneline` | 查看歷史 |
| `git branch` | 管理分支 |
| `git checkout` | 切換分支 |
| `git merge` | 合併分支 |
| `git push` | 推上 GitHub |
| `git pull` | 從 GitHub 拉下來 |

這 10 個指令，已經能應付你 90% 的日常需求了。

**接下來你可以做什麼？**
現在你有了作品、有了 GitHub，但如果能讓別人直接在瀏覽器上看到你的網站，那就更棒了！下一篇我們要學如何用 **GitHub Pages 免費部署靜態網站**，讓你的作品真正上線！

**準備好讓全世界看到你的作品了嗎？下一篇見！**
