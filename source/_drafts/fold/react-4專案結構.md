---
title: React 4 使用 cli 建立專案
tags: 
- JavaScript
- React
categories:
- JavaScript
- React
---
### 安裝 react cli
電腦安裝好 node.js 後.輸入指令碼建立新專案
```
npx create-react-app 專案名稱
```

跑完之後進去檔案裡面.輸入下面指令啟動專案
```
npm start
```
### 專案結構
- public 資料夾主要放靜態檔，不需要再經任任何前處理(preprocess)或編譯(compile)
- public/index.html 主要放 ```<div id="root"></div>``` 讓 React 知道把內容轉譯到哪個 div 上
- src 資料夾最常用的放很多元件，裡面的 js 會被 Webpack 編譯打包成一個或多個 js 檔讓 index.html 使用。
進入點....
圖片也是放在 src 裡面
src 中主要先開始的檔案是 index.js
```
// 1.載入 React 相關套件
import React from 'react';
import ReactDOM from 'react-dom';

// 2.載入 css、元件
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

// 3.將元件跟 HTML 互相綁定
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

### css reset
先把各個瀏覽器的設定變成一致，使用 normalize.css
1. 安裝 normalize.css
```
npm install --save normalize.css
```

2. 引入(在 ./src/index.js )
```
// 1.載入 React 相關套件
import React from 'react';
import ReactDOM from 'react-dom';

// 2.載入 css、元件
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import 'normalize.css';  // 引入這行
```

3. 調整全域環境 index.css 下的 css 樣式
在檔案的最上加加入下面 css 語法
```
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#root {
  height: 100%;
  width: 100%;
}
```

### 使用套件把 css 名稱元件化
這部分專案很大時可以使用.避免不同檔案的 css 名稱相衝，專案太小不用使用這塊就可以跳過去看下一個(HTML 放到 JSX 中)。

1. 安裝 emotion
```
npm install @emotion/react
```

一開始是用這個安裝，但是會跑錯，好像是因為版本問題後來換上面方式安裝。
```
npm install --save @emotion/core @emotion/styled
```

2. 引入 (在 ./src/App.js ) 
跟上面 normalize 引入位置不同
```
import './App.css';
import styled from '@emotion/styled'; // 引入

function App() {...}

export default App;
```

3. 使用 styled components
把 css 用元件的方式呈現。(style components 也是一個套件名稱，emotion 是以這個概念延伸做的，2者用法很接近。)
元件要用大駝峰
```
import './App.css';
import styled from '@emotion/styled';

// css 元件化，div 是放標籤的部分，後面用反引號
const TextColor = styled.div`
  border: 1px solid #ededed;
  box-shadow: 0 0 10px #ccc;
  margin: 30px;
`;
const H1Style = styled.h1`
  color: #ccc;
`;

function App() {
  return (
    // 可以使用變成標籤
    <TextColor> 
      <H1Style>我是標題</H1Style>
    </TextColor>
  )
}

export default App;
```

編譯後 HTML 上會變成下面
標籤是上面自己寫的 div，class 的名稱是編譯後產生讀一性
```
<div class="css-gx3v3x">
  <h1 class="css-15esflk">我是標題</h1>
</div>
```

### HTML 放到 JSX 中
#### A.放入 css
一個元件對應一個 css 檔案，以這個新建的專案 App.js 對應的是 App.css，把使用的 css 放入，在元件中引入即可。(範例在下面程式碼)

#### B.使用元件
元件簡單說是一個 function，最後要被引用所以寫好後需要匯出。(注意元件的名稱要大寫開頭)
```
import './App.css';  // 引入這個元件的 css
import React from 'react'; // 引入這個才可以使用 JSX

// 下面是一個名為 App 的元件
function App() {
  return (
    {/*放 HTML*/}
  );
}

export default App; // 因為是一個 component 所以完成需要匯出
```

##### 引入規則
第三方往上靠，自己寫的往下，樣式放最後。
```
import React, {Component} from 'react'; //第三方
import Header from './components/Header'; //自己寫的組件
import './style.css'; //樣式

export default class Index extends Component {
  render() {
    return(
      <div>
        <Header/>
        <p>您好!!!</p>
      </div>
    )
  }
}
```

#### C.使用 JSX
1. 把原本的 HTML 中 class、style 做修改。
2. 需要加的事件 & 監控的資料(使用 useState 這個 hook)。



### Todo
1. 在 src 資料夾中建立 component 資料夾並放各種組件。
2. 在 src/App.js 中把需要的組件引入進去。
3. 把專案運行起來看有沒有成功顯示。


