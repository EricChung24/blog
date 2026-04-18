---
title: "部落格終於有留言板了！聊聊我為什麼選 Giscus"
date: 2026-04-18
draft: false
description: "從零開始架這個部落格以來，一直有一件事沒做完——留言板。今天終於搞定了，順便聊聊為什麼選 Giscus，以及它怎麼運作的。"
image: "https://images.unsplash.com/photo-1516321497487-e288fb19713f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["Giscus", "Hugo", "部落格", "GitHub"]
categories: ["部落格紀錄"]
---

如果你以前來過這裡，你可能注意到一件事：

**每篇文章的最下面，什麼都沒有。**

沒有留言區、沒有回覆按鈕、沒有「你怎麼看？」的欄位。

只有文章結尾，然後就是頁尾。

這不是故意的，只是一直沒時間把留言板搞定。

今天，這件事終於完成了。

---

## 為什麼留言板拖了這麼久？

其實留言板本身不難，難的是「選哪一個」。

市面上常見的選項大概是這些：

- **Disqus** — 最老牌，但免費版有廣告，資料不在自己手上
- **Waline / Artalk** — 功能強，但需要自己架後端伺服器
- **Utterances** — 輕量，存在 GitHub Issues，但設計比較陽春
- **Giscus** — 存在 GitHub Discussions，開源、免費、支援 dark mode

我本來想用 **Artalk**，因為介面很漂亮。

但 Artalk 需要一台後端伺服器。自己架要花時間維護，用雲端托管平台又多了一層依賴。

對一個靜態部落格來說，這有點殺雞用牛刀。

最後我選了 **Giscus**。

---

## Giscus 是什麼？

簡單說：

> **Giscus 把你的 GitHub repo 的 Discussions，當作留言板的資料庫。**

每一篇文章，對應一個 GitHub Discussion。  
有人留言，就等於在那個 Discussion 底下回覆。  
你的回覆，也會直接出現在文章頁面上。

這個設計有幾個我很喜歡的地方：

### 1. 完全不需要後端伺服器

留言存在 GitHub，不用自己租 VPS，不用架 Docker，不用管資料庫備份。

對靜態網站來說，這是最舒服的架法。

### 2. 資料永遠在自己手上

留言存在你的 GitHub repo，你隨時可以看、可以匯出、可以刪除。  
不像 Disqus，資料放在別人的伺服器上，哪天服務關掉就沒了。

### 3. 完全免費

GitHub Discussions 完全免費。  
Giscus 本身也是開源的，沒有廣告、沒有付費方案差異。

### 4. 自動支援 dark mode

這個部落格有深色模式，Giscus 設定成 `preferred_color_scheme` 之後，  
深色模式下留言板也會跟著變暗，不會突然出現一個刺眼的白色區塊。

---

## 怎麼裝的？

這個部落格用 Hugo 搭配 Stack 主題。

Stack 主題原生就支援 Giscus，只需要三個步驟：

**Step 1** — 在 GitHub repo 開啟 Discussions 功能  
**Step 2** — 安裝 [Giscus App](https://github.com/apps/giscus)，授權給你的 repo  
**Step 3** — 在 `params.toml` 填入 repo ID 和 category ID

```toml
[comments]
enabled  = true
provider = "giscus"

[comments.giscus]
repo           = "你的帳號/你的repo"
repoID         = "R_xxxxxx"
category       = "Announcements"
categoryID     = "DIC_xxxxxx"
mapping        = "pathname"
lightTheme     = "light"
darkTheme      = "dark_dimmed"
reactionsEnabled = 1
```

設定完 `git push`，留言板就出現了。

沒有伺服器，沒有資料庫，沒有額外費用。

---

## 給你的邀請

這個部落格寫了快二十篇文章，

一直是我單方面在輸出，不知道你有沒有看、有什麼問題、或是文章哪裡沒講清楚。

現在留言板裝好了。

如果哪篇文章你有問題、有補充、或是覺得我哪裡寫錯了，  
都歡迎在下面留言。

**你是第一個能在這裡留言的人。**