---
title: Source maps 筆記
tags: source maps
---
直播的筆記與其他的整理
[前端工程師不可不知的 Source Maps 應用技巧](https://www.facebook.com/will.fans/videos/1834092806619855)

### 什麼是 Source maps 
(原始碼地圖、來源對應)
產生 *.map 的檔案<!--more-->
會紀錄原始碼關鍵字和座標(第幾行的位置)。
css、js都支援 Source maps
主要給瀏覽器用 

(用途)
網站上使用的 min 壓縮檔
透過 map 找到原始檔案的位置來修改維護。

### 瀏覽器對壓縮最佳化的 js 解壓縮
1. 自動格式化原始碼( google 擴充套建 PrettyPrint )
網頁左上角應用程式 -> 現在應用程式商片 -> 進去搜尋
<img src="https://lh3.googleusercontent.com/xGYFnx7QNmqWf63dEKrBHPTdhKK49dLYKmo376aiN4-fM0lR_0lxiXtJrFZOVjFzhuWN8HuasA=w440-h280-e365" width="200px">

2. f12 的 Sources 點要使用的 min.js 
再點『{}』就可以解析 (在程式碼那塊的左下角)

如果壓縮檔的名稱有壓過會變成很簡易的代號.不容易看懂.這時就需要使用 Source maps 來產生 *.map 檔跟原始檔連結

### Source maps 方式 (偵錯時使用)
先下載要使用的工具(直播中使用 uglify-js )
再用下面的方式
成功在網頁上.會先讀入壓縮檔自動轉換成原始檔顯示

#### (方法一) 壓縮檔與 map 連結
在壓縮檔 *.min.js 的最後一行打
(同樣位置)
```
//# sourceMappingURL=*.min.js.map
```
(不同位置)
```
//# sourceMappingURL=/path/to/*.min.js.map
```
缺點是要手動在 min.js 最後加入這個

#### (方法二) 在 http header 加入程式碼
```
X-SourceMap: /path/to/*.js.map
```

### 更改完原始的 js 後
要再重新產生新的壓縮 js 和 Source maps 才會生效

### 檔案壓縮是為了網頁的效能
JS 最佳化:
1. 合併
  - 多個 js 檔合併一個(越多 js 檔網頁跑越慢)
  - 減少 HTTP 要求次數來提升瀏覽效率
2. 壓縮
  - js 中多餘的空白字刪除
  - 過長的區域變數變短
  (改掉原本的名稱.所以需要用 Source maps. 只用 PrettyPrint 可能還會看不懂。 ex: event 變 n )
  - 縮小檔案加快檔案的下載速度
3. 常用工具: uglify-js、webpack module bundler、TypeScript、Babel
cli 裡面也有

目標:
- 縮小檔案大小，降低網路流量
- 讓變數及函式名稱變成無意義文字，讓別人不容易反推程式邏輯
( js 是送到用戶端，網站上線時需要加工處理。)

### 其他
```debugger``` js 會停下來.接下來一步步的執行
開發時不要用壓縮.上線在用.但通常上線才發現 bug!
才會需要用 Source maps