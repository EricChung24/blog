---
title: "新手第九步：Tailwind CSS 入門　用 class 直接堆出你要的樣式！"
date: 2026-04-17
draft: false
description: "Tailwind 和 Bootstrap 完全不同——它不給你做好的元件，而是給你幾百個小 class 讓你自由組合。第一次看會覺得 HTML 很醜，用過就回不去了。"
image: "https://images.unsplash.com/photo-1618477388954-7852f32655ec?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["Tailwind CSS", "CSS 框架", "前端工具", "新手入門"]
categories: ["基礎教學"]
---

學完 Bootstrap，你已經體驗過 CSS 框架的威力。但 Bootstrap 有一個隱藏的痛點：**所有用 Bootstrap 做的網站看起來都長得差不多**。

Tailwind CSS 採用了完全不同的思路——它不給你預設好的元件，而是給你幾百個「工具類別」，讓你像積木一樣自由組合出任何你想要的樣式。

---

## 1. Tailwind 和 Bootstrap 的哲學差異

| | Bootstrap | Tailwind CSS |
|---|---|---|
| 思路 | 給你做好的元件，直接用 | 給你工具類別，自己組合 |
| 客製化程度 | 中（需要覆寫樣式） | 高（完全自由） |
| HTML 可讀性 | 較乾淨 | class 比較多 |
| 學習曲線 | 較平緩 | 需要記 class 名稱 |
| 設計一致性 | 容易長得一樣 | 每個網站可以完全不同 |

兩個都是好工具，端看你的需求選擇。

---

## 2. 快速上手：用 CDN 體驗 Tailwind

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tailwind 練習</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 p-8">

    <h1 class="text-3xl font-bold text-blue-600 text-center mb-4">
        你好，Tailwind！
    </h1>

    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        點我
    </button>

</body>
</html>
```

> 注意：CDN 方式適合學習和原型開發，正式專案建議用 npm 安裝以獲得完整功能（後面的 Vite 篇會介紹）。

---

## 3. Tailwind 的命名邏輯

Tailwind 的 class 名稱設計得非常直覺，只要懂幾個規律就能舉一反三：

### 間距（Spacing）
```html
<!-- p = padding, m = margin -->
<!-- t=top, b=bottom, l=left, r=right, x=左右, y=上下 -->
<!-- 數字 0,1,2,3,4,5,6,8,10,12,16,20... 代表大小（1 = 4px） -->

<div class="p-4">內距 16px</div>
<div class="mt-8">上方外距 32px</div>
<div class="px-6 py-3">左右內距 24px，上下內距 12px</div>
```

### 顏色（Colors）
```html
<!-- 顏色名稱-深淺（100最淺，900最深） -->
<div class="bg-blue-500 text-white">藍底白字</div>
<div class="bg-gray-100 text-gray-800">淺灰底深灰字</div>
<div class="text-red-600">紅色文字</div>

<!-- Tailwind 內建顏色：slate, gray, zinc, red, orange, yellow, green, blue, purple, pink... -->
```

### 字體（Typography）
```html
<p class="text-sm">小字（14px）</p>
<p class="text-base">預設大小（16px）</p>
<p class="text-xl">大字（20px）</p>
<p class="text-4xl font-bold">超大粗體（36px）</p>
<p class="text-center italic text-gray-500">置中斜體灰色</p>
```

### 彈性布局（Flexbox）
```html
<div class="flex justify-between items-center">
    <span>左</span>
    <span>右</span>
</div>

<div class="flex flex-col gap-4">
    <div>垂直</div>
    <div>排列</div>
    <div>有間距</div>
</div>
```

### 響應式（Responsive）
```html
<!-- 斷點前綴：sm: md: lg: xl: 2xl: -->
<div class="text-sm md:text-base lg:text-lg">
    手機小字、平板中字、桌機大字
</div>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <!-- 手機單欄，平板雙欄，桌機三欄 -->
</div>
```

### 互動狀態
```html
<!-- hover:、focus:、active: 前綴 -->
<button class="bg-blue-500 hover:bg-blue-700 active:scale-95 transition-all">
    有互動效果的按鈕
</button>
```

---

## 4. 常用的元件範例

### 按鈕
```html
<!-- 主要按鈕 -->
<button class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-5 rounded-lg transition-colors">
    主要操作
</button>

<!-- 外框按鈕 -->
<button class="border-2 border-blue-600 text-blue-600 hover:bg-blue-600 hover:text-white font-semibold py-2 px-5 rounded-lg transition-all">
    次要操作
</button>
```

### 卡片
```html
<div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow">
    <img class="w-full h-48 object-cover" src="圖片網址" alt="...">
    <div class="p-6">
        <h3 class="text-xl font-bold text-gray-800 mb-2">卡片標題</h3>
        <p class="text-gray-600 mb-4">卡片描述文字</p>
        <a href="#" class="text-blue-600 font-semibold hover:underline">閱讀更多 →</a>
    </div>
</div>
```

---

## 5. 給新手的實戰練習：用 Tailwind 重做作品集

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的作品集</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 font-sans">

    <!-- 導覽列 -->
    <nav class="bg-gray-900 text-white px-8 py-4 flex justify-between items-center">
        <span class="text-xl font-bold">Eric's Portfolio</span>
        <div class="flex gap-6 text-gray-300">
            <a href="#" class="hover:text-white transition-colors">首頁</a>
            <a href="#" class="hover:text-white transition-colors">作品</a>
            <a href="#" class="hover:text-white transition-colors">聯絡</a>
        </div>
    </nav>

    <!-- Hero -->
    <div class="bg-blue-600 text-white text-center py-24 px-4">
        <h1 class="text-5xl font-bold mb-4">你好，我是前端新手</h1>
        <p class="text-xl text-blue-200 mb-8">正在努力學習 HTML、CSS 和 JavaScript</p>
        <a href="#" class="bg-white text-blue-600 font-bold py-3 px-8 rounded-full hover:bg-blue-50 transition-colors">
            查看我的作品
        </a>
    </div>

    <!-- 作品卡片 -->
    <div class="max-w-5xl mx-auto py-16 px-4">
        <h2 class="text-3xl font-bold text-center text-gray-800 mb-10">我的作品</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="bg-white rounded-xl p-6 shadow hover:shadow-md transition-shadow">
                <h3 class="text-lg font-bold text-gray-800 mb-2">計數器 App</h3>
                <p class="text-gray-500 mb-4">用原生 JavaScript 做的互動計數器。</p>
                <a href="#" class="text-blue-600 font-semibold hover:underline text-sm">查看作品 →</a>
            </div>
            <div class="bg-white rounded-xl p-6 shadow hover:shadow-md transition-shadow">
                <h3 class="text-lg font-bold text-gray-800 mb-2">個人介紹頁</h3>
                <p class="text-gray-500 mb-4">用 HTML + CSS Flexbox 做的靜態介紹頁。</p>
                <a href="#" class="text-blue-600 font-semibold hover:underline text-sm">查看作品 →</a>
            </div>
            <div class="bg-white rounded-xl p-6 shadow hover:shadow-md transition-shadow">
                <h3 class="text-lg font-bold text-gray-800 mb-2">Vue 練習</h3>
                <p class="text-gray-500 mb-4">用 Vue.js 做的響應式互動頁面。</p>
                <a href="#" class="text-blue-600 font-semibold hover:underline text-sm">查看作品 →</a>
            </div>
        </div>
    </div>

</body>
</html>
```

同樣的頁面，Tailwind 版和 Bootstrap 版的結果看起來**截然不同**，因為每個樣式都是你自己決定的。

---

## 結語：Tailwind 讓設計真的是你的設計

Tailwind CSS 的學習曲線稍高——前幾天你會一直在查 class 名稱。但一旦熟悉了，你會發現自己從「設計稿到程式碼」的速度快了很多，而且不用擔心和別人的網站「撞臉」。

**接下來你可以做什麼？**
現在我們用的都是 CDN 引入，沒有辦法用到 Tailwind 的 JIT 模式或 SCSS 的完整功能。下一篇要學 **Vite**——現代前端的建置工具，讓你的開發環境真正「工程化」起來！

**準備好打造專業開發環境了嗎？下一篇見！**
