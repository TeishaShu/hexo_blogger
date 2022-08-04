---
title: redux、redux-saga
tags: JavaScript
categories: JavaScript
---
### 1. Redux
由來：開發時，畫面(修改component)、資料(修改redux)分離達到好管理比較快找到問題。
目的：讓組件資料(state)統一管理。

>三大元件：
action: 一個物件.寫著事件名稱和資訊
```
{
  type:'ADD_TODO',
  payload: '運動'
}
```

reducer:根據 action 的資料.更新 state 的函式。
```
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}
```

store: Redux 運作的核心，負責儲存整個 state tree，每個專案只會有一個 store。
透過 Redux.createStore(counter) 創建。
store.subscribe(render) 只要 store 更新重新 render。


https://codesandbox.io/s/github/reduxjs/redux/tree/master/examples/counter-vanilla?from-embed=&file=/index.html
https://note.pcwu.net/2017/03/04/redux-intro/

---------------------------------------------------------------------------
### 2. react-redux
(react 和 redux 一起用)
react => component 開發，每個 component 有自己的 state，元件之間透過 props 傳資料。
redux => ui、state 分開管理，透過 dispatch 傳資料到 redux 中，用 store 統一管理。
component 使用 connect 連結資料。(只用 redux 畫畫面 store.subscribe() 會有效能問題)

----------------------------------------------------------------------------
### 3. redux-saga
目的：強化非同步的處理，讓程式在處理非同步時，流程看起來更清晰。
- 傳送 action 進入 store 前(middleware 的位置)先拿到資料解決完問題，才會繼續執行。

1. redux-saga 中的 effects 有很多指示(ex: put、all、takeEvery...)
使用 yield+動作 來執行。==> 看到 yield 會先停止處理好後面的事情。

put 打 api (可以當 dispatch 使用)
call 執行 function 有點像 callback
select 取 state 的資料
all 很多 api 要打時
take 監控1個 action
takeEvery 監控多個 action 事件(下面例子_每次觸發type，後面function都會執行)
delay 延遲
```
import { put, call, select, all, takeEvery, delay } from 'redux-saga/effects'

function* fetchSome(){
yield put({ type: 'INCREMENT', payload });
const callApi = yield call(fetchApi, payload);
const selectState = yield select(state => state.name);
yield all([
    user(),
    data(),
  ]);
yield takeEvery(reducer的type, function); 
yield delay(1000);
}

function fetchApi(reddit) {
  return fetch(`https://www.xxxx`)
    .then(response => response.json())
    .then(json => {
      return (json);
    });
}
```

2. 「*」 是 JavaScript 中的一種 Function ==> Generator Function ，能配能 yield 在執行過程中停止。透過 .next() 讓 Function 依序執行到下一個 yield。
```
// 一般
function printNumber() {
  for (let i = 0; i <= 10; i += 1) {
    console.log(i);
  }
}
printNumber() // 0 1 2 3 ... 10

// *
function* printNumber() {  //這邊加 *
  for (let i = 0; i <= 10; i += 1) {
    yield console.log(i);  //這邊加 yield
  }
}
const tem = printNumber();
tem.next()
```
