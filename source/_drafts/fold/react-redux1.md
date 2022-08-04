---
title: Redux
tags: Redux
categories: React
---
### 介紹
- 什麼是 redux?
跨組件需要用的資料交給 redux 統一管理==>集中式狀態管理
Action、Dispatch、Action、Store、View
<img src='https://note.pcwu.net/assets/images/2017-03-04-redux-intro-8c335.png' alt="">
資料流(圖from: https://www.slideshare.net/nikgraf/react-redux-introduction)

- 什麼狀態下須使用?
A. 共享：需要跨組件拿到狀態 state
B. 通信：一個組件需要改另一個組件的資料(不一定是父子關係)
C. "能不用就不用"，比較後.不用比較吃力才用。

- 現實情境模擬：
[角色]
Components 一家公司的很多客戶
Action Creators 負責接待客戶的業務
Store 公司的老闆(只有一位負責人)
Reducers 很多位員工專門處理各項事務

[情境]
客戶(Components)跟業務說很多自己的需求。
業務成功接到業績後，整理成一張單子標示需要執行的任務標題和相關需要用到的資料(action = {type: "things type 標題", data: things data 資料})。整理好後把這些案子交給老闆(Store)。
老闆馬上分配給專門處理不同任務的員工(Reducers)。
員工處理好後把案件交給老闆 (return new State)。
客戶跟老闆拿貨品(getState())。


### Action Creators 創建行為
#### Action
- 負責「改變」state 資料狀態，也可以放非同步(獲取 API 資料)
- action 是一個物件，包含了 type、data。
type 類型：要做什麼行為、動作(api 在程式內的位置)。<b>只能是字串</b>
data 數據：行為的資料(要傳到 api 的資料)
```
const action = {
  type: 'authList/initAuthResult', 
  data: {
    text: '想顯示的文字內容'  
  }
}

dispatch(action);
```

- 異步 action 返回的是函式
要先在 store 引入 redux-thunk
```
import countReducer from './count_reducer'

// 增加 applyMiddleware 中間鍵方法
import { createStore,applyMiddleware } from 'redux'

// 引入套件
import thunk from 'redux-thunk'

// 輸出 store 時，把 applyMiddleware 當成第二個值傳入並傳入 thunk 值
export default createStore(countReducer,applyMiddleware(thunk))
```

在返回函式，不然會報錯
```
export const incrementAsyncAction = (data, time) => {
  return () => { //返回函式
    setTimeout(() => {
      store.dispatch({ type: INCREMENT, data })
    }, time)
  }
}
```

*返回物件是 reducers 執行，返回函式(非同步)是 store 自己執行


#### Dispatch 發送、派遣
- dispatch 是一個函數，把 action (動作對象)帶入往下送，是 UI 跟 Store (處理資料)的溝通橋梁。
<!-- - 每個 App 只有一個，向所有 Store 發送 action 事件 -->

### Store 
- 核心地區(C位)，類似公司的主管(指揮者、調度的人)，所有任務都會到主管手中，不會停留馬上將任務往下分派給其他人員處理
- 一個 App 只有一個 Store。把 state、action、reducer 連結在一起。

#### Reducers
- Store 的屬下，reducers 像很多的員工，有很多位分別處理不同的業務，做完交付內容給老闆完成。
- 需要拿到 Store 給的 action 資料，負責改變 state 的狀態。
- 單向的資料流：過程中 state 只能讀取，透過回傳修改值，不能直接改 state。
Store 給 (previousState 之前的狀態, action)，reducers 工作完透過回傳新的狀態 return newState 改變 state 的值。
- 初始的
  previousState 是 undefined，
  action ={ type: "@@redux/INIT.......隨機的字" }

#### getState()
幫 component 拿到資料狀態的函式。

redux 只管狀態，不管頁面有沒有 render 更新。
破解方式是使用生命週期 componentDidMount
```
componentDidMount(){
  store.subscribe(()=> {
    //只要 store 狀態一改變就會觸發
  })
}
```

### View
React 負責的各種事情發生後，負責把資料呈現在 UI 上。