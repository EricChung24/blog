---
title: "新手第六步：Vue.js 入門　前端框架到底在解決什麼問題？"
date: 2026-04-17
weight: 6
draft: false
description: "學完原生 JS 後，你會發現程式碼越寫越亂。Vue.js 就是來解救你的——讓你用更少的程式碼，做出更強大、更好維護的網頁。"
image: "https://images.unsplash.com/photo-1555099962-4199c345e5dd?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["Vue.js", "JavaScript", "前端框架", "新手入門"]
categories: ["前端框架", "Vue"]
---

上一篇我們用原生 JavaScript 做了計數器。雖然可以動，但你有沒有發現——當功能一多，程式碼就開始變得雜亂？

這正是前端框架要解決的問題。今天我們來聊聊目前最適合新手入門的框架：**Vue.js**。

---

## 1. 為什麼要用框架？

先想像一個場景：你要做一個購物車頁面，商品數量改了，頁面上的「小計」、「總計」、「結帳按鈕顯示金額」都要跟著更新。

用原生 JS 你要：
1. 抓到「小計」元素，修改它
2. 抓到「總計」元素，修改它
3. 抓到「按鈕」元素，修改它
4. 下次改需求還要重來一遍...

**用 Vue.js 你只需要：**
修改一個變數，頁面上所有相關顯示自動同步更新。

這個核心概念叫做**「響應式（Reactivity）」**——數據變了，畫面自動跟著變。

---

## 2. Vue.js 是什麼？

Vue.js 是一個用 JavaScript 寫的前端框架，由前 Google 工程師尤雨溪（Evan You）在 2014 年創建。

它有幾個讓新手特別喜歡的特點：
* **學習曲線平緩**：和 React 相比，Vue 對新手更友善，語法更接近原生 HTML/JS
* **文件超完整**：官方中文文件寫得非常好，遇到問題查文件通常就能解決
* **漸進式引入**：可以只在部分頁面使用 Vue，不用整個專案重寫

---

## 3. 快速體驗 Vue：不需要安裝任何東西

最快的方式是直接用 CDN 引入 Vue，就像引入一個 JS 檔案一樣：

```html
<!DOCTYPE html>
<html>
<head>
    <title>我的 Vue 練習</title>
</head>
<body>
    <div id="app">
        <h1>{{ message }}</h1>
        <button @click="changeMessage">點我換訊息</button>
    </div>

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
        const { createApp, ref } = Vue;

        createApp({
            setup() {
                const message = ref("你好，Vue！");

                function changeMessage() {
                    message.value = "訊息被改掉了！";
                }

                return { message, changeMessage };
            }
        }).mount("#app");
    </script>
</body>
</html>
```

存檔，打開瀏覽器，你會看到標題寫著「你好，Vue！」，點按鈕後自動變成「訊息被改掉了！」——不需要手動 `getElementById`，Vue 自動幫你搞定！

---

## 4. Vue 的核心概念

### 模板語法：`{{ }}`

雙大括號是 Vue 的「插值語法」，把變數的值直接顯示在 HTML 裡：

```html
<p>你好，{{ name }}！你今年 {{ age }} 歲。</p>
```

只要 `name` 或 `age` 變數的值改變，頁面會**自動更新**，不需要任何額外操作。

### 響應式變數：`ref()`

在 Vue 3 裡，用 `ref()` 建立會「被追蹤」的響應式變數：

```javascript
const count = ref(0);   // 數字
const name = ref("小明"); // 文字
const show = ref(true); // 布林值
```

修改時要用 `.value`：

```javascript
count.value = count.value + 1;
```

但在 HTML 模板裡用 `{{ count }}` 就好，Vue 自動處理 `.value`。

### 事件綁定：`@click`

Vue 用 `@` 符號取代原本的 `addEventListener`，寫起來清爽很多：

```html
<!-- 原生 JS -->
<button id="btn">點我</button>
<script> document.getElementById("btn").addEventListener("click", doSomething) </script>

<!-- Vue 的寫法 -->
<button @click="doSomething">點我</button>
```

### 屬性綁定：`v-bind` 或 `:`

想把 JS 變數的值套用到 HTML 屬性上，用 `:` 綁定：

```html
<img :src="imageUrl" :alt="imageAlt">
<a :href="linkUrl">點我</a>
```

### 條件渲染：`v-if`

根據條件決定要不要顯示某個元素：

```html
<p v-if="isLoggedIn">歡迎回來！</p>
<p v-else>請先登入。</p>
```

### 列表渲染：`v-for`

用來把陣列資料一筆一筆顯示出來：

```html
<ul>
    <li v-for="item in fruits" :key="item">{{ item }}</li>
</ul>
```

```javascript
const fruits = ref(["蘋果", "香蕉", "橘子"]);
```

---

## 5. 給新手的實戰練習：用 Vue 重做計數器

還記得上一篇用原生 JS 做的計數器嗎？現在用 Vue 來做同樣的功能，感受一下差異：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Vue 計數器</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f4f8;
            font-family: Arial, sans-serif;
        }
        .counter { text-align: center; }
        #count-display { font-size: 80px; color: #2c3e50; margin: 0; }
        button {
            font-size: 18px;
            padding: 10px 30px;
            margin: 10px;
            cursor: pointer;
            border: none;
            border-radius: 8px;
            background-color: #3498db;
            color: white;
        }
        button:hover { background-color: #2980b9; }
    </style>
</head>
<body>
    <div id="app" class="counter">
        <p id="count-display">{{ count }}</p>
        <button @click="count++">＋ 加一</button>
        <button @click="count = 0">重置</button>
    </div>

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
        const { createApp, ref } = Vue;

        createApp({
            setup() {
                const count = ref(0);
                return { count };
            }
        }).mount("#app");
    </script>
</body>
</html>
```

注意到了嗎？**JavaScript 的部分從 10 行縮短到 3 行**。Vue 幫你處理了所有「抓元素、更新畫面」的瑣事，你只需要專注在「資料邏輯」本身。

---

## 6. Vue vs 原生 JS：什麼時候用哪個？

| 情境 | 建議 |
|------|------|
| 簡單的互動（一個按鈕、一個動畫） | 原生 JS 就夠了 |
| 需要管理很多資料狀態的頁面 | 用 Vue |
| 單頁應用程式（SPA） | 強烈建議用 Vue |
| 學習基礎概念 | 先學原生 JS，再學 Vue |

---

## 結語：框架是工具，不是魔法

Vue.js 讓你寫更少的程式碼、更快做出功能，但它的底層還是 JavaScript。所以上一篇學的變數、函式、DOM 概念，在 Vue 裡全都用得到。

框架只是幫你把重複的工作自動化，**你的 JS 基礎夠紮實，框架學起來就會快很多**。

**接下來你可以做什麼？**
有了 Vue 的基礎後，下一篇我們要學 **Git 版本控制**——這是所有工程師都必備的技能，讓你的程式碼永遠有「後悔藥」可以吃，也是團隊協作的核心工具。

**準備好學工程師的必備神器了嗎？下一篇見！**
