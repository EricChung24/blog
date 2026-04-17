---
title: "新手第十三步：Async / Await 與 API 串接　讓網頁讀取真實世界的資料！"
date: 2026-04-17
draft: false
description: "靜態網頁的內容是死的，串接 API 才能讓你的網頁活起來！這篇從同步非同步的概念、fetch、Promise，到 async/await 和實戰 API 串接，一步一步帶你搞懂。"
image: "https://images.unsplash.com/photo-1558494949-ef010cbdcc31?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&q=80"
tags: ["JavaScript", "API", "Async", "Fetch", "新手入門"]
categories: ["JavaScript", "API"]
---

到目前為止，你網頁上的所有資料都是**自己寫死**的。標題、卡片內容、圖片——全都是你親手打進去的。

但真實的網站不是這樣運作的。你打開天氣 App，資料是從氣象局的伺服器來的；你滑 Instagram，圖片是從 Meta 的資料庫來的；你用 Google 搜尋，結果是從爬過全世界網頁的資料庫來的。

這一切都靠一個東西：**API 串接**。

---

## 1. 什麼是 API？

**API（Application Programming Interface，應用程式介面）** 是一個讓不同系統之間互相溝通的「窗口」。

用餐廳來比喻：
* **你**是前端（客人）
* **廚房**是後端（資料庫 / 伺服器）
* **服務生**就是 API

你不需要進廚房，只要告訴服務生你要什麼（送出 Request），服務生就會把廚房做好的食物端給你（回傳 Response）。

**常見的 API 使用場景：**
* 天氣資訊（OpenWeatherMap API）
* 地圖（Google Maps API）
* 金流（綠界、藍新 API）
* 社群登入（Google / Facebook OAuth API）
* AI 功能（OpenAI API）

---

## 2. 同步 vs 非同步：一個讓新手頭痛的概念

### 同步（Synchronous）
程式碼**一行一行按順序執行**，下一行必須等上一行執行完才能開始。

```javascript
console.log("第一步");
console.log("第二步");
console.log("第三步");

// 輸出順序：第一步 → 第二步 → 第三步
```

### 非同步（Asynchronous）
某些操作**很耗時**（例如向伺服器請求資料，可能需要 1~3 秒），如果用同步的方式執行，整個頁面會**卡住**等待，什麼事都不能做。

非同步讓 JavaScript 可以：「你去向伺服器拿資料，我先繼續做其他事，**等你拿回來再處理**。」

```javascript
console.log("開始請求資料");

// 向 API 請求資料（非同步，需要時間）
fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => console.log("資料回來了：", data));

console.log("這行不等資料，先執行");

// 輸出順序：
// 開始請求資料
// 這行不等資料，先執行
// 資料回來了：{ ... }  ← 等 API 回應後才執行
```

---

## 3. Promise：非同步操作的承諾

**Promise** 是 JavaScript 表示「未來會完成的操作」的物件。

想像你去餐廳點餐，服務生給你一個**號碼牌**（Promise）：
* 等一下食物做好，你拿號碼牌去領（`.then()`）
* 如果廚房失火做不了，你也會被通知（`.catch()`）

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => {
        return response.json();   // 把回應轉成 JSON 格式
    })
    .then(data => {
        console.log(data);        // 使用資料
    })
    .catch(error => {
        console.error("出錯了：", error);  // 處理錯誤
    });
```

`.then()` 可以串聯多個，每個 `.then()` 接收上一個 `.then()` 的 `return` 值。

---

## 4. Async / Await：讓非同步程式碼看起來像同步

Promise 的 `.then()` 鏈寫多了會很難閱讀。**`async / await`** 是更現代、更好讀的寫法，本質上還是 Promise，只是語法更直覺。

### 基本語法

```javascript
// 在函式前加 async，代表這個函式裡面有非同步操作
async function getData() {
    // await 代表「等這行執行完再繼續」
    const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const data = await response.json();
    console.log(data);
}

getData();
```

### 加上錯誤處理

```javascript
async function getData() {
    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");

        if (!response.ok) {
            throw new Error(`HTTP 錯誤：${response.status}`);
        }

        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("請求失敗：", error.message);
    }
}
```

`try...catch` 是處理非同步錯誤的標準做法：`try` 裡面放正常流程，`catch` 裡面處理例外狀況。

### async / await vs .then() 對比

```javascript
// .then() 寫法（舊式）
function getUser() {
    fetch("/api/user")
        .then(res => res.json())
        .then(user => {
            fetch(`/api/posts/${user.id}`)
                .then(res => res.json())
                .then(posts => console.log(posts));
        });
}

// async/await 寫法（現代，推薦）
async function getUser() {
    const userRes = await fetch("/api/user");
    const user = await userRes.json();

    const postsRes = await fetch(`/api/posts/${user.id}`);
    const posts = await postsRes.json();

    console.log(posts);
}
```

同樣的功能，`async/await` 版本閱讀起來就像普通的同步程式碼，清楚多了。

---

## 5. fetch API：瀏覽器內建的 HTTP 請求工具

`fetch` 是現代瀏覽器內建的 API，讓你不需要安裝任何套件就能發送 HTTP 請求。

### GET 請求（取得資料）

```javascript
async function getPosts() {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    const posts = await response.json();
    return posts;
}
```

### POST 請求（送出資料）

```javascript
async function createPost(title, body) {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",   // 告訴伺服器你送的是 JSON
        },
        body: JSON.stringify({                     // 把物件轉成 JSON 字串
            title: title,
            body: body,
            userId: 1,
        }),
    });

    const newPost = await response.json();
    console.log("建立成功：", newPost);
}
```

### HTTP 方法速查

| 方法 | 用途 |
|------|------|
| `GET` | 取得資料 |
| `POST` | 建立新資料 |
| `PUT` | 完整更新資料 |
| `PATCH` | 部分更新資料 |
| `DELETE` | 刪除資料 |

---

## 6. 認識 JSON：API 的通用語言

API 傳回來的資料通常是 **JSON（JavaScript Object Notation）** 格式。

```json
{
    "id": 1,
    "name": "小明",
    "email": "ming@example.com",
    "age": 18,
    "hobbies": ["前端開發", "打籃球", "看動漫"],
    "address": {
        "city": "台北市",
        "district": "信義區"
    }
}
```

JSON 的規則：
* 所有 key 要用**雙引號**包起來
* 字串值也要用**雙引號**
* 支援 String、Number、Boolean、Array、Object、null

**在 JavaScript 中操作 JSON：**
```javascript
// JSON 字串 → JavaScript 物件
const obj = JSON.parse('{"name": "小明", "age": 18}');
console.log(obj.name);  // "小明"

// JavaScript 物件 → JSON 字串
const json = JSON.stringify({ name: "小明", age: 18 });
console.log(json);  // '{"name":"小明","age":18}'
```

---

## 7. 實戰練習一：串接公開 API 顯示文章列表

我們用 [JSONPlaceholder](https://jsonplaceholder.typicode.com)（一個免費的假 API）來練習。

**HTML：**
```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>文章列表</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 700px; margin: 40px auto; padding: 0 20px; background: #f5f5f5; }
        h1 { color: #2c3e50; }
        .post-card { background: white; border-radius: 8px; padding: 20px; margin-bottom: 16px; box-shadow: 0 2px 6px rgba(0,0,0,0.08); }
        .post-card h3 { margin: 0 0 8px; color: #34495e; text-transform: capitalize; }
        .post-card p { margin: 0; color: #666; line-height: 1.6; }
        #loading { text-align: center; color: #888; padding: 40px; }
    </style>
</head>
<body>
    <h1>最新文章</h1>
    <div id="loading">載入中...</div>
    <div id="post-list"></div>

    <script>
        async function loadPosts() {
            try {
                const response = await fetch("https://jsonplaceholder.typicode.com/posts?_limit=10");
                const posts = await response.json();

                const loading = document.getElementById("loading");
                const postList = document.getElementById("post-list");

                loading.style.display = "none";  // 隱藏載入提示

                posts.forEach(post => {
                    const card = document.createElement("div");
                    card.className = "post-card";
                    card.innerHTML = `
                        <h3>${post.title}</h3>
                        <p>${post.body}</p>
                    `;
                    postList.appendChild(card);
                });

            } catch (error) {
                document.getElementById("loading").textContent = "載入失敗，請稍後再試。";
                console.error(error);
            }
        }

        loadPosts();
    </script>
</body>
</html>
```

打開瀏覽器，你會看到 10 篇從 API 取得的文章自動渲染到頁面上！

---

## 8. 實戰練習二：在 Vue 3 + Vite 中串接 API

在 Vue 專案中，搭配 `ref` 和 `onMounted` 來串接 API 是最標準的做法：

```vue
<template>
    <div class="container">
        <h1>使用者列表</h1>

        <!-- 載入中狀態 -->
        <p v-if="loading" class="loading">載入中...</p>

        <!-- 錯誤狀態 -->
        <p v-else-if="error" class="error">{{ error }}</p>

        <!-- 成功顯示資料 -->
        <div v-else class="user-grid">
            <div v-for="user in users" :key="user.id" class="user-card">
                <h3>{{ user.name }}</h3>
                <p>📧 {{ user.email }}</p>
                <p>🌐 {{ user.website }}</p>
                <p>🏙️ {{ user.address.city }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);
const loading = ref(true);
const error = ref(null);

async function fetchUsers() {
    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");

        if (!response.ok) throw new Error("無法取得資料");

        users.value = await response.json();
    } catch (err) {
        error.value = err.message;
    } finally {
        loading.value = false;  // 不管成功或失敗，都結束載入狀態
    }
}

// onMounted：元件掛載到頁面後自動執行
onMounted(() => {
    fetchUsers();
});
</script>

<style scoped>
.container { max-width: 900px; margin: 40px auto; padding: 0 20px; }
.loading { text-align: center; color: #888; }
.error { color: red; text-align: center; }
.user-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
}
.user-card {
    background: white;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}
.user-card h3 { margin: 0 0 12px; color: #2c3e50; }
.user-card p { margin: 4px 0; color: #555; font-size: 14px; }
</style>
```

這段程式碼示範了 API 串接最重要的三個狀態管理：
* **loading**：資料還在載入時顯示等待畫面
* **error**：請求失敗時顯示錯誤訊息
* **data**：成功後顯示資料

---

## 9. 使用需要 API Key 的服務

很多真實 API 需要申請 **API Key** 才能使用（用來識別是誰在呼叫 API）。

以 **OpenWeatherMap 天氣 API** 為例：

```javascript
const API_KEY = "你的API金鑰";
const city = "Taipei";

async function getWeather() {
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric&lang=zh_tw`;

    const response = await fetch(url);
    const data = await response.json();

    console.log(`${data.name} 目前氣溫：${data.main.temp}°C`);
    console.log(`天氣狀況：${data.weather[0].description}`);
}

getWeather();
```

> **重要安全提醒：** API Key 絕對不能放在前端程式碼裡 commit 到 GitHub（任何人都看得到！）。正確的做法是放在 `.env` 檔案裡，並在 `.gitignore` 排除它。

```bash
# .env 檔案
VITE_WEATHER_API_KEY=你的API金鑰
```

```javascript
// 在 Vue 裡使用
const API_KEY = import.meta.env.VITE_WEATHER_API_KEY;
```

---

## 10. 常見錯誤與解法

### CORS 錯誤
```
Access to fetch at 'https://...' has been blocked by CORS policy
```
這是最常見的 API 錯誤。CORS 是瀏覽器的安全機制，防止網頁隨意存取其他網域的資源。

解法：
* 確認 API 有開放 CORS（公開 API 通常都有）
* 若是自己的後端，在伺服器端設定允許的來源
* 開發階段可在 `vite.config.js` 設定代理（proxy）繞過

### response.json() 失敗
```
SyntaxError: Unexpected token < in JSON at position 0
```
表示 API 回傳的不是 JSON，可能是 HTML 錯誤頁面。先用 `console.log(response.status)` 確認狀態碼。

### 404 / 401 / 500 錯誤
```javascript
if (!response.ok) {
    // response.status 會是 404、401、500 等
    throw new Error(`錯誤代碼：${response.status}`);
}
```
* `401`：未授權，需要 API Key 或登入
* `403`：禁止存取，權限不足
* `404`：找不到資源，確認 URL 是否正確
* `500`：伺服器錯誤，對方的問題

---

## 結語：你的網頁現在連接到真實世界了

學完這篇，你已經能夠：
* 理解同步 vs 非同步的差異
* 用 `fetch` + `async/await` 串接任何 REST API
* 正確處理載入、成功、失敗三種狀態
* 在 Vue 3 中整合 API 資料
* 避免把 API Key 洩漏到 GitHub

**接下來你可以做什麼？**
有了 API 串接能力，下一篇我們要學 **Vue Router**——讓你的 Vue 應用程式擁有多個頁面，實現真正的「單頁應用程式（SPA）」，做出有導覽列、有路由切換的完整網站架構！

**準備好蓋出多頁面的網站了嗎？下一篇見！**
