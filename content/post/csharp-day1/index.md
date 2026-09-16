---
title: "學習 C# Day 1：基礎型別、判斷式、陣列與迴圈"
date: 2026-09-15T09:00:00+08:00
draft: false
description: "記錄 C# Day 1 學到的基礎型別、型別轉換、條件判斷、陣列、迴圈與方法，並以成績統計小程式整合練習。"
tags: ["C#", ".NET", "程式學習", "學習筆記", "基礎語法"]
categories: ["程式學習"]
---

# 學習 C# Day 1

今天開始接觸 C#。第一天的目標不是把所有語法背起來，而是先建立一個基本觀念：**資料要用什麼型別保存、程式如何依條件做選擇，以及如何重複處理一批資料。**

我把今天的內容整理成筆記，之後忘記時可以快速回來複習。

## 先認識 C# 程式的入口

在 Console 專案中，程式會從 `Main` 開始執行。可以先把它想成：「按下執行後，電腦從這裡往下看。」

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, C#!");
    }
}
```

`Console.WriteLine` 會在終端機印出文字，這是初學時觀察程式是否照預期執行的好工具。

> 小提醒：C# 大小寫有差別。`Console` 不能寫成 `console`，`Main` 也不能寫成 `main`。

## 基礎型別：先決定資料長什麼樣子

變數可以想成有名字的盒子，而「型別」是在告訴 C# 這個盒子能裝什麼資料。先選對型別，後面做運算或判斷才不容易出問題。

```csharp
int age = 25;                 // 整數
double temperature = 28.5;    // 小數，適合一般量測值
decimal price = 199.90m;      // 金額建議用 decimal，m 不可省略
bool isLoggedIn = true;       // true 或 false
char grade = 'A';             // 單一字元，要用單引號
string name = "Eric";         // 一串文字，要用雙引號

Console.WriteLine($"{name} 的年齡是 {age} 歲，商品價格是 {price} 元。");
```

目前最常用到的型別可以這樣記：

- `int`：沒有小數點的數字，例如年齡、數量、分數。
- `double`：一般小數，例如身高、溫度、平均值。
- `decimal`：金額或需要較精準十進位計算的數字。
- `bool`：只有「是／否」兩種狀態。
- `char`：一個字元；`string`：一段文字。

### `var` 可以用，但不是萬用型別

`var` 不是「不管什麼都能放」的型別，而是讓編譯器根據右邊的值推斷型別。推斷完後，型別就固定了。

```csharp
var city = "Taipei"; // 編譯器推斷為 string
var count = 3;        // 編譯器推斷為 int

// count = "three"; // 錯誤：count 已經是 int
```

當右邊很明確時可以使用 `var`；如果明確寫出型別能讓程式更容易閱讀，直接寫 `string`、`int` 也很好。

> 常見錯誤：`char` 用單引號，`string` 用雙引號；而金額的 `decimal` 數值後面要加 `m`，例如 `99.5m`。

## 型別轉換與使用者輸入

從 `Console.ReadLine()` 取得的內容永遠是文字（`string`）。如果想把使用者輸入的年齡拿來比較，就要先轉成數字。

```csharp
Console.Write("請輸入年齡：");
string? input = Console.ReadLine();

if (int.TryParse(input, out int userAge))
{
    Console.WriteLine($"明年你會是 {userAge + 1} 歲。");
}
else
{
    Console.WriteLine("請輸入有效的整數年齡。");
}
```

以前看到 `Convert.ToInt32()` 覺得很直覺，但使用者若輸入 `abc`，程式就可能直接拋出例外。`TryParse` 比較適合處理外部輸入，因為它會回傳 `true` 或 `false`，讓我們決定下一步怎麼做。

```csharp
string text = "42";
int number = Convert.ToInt32(text);
```

這種寫法適合你非常確定 `text` 一定是數字的情況；面對使用者輸入，優先使用 `TryParse`。

## 條件判斷：讓程式做選擇

`if` 用來判斷某件事是否成立。條件的結果必須是 `bool`，也就是 `true` 或 `false`。

```csharp
int score = 78;

if (score >= 90)
{
    Console.WriteLine("A：表現很好！");
}
else if (score >= 60)
{
    Console.WriteLine("及格，繼續保持。");
}
else
{
    Console.WriteLine("還沒及格，找出不熟的章節再練一次。");
}
```

判斷式的順序很重要。上面的 `score >= 90` 必須放在 `score >= 60` 前面，否則 90 分會先符合 60 分的條件，永遠走不到 A 的分支。

### 邏輯運算子

當條件不只一個時，可以用邏輯運算子組合。

```csharp
int age = 20;
bool hasTicket = true;

if (age >= 18 && hasTicket)
{
    Console.WriteLine("可以入場。");
}

if (age < 12 || age >= 65)
{
    Console.WriteLine("符合優惠資格。");
}

if (!hasTicket)
{
    Console.WriteLine("請先購票。");
}
```

- `&&`：兩個條件都要成立。
- `||`：至少一個條件成立。
- `!`：把 true 變 false、false 變 true。

### `switch`：固定選項時更好讀

如果是根據一個值決定多個固定結果，`switch` 通常比一長串 `if...else if` 更清楚。

```csharp
string role = "admin";

switch (role)
{
    case "admin":
        Console.WriteLine("擁有完整管理權限。");
        break;
    case "editor":
        Console.WriteLine("可以編輯文章。");
        break;
    default:
        Console.WriteLine("一般訪客權限。");
        break;
}
```

> 常見錯誤：比較相等要用 `==`，不是 `=`。單一 `=` 是「指派值」，例如 `score = 100`。

## 陣列：把同類資料放在一起

當資料不只一筆，例如一班同學的分數，就可以使用陣列。陣列建立後長度固定，而且索引從 **0** 開始。

```csharp
int[] scores = { 88, 72, 95, 61, 49 };

Console.WriteLine(scores[0]);      // 88，第一筆資料
Console.WriteLine(scores.Length);  // 5，陣列共有五筆資料

scores[1] = 75; // 修改第二筆資料
```

索引和日常數數不同：第一筆是 `scores[0]`，最後一筆是 `scores[scores.Length - 1]`。

```csharp
string[] fruits = new string[3];
fruits[0] = "蘋果";
fruits[1] = "香蕉";
fruits[2] = "芒果";
```

> 常見錯誤：三個元素的陣列可用索引只有 `0`、`1`、`2`。存取 `fruits[3]` 會發生 `IndexOutOfRangeException`。

## 迴圈：重複做一件事

遇到重複工作時，不需要一直複製貼上。迴圈能讓程式依規則重複執行。

### `for`：需要索引或固定次數時

`for` 適合要知道目前第幾筆資料，或需要控制執行次數的情況。

```csharp
int[] scores = { 88, 72, 95, 61, 49 };

for (int index = 0; index < scores.Length; index++)
{
    Console.WriteLine($"第 {index + 1} 位同學：{scores[index]} 分");
}
```

這裡條件是 `index < scores.Length`，不是 `<=`。因為最後一個合法索引是 `scores.Length - 1`。

### `foreach`：只需要逐一讀取時

如果只要讀取每一筆值，不需要索引，`foreach` 更簡潔。

```csharp
string[] languages = { "C#", "JavaScript", "TypeScript" };

foreach (string language in languages)
{
    Console.WriteLine($"正在學習：{language}");
}
```

`foreach` 的優點是少了索引越界的機會；不過要直接修改原本陣列的元素時，通常改用 `for` 會比較合適。

### `while`：不知道要跑幾次時

`while` 會在條件成立時持續執行，適合「一直問到輸入正確」這一類需求。

```csharp
string? password = "";

while (password != "1234")
{
    Console.Write("請輸入密碼：");
    password = Console.ReadLine();
}

Console.WriteLine("登入成功。");
```

> 常見錯誤：`while` 裡的條件相關變數一定要有機會改變，不然程式會無限迴圈。除錯時可先在迴圈內印出變數，確認條件是否真的會變成 `false`。

### `break` 與 `continue`

`break` 是立刻離開整個迴圈；`continue` 是略過本次，直接進入下一輪。

```csharp
for (int number = 1; number <= 10; number++)
{
    if (number == 3)
    {
        continue; // 不印出 3
    }

    if (number == 8)
    {
        break; // 到 8 就停止
    }

    Console.WriteLine(number);
}
```

## 方法：幫重複邏輯取名字

當一段邏輯有明確用途，而且可能會重複使用，就可以抽成方法。方法能讓主程式更像在閱讀流程，而不是被細節塞滿。

```csharp
static bool IsPassed(int score)
{
    return score >= 60;
}

static void PrintResult(string name, int score)
{
    string result = IsPassed(score) ? "及格" : "未及格";
    Console.WriteLine($"{name}：{score} 分，{result}");
}
```

呼叫方法時，把需要的資料傳進去：

```csharp
PrintResult("小明", 85);
PrintResult("小美", 55);
```

- `void`：方法只做事、不回傳資料。
- `bool`：方法回傳 `true` 或 `false`。
- `int`、`string` 等型別：代表方法回傳對應型別的資料。

> 小提醒：方法的參數型別和傳入的值要對得上；另外，`static` 方法可以直接從 `Main` 呼叫，這是 Console 入門練習常見的寫法。

## 整合練習：成績統計小程式

這個練習把今天的重點放在一起：陣列儲存成績、迴圈逐一處理、條件判斷及格人數，最後用方法計算平均。

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] scores = { 88, 72, 95, 61, 49 };
        int passedCount = 0;

        foreach (int score in scores)
        {
            if (score >= 60)
            {
                passedCount++;
            }
        }

        double average = CalculateAverage(scores);

        Console.WriteLine($"平均分數：{average:F1}");
        Console.WriteLine($"及格人數：{passedCount} / {scores.Length}");

        if (average >= 80)
        {
            Console.WriteLine("整體表現很好。");
        }
        else
        {
            Console.WriteLine("可以找出較弱的題型，再多練習。\");
        }
    }

    static double CalculateAverage(int[] scores)
    {
        int total = 0;

        foreach (int score in scores)
        {
            total += score;
        }

        return (double)total / scores.Length;
    }
}
```

這裡最值得注意的是 `(double)total / scores.Length`。如果兩邊都是 `int`，C# 會做整數除法，小數會被捨去；先把 `total` 轉成 `double`，才能得到有小數的平均值。

## Day 1 重點整理

1. 型別描述資料的種類，金額優先使用 `decimal`，真假狀態使用 `bool`。
2. 陣列索引從 0 開始，最後一個索引是 `Length - 1`。
3. 處理使用者輸入時，`TryParse` 比直接轉換更安全。
4. 需要索引用 `for`、只讀取資料用 `foreach`、未知重複次數時用 `while`。
5. 把重複或有明確用途的邏輯抽成方法，程式會更容易閱讀與維護。

## 今天踩到的坑

- 把 `=` 當成比較符號；比較是否相等要用 `==`。
- `for` 寫成 `index <= scores.Length`，導致最後一次索引超出範圍。
- 忘記 `decimal` 後面的 `m`，或忘記整數除法會捨去小數。
- `while` 的條件永遠不會改變，程式一直卡在迴圈中。

## Day 2 可以接著學什麼

下一步想接著了解 `List<T>` 與陣列的差異、字串常用方法、例外處理（`try...catch`），以及類別與物件（class / object）。先把今天的範例自己改幾次，例如讓使用者輸入多筆成績、找出最高分和最低分，會比只看懂更有感。
