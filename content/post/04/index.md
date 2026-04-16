---
title: "新手第四步：CSS Flexbox　排版終於不再靠感覺！"
date: 2026-04-17
draft: false
description: "還在用 margin 硬推元素位置？學會 Flexbox，左右並排、垂直置中這些讓新手崩潰的版面，5 行 CSS 就搞定！"
image: "https://images.unsplash.com/photo-1545670723-196ed0954986?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["CSS", "Flexbox", "排版", "新手入門"]
categories: ["基礎教學"]
---

上一篇學完 CSS 基礎，你已經能改顏色、換字型了。但你一定還遇過這個問題：**「為什麼我要的左右並排，偏偏是上下疊在一起？！」**

別崩潰，這是每個新手都會撞牆的地方。今天要學的 **Flexbox** 就是專門解決這件事的！

---

## 1. 為什麼需要 Flexbox？

在 Flexbox 出現之前，工程師為了做一個「垂直置中」的效果，要寫一堆奇怪的 CSS hack，有時候甚至要靠「玄學」才能對齊。

Flexbox 出現後，那些折磨人的問題全部消失了：
* 元素左右並排 ✅
* 全部垂直置中 ✅
* 平均分散間距 ✅
* 自動換行 ✅

它不是什麼新技術，現在**所有主流瀏覽器**都完整支援，你可以安心使用。

---

## 2. 開啟 Flexbox 只需要一行

Flexbox 的用法超直覺。你只需要在**父元素**（包著其他元素的那個）加上一行 CSS：

```css
.container {
    display: flex;
}
```

就這樣，裡面的子元素就會**自動變成左右並排**！

**HTML：**
```html
<div class="container">
    <div>方塊 1</div>
    <div>方塊 2</div>
    <div>方塊 3</div>
</div>
```

**CSS：**
```css
.container {
    display: flex;
    background-color: #f0f0f0;
    padding: 10px;
}

.container div {
    background-color: #3498db;
    color: white;
    padding: 20px;
    margin: 5px;
}
```

套上 `display: flex` 之前，三個方塊是**上下堆疊**的。套上之後，直接變成**左右並排**，就這麼簡單。

---

## 3. 最常用的 Flexbox 屬性

### `justify-content`：控制「水平方向」的排列

```css
.container {
    display: flex;
    justify-content: center; /* 置中 */
}
```

| 值 | 效果 |
|---|---|
| `flex-start` | 靠左對齊（預設） |
| `flex-end` | 靠右對齊 |
| `center` | 水平置中 |
| `space-between` | 兩端對齊，元素之間平均留白 |
| `space-around` | 每個元素左右平均留白 |
| `space-evenly` | 所有間距完全相等 |

### `align-items`：控制「垂直方向」的對齊

```css
.container {
    display: flex;
    height: 200px;
    align-items: center; /* 垂直置中 */
}
```

| 值 | 效果 |
|---|---|
| `stretch` | 拉伸填滿容器高度（預設） |
| `flex-start` | 靠上對齊 |
| `flex-end` | 靠下對齊 |
| `center` | 垂直置中 |

---

## 4. 傳說中的「垂直 + 水平置中」

這是每個新手都夢寐以求的效果，用 Flexbox 只要三行：

```css
.container {
    display: flex;
    justify-content: center; /* 水平置中 */
    align-items: center;     /* 垂直置中 */
    height: 100vh;           /* 佔滿整個視窗高度 */
}
```

```html
<div class="container">
    <p>我在正中間！</p>
</div>
```

以前要寫半天的效果，現在三行搞定。第一次看到這個的新手通常都會感動到不行。

---

## 5. `flex-direction`：改變排列方向

Flexbox 預設是**水平排列（橫向）**，但你可以改成垂直：

```css
.container {
    display: flex;
    flex-direction: column; /* 改成垂直排列 */
}
```

| 值 | 效果 |
|---|---|
| `row` | 水平排列（由左到右，預設值） |
| `row-reverse` | 水平排列（由右到左） |
| `column` | 垂直排列（由上到下） |
| `column-reverse` | 垂直排列（由下到上） |

---

## 6. `flex-wrap`：元素太多時自動換行

預設情況下，Flexbox 會把所有元素擠在同一行，擠到變形也不換行。加上這個屬性就能讓它自動換行：

```css
.container {
    display: flex;
    flex-wrap: wrap; /* 滿了自動換行 */
}
```

這在做「卡片清單」這類版面時非常好用。

---

## 7. 給子元素的屬性：`flex`

不只是父元素，Flexbox 也讓你控制**每個子元素**如何佔用空間：

```css
.item-a {
    flex: 1; /* 佔用剩餘空間的 1 份 */
}

.item-b {
    flex: 2; /* 佔用剩餘空間的 2 份（比 item-a 大兩倍） */
}
```

這讓你能輕鬆做出「側邊欄 + 主內容區」的經典網頁版面。

---

## 8. 給新手的實戰練習：做一個導覽列

導覽列（Navbar）是幾乎每個網站都有的東西，用 Flexbox 做超級適合。

**HTML：**
```html
<nav class="navbar">
    <div class="logo">我的網站</div>
    <ul class="nav-links">
        <li><a href="#">首頁</a></li>
        <li><a href="#">關於我</a></li>
        <li><a href="#">作品集</a></li>
        <li><a href="#">聯絡我</a></li>
    </ul>
</nav>
```

**CSS：**
```css
.navbar {
    display: flex;
    justify-content: space-between; /* logo 靠左，連結靠右 */
    align-items: center;            /* 垂直置中 */
    background-color: #2c3e50;
    padding: 0 40px;
    height: 60px;
}

.logo {
    color: white;
    font-size: 20px;
    font-weight: bold;
}

.nav-links {
    display: flex;        /* 讓連結們水平排列 */
    list-style: none;     /* 去掉圓點 */
    gap: 30px;            /* 連結間距 */
    margin: 0;
    padding: 0;
}

.nav-links a {
    color: #ccc;
    text-decoration: none;
}

.nav-links a:hover {
    color: white;
}
```

這段程式碼就能產出一個**專業感十足的導覽列**，Logo 靠左、選單靠右，垂直完美置中。

---

## 結語：排版從此不靠感覺

Flexbox 是現代前端開發的必備技能。掌握了 `display: flex`、`justify-content`、`align-items` 這三個核心屬性，你會發現之前 90% 排版問題都能解決。

**接下來你可以做什麼？**
有了 Flexbox 做排版，下一篇我們要學 **JavaScript 入門**——讓網頁不只是靜態的頁面，而是能「動起來」、回應使用者點擊的互動網頁！

**準備好給你的網頁加上靈魂了嗎？下一篇見！**
