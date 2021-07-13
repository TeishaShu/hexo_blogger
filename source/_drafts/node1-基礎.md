---
title: Node(1) - 基礎
tag: Node.js
categories: Node.js
---
### V8
用途：可以解讀、執行 js 程式碼。
Javascript 的引擎，google 瀏覽器也有使用
因此 node.js 透過 v8 開發 C++。

### Node.js 介紹
在 github 上有.可以看他的架構
有核心程式碼觀念比較了解、可以推敲他的邏輯，要查問題不會不知道怎麼找
- deps 裡面放開發的插件
使用插件是站在前人、巨人的肩膀上
沒有開發者是從頭開始寫完的。
裡面有 v8、zlib壓縮檔功能
- src 仰賴 v8 寫各種 c++ 的語言
裡面有很多東西.編譯後才可以做各種事情.核心的程式碼
- lib 相關 api 文件
ex: http.js 可以開啟伺服器。使用內建模組開啟 serve。使用 function 原理。

### 模組設計
[Node.js 官網 API文件](https://nodejs.org/dist/latest-v14.x/docs/api/)
官網左邊欄位都是各種模組可以應用。

#### 1. 執行
很多 js 檔來執行
例如有 a.js 檔案，在終端機打下面指令可以執行。
```
node a.js
```

#### 2. 引用其他模組
在 a.js 檔案引用另一個 b.js 檔案。

##### require 仔入其他模組
a.js 檔案，使用 require (1個點是同一層的資料，2個點是上一層)
```
var content = require('./b');
console.log(content)
```
##### exports 輸出資料
b.js 檔案，使用 module.exports = 要給其他模組使用的值。
沒寫只會得到一個空物件。如果要傳很多值可以給個物件
```
var number = 1;
module.exports = number;

// 若要給很多資料
module.exports = {
  title: '標題',
  content: '我是內容...'
};
```

寫法有2種
exports.屬性 -> 可以單獨寫很多個屬性
module.exports -> 一個大物件裡面包好。(與上面是不能共用的，不然上面會被蓋掉)
```
exports.a = 2; //空物件裡面加個 a 屬性。
exports.b = 3; 
exports.c = 4; 
module.exports = {
  a: 2
}
```

如果使用到 function 
另一邊要使用 content.more() 執行
```
exports.move = function() {
  return '我在移動';
};
```

#### Node 核心模組
可以看 api 文件
##### 開啟 web 伺服器
```
var http = require('http);
http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write('hi!'); // 回傳寫資料進去
  response.end(); //回傳結束
}).listen(8080);
```

http.createServer() 開啟網頁伺服器，裡面一個匿名函式帶2個參數，
request 當使用者讀到網站會接受到網站相關資料。
console 會顯示這使用者詳細的資訊：從哪個網址進來、使用什麼瀏覽器...
常使用 request.url 如果回傳 / 代表是首頁
response 接收到資料後要回傳資料。

response.writeHead() 回傳表頭，200代表回傳成功，後面的物件是格式
(Content-Type 內容格式，回傳文字內容 text/plain、html檔 text/html。)

listen(8080) 表示監聽一個 port 叫 8080，開啟網頁伺服器 127.0.0.1:8080。

寫完後在終端機執行 node 資料夾名稱.js，執行完後打開 127.0.0.1:8080 看資料有沒有進去。

###### network
重新整理可以看到 127.0.0.1 的 Headers 中詳細的資訊
General 中的狀態碼 200
Response Headers 回傳什麼資料格式，text/plain 文字，頁簽 Response 中顯示內容
Request Headers 各種資料，跟你講我是誰、用啥瀏覽器

###### port 通訊埠
解析 127.0.0.1:8080 

1. 127.0.0.1 代表
伺服器開啟的 IP 位址，也可以是 localhost
代表本地主機 - 自己的電腦(模擬伺服器.外部看不到)
2. 埠號
冒號後面加數字，一個埠號執行一個應用程式。

常用的 port
:21 FTP
:50 http
:3389 遠端操縱桌面
:8080 開發時常用的

###### 中斷點
程式碼左邊的空白點一下會出現紅色的圈圈(中斷點)，程式執行時會卡在那地方，左邊欄有偵錯+綠色撥放的按鈕，點下後會再編輯器中的上方會有個撥放系列相關的東西可以控制。

###### 路徑
[Node.js PATH API文件](https://nodejs.org/api/path.html)
1. _dirname、_filename
在 Node.js 中不是只有自己的變數，左邊的本機中會有些預設內容。
有 _dirname、_filename、exports、module、require、this、自己設定的變數。
_dirname：資料夾的路徑
_filename：檔案的路徑

2. 路徑應用
join()字串相加變成一個新路徑
假設有個在資料夾 /js/api/url.js 有的檔案。
```
var path = require('path');
// 抓目錄路徑
console.log(path.dirname('/js/api/url.js'));  // 顯示 /js/api
// 路徑合併
console.log(path.join(_direname,'/123')); // 顯示 /Users/.../project/123
// 抓檔名
console.log(path.basename('/js/api/url.js')); // 顯示 url.js
// 抓副檔名
console.log(path.extname('/js/api/url.js')); // 顯示 .js
// 分析路徑
console.log(path.parse('/js/api/url.js')); // 顯示一個物件，(root 路徑、dir 資料夾路徑位置、base 檔案名稱、ext 副檔名、name 檔案名稱)
```

### vscode 除錯
1. 類似撥放器的功能
vscode 上左邊有個蜘蛛圖形，找綠色撥放鍵可以自動偵錯
中間會顯示類似撥放器的東西。搭配中斷點(滑鼠在編輯器數字空白點出紅色中斷點)，再點一下就關掉。
撥放鍵-繼續，到下一個中斷點
逆向的箭頭-重新啟動
往下箭頭-逐步執行
往上箭頭-跳離函式
方形-全部中止

中斷點也可以寫程式 debugger

2. 移動到原本的程式
在要搜尋的程式上面按「右鍵->移至定義」
這樣就不用慢慢找

3.不想開啟分頁來看程式
在要搜尋的程式上面按「右鍵->預覽定義」
會開啟一個有程式碼的狀態，看完用 esc、按關閉鍵