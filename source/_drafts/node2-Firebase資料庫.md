---
title: Node(2) - Firebase 資料庫
tags: 
- Node.js
- Firebase
categories: Node.js
---
[Firebase](https://firebase.google.com/)

只要有 google 帳戶就可以登入使用，有很多功能!!
有點像資料庫!??<b style="color:red">給連結</b>
[Firestore 安裝、寫入和讀取](https://www.oxxostudio.tw/articles/201905/firebase-firestore.html)

優點：
1. 可以用 js 操控資料庫資料
2. 免費方案不錯用

### 建立專案
裡面有很多功能
Database 資料庫
Authentication 會員驗證
Analytics 分析資料
Storage 可以存各種內容

-------------------------------------------------------
### Realtime Database 建立資料庫
1. 建立資料庫
2. 有聯結的地方可以點
3. 把 Firebase 引入到專案中
確認有沒有引入成功
```
// 因為版本不同，要再增加這支.預設引入的 firebase-app.js 是 firebase 的主要核心，其他的功能都被拆分成各個子項目了
<script src="https://www.gstatic.com/firebasejs/7.15.1/firebase-database.js"></script>

// 驗證之後才寫下面程式
var database = firebase.database();
console.log(database);
```

### 操控資料庫
#### 新增 set
ref() 尋找資料庫路徑
set() 新增資料、設定新的內容：可以放字串、資料物件。
database 表示資料庫。

ref()裡面不寫會從根目錄開始找
```
firebase.database().ref().set('hi')
```

錯誤顯示：PERMISSION_DENIED: Permission denied
-> 沒有權限寫入上面程式。因為 firebase 是很安全的資料庫，看資料庫的規則怎麼寫。
auth 會員驗證過才可以使用
```
{
  "rule": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

#### 修改資料庫寫入權限
要練習資料庫改成下面這樣，平時不會這樣寫，按下發布。
重整頁面沒變，但是回資料庫的資料會顯示。
```
{
  "rule": {
    ".read": true,
    ".write": true
  }
}
```

#### firebase 全部物件格式
firebase 全部物件格式，不能陣列內容。
```
// 不能這樣寫，會變成物件形式。
firebase.database().ref().set([0,1,2]); 
```

可以在開發者工具的 console 寫來測試。也可以在資料庫上直接視覺上的操作新增、刪除

#### 修改 ref
找指定位置修改 ref 的部分，用資料夾方式的路徑思考。
```
// 預設
var data = null; 

// 設計資料庫樣子
data = {
  farm1:{
    name: "小米農場",
    fruit: "apple"
  },
  farm2:{
    name: "阿明農場",
    fruit: "banana"
  },
}

// 新增資料
firebase.database().ref().set(data);

// 修改
firebase.database().ref('farm1/name').set('天天都是農場');
```

#### 取得資料庫資料 once、on
once 讀取一次資料庫的資料 (比較多使用)
on 隨時監聽，寫法跟 once 一樣，資料庫的資料改變顯示的資料隨時變更，很適合用在聊天室，不用固定時間更新。

##### snapshot 快照
回傳後執行 function，讀取快照內容 snapshot.val() ---> node 語法，讓資料顯示出來。
(snapshot 雖然是物件但是 console.dir 跟一般物件不同的是可以使用 forEach 把內容印一個個出來，例子在下面 - 資料翻轉 reverse)
```
var my = firebase.database().ref('my');
my.once('value', function(snapshot){
  var str = snapshot.val();
  console.log(str);
});
```

注意：非同步
撈資料需要花時間。造成後面的資料會先跑。

#### 新增資料 push
寫法跟陣列需要 push 資料一樣，會有隨機編號的 key 值。
ex:電子商務的訂單都有自己的編號
```
var buys = firebase.database().ref('buys');
buys.push({content: "蘋果"});

// 實際上
var data = {
  buys:{
    "-MLzzB7K7jBQMFHDBo53": {
      content: "蘋果"
    },
    "-MLzzeTN92tkKX4O7fjd": {
      content: "牛奶"
    }
  }
}
```

#### 移除資料 remove、child
child 子路徑
下面2個寫法是相同的，第二個是先從根目錄下去找
```
var buys = firebase.database().ref('buys');
var buys = firebase.database().ref().child('buys');
```

刪除
```
var buys = firebase.database().ref('buys');
buys.child('-MLzzeTN92tkKX4O7fjd').remove();
```

### 使開發變快速
不用一直看 firebase 的資料庫，直接顯示在 index 頁面上
```
// HTML 上
<div id="content"></div>

// 最下面的程式
var ref = firebase.database().ref();
ref.on('value', function(snapshot) {
  var el = document.getElementById('content');
  el.textContent = JSON.stringify(snapshot.val(), null, 3)
})
```

也可以不要看全部的，指定位置
```
var title = firebase.database().ref('title');
title.on('value', function(snapshot) {
  var el = document.getElementById('content');
  el.textContent = JSON.stringify(snapshot.val(), null, 3)
})
```

### for...in
顯示屬性

陣列
```
var area = [
  {
    city: "台中",
    feature: "太陽餅"
  },
  {
    city: "雲林",
    feature: "土豆"
  }
];

for(var item in area) {
  console.log(area[item].city); // 台中 雲林
}
```

物件
```
var farm = {
  num1: {
    name: "小米農場",
    fruit: "apple"
  },
  num2: {
    name: "阿明農場",
    fruit: "banana"
  },
}

for(var item in farm) {
  console.log(farm[item].name); // 小米農場 阿明農場
}
```

### 抓資料方式
路徑 >> 排序 orderByChild('要比較的屬性') >> 過濾 >> 限制筆數 >> 讀取 once >> 依序撈出資料 forEach
#### 排序
##### orderByChild
排的順序：由小到大
混和時 Ex：null、boolean、數字、字串、物件
1. null 沒有資料
2. false
3. true
4. 123 數字以小到多
5. "我是字串" 以字典的順序排，英文是 a-z
6. {...}
```
const people = firebase.database().ref('people');
const data = {
  Ann: {height: 145, weight: 45},
  Bella: {weight: 50},
  Cindy: {height: 160, weight: 60},
  Daisy: {height: false, weight:30},
  Elsa: {height: {my: 123}, weight: 80},
  Faith: {height: true, weight: 20},
  Gloria: {height: "secret", weight: 60},
  Helen: {height: "I dont know", weight: 70}
}
people.set(data);
people.orderByChild('height').once('value', function(snapshot) {
  snapshot.forEach(function(item) {
    console.log(item.val());
  })
})
```

##### orderByChild 搭配 forEach
<div style="color:red;">注意使用 forEach 顯示資料的方式</div>
item.val()  --> 值
item.key    --> 屬性名稱(父層的屬性)
```
const people = firebase.database().ref('people');
const data = {
  Ann: {height:145,weight:45},
  Bella: {height:170,weight:50},
  Cindy: {height:160,weight:60}
}
people.set(data);
people.orderByChild('height').once('value', function(snapshot) {
  snapshot.forEach(function(item) {
    console.log(item.val());
    console.log(item.key);
  })
})
```

#### 過濾 startAt、endAt、equalTo
startAt(123) 多少以上
endAt(123) 多少以下
equalTo(123) 等於。(使用情境：查詢資料時)

範例 startAt、endAt
```
const people = firebase.database().ref('people');
const data = {
  Ann: {height:145,weight:45},
  Bella: {height:175,weight:50},
  Cindy: {height:160,weight:60}
}
people.set(data);
people.orderByChild('height').startAt(160).endAt(170).once('value', function(snapshot) {
  snapshot.forEach(function(item) {
    console.log(1,item.val());
    console.log(2,item.key);
  })
})
// 顯示 1 {height:160,weight:60}
// 顯示 2 "Cindy"
```

範例 equalTo
```
const people = firebase.database().ref('people');
const data = {
  Ann: {height:145,weight:45},
  Bella: {height:175,weight:50},
  Cindy: {height:160,weight:60}
}
people.set(data);
people.orderByChild('height').equalTo(175).once('value', function(snapshot) {
  snapshot.forEach(function(item) {
    console.log(1,item.val());
    console.log(2,item.key);
  })
})
```   

#### 限制筆數 limit
limitToFirst(1)   撈出第一筆資料(從前面抓)
limitToLast(1)   撈出最後一筆資料(從後面抓)
```
const people = firebase.database().ref('people');
const data = {
  Ann: {height:145,weight:45},
  Bella: {height:175,weight:50},
  Cindy: {height:160,weight:60},
  Daisy: {height: 180, weight:30},
}
people.set(data);
people.orderByChild('height').startAt(170).limitToFirst(1).once('value', function(snapshot) {
  snapshot.forEach(function(item) {
    console.log(1,item.val());
    console.log(2,item.key);
  })
})
```

#### 資料翻轉 reverse
新的資料在最上面：把資料變成陣列後翻轉。
snapshot 雖然是物件但可以用 forEach(這裡的 forEach 是屬於 firebase 的 forEach 而不是 JavaScript 的 forEach [官方文件用法](https://firebase.google.com/docs/reference/js/firebase.database.DataSnapshot?hl=zh-tw#foreach))，注意裡面 item 的用法，屬性名稱是 item.key，值是 item.val() 可以看到物件。
```
// 假如資料是 push 上去資料庫
// 1. 抓資料
const inputForm = firebase.database().ref('inputForm);
inputForm.once('value', function(snapshot) {
  // 2. 改成陣列格式把資料反轉
  const dataAry = [];
  snapshot.forEach(item => {
    dataAry.push(item);
  })
  dataAry.reverse();
  // 3. 顯示在畫面上
  let content = '';
  dataAry.forEach(item => {
    content += `<li>${item.val().content}<i class="far fa-trash-alt" style="padding-left:30px" data-id="${item.key}" onclick="del(this)"></i></li>`;
  })
  list.innerHTML = content;
})
```

----------------------------------------------------------
### 日期
#### 表現方式
注意：getTime、getMonth、getDay 的使用方式
```
var time = new Date();
console.log(time); // 所有日期資料
console.log(time.getTime()); // UNIX 時間(timestamp 時間戳記)，從 1970/1/1 的 00:00:00 開始到現在的總秒數，工程師制定格式上常用的方法。
console.log(time.getFullYear()); // 年
console.log(time.getMonth()); // 月。(0 = 1月)
console.log(time.getDay()); // 禮拜。(禮拜7 = 0、禮拜1 = 1)
console.log(time.getHours()); // 小時
console.log(time.getMinutes()); // 分鐘
console.log(time.getSeconds()); // 秒
console.log(time.getMilliseconds()); // 1000毫秒 = 1秒
```

#### 格式
「/」、「-」都可以，但是「-」瀏覽器可能不吃。
```
new Date('2020/10/10');
new Date('2020-10-10');
```

#### 時間區間設定
- input 有個 date 的屬性，點了有選日期的效果。
- setHours(24 小時, 分, 秒, 毫秒)。 (1000毫秒 = 1秒)。
注意怎麼設定一開始和最後的時間
```
// html 格式
<input type="date" id="time" value="">
<input type="button" id="send" value="送出">

// js
const time = document.getElementById('time');
const send = document.getElementById('send');

send.addEventListener('click',function(e) {
  const now = new Date(time.value);
  const starTime = now.setHours(0,0,0,0);
  const endTime = now.setHours(23,59,59,999);
  console.log(time.value, starTime, endTime)
  // 搭配資料庫的 endAt()、starAt()
})
```

[CodePen](https://codepen.io/teisha-hsu/pen/vYKoPRG)
