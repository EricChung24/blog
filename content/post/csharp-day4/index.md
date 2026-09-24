---
title: "學習 C# Day 4：猜數字遊戲與輸入驗證"
date: 2026-09-18T09:00:00+08:00
draft: false
description: "用 Random、while、TryParse 與條件判斷完成一個可重複輸入的猜數字遊戲。"
tags: ["C#", ".NET", "Random", "TryParse", "Console"]
categories: ["C# 學習筆記"]
---

# 學習 C# Day 4：猜數字遊戲與輸入驗證

今天把前幾天的內容組合起來：用亂數出題、讀取使用者輸入、驗證輸入格式，並在答對前持續執行迴圈。

![猜數字遊戲的輸入驗證與重試流程](https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=1200&q=80)

## 產生 1 到 9 的亂數

`Random().Next(min, max)` 的最小值會包含，最大值不包含。因此 `Next(1, 10)` 會得到 `1` 到 `9`。

```csharp
int answer = new Random().Next(1, 10);
```

常見錯誤是寫成 `Next(1, 9)`，那樣永遠不會得到 `9`。

## 讀取使用者輸入

`Console.ReadLine()` 的結果是文字，型別為 `string?`。即使使用者輸入的是數字，也不能直接拿來和 `int` 比較。

```csharp
Console.Write("請輸入你的名稱：");
string? name = Console.ReadLine();

Console.WriteLine($"{name}，歡迎來到猜數字遊戲！");
```

## 用 `TryParse` 安全轉成數字

使用者可能輸入 `abc`、空白或其他非數字內容。`int.TryParse` 不會因為格式錯誤讓程式中斷，而是回傳 `false`。

```csharp
string? input = Console.ReadLine();

if (int.TryParse(input, out int guess))
{
    Console.WriteLine($"你輸入的是 {guess}");
}
else
{
    Console.WriteLine("請輸入數字。");
}
```

## 完整猜數字遊戲

這個範例會在輸入不是數字、超出範圍或猜錯時繼續詢問；猜中才用 `break` 結束迴圈。

```csharp
int answer = new Random().Next(1, 10);

Console.WriteLine("歡迎來到猜數字遊戲");
Console.Write("請輸入你的名稱：");
string? name = Console.ReadLine();
Console.WriteLine($"{name}，請猜 1 到 9 的數字。");

while (true)
{
    Console.Write("你的答案：");
    string? input = Console.ReadLine();

    if (!int.TryParse(input, out int guess))
    {
        Console.WriteLine("輸入格式錯誤，請輸入數字。");
        continue;
    }

    if (guess < 1 || guess > 9)
    {
        Console.WriteLine("請輸入 1 到 9 之間的數字。");
        continue;
    }

    if (guess == answer)
    {
        Console.WriteLine("答對了！");
        break;
    }

    Console.WriteLine("猜錯了，再試一次。\n");
}
```

## 程式流程

1. 先產生一個 `1` 到 `9` 的答案。
2. 在 `while (true)` 中持續讀取輸入。
3. 用 `TryParse` 檢查是否能轉成整數。
4. 不合法時用 `continue` 回到迴圈開頭；答對時用 `break` 結束。

## Day 4 重點整理

1. `Random().Next(1, 10)` 會產生 `1` 到 `9`，上限 `10` 不會出現。
2. `Console.ReadLine()` 讀到的是文字，需要轉型才能做數值比較。
3. `TryParse` 比 `Convert.ToInt32` 更適合處理使用者輸入，因為格式錯誤不會直接拋出例外。
4. `continue` 處理無效輸入；`break` 結束猜中的遊戲流程。

可以嘗試的下一步：加入猜測次數，並在答對時顯示一共猜了幾次。
