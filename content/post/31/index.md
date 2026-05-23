---
title: "json-server 是什麼？前端開發很常用的假 API 工具介紹"
date: 2026-05-23T20:05:00+08:00
draft: false
description: "介紹 npm 上的 json-server 套件頁面，整理它的用途、安裝方式、適合情境，以及為什麼前端工程師會常拿它來快速建立假 API。"
image: "/json-server-npm.png"
tags: ["json-server", "npm", "mock api", "frontend", "react"]
categories: ["前端工具"]
---

前端開發最常遇到的問題之一，就是畫面想先做，但 API 還沒完成。這時候，如果還要自己手刻一個後端，只是為了讓前端有資料可以串，通常很浪費時間。`json-server` 就是在解決這個問題。

[`json-server` 的 npm 頁面](https://www.npmjs.com/package/json-server) 介紹的是一個非常實用的工具：你只要準備一份 JSON 資料，它就能快速幫你產生一組可用的 REST API。對前端工程師來說，這代表你不用等後端，也能先把列表、表單、編輯、刪除這些功能做起來。

![json-server npm 頁面截圖](/json-server-npm.png)

## 這個網站在做什麼？

這個網站其實是 npm 上的套件介紹頁。它的用途不是單純下載，而是讓開發者快速了解：

- 這個套件是做什麼的
- 要怎麼安裝
- 怎麼啟動
- 支援哪些功能
- 套件目前版本和使用狀況

以 `json-server` 這頁來看，頁面上可以直接看到安裝指令：

```bash
npm i json-server
```

也可以看到最基本的啟動方式：

```bash
npx json-server db.json
```

這兩個資訊就已經很夠你快速上手。

## json-server 的核心功能是什麼？

它最核心的功能，就是把一個 JSON 檔案變成一組 REST API。

例如你有一個 `db.json`：

```json
{
  "posts": [
    { "id": 1, "title": "Hello" },
    { "id": 2, "title": "World" }
  ]
}
```

啟動 `json-server` 後，就可以得到類似下面的 API：

```bash
GET /posts
GET /posts/1
POST /posts
PUT /posts/1
PATCH /posts/1
DELETE /posts/1
```

這代表什麼？代表你前端原本需要後端才能做的 CRUD 流程，現在可以先自己模擬出來。

## 為什麼前端工程師會常用它？

原因很實際，因為它真的省時間。

第一，它可以讓前端先開發，不用卡在「API 還沒好」。
第二，它很適合做 demo、作品集、教學範例。
第三，它能讓你提早驗證資料格式和畫面流程。
第四，它的使用門檻低，不需要先寫很多後端程式。

如果你是 React 開發者，這種工具特別方便，因為你可以直接拿 `fetch` 或 `axios` 去串它，流程和串正式 API 很接近。

## 這個 npm 頁面還透露哪些資訊？

根據我查看頁面時的內容，截至 **2026-05-23**，可以看到幾個重點：

- 版本是 `1.0.0-beta.15`
- 每週下載量約 `332,131`
- License 是 `MIT`
- GitHub repository 是 `typicode/json-server`
- 有 `412` 個 dependents
- 累積 `165` 個版本

這些資訊代表它不是冷門工具，而是真的有不少開發者在使用。不過也要注意，頁面顯示的版本仍然是 `beta`，如果你要放進正式團隊開發流程，最好先確認版本相容性和使用情境。

## 它適合用在哪些情境？

`json-server` 很適合這幾種情況：

- 前端畫面先做，但後端還沒完成
- 想快速做一個假資料 API
- 想練習 CRUD 串接
- 要做作品集或 demo
- 教學時想快速展示 API 行為

但它比較不適合拿來當真正的正式後端。因為它的主要目的是開發輔助，不是完整商業系統的後端解法。

## 總結

如果你把 `json-server` 想成「前端開發時的假後端工具」，這個理解基本上就是對的。它最大的價值不是功能多複雜，而是可以讓你非常快地把資料流跑起來。對前端來說，這件事很重要，因為很多畫面問題、互動問題、狀態管理問題，都要真的有 API 可以串時才會看得清楚。

所以，如果你常常碰到「前端要先做，但 API 還沒來」這種情況，那 `json-server` 是非常值得認識的一個工具。
