---
title: "新手第十二步：GitHub Pages 部署　免費讓你的網站上線，讓全世界看到！"
date: 2026-04-17
draft: false
description: "做完的作品放在電腦裡誰都看不到。這篇教你用 GitHub Pages 免費部署靜態網站，從靜態 HTML 到 Vite 專案全部涵蓋，5 分鐘讓你的網站有專屬網址！"
image: "https://images.unsplash.com/photo-1498050108023-c5249f4df085?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["GitHub Pages", "部署", "Git", "新手入門"]
categories: ["部署", "版本控制"]
---

你辛苦做好的網站，現在只能在自己電腦上看。把網址傳給朋友，他們看到的是一片空白。

這篇要解決這個問題——用 **GitHub Pages**，完全免費，讓你的網站有一個真正的網址，任何人在任何地方都能打開。

---

## 1. GitHub Pages 是什麼？

GitHub Pages 是 GitHub 提供的**免費靜態網站托管服務**。

你把程式碼推到 GitHub 上，GitHub 自動幫你把網站掛到網路上，給你一個這樣格式的網址：

```
https://你的帳號.github.io/你的專案名稱/
```

**它的限制：**
* 只能放**靜態網站**（HTML、CSS、JS）
* 不能跑後端程式（PHP、Node.js 伺服器端）
* 儲存庫必須是 **Public（公開）** 才能免費使用

對於前端新手來說，這些限制根本不是問題，靜態網站就夠了。

---

## 2. 方法一：部署純 HTML 靜態網頁（最簡單）

這是給剛學完 HTML/CSS/JS，還沒用 Vite 的新手。

### Step 1：建立 GitHub 儲存庫

1. 登入 GitHub，點擊右上角 **「+」→「New repository」**
2. Repository name 輸入：`portfolio`（或任何名稱）
3. 選擇 **Public**
4. 點擊 **「Create repository」**

### Step 2：把你的網站推上去

```bash
cd your-project-folder

git init
git add .
git commit -m "初次部署個人作品集"
git branch -M main
git remote add origin https://github.com/你的帳號/portfolio.git
git push -u origin main
```

### Step 3：開啟 GitHub Pages

1. 進入你的 GitHub 儲存庫頁面
2. 點擊上方的 **「Settings」**（齒輪圖示）
3. 左側選單找到 **「Pages」**
4. 在 **「Branch」** 欄位選擇 **`main`**，資料夾選 **`/ (root)`**
5. 點擊 **「Save」**

等待約 1~2 分鐘，重新整理頁面，你會看到：

```
Your site is live at https://你的帳號.github.io/portfolio/
```

**點進去，你的網站上線了！**

---

## 3. 方法二：部署 Vite 專案（進階版）

用 Vite 建立的 Vue / React 專案，不能直接部署原始碼，需要先**打包（build）**成靜態檔案，再部署打包後的結果。

### Step 1：設定 Vite 的 `base` 路徑

打開 `vite.config.js`，加入 `base` 設定：

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
    plugins: [vue()],
    base: '/你的專案名稱/',   // ← 加入這行，名稱要和 GitHub repo 名稱一致
})
```

> 為什麼需要這個？因為 GitHub Pages 的網址是 `/專案名稱/` 開頭，不設定的話圖片和 JS 會找不到路徑。

### Step 2：在本地測試打包結果

```bash
npm run build
npm run preview
```

打開 `http://localhost:4173/你的專案名稱/`，確認打包後的頁面正常。

### Step 3：使用 GitHub Actions 自動部署

這是最推薦的方式——每次你 `git push`，GitHub 自動幫你重新打包並部署，完全不需要手動操作。

在專案根目錄建立以下路徑的檔案：

```
.github/
└── workflows/
    └── deploy.yml
```

**`.github/workflows/deploy.yml` 的內容：**

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main   # 只有推送到 main 分支時才觸發

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

### Step 4：推上 GitHub 觸發自動部署

```bash
git add .
git commit -m "設定 GitHub Actions 自動部署"
git push
```

### Step 5：在 GitHub 設定 Pages 來源

1. 進入 GitHub 儲存庫的 **Settings → Pages**
2. **Branch** 改選 **`gh-pages`**（GitHub Actions 會自動建立這個分支）
3. 點擊 **Save**

等待 1~3 分鐘，你的 Vite 專案就上線了！

之後每次 `git push` 到 `main`，GitHub Actions 自動重新部署，完全不需要你做任何額外動作。

---

## 4. 查看部署狀態

怎麼知道部署有沒有成功？

1. 進入 GitHub 儲存庫頁面
2. 點擊上方的 **「Actions」** 分頁
3. 你會看到每一次觸發的部署流程，綠色勾勾 ✅ 代表成功，紅色叉叉 ❌ 代表有錯誤

點進去可以看到詳細的 log，方便排查問題。

---

## 5. 自訂網域（選用）：讓網址更專業

預設的網址是 `你的帳號.github.io/專案名稱`，如果你買了自己的網域（例如 `ericweb.com`），可以設定讓 GitHub Pages 使用你的網域。

### Step 1：在 GitHub Pages 設定自訂網域

1. Settings → Pages → Custom domain
2. 輸入你的網域（例如 `www.ericweb.com`）
3. 勾選 **「Enforce HTTPS」**

### Step 2：在你的網域服務商設定 DNS

**如果用 `www` 子網域（建議）：**

新增一筆 `CNAME` 紀錄：
```
類型: CNAME
名稱: www
值:   你的帳號.github.io
```

**如果用根網域（例如直接 `ericweb.com`）：**

新增四筆 `A` 紀錄：
```
類型: A
名稱: @
值:   185.199.108.153
      185.199.109.153
      185.199.110.153
      185.199.111.153
```

DNS 生效需要幾分鐘到數小時，生效後你的網域就會指向 GitHub Pages 的內容。

---

## 6. 常見問題排查

### 網站打開是空白的 / 404
* 確認 `vite.config.js` 的 `base` 路徑和 GitHub repo 名稱**完全一致**
* 確認 GitHub Pages 設定的 Branch 是否正確（靜態網站選 `main`，Vite 專案選 `gh-pages`）

### 圖片顯示不出來
* 檢查圖片路徑是否使用**相對路徑**
* 放在 `public/` 資料夾的圖片，在程式碼裡用 `/圖片名稱.jpg` 引用

### GitHub Actions 部署失敗
* 點進 Actions 頁面查看錯誤訊息
* 最常見原因：`npm install` 失敗（`package.json` 有問題）或 `npm run build` 有語法錯誤

### 更新了程式碼但網站沒變
* GitHub Pages 有快取，等待幾分鐘再重新整理
* 或按 `Ctrl + Shift + R`（強制重新整理，清除瀏覽器快取）

---

## 7. 完整部署流程速查

```
靜態 HTML 網站
──────────────
git init → git add . → git commit → git push
→ GitHub Settings → Pages → 選 main 分支 → 完成

Vite 專案
──────────
1. vite.config.js 加入 base: '/repo名稱/'
2. 建立 .github/workflows/deploy.yml
3. git add . → git commit → git push
4. GitHub Settings → Pages → 選 gh-pages 分支 → 完成
5. 往後每次 git push 自動重新部署
```

---

## 8. 給新手的實戰練習

把你之前做的作品集網頁部署上 GitHub Pages：

1. 確認你的 `index.html` 在專案的根目錄
2. 確認有 `.gitignore`，排除 `node_modules/`
3. 執行部署流程
4. 把網址傳給朋友，讓他們幫你看看！

---

## 結語：你的作品現在活在網路上了

從今天起，你做的每一個前端作品都可以有一個真實的網址：

* 求職時附在履歷上
* 貼在社群媒體讓更多人看到
* 傳給朋友炫耀

GitHub Pages 是你踏入真實世界的第一步。免費、穩定、和 Git 工作流程無縫整合——沒有理由不用。

**接下來你可以做什麼？**
你已經學完了前端開發的完整路徑，從 HTML 到 Vite，從 Git 到部署。接下來我們要進入一個讓很多人又愛又怕的主題：**JavaScript 非同步（Async / Await）與 API 串接**——讓你的網頁能從後端取得真實資料，做出動態內容！

**準備好讓網頁和真實資料連接了嗎？下一篇見！**
