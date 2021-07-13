---
title: Node(4) - EJS
tags: 
- EJS
categories: Node.js
---
EJS 是個樣板語言
<!--more-->
### 安裝並建立好資料夾
1. npm 安裝
```
npm install ejs-locals --save
```

2. 引入檔案中
- 下面：
(程式碼10)：set 可以設定 express 的各種方式。
(程式碼10)：設定樣板位置，第一個'views'名稱，在第二個'./views'資料夾檔案位置。(完成後記得新增一個 views 的資料夾)
(程式碼11)：使用什麼引勤跑，ex: pug或其他...。完成後在 views 資料夾中新增 index.ejs 檔案，裡面放普通 html。
(程式碼14)：載入 index，從上面11程式中可以看到是 ejs 樣板的 index，檔案位置在程式10的路徑上。
```
const express = require('express')
const app = express();

// 增加靜態檔案路徑
app.use(express.static('public'))

// 這邊引入 ejs 樣板
const engine = require('ejs-locals')  // 引入
app.engine('ejs',engine)  // 載入核心.使用 express 的 ejs 做樣板的控制
app.set('views', './views')  // 上面說明.指定樣板資料夾位置
app.set('view engine', 'ejs')  // 使用引勤
app.get('/',function(req, res) {
  // res.send('132000000000')  --> 原本的方式.把顯示放這裡
  res.render('index')  // 載入模板的方式，不用寫 index.ejs
})
app.get('/user',function(req, res) {
  res.render('user') 
})

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port)
```

### 資料傳送
#### 參數導入與渲染格式
app.js 中
```
const express = require('express')
const app = express();

app.use(express.static('public'))

const engine = require('ejs-locals')  
app.engine('ejs',engine)  
app.set('views', './views')  
app.set('view engine', 'ejs')  
app.get('/',function(req, res) {
  res.render('index', {
    'title':'<h1>我是標題</h1>',
    'name':'teisha',
    'show': true,
    'list':['html', 'css', 'js']
    })  // 這邊寫資料
})

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port)
```

index.ejs 中，以符號「<% %>」包住，
A. 變數顯示字串 「<%= 變數 %>」
B. 透過 ejs 整理 html 格式 「<%- html格式 %>」
C. 判斷 「<% 一堆判段的內容 %>」(注意這邊寫的方式!)
D. 陣列(注意這邊寫的方式!)
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <%= title%>  // <h1>我是標題</h1> ==>字串
  <%- title%>  // 我是標題 ==>有h1格式
  <h2><%= name%></h2>  // teisha
  <h2><%= name -%></h2>  // 後面有個「-」表示去掉沒有的空格

  // 判斷式 - 注意下面寫的方式!
  <% if(show){ %>  
    <span>畫面顯示</span>
  <% }%>

  // 陣列 - 注意下面寫的方式!
  <ul>
  <% for(let i=0; list.length>i; i++){ %>
    <li><%- list[i] %></li>
  <% } %>
  </ul>

</body>
</html>
```

### 模板管理
同樣的地方統一管理
1. 在資料夾 views 中新增一個檔案 layout.ejs 
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <%- body %>  // 這邊
</body>
</html>
```

2. 在要載入版面的地方第一行增加要載入的模板
```
<% layout('layout') %>
```

因此跑檔案時會先看到要先載入什麼模板，在顯示內容



