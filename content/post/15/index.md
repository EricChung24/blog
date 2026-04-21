---
title: "新手第十五步：React 入門　前端最熱門的框架，到底在紅什麼？"
date: 2026-04-17
draft: false
description: "你一定聽過 React，很紅、很多公司在用、職缺也很多。但 React 到底在解決什麼問題？這篇用新手聽得懂的方式，帶你一次搞懂 React 的核心觀念。"
image: "https://legacy.reactjs.org/logo-og.png"
tags: ["React", "JavaScript", "前端框架", "新手入門"]
categories: ["React", "前端框架"]
---

你學完 HTML、CSS、JavaScript 之後，應該已經可以做出會動的網頁了。

但只要功能一變多，很快就會開始出現這些問題：
* 一個資料改了，很多地方都要手動更新
* 按鈕事件越綁越多，程式碼開始打結
* 頁面狀態一多，很難知道現在到底是哪裡出了問題
* 同樣的 UI 要重複寫很多次

這就是前端框架存在的原因。  
而在所有前端框架裡，**React** 幾乎是目前最熱門、也最常出現在職缺上的名字。

---

## 1. React 是什麼？

React 是由 **Meta（Facebook）** 開發的前端函式庫，用來建立使用者介面（UI）。

你可以把它理解成一套更有組織的方式，讓你去寫：

* 畫面怎麼長
* 資料怎麼變
* 當資料改變時，畫面怎麼自動更新

React 最有名的地方，不是它「能做動畫」或「能發 API」，而是它把前端畫面拆得更清楚、更容易維護。

簡單說：

> **React 幫你把「資料」和「畫面」的關係整理好。**

---

## 2. 為什麼前端要用 React？

先想像一個購物車頁面。

當你把商品數量從 1 改成 2 的時候，頁面上很多地方都要一起改：

* 商品小計要更新
* 總金額要更新
* 導覽列上的購物車數量要更新
* 如果超過免運門檻，提示訊息也要更新

如果你用原生 JavaScript 手動處理，通常會變成：

1. 先抓商品數量的 DOM
2. 再抓總金額的 DOM
3. 再抓購物車 icon 的 DOM
4. 每改一次資料，就手動一個一個改畫面

這樣在小專案還可以，但功能一多就會變得很痛苦。

**React 的想法不一樣：**

你不用一直想「我要改哪個 DOM」，你只要想：

* 現在資料是什麼
* 這份資料應該長出什麼畫面

當資料改變時，React 會幫你把該更新的地方更新掉。

這種寫法叫做 **宣告式（Declarative）**。

---

## 3. React 在解決什麼問題？

React 主要在解決 3 件事：

### 1. 畫面重複利用

一個按鈕、一張商品卡片、一個導覽列，常常會在網站很多地方重複出現。  
React 可以把它們拆成**元件（Component）**，寫一次、重複使用很多次。

### 2. 資料和畫面同步

當資料變了，畫面要跟著變。  
React 幫你把這件事變得很自然，不需要你一直自己手動操作 DOM。

### 3. 大型專案的可維護性

當頁面越來越多、互動越來越複雜時，React 的元件化寫法會比一大包原生 JS 更容易整理。

---

## 4. React 的 3 個核心觀念

如果你剛接觸 React，先搞懂這三個觀念就夠了。

### 元件（Component）

React 把 UI 當成一塊一塊的小積木。

例如一個網站可以拆成：
* Header
* Sidebar
* ProductCard
* Button
* Footer

每一塊都可以是一個 React 元件。

```jsx
function Welcome() {
    return <h1>歡迎來到我的網站</h1>;
}
```

這就是最基本的 React 元件。它本質上就是一個函式，回傳一段 UI。

### Props

元件之間要傳資料時，會用到 **props**。

```jsx
function Welcome(props) {
    return <h1>你好，{props.name}</h1>;
}
```

```jsx
<Welcome name="Eric" />
```

這樣畫面就會顯示：`你好，Eric`

你可以把 props 想成「父元件傳給子元件的參數」。

### State

如果 props 是外面傳進來的資料，那 **state** 就是元件自己管理的資料。

最常見的例子就是計數器：

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            目前次數：{count}
        </button>
    );
}
```

當 `count` 改變時，React 會自動重新 render，畫面上的數字也會跟著更新。

---

## 5. 一個最小 React 範例

來看一個最簡單、最能感受到 React 特色的例子。

```jsx
import { useState } from "react";

function App() {
    const [message, setMessage] = useState("你好，React！");

    function changeMessage() {
        setMessage("訊息被改掉了！");
    }

    return (
        <div>
            <h1>{message}</h1>
            <button onClick={changeMessage}>點我換訊息</button>
        </div>
    );
}

export default App;
```

這段做了什麼？

* 用 `useState` 建立一個狀態 `message`
* 畫面先顯示 `你好，React！`
* 點按鈕後呼叫 `setMessage`
* React 發現 state 變了，就重新更新畫面

這裡最重要的地方是：

**你完全沒有手動去抓 DOM，也沒有自己寫 `document.getElementById()`。**  
你只是在改資料，React 幫你把畫面同步更新。

這就是 React 最核心的爽感。

---

## 6. JSX 是什麼？為什麼看起來像 HTML？

React 程式碼裡最讓新手困惑的地方，通常就是這個：

```jsx
return <h1>Hello React</h1>;
```

這看起來像 HTML，但它其實不是純 HTML，而是 **JSX**。

JSX 是一種讓你可以在 JavaScript 裡面寫類似 HTML 語法的寫法。  
它的目的是讓 UI 結構更直覺、更容易閱讀。

例如：

```jsx
const name = "Eric";

return <h1>你好，{name}</h1>;
```

這裡的 `{name}` 代表「把 JavaScript 變數插進畫面裡」。

你可以把 JSX 想成：

> **用比較好讀的方式去描述 UI 長什麼樣子。**

---

## 7. React vs 原生 JavaScript：差在哪？

這個問題很多新手都會問，而且問得很好。

### 原生 JavaScript 的做法

你通常會：

* 先抓 DOM
* 幫按鈕綁事件
* 在事件裡手動更新文字
* 有更多區塊時，再一個一個更新

這樣的好處是：
* 沒有額外框架
* 很直接
* 很適合做小功能

但缺點是：
* 畫面邏輯和 DOM 操作很容易混在一起
* 當功能變多，維護成本會快速上升

### React 的做法

React 比較像是：

* 先定義資料
* 再定義資料對應的畫面
* 當資料改變時，React 幫你更新 UI

它的優點是：
* 更適合大型專案
* 元件可以重複使用
* 狀態管理比較清楚

所以結論不是「React 取代原生 JS」，而是：

> **原生 JS 是基礎，React 是讓大型 UI 開發更有效率的工具。**

---

## 8. React vs Vue：新手該怎麼看？

你前面已經看過 Vue 文章了，那 React 和 Vue 差在哪？

先講結論：

* **Vue** 對新手通常比較友善
* **React** 在職場上更常見，生態系也非常大

### Vue 的感覺

Vue 的模板語法比較接近 HTML，很多新手第一次看會覺得比較自然。

例如 Vue 會寫：

```html
<button @click="count++">點我</button>
```

對剛接觸前端框架的人來說，這種寫法通常比較好懂。

### React 的感覺

React 會把 UI 和邏輯更緊密地寫在一起，用 JSX 來組合。

```jsx
<button onClick={() => setCount(count + 1)}>點我</button>
```

一開始你可能會覺得 React 比較「像在寫 JavaScript」，門檻稍微高一點。  
但也因為這樣，它在組合彈性和工程化上非常強。

### 那到底學哪個？

如果你是完全新手：
* Vue 通常比較快上手

如果你考慮求職市場：
* React 通常更值得優先投入

不過你不用把它想成二選一。  
**框架只是工具，重點還是你對 HTML、CSS、JavaScript 基礎有沒有真的懂。**

---

## 9. 給新手的學習順序建議

如果你準備開始學 React，我建議順序是這樣：

1. 先把 JavaScript 基礎打穩
2. 學 React 元件、props、state
3. 再學事件處理和列表渲染
4. 接著學 `useEffect`
5. 最後再碰 API 串接、路由、狀態管理

很多人卡住不是因為 React 太難，而是因為 JavaScript 基礎不夠穩，就直接跳進框架。

React 確實有學習曲線，但只要你知道它在解決什麼問題，很多概念會突然變清楚。

---

## 結語：React 紅不是沒有原因

React 之所以紅，不是因為它比較潮，而是因為它真的很適合拿來開發大型、互動複雜的前端介面。

它的核心思想其實不花俏：

* 把 UI 拆成元件
* 把資料和畫面關係整理清楚
* 讓資料改變時，畫面自動同步

只要你把這三件事理解了，React 就不會再只是「那個很紅的框架」，而是你手上很有用的工具。

**接下來你可以做什麼？**  
下一篇我們可以直接接著寫 **React `useState` 入門**，因為 state 是 React 最核心、也最早一定會碰到的觀念。等你把 `useState` 和 `useEffect` 都打通之後，React 就會開始真正連起來。

**準備好正式進入 React 的世界了嗎？下一篇見！**
