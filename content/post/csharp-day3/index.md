---
title: "學習 C# Day 3：方法與九九乘法表"
date: 2026-09-17T09:00:00+08:00
draft: false
description: "認識 C# 方法的參數與回傳值，並用巢狀迴圈完成九九乘法表。"
tags: ["C#", ".NET", "方法", "迴圈"]
categories: ["C# 學習筆記"]
---

# 學習 C# Day 3：方法與九九乘法表

今天的目標是把重複邏輯抽成方法（method），並透過巢狀迴圈輸出九九乘法表。方法能讓程式更容易閱讀、測試與重複使用。

## 沒有回傳值的方法：`void`

`void` 表示方法只負責做事，不回傳結果。沒有參數時，呼叫時的括號內也不需要傳值。

```csharp
void PrintSentence()
{
    Console.WriteLine("This is a sentence");
}

PrintSentence();
```

## 有參數與回傳值的方法

`Power` 接收一個 `int` 參數 `number`，計算平方後回傳 `int`。

```csharp
int Power(int number)
{
    return number * number;
}

Console.WriteLine(Power(3)); // 9
```

方法可以接收多個參數，也可以回傳不同型別。

```csharp
double Add(double left, double right)
{
    return left + right;
}

string DoubleString(string text)
{
    return text + text;
}

Console.WriteLine(Add(3, 4));
Console.WriteLine(DoubleString("Hi "));
```

### 箭頭函式

當方法只有一行回傳邏輯時，可使用 `=>` 簡寫。

```csharp
double Subtract(double left, double right) => left - right;
```

這種寫法適合簡單運算；邏輯變多時，使用 `{ }` 與 `return` 會更容易閱讀。

## 巢狀迴圈：九九乘法表

外層迴圈控制乘數，內層迴圈控制被乘數。外層每跑一次，內層都會完整跑完一次。

```csharp
for (int multiplier = 1; multiplier <= 9; multiplier++)
{
    for (int multiplicand = 1; multiplicand <= 9; multiplicand++)
    {
        Console.Write($"{multiplier} × {multiplicand} = {multiplier * multiplicand}\t");
    }

    Console.WriteLine();
}
```

## 把一組乘法表抽成方法

以下 `PrintRows` 一次印出三組乘法表。`{value,2}` 讓數字至少佔兩格並靠右對齊，因此輸出較整齊。

```csharp
void PrintRows(int start)
{
    for (int multiplicand = 1; multiplicand <= 9; multiplicand++)
    {
        for (int multiplier = start; multiplier < start + 3; multiplier++)
        {
            Console.Write($"{multiplier} × {multiplicand} = {multiplier * multiplicand,2}\t");
        }

        Console.WriteLine();
    }
}

for (int start = 1; start <= 9; start += 3)
{
    PrintRows(start);
    Console.WriteLine();
}
```

## Day 3 重點整理

1. `void` 方法沒有回傳值；其他回傳型別的方法必須 `return` 對應型別的資料。
2. 參數是方法需要的輸入；引數是呼叫方法時實際傳入的值。
3. 巢狀迴圈中，外層跑一次，內層會從頭跑到尾。
4. 重複邏輯應抽成方法，避免複製貼上造成維護困難。

下一天會把迴圈、條件判斷與輸入驗證組合成一個猜數字遊戲。
