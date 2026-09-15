# C# Day 1 學習筆記設計

## 目標

在 Hugo 部落格新增一篇可供初學者回顧的繁體中文 C# Day 1 學習筆記，記錄基礎語法與實作心得。

## 文章定位

文章採「實作筆記型」而非教科書式說明：每個主題先用一兩句話說明用途，再提供小型 C# 範例、注意事項與當日理解。內容以第一天能吸收與練習的範圍為限，但比速查筆記更完整。

## 內容結構

1. 開場：當日學習目標與 C# 程式的基本執行概念。
2. 基礎型別：`int`、`double`、`decimal`、`bool`、`char`、`string`，以及 `var` 的合適使用時機。
3. 型別轉換與使用者輸入：`Convert`、`TryParse` 與避免程式因不合法輸入中斷。
4. 條件判斷：`if`、`else if`、`else`、`switch` 與邏輯運算子。
5. 陣列：建立、索引、長度與常見越界錯誤。
6. 迴圈：`for`、`foreach`、`while` 與 `break`／`continue`。
7. 方法：用參數與回傳值將重複邏輯整理成可重用單位。
8. 整合練習：以「成績統計小程式」串連陣列、條件判斷、迴圈與方法。
9. Day 1 重點、常見踩雷與 Day 2 練習方向。

## 呈現與技術細節

- 建立一個 Hugo leaf bundle：`content/post/csharp-day1/index.md`。
- Front matter 使用繁體中文標題、說明、標籤與分類；文章為非草稿。
- Markdown 程式碼區塊使用 `csharp` 標記，所有範例均可置於 C# Console 專案中理解或練習。
- 不使用外部圖片、套件或網路資料，避免不必要的載入與授權問題。

## 驗證條件

- 文章檔案為 UTF-8，中文標題與內文不會產生亂碼。
- Front matter 正確且包含 `title`、`date`、`draft`、`description`、`tags`、`categories`。
- Markdown 有完整章節與正確閉合的程式碼區塊。
- 若專案已安裝 Hugo，使用 Hugo 建置確認文章能被解析。
