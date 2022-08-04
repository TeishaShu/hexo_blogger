---
title: React-Redux
tags: 
- Redux
- React
categories: React
---
Redux 資料集中管理，跟 React 沒有關係也可以使用在其他前端框架，但是比較多人搭配 React 使用，因此後來 facebook 出版了 React-Redux。

安裝插件 react-redux

### 架構介紹
<img src="./react_redux.JPG" alt="">

#### UI 與資料容器的關係
UI 都有個資料容器並且是父子關係:connect 資料容器(父層)，UI(子層)。
- UI：展示資料在介面呈現、事件監聽、根據用戶行為傳送行為，不能直接使用 redux，讓資料容器幫忙觸發 redux。
- connect 資料容器：負責跟 redux 溝通，可以用 redux 中所有的 api。
- 一個組件裡面有 UI 和資料容器的部分，透過 props 溝通。
props 中有 redux 保存的 state 狀態、操作狀態的方法

#### 組件與 Redux 關係
資料的部分在跟 redux 溝通，傳送過去 store.dispatch(action)，接到資料 store.getState()


### Connect
- connect是個函式，返回的也是一個函式所以才有兩個括號。
第一個括號中放2個函式，第二個括號放 UI 組件。
- 第一個括號返回2個函式。(下面範例)
> 第一個 mapStateToProps 函式:
  1. 返回要傳入 UI 的 state 狀態，因此返回一個具有key、value值的物件。
  2. 返回的值是 react-redux 給的，已經把狀態帶入


> 第二個 mapDispatchToProps 函式:返回操作狀態。因此 react-redux 會給一個 dispatch 使用。
- 使用 connect 自動有監測 store 值改變的能力。因此在 react-redux 中不用特別在引入 store。


```
import { connect } from "react-redux";
import CountUI from '../../components/Count';

const mapStateToProps = (state) => {
  return {count:state}
  // return {total:20} ==> 寫法相當於 <CountUI total={20}>
}
const mapDispatchToProps = (dispatch) => {
  return {'increase': (num)=>{
    dispatch({type:'increase', data: num})
  }}
}

export default connect(mapStateToProps, mapDispatchToProps)(CountUI)
```

簡化的方式
```
export default connect(
  state => ({ count: state }),
  // mapDispatchToProps 精簡寫法
  // 因為在 action 中有詳細寫了，裡面是用函式並且有返回值，返回的是 action
  {
    increment: incrementAction,
    decrement: decrementAction,
    incrementAsync: incrementAsyncAction
  }
  // mapDispatchToProps 一般寫法
  /* dispatch => ({
    increment: num => dispatch(incrementAction(num)),
    decrement: num => dispatch(decrementAction(num)),
    incrementAsync: (num, time) => dispatch(incrementAsyncAction(num, time))
  }) */
)(Count)
```

### store
統一一起的使用
在 index.js 中引入 Provider
```
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import store from './redux/store'
import { Provider } from 'react-redux'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)

```







