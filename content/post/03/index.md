---
title: "新手第三步：CSS 入門　讓你的網頁從黑白變彩色！"
date: 2026-04-16
weight: 3
draft: false
description: "學完 HTML 只有骨架，現在要替網頁穿上衣服了！5 分鐘帶你看懂 CSS 的核心觀念，讓你的網頁立刻好看起來。"
image: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/512px-CSS3_logo_and_wordmark.svg.png"
tags: ["CSS", "網頁基礎", "新手入門"]
categories: ["網頁基礎", "CSS"]
---

上一篇我們學了 HTML，做出了一個「能動但很醜」的網頁。今天我們要學 **CSS**，讓你的網頁從工地毛胚屋，搖身一變成精心裝潢的新家！

---

## 1. 什麼是 CSS？

CSS 的全名是 **階層式樣式表（Cascading Style Sheets）**。

繼續用蓋房子的比喻：
* **HTML** 是鋼筋牆壁，決定結構在哪裡。
* **CSS** 就是油漆、壁紙、燈光，決定**每個地方長什麼樣子**。

一句話總結：**HTML 說「有什麼」，CSS 說「長什麼樣」**。

---

## 2. CSS 怎麼接上 HTML？

你有三種方式可以把 CSS 加進網頁，新手最推薦的是 **外部引入**：

### 方法一：外部引入（最推薦）
新建一個 `style.css` 檔案，然後在 HTML 的 `<head>` 裡加一行：

```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

這樣 CSS 和 HTML 分開管理，最乾淨也最好維護。

### 方法二：直接寫在標籤裡（偶爾用）
```html
<h1 style="color: red;">這是紅色標題</h1>
```

只適合臨時測試，正式專案不建議這樣寫，因為改起來很痛苦。

---

## 3. CSS 的基本語法長什麼樣？

CSS 的寫法超級固定，記住這個公式就對了：

```css
選擇器 {
    屬性: 值;
}
```

**實際範例：**
```css
h1 {
    color: blue;
    font-size: 32px;
}
```

這段 CSS 的意思是：**「把所有 `<h1>` 標題的文字顏色設成藍色，字體大小設成 32px」**。

---

## 4. 三大「選擇器」你一定要學

選擇器就是告訴 CSS「我要改的是哪個 HTML 元素」。

### 標籤選擇器
```css
p {
    color: gray;
}
```
這樣會把**所有** `<p>` 段落都變成灰色文字。

### Class 選擇器（最常用）
```html
<p class="highlight">這段文字很重要</p>
```
```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```
在 HTML 元素上加 `class="名稱"`，然後 CSS 用 `.名稱` 來選取。
一個 class 可以用在很多元素上，超級靈活！

### ID 選擇器
```html
<div id="header">網站標題區</div>
```
```css
#header {
    background-color: black;
    color: white;
}
```
ID 在一個頁面只能用一次，比 class 更「專屬」。

> **口訣記憶：** 標籤選全部、class 選一類、ID 選唯一。

---

## 5. 新手最常用的 CSS 屬性

只要學會這幾個，你馬上就能把網頁整理得有模有樣：

| 屬性 | 用途 | 範例 |
|------|------|------|
| `color` | 文字顏色 | `color: #333333;` |
| `background-color` | 背景顏色 | `background-color: #f0f0f0;` |
| `font-size` | 字體大小 | `font-size: 18px;` |
| `font-weight` | 字體粗細 | `font-weight: bold;` |
| `text-align` | 文字對齊 | `text-align: center;` |
| `margin` | 元素外側的空白 | `margin: 20px;` |
| `padding` | 元素內側的空白 | `padding: 10px;` |
| `border` | 外框線 | `border: 1px solid black;` |
| `width` / `height` | 寬度 / 高度 | `width: 100%;` |

---

## 6. 最讓新手頭痛的東西：Box Model（盒子模型）

每一個 HTML 元素，在 CSS 眼中都是一個**「盒子」**。這個盒子由四層組成，從內到外分別是：

```
┌─────────────────────────────┐
│          margin（外距）       │
│  ┌───────────────────────┐  │
│  │      border（外框）     │  │
│  │  ┌─────────────────┐  │  │
│  │  │  padding（內距）  │  │  │
│  │  │  ┌───────────┐  │  │  │
│  │  │  │  content  │  │  │  │
│  │  │  │  （內容）   │  │  │  │
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

* **content**：你的文字、圖片等實際內容。
* **padding**：內容到邊框之間的距離（像是包裝紙）。
* **border**：盒子的外框線。
* **margin**：這個盒子和其他盒子之間的距離（像是盒子放在桌上，和旁邊盒子的間距）。

---

## 7. 給新手的實戰練習

跟著做一次，絕對比看十遍有效！

**第一步：建立 HTML 檔案 `index.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>我的 CSS 練習</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1 id="main-title">我的自我介紹</h1>
    <p class="intro">大家好，我正在學習前端開發！</p>
    <p class="intro">我的目標是做出一個超帥的個人網站。</p>
</body>
</html>
```

**第二步：建立 CSS 檔案 `style.css`**
```css
body {
    background-color: #f5f5f5;
    font-family: Arial, sans-serif;
    padding: 40px;
}

#main-title {
    color: #2c3e50;
    text-align: center;
    border-bottom: 3px solid #3498db;
    padding-bottom: 10px;
}

.intro {
    color: #555;
    font-size: 18px;
    line-height: 1.8;
    margin: 10px 0;
}
```

**第三步：用瀏覽器打開 `index.html`**，看看和之前純 HTML 的差別有多大！

---

## 結語：骨架穿上衣服了！

恭喜你！你已經掌握了 CSS 最核心的觀念。現在你知道怎麼改顏色、改大小、加邊框、控制間距——這些就是網頁排版的基本功。

**接下來你可以做什麼？**
現在的網頁還是「垂直堆疊」，元素一個壓一個。下一篇我們要學 **CSS Flexbox**，它是現代網頁排版的神器，讓你能輕鬆做出「左右並排」、「置中對齊」這些漂亮的版面！

**準備好打破垂直限制了嗎？下一篇見！**
