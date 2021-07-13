---
title: Node(3) - Express
tags: 
- Node.js
- Express
categories: Node.js
---
### 介紹
Express 是 Node.js 的 npm ，輕量型的網頁應用框架。

可以整合資料庫
ex: firebase、mongo、mySQL

了解後端邏輯觀念
AJAX post、EJS template、jade(pug)

### 安裝
step1. 終端機上
```
// 1. 安裝 package.json
npm init
// 2. 裝 npm 套件
npm i express --save
```

step2. 主要 js 檔案 app.js 上的設定
```
// 載入套件
const express = require('express')
// 透過 app 取得 express 裡面所有功能
const app = express();
console.log(app);
```

step3. 測試安裝成功
終端機上執行，會出現超多可以用的就安裝成功了。
```
node app.js
```
### 網址
#### 開啟網頁伺服器
```
const express = require('express')
const app = express();

// 路徑/ -> 到首頁.自己設定，req -> request，res -> response
app.get('/user', function(req, res){
  res.send('123'); // 想要在網頁呈現什麼畫面，也可以放 html 標籤 <html><head></head><body><p>00000</p></body></html>
})

// 監聽 port
const port = process.env.PORT || 3000; // 使用雲端主機的 port，沒有設定時顯示 3000
app.listen(port); // 持續監聽
```

終端機上執行 node app.js
然後在網址上打 127.0.0.1:3000 會顯示上面 send 的內容

#### 網址規則
https://www.google.com/search?q=%E6%8B%BC%E5%9C%96&rlz=1C1CHBF_zh-TWTW906TW906&oq=%E6%8B%BC%E5%9C%96&aqs=chrome..69i57j0i433j0j0i395l7.1049j1j15&sourceid=chrome&ie=UTF-8

分析：
- http、https 傳輸協定
https 加密比較嚴謹的協定，尤其網站有表單輸入，不希望資料洩漏。
如果在網站上需要輸入資料網頁卻是 http 就比較不安全。
- domain 網址
1. 專屬有購買的網址 www.google.com，本地端虛擬網址 127.0.0.1 或 localhost。
2. www 子(次)網域 sub domain，可以掛在主網域下，依據不同服務設置(ex: mail.google.com、cloud.google.com。可以透過一個主網域生成很多網站，因此做很多網站不用買很多網域)
3. google.com 主網域 domain，通常由域名供應商提供
- 路徑、路由 /path
search、user.....。(使用者在網站上搜尋一個東西後，1.網只會變，2.變成一個物件格式傳給後端伺服器溝通，3.網頁顯示搜尋的結果)
- 參數 parameter
路徑後面「?」連接參數、「q=」、2個參數以上用「&」連接

多分析網站，思考如何設計路徑、參數

#### 動態路由 
app.js中
```
app.get('/user/:name/:txt', function(req, res){
  const myName = req.params;
  const myTxt = req.params;
  console.log(myName, myTxt)
  res.send('123');
})
```
