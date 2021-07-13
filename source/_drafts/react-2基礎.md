---
title: React 2基礎 - 事件、useState
tags: 
- JavaScript
- React
categories:
- JavaScript
- React
---

### 建立元件 component
有時候開發在同一個頁面或不同頁面上有差不多同樣的畫面，這時為了不要重複寫一樣或差不多的程式，也為了方便維護不用改一個地方全部都要分別改，這時就用到了元件。

當我讀到這[將計數器頁面改成用 JSX 來寫](https://ithelp.ithome.com.tw/articles/10218644)網頁中的建立 React 組件時，提到組件就是建立一個函式把 JSX 的內容回傳出來，這部分非常的困惑，思考元件跟函式是什麼關係，之前學 Vue 時怎麼感覺好像不太一樣，查了這文章[Vue component 元件基本用法](https://medium.com/pierceshih/vue-js-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-day15-vue-component-%E5%85%83%E4%BB%B6%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-a414e2333e2b)後了解了!
跟 Vue 的寫法不太一樣，但是概念差不多，元件的重點在可以重複使用，所以不管是 Vue、React 都要使用函式 function + return 才可以把資料回傳，只是這2個寫法有點差異。

React 元件稱作 Function Component，就是建立一個函式把 JSX 內容回傳(JSX 是把 HTML 當成一個變數使用所以回傳的是一個變數)。
需要使用那個元件時只要把名稱當標籤使用即可。
```
// 原本 JSX
const Content = (
    <div>{{text}}</div>
);
ReactDOM.render(Content, document.getElementById('root'));

// 改成元件 component
const Content = (text) => {
  return (
    <div>{{text}}</div>
  );
};
ReactDOM.render(<Content/>, document.getElementById('root'));
```

注意!!
React 元件的名稱需要使用「大駝峰」- 開頭大寫，如果不是這樣寫會當成一般 html 顯示錯誤!
Vue 就沒有這規定，但是之前帶我的前輩也是規定我要開頭大寫比較好。
這樣統一規定的特色是看到大寫開頭的命名比較容易是元件而不是一般的函式做出區別。

Vue 元件 data 一定要是函式才能回傳，使用時會回傳一個新物件。
```
<div id="app">
 <my-component></my-component>
</div>
<script>
Vue.component("my-component", {
  template: '<div>{{text}}</div>',
  data(){  // Vue 這邊一定要是函式回傳
    return{  
      text:'Vue 元件中 data 為函式'
    }
  }
});
let vm = new Vue({
  el: "#app"
});
<script>
```

### 事件
JSX 在 HTML 標籤屬性上是使用「小駝峰」來命名，因此事件變成 onClick、onKeypress、onKeyUp、Oninput...
[官方文件-事件相關](https://zh-hant.reactjs.org/docs/events.html)
```
const Content = (
  let math = 0;
  return(
    <div onClick={() => {
      math = math + 1;
      console.log(math)
    }>{{text}}</div>
    {/* 只要 React 有更新畫面，JSX執行 */}
    {console.log('render')}
  );
);
ReactDOM.render(Content, document.getElementById('root'));
```

獨立出來
事件處理的命名通常使用 handle 開頭
```
function handleClick(math) {
  math = math + 1;
  console.log(math)
}
// 也可以寫成
// const handleClick = (math) => { math = math + 1;}

const Content = (
  let math = 0;
  return(
    <div onClick={(math) => { handleClick(math)} >{{text}}</div>
    {/* 如果寫成下面這樣.會直接執行.因此外面要在一個 function */}
    {/* <div onClick={handleClick(math)} >{{text}}</div> */}
  );
);
ReactDOM.render(Content, document.getElementById('root'));
```

但是執行後畫面不會更新，只有資料更新，render 只跑一次，之後怎麼按 onclick 都只有數字增加而已，不會跑出 render 的字，因為 React 不知道需要幫我們更新畫面。

### useState
資料有變動時就會更新畫面，React Hooks 的其中一個。
改變 data (資料) 被稱為 state (狀態)，主要就是操作 data 資料。
只要以 use 開頭的函式代表是個 Hook。
注意： use 開頭的函式不可以放在判斷式內。

3個步驟建立 useState
```
const { useState } = React; // 1. 從 React 物件中取出 useState 方法。解構方式比較多人用。
// React.useState();  也可以使用這方式取出 React 物件的方法。

const Content = (
  // let math = 0; 原本是這樣寫改成下行
  const [math, setMath] = useState(0); // 2. [想要監控的資料變數, 修改資料變數的方法] = useState(預設值)

  return(
    <div onClick={() => {
      // math = math + 1; 原本是這樣寫改成下行的方式
      setMath(math + 1);
    }>{{text}}</div>

    {/* 只要 React 有更新畫面，JSX執行 */}
    {console.log('render')}
  );
);
ReactDOM.render(Content, document.getElementById('root'));
```

透過 useState 監控一個資料(上面的 math)，透過 setMath 改變 math 數值時畫面會重新刷出來。
預設值可以放字串、數值、物件。
使用 useState 時會回傳一個陣列，第一個是陣列的第一個值，第二個是第二個值，為了方便直接使用物件的解構賦值
裡面變數的名稱都可以自己取只是第二個通常以 set 開頭。
在更換時始會更會有改變的部分，不會整個 DOM 換掉，能讓網頁效能提升。

useState 在使用 CDN 時是用 const { useState } = React; 使用這功能。
在 cli 中是使用  import React, { useState } from 'react';