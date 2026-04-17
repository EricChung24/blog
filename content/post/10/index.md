---
title: "新手第十步：Vite 入門　現代前端開發環境，快到你不敢相信！"
date: 2026-04-17
draft: false
description: "還在用 CDN 引入套件？Vite 讓你在 0.1 秒內啟動開發伺服器，熱更新快到眼睛跟不上，一鍵整合 Vue、Tailwind、SCSS，是現代前端的標配工具。"
image: "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["Vite", "前端工具", "開發環境", "新手入門"]
categories: ["基礎教學"]
---

到目前為止，我們都是用 CDN 的方式引入 Bootstrap、Tailwind、Vue，這樣雖然方便，但有幾個問題：
* 每次都要連網路載入套件
* 無法使用 npm 生態系的大量套件
* 沒辦法用 SCSS、TypeScript 等工具
* 程式碼無法優化打包，上線版本會比較大

**Vite** 就是解決這些問題的現代前端建置工具，而且快得離譜。

---

## 1. Vite 是什麼？

Vite（法文「快速」的意思）是由 Vue 作者尤雨溪開發的前端建置工具。它的主要功能是：

* **開發伺服器（Dev Server）**：啟動超快，儲存檔案後頁面即時更新（HMR）
* **打包（Build）**：把你的 JS、CSS、圖片等資源打包成最優化的上線版本
* **整合能力**：支援 Vue、React、SCSS、TypeScript、Tailwind 等，幾乎什麼都能接

傳統的打包工具（如 Webpack）在大型專案啟動時可能要等 30~60 秒，**Vite 通常在 1 秒以內**。

---

## 2. 環境準備：安裝 Node.js

使用 Vite 之前，你需要安裝 **Node.js**（一個讓 JavaScript 能在電腦上執行的環境）。

1. 前往 [https://nodejs.org](https://nodejs.org)
2. 下載 **LTS 版本**（長期支援版，較穩定）
3. 安裝完畢後，打開終端機（Terminal / 命令提示字元），輸入：

```bash
node -v
npm -v
```

如果看到版本號就代表安裝成功！

---

## 3. 用 Vite 建立第一個專案

打開終端機，輸入以下指令：

```bash
npm create vite@latest my-project
```

接著會出現互動式選單，讓你選擇框架和語言：

```
✔ Select a framework: › Vue
✔ Select a variant: › JavaScript
```

> 這裡選 Vue + JavaScript，後面的篇章也會用這個組合繼續練習。

建立完成後，跟著提示執行：

```bash
cd my-project
npm install
npm run dev
```

打開瀏覽器，連到 `http://localhost:5173`，你的 Vue 專案就跑起來了！

---

## 4. 專案結構解說

```
my-project/
├── public/             # 靜態資源（不會被處理的圖片、字型等）
├── src/                # 你的主要程式碼
│   ├── assets/         # 會被 Vite 處理的靜態資源
│   ├── components/     # Vue 元件
│   ├── App.vue         # 根元件
│   └── main.js         # 進入點
├── index.html          # 主 HTML 檔案
├── package.json        # 專案設定與相依套件清單
└── vite.config.js      # Vite 設定檔
```

**最重要的概念：**
* 你寫的程式碼都放在 `src/` 裡面
* `App.vue` 是整個應用的根，從這裡開始組合所有頁面
* `main.js` 是 Vite 的進入點，負責啟動 Vue 應用

---

## 5. 認識 `.vue` 單文件元件（SFC）

Vite + Vue 的核心是 **Single File Component（SFC）**，每個 `.vue` 檔案把 HTML、CSS、JS 全部包在一起：

```vue
<template>
    <!-- 你的 HTML 結構 -->
    <div class="card">
        <h2>{{ title }}</h2>
        <p>{{ description }}</p>
        <button @click="handleClick">按我</button>
    </div>
</template>

<script setup>
// 你的 JavaScript 邏輯
import { ref } from 'vue';

const title = ref("我的第一個元件");
const description = ref("這是一個 Vue SFC 元件");

function handleClick() {
    title.value = "你點了按鈕！";
}
</script>

<style scoped>
/* scoped 代表這些樣式只影響這個元件，不會外洩 */
.card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 20px;
    max-width: 400px;
}

h2 {
    color: #2c3e50;
}
</style>
```

`<style scoped>` 是個很棒的功能：裡面的 CSS 只會作用在這個元件上，不用擔心樣式衝突。

---

## 6. 在 Vite 專案中加入 Tailwind CSS

這是現代前端最流行的組合之一，設定步驟非常簡單：

**第一步：安裝 Tailwind**
```bash
npm install -D tailwindcss @tailwindcss/vite
```

**第二步：在 `vite.config.js` 加入 plugin**
```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
    plugins: [
        vue(),
        tailwindcss(),
    ],
})
```

**第三步：在 CSS 入口檔加入 Tailwind 指令**

在 `src/style.css`（或你的主 CSS 檔）最頂部加入：
```css
@import "tailwindcss";
```

**第四步：確認 `main.js` 有引入這個 CSS**
```javascript
import './style.css'
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

完成！現在你的 Vue 元件裡可以直接用 Tailwind 的 class 了。

---

## 7. 在 Vite 專案中加入 SCSS

一樣很簡單，只要安裝一個套件：

```bash
npm install -D sass
```

安裝完畢後，你的 `.vue` 檔案就能直接用 SCSS：

```vue
<style scoped lang="scss">
$primary: #3498db;

.card {
    border-radius: 8px;
    padding: 20px;

    h2 {
        color: $primary;
        font-weight: bold;
    }

    &:hover {
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
}
</style>
```

只要在 `<style>` 標籤加上 `lang="scss"`，Vite 就會自動用 Sass 來編譯，不需要任何額外設定。

---

## 8. 打包上線

開發完成後，只需要一個指令就能打包：

```bash
npm run build
```

Vite 會在 `dist/` 資料夾產生優化過的靜態檔案，你可以直接把這個資料夾上傳到任何靜態網站服務（GitHub Pages、Netlify、Vercel）。

---

## 結語：現在你的開發環境是真正工程化的了

從這篇開始，你的前端開發工作流程已經和業界接軌了：

| 工具 | 負責的事 |
|------|---------|
| **Vite** | 開發伺服器、打包、整合各種工具 |
| **Vue.js** | UI 元件化開發、響應式資料管理 |
| **Tailwind CSS** | 快速客製化樣式 |
| **SCSS** | 複雜樣式的變數、巢狀管理 |

**你已經掌握了：**
HTML → CSS → Flexbox → SCSS → Bootstrap → Tailwind → JavaScript → Vue.js → Vite

這套技術組合，就是目前台灣前端職場的主流技能樹。恭喜你走到這一步！

**接下來你可以做什麼？**
技術工具都有了，但工程師還少一樣關鍵技能——**Git 版本控制**。下一篇我們來學怎麼用 Git 管理你的程式碼，讓你的作品能放上 GitHub，讓全世界都看到！

**準備好讓作品被看見了嗎？下一篇見！**
