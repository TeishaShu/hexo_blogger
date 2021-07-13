---
title: NPM
tags: NPM
categories: NPM
---
### 介紹
全名 Node Package Manager ，一個線上套件庫，用 JavaScript 編寫軟體套件的管理系統。主要是管理 node.js 的各種套件，透過這個下載別人很多模組。透過 npm 的指令安裝

裡面有很多東西 ex：cordova 寫 app...

電腦需要安裝 node、npm 

### package.json
初始化，建立 package.json
```
npm init
```

開始問一些問題
version: 直接用預設即可
description: 專案描述.沒有可以空白按 enter
entry point: 切入，主要執行的檔案是哪一個。(因為可能有很多檔案)
test command: 測試程式碼.沒有可以空白按 enter
git repository: 是否有 git 數據庫.如果沒有要放 git 可以省略
keywords: 希望有哪些關鍵字讓其他開發者找到這個 npm 或相關資料
author: 要打一下
license: 這個專案有要開源嗎? 可以直接按 enter 先忽略掉

設定完專案中會出現 package.json

### 安裝套建
在 [npm 官網](https://www.npmjs.com/) 中搜尋要的套件，查看使用者多不多判斷是不是可以用的、較成熟的套件。
再根據裡面文件的說明方式安裝。
1. dependencies
安裝成功後 package.json 裡面會多個 dependencies 裡面放安裝的套件
和版本號，透過這個可以知道使用多少模組。
```
"dependencies": {
    "axios": "^0.19.2", // 我是安裝 axios 套件
}
```

2. node_modules
專案中多個 node_modules 資料夾，針對很多附加的套件。
通常檔案很大，因此版本控制時忽略
其他使用者只要打下面指令(install 可以簡寫成i)
```
npm install
// 或下面簡寫
npm i
```
他會抓 package.json 的 dependencies 來安裝。

3. 確認有沒有安裝成功

A. 在主要執行的 js 檔案中引用套件
```
var axios = require('axiox');
console.log(axios);
```

B. 執行 node
成功會顯示安裝的各種語法
(假設主要執行的 js 檔案叫 app.js)
每次執行都要打
```
node app.js
```

如果想要儲存就自動執行，使用套件 nodemon
```
npm install nodemon -g  // 安裝
nodemon app.js  // 啟動.之後儲存就直接執行
```

### 版本號
如果載別人 npm 掛掉，
可能 node 版本要更新，也可能他太舊了跟其他有衝突。

```
"dependencies": {
    "axios": "^0.19.2", 
}
```
#### 版本號意義
- 0 :主要版本號 - 重大改版.可能核心都會換
- 19:次要版本號 - 改一些小功能
- 2: bug 修正

#### 前面的符號
- 「^」安裝：0.x.x 次要版本跟 bug 修正，都會自動更新，只有主要版本不會換
- 「~」安裝：0.19.x 只改變 bug 修正，因為次要版本修正可能有些模組的 api 方式會變。
- 前面「沒有符號」：永遠指定這版本
- 「latest」：這版本永遠是最新的。(很少人這樣用)

### 語法
- --save node
應用程式上會用到的 npm，在終端機上打
```
npm install axios --save
```

在 package.json 的 dependencies 會顯示，現在不打「--save」很多都還是會加，但有些會漏掉還是寫一下保險。
```
"dependencies": {
    "axios": "^0.19.2", 
}
```

- --save-dev 
只有測試、開發時使用的輔助工具，不會影響上線的狀況
常使用的 jshint(檢視程式有沒有錯誤)、mocha(測試用的npm)
在終端機上打
```
npm install axios --save-dev
```

在 package.json 中顯示
```
"devDependencies": {
    "axios": "^0.19.2", 
}
```

- -g 全域
在很底層的資料夾放 node_modules
(路徑 C:\Users\名稱\AppData\Roaming\npm\node_modules)
好處是各種專案就不用在獨自安裝，只要裝一次都可以用。
專案中使用模組主要還是使用 --save

package.json 是專案本地端資料夾
在終端機上打
```
npm install nodemon -g
```

### 指令整理
```
npm -v // 看版本
npm init // 新增 package.json
npm install [模組名稱] [安裝位置] // 安裝模組，安裝位置：-g、--save、--save-dev
npm list //顯示安裝 npm 列表
npm uninstall [模組名稱] //刪除模組
```