---
title: Redux 相關(2) - React-Redux
tags: 
- Redux
- React
categories: React
---
Redux 資料集中管理，跟 React 沒有關係也其他前端框架也可使用，
但比較多人搭配 React ，後來 FB 出版了 React-Redux。
<!-- more -->
先安裝插件 react-redux

### A. 架構介紹
#### 說明：
這邊有張圖引用不上來，請自己點選 [react-redux 模型图](https://blog.51cto.com/u_15305087/3111942) (搭配連結比較好懂)
  Component 連結 Redux 使用 Connect 方式。
  一個 Component 裡面有 Connect (跟 Redux 溝通)，裡面再有 UI (處理介面、事件...)。

#### Component 內部：Connect、UI 關係
- Connect、UI 父子關係：透過 <span style="color:red">props 溝通</span>。
   - Connect 資料容器 (父層)：負責跟 Redux 溝通，可以用 Redux 中所有的 API。
   - UI (子層)：展示資料在介面呈現、事件監聽、根據用戶行為傳送行為，不能直接使用 redux，讓資料容器幫忙觸發 redux。
- props 中有 redux 的 state、操作狀態的方法。
  
#### Component 外部：與 Redux 關係
上面 Component 內部是用 props 傳遞資料溝通，而外部 Component 跟 Redux 資料的溝通方式
- 傳送過去：store.dispatch(action)
- 接到資料：store.getState()

-------------------------------------------------------------------------
### B. Connect 介紹
- Connect 結構
  - Connect 是 Function，返回的也是 Function ，所以有兩個括號。
  第一個()放2個函式，第二個()放 UI 組件。
  ```
  import  CountUi from './components/CountUi'; //ui
  import {connect} from 'react-redux'

  export default connect()(CountUi)
  ```

  - 第一個()返回2個Function。
    1. 返回要傳入 UI 的 state 狀態，並具有 key、value 值的物件。
    2. 返回的值是 react-redux 給的，已經把狀態帶入
   
- 自動監測 store：state 改變 render 。(在 react-redux 中不用特別在引入 store)

```
import  CountUi from './components/CountUi'; // 引入 ui
import {increment, decrement} from '../redux/actions/count'; // 引入 actions
import {connect} from 'react-redux'


export default connect(
  state => ({  // 映射狀態
    count: state.count,
    person:state.person
  }),
  { increment, decrement} // 操作狀態的方法
)(CountUi)  // ui
```

---------------------------------------------------------------------
### 補充：Connect 結構的演變過程
Connect 後面2個括號，第一個()放2個函式，第二個()放 UI 組件。
- 第一個 mapStateToProps 函式:
  1. 返回要傳入 UI 的 state 狀態，有 key、value 的物件。
  2. 返回的值是 react-redux 給的，已經把狀態帶入

- 第二個 mapDispatchToProps 函式:
  返回操作狀態，使用 dispatch。

#### 原本
```
import { connect } from "react-redux";
import CountUI from '../../components/Count';

const mapStateToProps = (state) => {
  return {count: state}
  // return {total: 20} ==> 寫法相當於 <CountUI total={20}>
}
const mapDispatchToProps = (dispatch) => {
  return {'increase': (num)=>{
    dispatch({type:'increase', data: num})
  }}
}

export default connect(mapStateToProps, mapDispatchToProps)(CountUI)
```

#### 簡化
```
export default connect(
  state => ({ count: state }),
  {
    increment: incrementAction,
    decrement: decrementAction,
    incrementAsync: incrementAsyncAction
  }
)(Count)
```

(說明)
- mapDispatchToProps 精簡寫法
  因為在 action 中有詳細寫了，裡面是用函式並且有返回值，返回的是 action
- mapDispatchToProps 一般寫法
  (在對應回上面程式，顯得很精簡)
  ```
  dispatch => ({
    increment: num => dispatch(incrementAction(num)),
    decrement: num => dispatch(decrementAction(num)),
    incrementAsync: (num, time) => dispatch(incrementAsyncAction(num, time))
  })
  ```

-----------------------------------------------------------------
### C. Store
一個專案只有一個 Store，放在最外層一起使用。
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