---
title: "學習 C# Day 2：陣列與迴圈"
date: 2026-09-16T09:00:00+08:00
draft: false
description: "用 C# 陣列保存多筆資料，並透過 for、while、do...while 與 foreach 逐一處理。"
tags: ["C#", ".NET", "陣列", "迴圈"]
categories: ["C# 學習筆記"]
---

# 學習 C# Day 2：陣列與迴圈

今天的重點是把多筆資料放進陣列，再用迴圈依序讀取它們。這是之後處理商品、成績或 API 資料的基礎。

![陣列中的資料由迴圈依序處理](https://images.unsplash.com/photo-1515879218367-8466d910aaa4?auto=format&fit=crop&w=1200&q=80)

## 陣列：同一類資料的集合

陣列可用來存放固定數量、相同型別的資料。索引從 `0` 開始。

```csharp
int[] scores = { 80, 90, 75 };

Console.WriteLine(scores[0]); // 80
Console.WriteLine(scores[1]); // 90
Console.WriteLine(scores.Length); // 3
```

若只先決定長度，元素會使用型別的預設值：`int` 是 `0`。

```csharp
int[] numbers = new int[3];

Console.WriteLine(numbers[0]); // 0
numbers[0] = 10;
```

> `new int[3]` 是建立三個元素的陣列，不會自動放入 `1、2、3`。

### 二維陣列

二維陣列可把資料想成表格，第一個索引是列，第二個索引是欄。

```csharp
int[,] table =
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};

Console.WriteLine(table[1, 1]); // 5
Console.WriteLine(table[1, 2]); // 6
```

字串也能放進陣列：

```csharp
string[] languages = { "C#", "JavaScript", "TypeScript" };
```

## `for`：知道索引時使用

`for` 適合需要索引、計數或修改特定位置的情境。

```csharp
int[] numbers = { 1, 2, 3 };

for (int index = 0; index < numbers.Length; index++)
{
    Console.WriteLine($"numbers[{index}] = {numbers[index]}");
}
```

條件要寫成 `index < numbers.Length`。若寫成 `<=`，最後一次會讀取不存在的位置，造成 `IndexOutOfRangeException`。

## `while` 與 `do...while`

`while` 在每次執行前判斷條件；條件一開始不成立時，內容完全不會執行。

```csharp
int index = 0;

while (index < numbers.Length)
{
    Console.WriteLine(numbers[index]);
    index++;
}
```

`do...while` 則一定至少執行一次，再判斷是否繼續。

```csharp
int index = 0;

do
{
    Console.WriteLine(numbers[index]);
    index++;
} while (index < numbers.Length);
```

## `foreach`：只需要逐筆讀取時使用

不需要索引時，`foreach` 更簡潔，也不容易寫錯邊界。

```csharp
int[] numbers = { 1, 2, 3, 4 };

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

## `continue`：跳過這一次

以下範例只印出奇數。遇到偶數時，`continue` 會直接進入下一輪。

```csharp
foreach (int number in numbers)
{
    if (number % 2 == 0)
    {
        continue;
    }

    Console.WriteLine(number);
}
```

## Day 2 重點整理

1. 陣列索引從 `0` 開始，最後一個索引是 `Length - 1`。
2. `for` 適合需要索引的情境；`foreach` 適合單純逐筆讀取。
3. `while` 可能執行零次；`do...while` 至少執行一次。
4. `continue` 跳過本輪迴圈，繼續處理下一筆資料。

下一天會把重複的邏輯包成方法，並用巢狀迴圈完成九九乘法表。
