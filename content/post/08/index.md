---
title: "新手第八步：Bootstrap 5 入門　不會設計也能做出專業版面！"
date: 2026-04-17
weight: 8
draft: false
description: "還在從零開始寫 CSS？Bootstrap 5 提供了現成的元件庫，按鈕、導覽列、卡片通通有，讓你快速搭出專業的響應式網頁。"
image: "https://i.imgur.com/B4jcvpV.png"
tags: ["Bootstrap 5", "CSS 框架", "響應式設計", "新手入門"]
categories: ["CSS 框架", "前端工具"]
---

每次做新專案，是不是又要從頭寫按鈕樣式、導覽列、卡片？**Bootstrap 5** 就是解決這個痛點的神器——它把最常用的 UI 元件全部做好了，你只要加幾個 class 名稱就能直接用。

---

## 1. Bootstrap 5 是什麼？

Bootstrap 是 Twitter 工程師開發的 CSS 框架，目前已發展到第 5 版，是全球使用量最大的 CSS 框架之一。

它幫你做好了：
* **Grid 格線系統**：12 欄式的響應式排版
* **元件庫**：按鈕、卡片、導覽列、Modal、輪播圖……數十種現成元件
* **工具類別（Utilities）**：快速調整間距、顏色、對齊的 class
* **響應式設計**：自動在手機、平板、電腦上顯示不同版面

---

## 2. 引入 Bootstrap 5：一行搞定

最快的方式是用 CDN，不需要安裝任何東西：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Bootstrap 練習</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

    <!-- 你的內容 -->

    <!-- Bootstrap JS（某些元件需要） -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

就這樣！引入之後，你的 HTML 裡只要加上 Bootstrap 定義好的 class 名稱，樣式就自動套上。

---

## 3. Grid 格線系統：響應式排版的核心

Bootstrap 把頁面分成 **12 欄**，你指定每個元素要佔幾欄：

```html
<div class="container">
    <div class="row">
        <div class="col-6">左半部（佔 6/12）</div>
        <div class="col-6">右半部（佔 6/12）</div>
    </div>
</div>
```

**響應式斷點：**

| class | 裝置 | 螢幕寬度 |
|-------|------|----------|
| `col-` | 全部裝置 | 所有寬度 |
| `col-sm-` | 手機（橫放） | ≥ 576px |
| `col-md-` | 平板 | ≥ 768px |
| `col-lg-` | 桌機 | ≥ 992px |
| `col-xl-` | 大螢幕 | ≥ 1200px |

**實用範例：手機單欄、平板雙欄、桌機三欄**
```html
<div class="container">
    <div class="row">
        <div class="col-12 col-md-6 col-lg-4">卡片一</div>
        <div class="col-12 col-md-6 col-lg-4">卡片二</div>
        <div class="col-12 col-md-6 col-lg-4">卡片三</div>
    </div>
</div>
```

---

## 4. 最常用的元件

### 按鈕

```html
<button class="btn btn-primary">主要按鈕</button>
<button class="btn btn-secondary">次要按鈕</button>
<button class="btn btn-danger">危險操作</button>
<button class="btn btn-outline-primary">外框按鈕</button>
<button class="btn btn-lg btn-success">大按鈕</button>
```

### 導覽列（Navbar）

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand" href="#">我的網站</a>
        <button class="navbar-toggler" type="button"
                data-bs-toggle="collapse" data-bs-target="#navMenu">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navMenu">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item"><a class="nav-link" href="#">首頁</a></li>
                <li class="nav-item"><a class="nav-link" href="#">關於</a></li>
                <li class="nav-item"><a class="nav-link" href="#">聯絡</a></li>
            </ul>
        </div>
    </div>
</nav>
```

這段 HTML 就能做出**完整的響應式導覽列**，手機上會自動折疊成漢堡選單。

### 卡片（Card）

```html
<div class="card" style="width: 18rem;">
    <img src="https://via.placeholder.com/280x160" class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">卡片標題</h5>
        <p class="card-text">卡片描述文字，可以放任何你想說的內容。</p>
        <a href="#" class="btn btn-primary">了解更多</a>
    </div>
</div>
```

---

## 5. 工具類別（Utilities）：快速調整樣式

Bootstrap 5 的另一個強項是「工具類別」，不用寫 CSS 就能調整樣式：

```html
<!-- 間距 -->
<div class="mt-3">上方外距 3 單位</div>
<div class="px-4">左右內距 4 單位</div>
<div class="mb-0">下方外距 0</div>

<!-- 文字 -->
<p class="text-center">置中文字</p>
<p class="text-primary fw-bold">藍色粗體</p>
<p class="fs-4">4 號字體大小</p>

<!-- 背景與顏色 -->
<div class="bg-dark text-white p-3">深色背景白色文字</div>

<!-- Flexbox -->
<div class="d-flex justify-content-between align-items-center">
    <span>左邊</span>
    <span>右邊</span>
</div>
```

間距規則：`m`=margin，`p`=padding；`t`=top，`b`=bottom，`s`=start(left)，`e`=end(right)，`x`=左右，`y`=上下；數字 `0~5` 代表大小。

---

## 6. 給新手的實戰練習：做一個個人作品集頁面

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的作品集</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

    <!-- 導覽列 -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand fw-bold" href="#">Eric's Portfolio</a>
        </div>
    </nav>

    <!-- Hero 區塊 -->
    <div class="bg-primary text-white text-center py-5">
        <h1 class="display-4 fw-bold">你好，我是前端新手</h1>
        <p class="lead">正在努力學習 HTML、CSS 和 JavaScript</p>
        <a href="#" class="btn btn-light btn-lg mt-3">查看我的作品</a>
    </div>

    <!-- 作品卡片 -->
    <div class="container py-5">
        <h2 class="text-center mb-4">我的作品</h2>
        <div class="row g-4">
            <div class="col-12 col-md-4">
                <div class="card h-100 shadow-sm">
                    <div class="card-body">
                        <h5 class="card-title">計數器 App</h5>
                        <p class="card-text">用原生 JavaScript 做的互動計數器。</p>
                        <a href="#" class="btn btn-outline-primary">查看作品</a>
                    </div>
                </div>
            </div>
            <div class="col-12 col-md-4">
                <div class="card h-100 shadow-sm">
                    <div class="card-body">
                        <h5 class="card-title">個人介紹頁</h5>
                        <p class="card-text">用 HTML + CSS Flexbox 做的靜態介紹頁。</p>
                        <a href="#" class="btn btn-outline-primary">查看作品</a>
                    </div>
                </div>
            </div>
            <div class="col-12 col-md-4">
                <div class="card h-100 shadow-sm">
                    <div class="card-body">
                        <h5 class="card-title">Vue 練習</h5>
                        <p class="card-text">用 Vue.js 做的響應式互動頁面。</p>
                        <a href="#" class="btn btn-outline-primary">查看作品</a>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

這個頁面有導覽列、Hero 區塊、三欄卡片，在手機上自動變成單欄——全部不到 60 行 HTML。

---

## 結語：框架讓你站在巨人的肩膀上

Bootstrap 5 不是讓你「偷懶」的工具，而是讓你把時間花在更有價值的地方——功能邏輯、使用者體驗、創意設計，而不是重複造輪子。

**接下來你可以做什麼？**
Bootstrap 雖好，但有時候你會想要更精細地控制每一個樣式，而不是被框架的設計限制住。下一篇我們來看 **Tailwind CSS**——一個完全不同的思路，讓你在 HTML 裡直接組合樣式，彈性超高！

**準備好看看 CSS 框架的另一種哲學嗎？下一篇見！**
