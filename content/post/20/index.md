---
title: "找免費圖片不用再怕版權：Unsplash 是前端工程師最好的朋友"
date: 2026-04-20T00:10:00+08:00
draft: false
description: "免費、高畫質、可商用、不用標示來源——Unsplash 幾乎是我每個 side project 都會用到的圖庫網站。"
image: "https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["Unsplash", "免費資源", "圖片素材", "前端工具"]
categories: ["工具與工作流"]
---

做 side project 的時候，有一個地方很容易卡住：

**圖片要從哪裡來？**

自己拍？沒那個美學和器材。

隨便去 Google 圖片抓？小心被版權找上門。

買付費圖庫？一張動輒好幾百塊，side project 根本不划算。

這個問題困擾我很久，直到我認真開始用 [Unsplash](https://unsplash.com)。

---

## Unsplash 是什麼？

一個**完全免費**的高品質圖片網站。

特色：

- **免費下載** — 不用付錢、不用訂閱
- **可以商用** — 做產品、做網站、印刷品都可以
- **不用標示來源**（但標了攝影師會很開心）
- **畫質超高** — 隨便一張都是幾千像素寬
- **量大** — 幾百萬張照片，幾乎什麼主題都找得到

簡單說，就是**一群專業攝影師把自己的作品無償釋出來給大家用**。

---

## 怎麼用？

### 1. 直接到 [unsplash.com](https://unsplash.com) 搜尋

輸入關鍵字，例如 `coffee`、`mountain`、`code`，結果會出來一堆高品質照片。

### 2. 下載你喜歡的圖

點進去之後，右上角有「Download free」按鈕，可以選不同尺寸。

### 3. 透過網址直接嵌入（進階）

Unsplash 有一個很讚的功能：**每張圖都有穩定的 CDN 網址**。

你不一定要把圖下載下來再上傳到自己的伺服器，可以直接 hotlink：

```html
<img src="https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?w=1200&q=80" />
```

網址後面可以加參數控制：

- `w=1200` — 寬度 1200px
- `q=80` — 壓縮品質 80%
- `fit=crop` — 裁切模式
- `auto=format` — 自動選擇最佳格式（WebP 之類）

這個部落格大部分的封面圖，就是直接用 Unsplash 的 CDN 網址。

---

## 前端工程師怎麼用最順？

### 情境 1：部落格封面圖

每篇文章都要一張封面？去 Unsplash 找，貼 URL，搞定。

### 情境 2：Landing page 英雄區

需要一張有氛圍的 hero image？Unsplash 的攝影作品比很多付費圖庫還有質感。

### 情境 3：Mockup 假資料

做 demo 時要放使用者頭像、產品圖？Unsplash 有 **[Unsplash Source API](https://unsplash.com/developers)**：

```html
<!-- 隨機一張分類為 nature 的圖 -->
<img src="https://source.unsplash.com/800x600/?nature" />
```

每次重新整理都會換一張，做 mockup 很方便。

### 情境 4：直接整合進設計工具

Figma、Canva、Notion 都有 Unsplash 外掛，不用離開工具就能插圖。

---

## 使用前要注意的事

雖然 Unsplash 非常寬鬆，但還是有一些**不能做**的事情：

1. **不能把 Unsplash 的圖原封不動重新打包成圖庫販售**
2. **不能用來做明顯詆毀照片中人物的內容**
3. **不能用來暗示照片中的人物代言你的產品**（除非你有模特兒授權）

講白一點：**只要你是把圖拿來用在自己的作品裡，基本上都 OK。**

完整條款在這裡：[Unsplash License](https://unsplash.com/license)

---

## 其他類似的網站

如果在 Unsplash 找不到你要的風格，可以試試這幾個：

| 網站 | 特色 |
|------|------|
| [Unsplash](https://unsplash.com) | 攝影感強，氛圍照最多 |
| [Pexels](https://www.pexels.com) | 同時有照片和影片 |
| [Pixabay](https://pixabay.com) | 照片、插畫、向量、音樂都有 |
| [Burst](https://burst.shopify.com) | Shopify 出的，電商產品圖多 |

我自己是以 Unsplash 為主，Pexels 當備援。

---

## 小結

Unsplash 解決了獨立開發者和小團隊最煩的問題之一：**找圖不用再怕版權**。

如果你還在 Google 圖片右鍵存檔，或是怕被告不敢放圖，趕快換個習慣：

👉 [unsplash.com](https://unsplash.com)

把時間花在寫 code、做產品，不是花在煩惱圖片授權。
