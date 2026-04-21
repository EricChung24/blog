---
title: "新手第十四步：React useEffect 入門　搞懂副作用，不再亂用！"
date: 2026-04-17
weight: 14
draft: false
description: "很多 React 新手一學到 useEffect，就什麼都想塞進去。其實它不是萬用鉤子，而是專門處理副作用的工具。這篇帶你從零搞懂它該用在哪裡。"
image: "https://legacy.reactjs.org/logo-og.png"
tags: ["React", "useEffect", "Hooks", "新手入門"]
categories: ["React", "前端框架"]
---

很多 React 新手一看到 `useEffect`，第一反應都是：「這個看起來很強，我是不是什麼事情都可以丟進去？」

結果寫著寫著，就開始出現這些狀況：
* 頁面一直重複 re-render
* API 被呼叫兩三次
* 明明只是想把名字組起來，卻還多寫一個 state
* 元件卸載後還在跑計時器，畫面越來越怪

**`useEffect` 不是萬用工具，它是拿來處理「副作用」的。**  
只要你先搞懂這句話，後面大部分問題都會少很多。

---

## 1. `useEffect` 是什麼？

React 元件最主要的工作，是根據 `state` 和 `props` 去**畫畫面**。

但有些事情不是單純畫畫面就能完成，例如：

* 向後端抓資料
* 監聽視窗大小變化
* 設定 `setInterval`
* 手動改 `document.title`
* 訂閱或解除訂閱外部事件

這些事情都會影響元件外部，或需要和外部世界互動，這種行為就叫做 **副作用（Side Effect）**。

而 `useEffect`，就是 React 提供給你的「副作用處理區」。

```jsx
import { useEffect } from "react";

function App() {
    useEffect(() => {
        console.log("元件渲染完成後執行");
    });

    return <h1>Hello React</h1>;
}
```

上面這段的意思是：**React 先把畫面渲染出來，然後再執行 `useEffect` 裡面的程式。**

---

## 2. 什麼時候該用 `useEffect`？

你可以先記一個最實用的判斷方式：

> **如果這件事跟「畫面外部」有關，就可能要用 `useEffect`。**

例如下面這些情況，就是典型的 `useEffect` 使用時機。

### 抓 API 資料
```jsx
useEffect(() => {
    fetch("/api/products")
        .then((res) => res.json())
        .then((data) => {
            console.log(data);
        });
}, []);
```

### 監聽事件
```jsx
useEffect(() => {
    function handleResize() {
        console.log(window.innerWidth);
    }

    window.addEventListener("resize", handleResize);
}, []);
```

### 改變瀏覽器標題
```jsx
useEffect(() => {
    document.title = "購物車頁面";
}, []);
```

這幾個例子有一個共同點：**它們都不是單靠 JSX render 就能完成的事。**

---

## 3. 什麼時候不該用 `useEffect`？

這才是新手最容易踩雷的地方。

如果某個值可以直接從現有資料算出來，那就**不要**再用 `useEffect` 多繞一圈。

### 錯誤示範：把可推導的值塞進 `useEffect`
```jsx
import { useEffect, useState } from "react";

function UserCard({ firstName, lastName }) {
    const [fullName, setFullName] = useState("");

    useEffect(() => {
        setFullName(firstName + " " + lastName);
    }, [firstName, lastName]);

    return <h2>{fullName}</h2>;
}
```

這段可以跑，但寫法不好，因為 `fullName` 明明可以直接算出來，沒必要多一份 state。

### 正確寫法：直接算
```jsx
function UserCard({ firstName, lastName }) {
    const fullName = firstName + " " + lastName;

    return <h2>{fullName}</h2>;
}
```

這樣更簡單，也更不容易出 bug。

**記住一句話：能在 render 階段直接算出來的東西，就不要丟進 `useEffect`。**

---

## 4. 依賴陣列到底在控制什麼？

`useEffect` 的第二個參數，通常是大家最容易看不懂的地方：

```jsx
useEffect(() => {
    // 做某些事情
}, []);
```

這個陣列叫做**依賴陣列（dependency array）**，它在控制的是：

**「哪些值改變時，這個 effect 要重新執行？」**

### 1. 不寫依賴陣列
```jsx
useEffect(() => {
    console.log("每次 render 都會執行");
});
```

只要元件重新 render，這段就會再跑一次。

### 2. 傳空陣列 `[]`
```jsx
useEffect(() => {
    console.log("只在初次掛載時執行");
}, []);
```

通常用在：
* 初次載入資料
* 初次註冊事件
* 初始化某些外部設定

### 3. 傳入特定依賴 `[count]`
```jsx
useEffect(() => {
    console.log("count 改變了");
}, [count]);
```

這表示只有 `count` 改變時，這個 effect 才會重新執行。

---

## 5. cleanup 是什麼？為什麼很重要？

有些副作用不是做完就算了，它還需要在適當時機**清掉**。

最常見的例子就是：

* 事件監聽
* 計時器
* WebSocket 連線
* 訂閱外部資料

這時候就要用 `return` 回傳一個清理函式，也就是 **cleanup**。

```jsx
useEffect(() => {
    function handleResize() {
        console.log(window.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    return () => {
        window.removeEventListener("resize", handleResize);
    };
}, []);
```

這段的意思是：

* 元件掛載時，註冊 `resize` 事件
* 元件卸載時，把事件監聽移除

如果你不做 cleanup，常見結果就是：
* 事件越綁越多
* 記憶體浪費
* 元件已經不在了，副作用卻還繼續跑

---

## 6. 給新手的實戰範例：切換網頁標題

先來看一個很簡單、但很適合理解 `useEffect` 的例子。

```jsx
import { useEffect, useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    useEffect(() => {
        document.title = `你點了 ${count} 次`;
    }, [count]);

    return (
        <div>
            <h2>目前次數：{count}</h2>
            <button onClick={() => setCount(count + 1)}>
                點我加一
            </button>
        </div>
    );
}
```

這段程式做了兩件事：

* 畫面上顯示 `count`
* 當 `count` 改變時，順便更新瀏覽器分頁標題

為什麼這裡適合用 `useEffect`？

因為 `document.title` 是**React 畫面外部的東西**。  
React 可以控制 `<h2>` 裡顯示什麼，但瀏覽器標題不是 JSX 自己就會處理的，所以這種時候就該交給 `useEffect`。

---

## 7. 新手最常犯的 3 個錯誤

### 錯誤 1：把所有邏輯都塞進 `useEffect`

很多人一遇到資料變化，就直覺寫 `useEffect`。但其實很多值都可以直接 render 時計算，不需要繞遠路。

### 錯誤 2：依賴沒寫完整

如果 effect 裡用到了某個值，但依賴陣列沒放進去，就可能造成資料不同步，或拿到舊值。

### 錯誤 3：忘了 cleanup

特別是事件監聽和計時器，忘記清掉的後果通常不是立刻爆炸，而是過一段時間才出現怪問題，最難查。

---

## 8. 你可以先這樣記

如果你現在腦袋有點亂，先不用急著背細節，記住下面這個版本就夠用了：

* `useEffect` 是拿來處理副作用的
* 能直接 render 算出來的值，不要用 `useEffect`
* `[]` 代表只在初次執行
* `[value]` 代表 `value` 改變時重新執行
* 有監聽、計時器、訂閱時，記得 cleanup

---

## 結語：先學會少用，才會真的用

很多新手學 `useEffect` 的第一個問題，是「它能做什麼？」  
但更重要的問題其實是：**「什麼時候不該用它？」**

因為 `useEffect` 本身不難，難的是你要分得出來：

* 這是單純 render 邏輯
* 還是這真的是副作用

只要這條線分清楚，你的 React 程式碼就會乾淨很多，也比較不容易掉進無限 re-render 的坑裡。

**接下來你可以做什麼？**  
下一篇如果你願意，我們可以接著寫 **React `useState` 與 `useEffect` 的搭配實戰**，用真正的 API 抓資料、載入中狀態、錯誤處理，一次把 React 最常見的流程串起來。

**學會 `useEffect` 之後，你就開始真的在寫 React 了。**
