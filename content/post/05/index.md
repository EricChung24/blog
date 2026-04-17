---
title: "新手第五步：JavaScript 入門　給你的網頁加上靈魂！"
date: 2026-04-17
weight: 5
draft: false
description: "HTML 是骨架、CSS 是外觀，JavaScript 才是讓網頁「動起來」的靈魂！這篇帶你從零開始，寫出你人生第一行 JS。"
image: "https://images.unsplash.com/photo-1579468118864-1b9ea3c0db4a?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["JavaScript", "網頁基礎", "新手入門"]
categories: ["JavaScript", "網頁基礎"]
---

HTML 決定結構、CSS 決定外觀，但這兩樣東西做出來的網頁是**死的**——不管使用者怎麼點按鈕，頁面都不會有任何反應。

今天要學的 **JavaScript（簡稱 JS）**，就是讓網頁「活起來」的關鍵！

---

## 1. JavaScript 能做什麼？

你每天用到的這些功能，全都是 JavaScript 在背後默默運作：

* 點按鈕後跳出提示訊息
* 表單輸入錯誤時出現紅色警告
* 圖片輪播自動切換
* 滾動頁面時出現動畫效果
* 即時搜尋、不刷頁更新內容

簡單說：**所有「互動」都是 JavaScript 的工作**。

---

## 2. JavaScript 寫在哪裡？

和 CSS 一樣，有三種方式，最推薦的是**獨立 .js 檔案**。

### 最推薦：獨立 JS 檔案
建立 `script.js`，然後在 HTML 的 `</body>` **結尾標籤前**引入：

```html
<body>
    <!-- 你的 HTML 內容 -->

    <script src="script.js"></script>
</body>
```

> 為什麼放在 `</body>` 前面？因為這樣瀏覽器會先把頁面畫出來，再執行 JS，使用者不會看到空白頁面等待。

### 臨時測試：直接寫在 HTML 裡
```html
<script>
    alert("你好！");
</script>
```

---

## 3. 你的第一行 JavaScript

打開 VS Code，建立 `script.js`，輸入這一行：

```javascript
console.log("哈囉，JavaScript！");
```

存檔後，打開瀏覽器，按下 **F12** 開啟開發者工具，點選 **「Console（主控台）」** 分頁，你就會看到這行文字出現。

**`console.log()`** 是 JS 工程師最常用的工具，就像是「印出來看看」，方便除錯。

---

## 4. 變數：存放資料的盒子

寫程式就是在處理「資料」。**變數**就是用來存放這些資料的盒子。

```javascript
let name = "小明";
let age = 18;
let isStudent = true;
```

* `let`：宣告一個**可以改變**的變數（現代 JS 最常用）
* `const`：宣告一個**不能改變**的常數（例如 PI、固定設定值）
* `var`：舊版寫法，現在不推薦使用

```javascript
const PI = 3.14159;  // 圓周率不會變，用 const

let score = 80;      // 分數可能會變，用 let
score = 95;          // 改變 score 的值，沒問題
```

---

## 5. 資料型別：變數裡能放什麼？

| 型別 | 說明 | 範例 |
|------|------|------|
| `String` | 文字（用引號包起來） | `"你好"` / `'Hello'` |
| `Number` | 數字（整數或小數） | `42` / `3.14` |
| `Boolean` | 布林值（真或假） | `true` / `false` |
| `Array` | 陣列（一串資料） | `["蘋果", "香蕉", "橘子"]` |
| `Object` | 物件（一組相關資料） | `{ name: "小明", age: 18 }` |

---

## 6. 函式：可以重複使用的程式積木

當你有一段程式碼需要重複執行，就把它包成**函式（Function）**。

```javascript
function greet(name) {
    console.log("你好，" + name + "！歡迎來到我的網站。");
}

greet("小明");  // 你好，小明！歡迎來到我的網站。
greet("阿花");  // 你好，阿花！歡迎來到我的網站。
```

* `function` 關鍵字：宣告一個函式
* `name`：括號裡的是「參數」，呼叫時帶入不同值
* 呼叫函式時不用再寫 `function`，直接寫函式名稱加括號

---

## 7. 操作網頁元素：DOM

這才是 JavaScript 最重要的能力！**DOM（文件物件模型）** 讓你用 JS 讀取或修改網頁上任何元素。

```javascript
// 抓取元素
const title = document.getElementById("main-title");

// 修改內容
title.textContent = "標題被 JS 改掉了！";

// 修改樣式
title.style.color = "red";
```

**HTML：**
```html
<h1 id="main-title">原本的標題</h1>
```

執行後，頁面上的標題會直接變成「標題被 JS 改掉了！」，變成紅色。

---

## 8. 事件監聽：讓網頁回應使用者

光是修改元素還不夠，我們要讓網頁**在使用者做某件事時才觸發**，這就是「事件監聽」。

```javascript
const btn = document.getElementById("my-btn");

btn.addEventListener("click", function() {
    alert("你點了按鈕！");
});
```

**HTML：**
```html
<button id="my-btn">點我看看</button>
```

`addEventListener` 的意思：「**監聽** `my-btn` 這個元素的 **click（點擊）** 事件，一旦發生，就執行後面這個函式。」

常見的事件類型：
* `click`：點擊
* `mouseover`：滑鼠移入
* `keydown`：按下鍵盤
* `submit`：表單送出

---

## 9. 給新手的實戰練習：計數器

來做一個點一下數字就加一的計數器，這個小專案會用到今天學的所有概念！

**HTML（index.html）：**
```html
<!DOCTYPE html>
<html>
<head>
    <title>計數器</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="counter">
        <h1 id="count">0</h1>
        <button id="increase-btn">＋ 加一</button>
        <button id="reset-btn">重置</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

**CSS（style.css）：**
```css
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f4f8;
    font-family: Arial, sans-serif;
}

.counter {
    text-align: center;
}

#count {
    font-size: 80px;
    color: #2c3e50;
    margin: 0;
}

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

button:hover {
    background-color: #2980b9;
}
```

**JavaScript（script.js）：**
```javascript
let count = 0;
const countDisplay = document.getElementById("count");

document.getElementById("increase-btn").addEventListener("click", function() {
    count = count + 1;
    countDisplay.textContent = count;
});

document.getElementById("reset-btn").addEventListener("click", function() {
    count = 0;
    countDisplay.textContent = count;
});
```

打開瀏覽器，你現在擁有一個有完整互動功能的計數器了！

---

## 結語：網頁有靈魂了！

恭喜你學完了前端三劍客的最後一塊拼圖：
* **HTML** — 結構
* **CSS** — 外觀
* **JavaScript** — 互動

這三樣東西組合在一起，你已經具備了做出任何靜態網頁的能力。

**接下來你可以做什麼？**
光有這三樣還不夠，現實世界的前端開發都是用**框架**在加速開發。下一篇我們來聊聊目前最熱門的前端框架 **Vue.js**，看看它如何讓你寫更少的程式碼、做出更強大的功能！

**準備好進入框架的世界了嗎？下一篇見！**
