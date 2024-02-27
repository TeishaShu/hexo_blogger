---
title: Redux(5) 比較 useContext、useReducer 
tags: 
- Redux
- React
categories: React
---
一開始 React 沒有相關資料狀態管理相關功能可以用，所以大家很常用 Redux 第三方套件來處理資料的傳遞，後來 React Hook 有了 useContext、useReducer 類似 Redux 的功能，就漸漸比較比較少人使用 Redux，並且使用 Redux 一定要4個步驟(1. 設定 action 有哪些動作和資料、2. 頁面觸發事件使用 dispatch 選定要處理的 action、3. reducer 根據 action 的資料更新 state 的函式、4. store 改變畫面更新 )，慢慢覺得比較麻煩減少使用。

但是不管選哪一個，都會增加日後維護的成本，因為 Store 中放很多資料牽動很多頁面，未來要改動相關的頁面要一個個確認。


- Context 本身也可以修改值
  下面是大致概念
```
store = { abc: 'hello' }

<AbcContext>
  <Component1 />
</AbcContext>

// 10 components, 3 ~ 30 reducers
<Component1>
  const { globalValue, setGlobalValue } = useAbcContext();
  state = ...
  value1 = reducer(... store.abc ...)
  // store.abc = ...
  const value1 = state1 + state2

<p>{ value1 }</p>
```

- 什麼情境比較適合?
  使用者登入，因為登入一次所有頁面需要知道。
  接續上面的程式概念
```
<Component2>
  state = ...
  <p>{ store.abc }</p>


<Page>
  // API login
  {user && (
    <AuthContext>
       <Page1 route="..." />
       <Page2 route="..." />
    </AuthContext>
  )}
</Page>

<Page1>
  const user = useAuthContext()
</Page1>
```