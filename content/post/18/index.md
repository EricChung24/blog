---
title: "我的 Obsidian 知識庫長什麼樣？前端工程師的筆記系統建立方法"
date: 2026-04-19T00:00:00+08:00
draft: false
description: "分享我如何用 Obsidian 建立一套系統化的前端知識庫，從資料夾架構、筆記方法，到如何讓知識真正被內化。"
image: "https://github.com/EricChung24/Obsidian-vault/blob/main/status.png?raw=true"
tags: ["Obsidian", "知識管理", "前端", "PKM", "學習方法"]
categories: ["工具與工作流"]
---

工程師最怕的一件事，不是學不會，是**學了又忘**。

看了一篇很棒的文章，當下覺得懂了，過三天回來看自己的 code 又像在看別人寫的。

這個問題困擾我很久。

直到我開始認真用 Obsidian，才覺得知識開始真正累積起來。

---

## 為什麼選 Obsidian？

市面上的筆記工具不少：Notion、Evernote、Logseq……

我試過不少，最後回到 Obsidian，原因很簡單：

1. **本地純文字（Markdown）** — 資料永遠在自己電腦上，不依賴任何雲端服務
2. **雙向連結** — 可以把不同主題的筆記串聯起來，像大腦一樣形成網狀結構
3. **完全客製化** — 外掛生態系非常豐富，可以打造符合自己習慣的系統
4. **速度快** — 不像 Notion 有時候載入要等，Obsidian 本地執行幾乎零延遲

---

## 知識庫的架構

我的 Obsidian Vault 公開放在 GitHub 上：

👉 [EricChung24/Obsidian-vault](https://github.com/EricChung24/Obsidian-vault)

整個 Vault 以**前端工程師**的知識地圖為核心，目前分成 12 個資料夾：

| 資料夾 | 主題 |
|--------|------|
| `01-基礎技術` | HTML、CSS、JavaScript 核心觀念 |
| `02-框架與函式庫` | React、Vue、Angular 等框架 |
| `03-狀態管理` | Redux、Zustand、Pinia 等 |
| `04-樣式解決方案` | Tailwind、CSS Modules、styled-components |
| `05-建置工具` | Vite、Webpack、Rollup |
| `06-測試` | Jest、Vitest、Cypress、Testing Library |
| `07-效能優化` | Lazy loading、Bundle size、Core Web Vitals |
| `08-瀏覽器與 Web APIs` | DOM、事件迴圈、Fetch、Web Storage |
| `09-設計模式` | 常見 Design Patterns 在前端的應用 |
| `10-無障礙與資安` | a11y、CSRF、XSS 防護 |
| `11-DevOps 與部署` | CI/CD、Docker、Vercel、GitHub Actions |
| `12-面試準備` | 常見面試題整理與解題思路 |

---

## 目前的進度快照

![知識庫進度截圖](https://github.com/EricChung24/Obsidian-vault/blob/main/status.png?raw=true)

這是現在 Vault 的大致狀態。

每個資料夾下面都在持續補充中，不是一次性整理好的，而是**隨著學習推進慢慢長出來的**。

---

## 我怎麼記筆記？

有一個關鍵觀念讓我的筆記系統變得更有用：

> **不要只抄原文，要用自己的話重新解釋一遍。**

這個方法叫做費曼技巧（Feynman Technique）。

做法很簡單：看完一個知識點，把書或文章闔上，嘗試用自己的話解釋給一個完全不懂的人聽。

如果解釋不出來，代表你還沒真正理解，回去重看。

所以我的筆記長這樣：

```markdown
## 什麼是閉包（Closure）？

函式記住了它被建立時的作用域，即使執行時已經離開了那個作用域。

### 用一句話說

「帶著背包的函式，背包裡裝著它出生時能看到的變數。」

### 常見應用

- 工廠函式
- 計數器
- setTimeout 裡面的變數保留
```

重點是：**有自己的比喻、有自己的例子**，不是複製貼上文件。

---

## 雙向連結怎麼用？

Obsidian 最強的功能之一是 `[[雙向連結]]`。

舉例：我在筆記「React useEffect」裡面提到了閉包（stale closure），我就會加一個 `[[閉包（Closure）]]` 的連結。

久了之後，Obsidian 的 Graph View 會畫出一張像這樣的網狀圖，讓你看到各個主題之間的關係。

這不只是整理筆記，而是**讓你的理解可視化**。

---

## 這個系統對我的改變

用 Obsidian 認真整理知識庫大概三到四個月了，有幾個明顯的變化：

1. **學新東西更快** — 因為舊的基礎筆記都在，不用每次從頭回想
2. **面試準備更有系統** — `12-面試準備` 那個資料夾，讓準備面試從「不知道從哪開始」變成有清單可以對照
3. **記憶變得更深** — 動手整理一遍，比看十遍文章更有用

最重要的是：**我終於有一個地方，可以放心把學到的東西存起來，知道以後找得回來。**

---

## 如果你也想建立自己的知識庫

幾個建議：

- **不要等架構完整才開始** — 先隨手記，架構之後再整理
- **不要只複製貼上** — 用自己的話寫，哪怕寫得不好
- **不要追求完整** — 知識庫是長出來的，不是一口氣建起來的
- **定期複習** — 配合 Spaced Repetition（間隔重複），Obsidian 有對應的外掛

我的 Vault 是公開的，如果你也是前端工程師，歡迎參考或 fork 來用：

👉 [github.com/EricChung24/Obsidian-vault](https://github.com/EricChung24/Obsidian-vault)

---

知識管理這件事，沒有標準答案。

重要的是找到一個**你願意持續用下去的系統**。

Obsidian 對我來說就是這個系統。
