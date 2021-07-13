---
title: Node(5) - 整合 Express、EJS
tags: 
- 
categories: Node.js
---

### 表單

--------------------------------------------------------------
### 頁面跳轉

--------------------------------------------------------------
### 整合 Express 產生器
[Express 應用程式產生器](https://expressjs.com/zh-tw/starter/generator.html)
#### 安裝
1. 建立好所有資料夾
但是沒有 node_modules
```
npm install express-generator -g
```

2. 建立 node_modules
```
npm install
```

3. 執行 npm star，輸入本地端網址
localhost:3000 或 http://127.0.0.1:3000/

#### 解析
```
var express = require('express');
var path = require('path'); // 路徑
var favicon = require('serve-favicon'); // 放ico
var logger = require('morgan'); // 紀錄日誌資料
var cookieParser = require('cookie-parser'); // 可以接受 cookie 資料做解析
var bodyParser = require('body-parser');

// 路由，用下面這2個管理程式26、27行
var index = require('./routes/index');
var users = require('./routes/users');

var app = express();

// view engine setup  使用到 ejs，如果需要 layout 可以在載入 ejs-locals
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

// uncomment after placing your favicon in /public
// app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
app.use(logger('dev'));
app.use(bodyParser.join()); // 使用 ejs 撈到 get、post資料
app.use(bodyParser.urlencoded({ extended: false})); // 使用 ejs 撈到 get、post資料
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));

// 更有效率的管理檔案：對應到 routes 資料夾中的 js 檔案
app.use('/', index);
app.use('/users', users);

// 404 
.....
```