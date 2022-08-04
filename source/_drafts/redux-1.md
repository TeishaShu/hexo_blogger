---
title: redux
tags: 
- redux
- React
categories: React
---
安裝 google 插件(Redux DevTools)


redux 專門用於<b>狀態管理</b>的 js 庫(不是react 插件庫)。(就像是java、javascript是不同的只是名字像)。

可以用在3大框架裡面，但主要是跟react配合(vue中是 vuex)。


### 原理
1. react components ==(做啥)==> 
2. action creators (創建行為)
透過 dispatch動作交給 store

(概念)
下面 action 是個物件，包含 type(方法)、data(資料)
- type: 方法。字串形式、必要的屬性
- data: 資料。可選的屬性
```
dispatch(action)
```

(action分2種.看 action 是函式還是物件來分辨)
A.同步 ---> obj{}
之後交給 reducer 處理
```
export const createIncrementAction = data => ({type:INCREMENT, data});
// { data: data } 簡寫 ==>直接寫 { data }

// 錯誤寫法
// export const createIncrementAction = data => {type:INCREMENT, data};
// 後面的大括號{}會被認為是函式的括弧
```

B.異步 ---> 返回 function
因為只有函式裡面才能放異步，需要安裝 redux-thunk  [影片102] 
異步裡面通常有同步的 action
```
export const createIncrementAction = (data,time) => {
  return () => {
    setTimeout(()=> {

    },time)
  }
};
```

3. Store (核心位置，負責儲存.指揮中心的概念，c位的人)
把前面 action 的動作對象交給 store
"只有一個"，其他不管是 components、action creators、reducers 都可以很多。

4. reducers 處理、加工的人
- store 把(previousState_之前的狀態、action)交給 Reducers 處理，處理完把新的 newState 交給 store。
在初始化時 previousState 是 undefined

5. getState() 獲取狀態
store把新的狀態透過 getState() 這方法返回給 component

### 主要管理狀態，不管理更新頁面
搭配生命週期、屬性
1. subscribe (訂閱)。只要 redux的任何狀態改變就調用。
2. 生命週期的this是組件的實例對象。
```
componentDidMount() {
  store.subscript(() => {
    this.setState({}) // 更新組件狀態(什麼也不更新)，會跑render
  })
}
```

----------
dispatch
getState
subscript

核心 store，讀取 getState()，更新dispatch
---------------------
redux 是另一個團隊，fb發現大家很喜歡在react中使用，增加一個 react-redux (fb後來用的)


[影片103-概念]

