---
title: "新手第十六步：CodePen 入門　不用建專案，也能立刻開始寫前端！"
date: 2026-04-17
weight: 16
draft: false
description: "剛學前端時，常常只是想試一小段 HTML、CSS、JavaScript，卻還要開資料夾、建檔案、跑 Live Server。CodePen 就是讓你打開瀏覽器就能直接寫前端的神器。"
image: "https://assets.codepen.io/t-1/codepen-wordmark-black.png"
tags: ["CodePen", "HTML", "CSS", "JavaScript", "新手入門", "前端工具"]
categories: ["前端工具", "開發工具"]
---

你有沒有遇過這種情況：

只是想測一個按鈕 hover 效果，結果卻要先：

* 建資料夾
* 開 VS Code
* 建 `index.html`
* 建 `style.css`
* 建 `script.js`
* 再開 Live Server

明明只是想試 10 行程式，卻先花了 5 分鐘準備環境。

這時候，**CodePen** 就非常好用。

---

## 1. CodePen 是什麼？

CodePen 是一個線上前端編輯器，你可以直接在瀏覽器裡寫：

* HTML
* CSS
* JavaScript

而且它會立刻幫你把結果顯示出來。

你可以把它想成：

> **前端版的線上遊樂場。**

不用安裝、不用建專案、不用設定環境，只要打開網站就能開始寫。

---

## 2. CodePen 能做什麼？

很多新手以為 CodePen 只是「拿來玩玩看」的網站，其實它很好用。

你可以拿它來：

* 練習 HTML / CSS / JavaScript
* 測試一小段 UI 效果
* 做按鈕、卡片、導覽列等小元件
* 分享作品給別人看
* 收藏別人的範例，學習寫法

尤其是學前端初期，你常常不是要做整個網站，而是想先試一個小功能。  
這時候 CodePen 比開一個完整專案快非常多。

---

## 3. CodePen 的畫面怎麼看？

CodePen 最常見的畫面分成四塊：

* **HTML 區**：放結構
* **CSS 區**：放樣式
* **JavaScript 區**：放互動邏輯
* **Preview 區**：即時預覽結果

這個設計很適合新手，因為你可以很清楚地看到：

* HTML 負責骨架
* CSS 負責外觀
* JavaScript 負責互動

三者的角色分工會非常直觀。

---

## 4. 為什麼新手很適合先用 CodePen？

因為它把「環境成本」降到幾乎沒有。

剛開始學前端的人，最容易被兩件事打亂節奏：

* 程式本身還沒學懂
* 開發環境又一堆設定

CodePen 的好處就是：**你可以先把注意力放在程式本身。**

例如你今天只是想練：

* `flex`
* `hover`
* `addEventListener`
* `fetch`
* 一個小型卡片 UI

那你直接開 CodePen 寫，速度通常最快。

---

## 5. 一個最簡單的 CodePen 範例

假設你想做一個按一下就改文字的按鈕，CodePen 會很好上手。

### HTML
```html
<div class="card">
    <h1 id="title">你好，CodePen！</h1>
    <button id="change-btn">點我換文字</button>
</div>
```

### CSS
```css
body {
    margin: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #f4f7fb;
    font-family: Arial, sans-serif;
}

.card {
    background: white;
    padding: 32px;
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
    text-align: center;
}

button {
    border: none;
    background: #2563eb;
    color: white;
    padding: 12px 20px;
    border-radius: 10px;
    cursor: pointer;
}
```

### JavaScript
```javascript
const title = document.getElementById("title");
const button = document.getElementById("change-btn");

button.addEventListener("click", function () {
    title.textContent = "文字被改掉了！";
});
```

你把這三段分別貼到 CodePen 的區塊裡，就能立刻看到結果。

---

## 6. CodePen 和本地開發有什麼差別？

這點很重要。

### CodePen 的優點

* 打開就能寫
* 適合做小範例
* 分享超方便
* 適合學習和展示

### CodePen 的限制

* 不適合大型專案
* 檔案結構比較簡化
* 不像真正專案那樣有完整資料夾管理
* 有些套件和工具鏈整合沒那麼自由

所以你可以這樣理解：

> **CodePen 很適合「練習」和「展示」，但不適合拿來做完整產品。**

---

## 7. 什麼時候該用 CodePen？

以下這幾種情況，CodePen 都很適合：

* 你想快速試一段 CSS 動畫
* 你想做一個小互動元件
* 你想把作品丟給朋友或面試官看
* 你看到別人的範例，想拆開研究
* 你想整理自己的前端練習作品集

尤其對新手來說，CodePen 最大的價值不是「很酷」，而是：

**它讓你更容易開始動手寫。**

---

## 8. 給新手的使用建議

如果你剛開始學前端，我會建議你這樣用：

1. 小效果、小練習，用 CodePen
2. 完整網站、小專案，用本地開發
3. 做完一個好作品，再把它整理成可分享的 Pen

這樣你既能享受 CodePen 的快速，也不會忽略真正專案的開發流程。

---

## 結語：先把「開始寫」這件事變簡單

很多新手不是不會寫，而是每次開始前就先被環境搞得很累。

CodePen 的價值，就在於它把「開始動手」這件事變得非常輕。

你不用先想專案架構、不用先管 build tool，也不用先開很多檔案。  
你只要專心回答一個問題：

**「我現在想試什麼效果？」**

這對前端學習初期非常有幫助。

**接下來你可以做什麼？**  
下一篇我們可以接著介紹 **Figma**，因為當你開始會切版、做元件之後，你就會發現前端工程師幾乎一定會碰到設計稿，而 Figma 幾乎就是現在的業界標配。

**準備好從寫畫面，進一步看懂設計稿了嗎？下一篇見！**
