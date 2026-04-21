---
title: "新手第七步：SCSS 入門　寫 CSS 終於不再複製貼上了！"
date: 2026-04-17
weight: 7
draft: false
description: "原生 CSS 寫久了會發現一個痛點：重複的顏色要改十幾個地方。SCSS 讓你用變數、巢狀、函式來寫 CSS，維護起來輕鬆十倍。"
image: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/96/Sass_Logo_Color.svg/512px-Sass_Logo_Color.svg.png"
tags: ["SCSS", "CSS", "前端工具", "新手入門"]
categories: ["CSS", "前端工具"]
---

你有沒有遇過這樣的情況：網站的主題色是 `#3498db`，結果整份 CSS 裡出現了四十幾次。有一天設計師說「主題色改一下」，你只能一個一個找、一個一個改，改到懷疑人生。

**SCSS** 就是來解決這個問題的！

---

## 1. SCSS 是什麼？

SCSS 是 **CSS 的超集合（Superset）**，意思是：所有合法的 CSS 都是合法的 SCSS。你可以直接把 `.css` 檔案改名成 `.scss`，它還是能正常運作。

SCSS 在 CSS 的基礎上加入了：
* **變數** — 統一管理顏色、字體大小等重複值
* **巢狀（Nesting）** — 讓選擇器的階層結構更清晰
* **Mixin** — 可重複使用的樣式片段（類似函式）
* **繼承（Extend）** — 讓選擇器共用樣式

瀏覽器看不懂 SCSS，所以寫完後需要**編譯**成普通的 CSS 才能使用。

---

## 2. 安裝 SCSS 編譯工具

最簡單的方式是在 VS Code 安裝 **Live Sass Compiler** 外掛：

1. 打開 VS Code 的擴充功能
2. 搜尋 `Live Sass Compiler`
3. 安裝後，點擊右下角的 **「Watch Sass」** 按鈕
4. 它會自動監聽你的 `.scss` 檔案，存檔時立刻編譯成 `.css`

---

## 3. 變數：統一管理設計規格

這是 SCSS 最受歡迎的功能，沒有之一。

```scss
// 在檔案最上方定義設計規格
$primary-color: #3498db;
$secondary-color: #2c3e50;
$font-size-base: 16px;
$border-radius: 8px;

// 之後到處使用變數
.button {
    background-color: $primary-color;
    border-radius: $border-radius;
    font-size: $font-size-base;
}

.navbar {
    background-color: $secondary-color;
}
```

現在要改主題色，只需要改最上面那一行 `$primary-color`，全站自動更新。

---

## 4. 巢狀：讓選擇器更有層次感

原生 CSS 的選擇器寫起來又臭又長：

```css
/* 原生 CSS */
.navbar { background: #333; }
.navbar a { color: white; }
.navbar a:hover { color: #3498db; }
.navbar .logo { font-size: 20px; }
```

SCSS 可以寫成巢狀結構，一眼看出階層關係：

```scss
// SCSS
.navbar {
    background: #333;

    a {
        color: white;

        &:hover {        // & 代表父選擇器（這裡是 a）
            color: $primary-color;
        }
    }

    .logo {
        font-size: 20px;
    }
}
```

`&` 符號代表**當前的父選擇器**，`&:hover` 就等於 `.navbar a:hover`。

---

## 5. Mixin：可重複使用的樣式積木

當你有一段樣式需要在多個地方使用，就把它做成 Mixin：

```scss
// 定義一個 Mixin（像是定義函式）
@mixin flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}

// 帶參數的 Mixin
@mixin card($shadow: 0 2px 8px rgba(0,0,0,0.1)) {
    border-radius: 8px;
    padding: 20px;
    background: white;
    box-shadow: $shadow;
}

// 使用 Mixin
.hero-section {
    @include flex-center;
    height: 100vh;
}

.product-card {
    @include card;
}

.featured-card {
    @include card(0 8px 24px rgba(0,0,0,0.2)); // 自訂陰影
}
```

---

## 6. `@use` 與模組化：把 SCSS 拆成多個檔案

專案大了之後，一個 SCSS 檔案裝不下所有樣式。用 `@use` 可以把樣式拆成多個檔案管理：

```
styles/
├── _variables.scss   // 變數
├── _mixins.scss      // Mixin
├── _navbar.scss      // 導覽列樣式
├── _buttons.scss     // 按鈕樣式
└── main.scss         // 主檔案，在這裡引入所有模組
```

```scss
// main.scss
@use 'variables';
@use 'mixins';
@use 'navbar';
@use 'buttons';
```

> 以底線 `_` 開頭的檔案叫做 **Partial（片段）**，表示這個檔案不會單獨編譯，只會被引入到其他地方使用。

---

## 7. 給新手的實戰練習

把之前寫的 CSS 改成 SCSS，感受一下整理後的清爽感：

```scss
// _variables.scss
$primary: #3498db;
$dark: #2c3e50;
$light-bg: #f5f5f5;
$radius: 8px;

// main.scss
@use 'variables' as v;

body {
    background-color: v.$light-bg;
    font-family: Arial, sans-serif;
    padding: 40px;
}

#main-title {
    color: v.$dark;
    text-align: center;
    border-bottom: 3px solid v.$primary;
    padding-bottom: 10px;

    &:hover {
        color: v.$primary;
    }
}

.btn {
    background-color: v.$primary;
    border: none;
    border-radius: v.$radius;
    color: white;
    padding: 10px 24px;
    cursor: pointer;

    &:hover {
        opacity: 0.85;
    }
}
```

---

## 結語：CSS 也可以很工程化

SCSS 不是什麼高深的技術，它就是讓你寫 CSS 的方式更有組織、更好維護。對於任何需要長期維護的專案，SCSS（或類似的 CSS 預處理器）幾乎是標配。

**接下來你可以做什麼？**
下一篇我們來看 **Bootstrap 5**——一個現成的 CSS 框架，內建幾百個元件，讓你不用從零開始，直接組出專業的版面！

**準備好「偷懶」式開發了嗎？下一篇見！**
