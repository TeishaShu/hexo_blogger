---
title: redux saga
tags: 
- Redux
- React
categories: React
---


**思考與redux差異.優點

## model.js - effects

```jsx
  // import 這2個不一定要寫
import { take, put, call, fork, cancel, cancelled, delay } from 'redux-saga/effects'
import { someApi, actions } from 'somewhere'; 

effects:{
 *fetchInfo(action){...},   //原型，dispatch後資料變成action
 *fetchInfo({payload}){...},   //從action中拿出常用的payload使用
 *fetchInfo({payload, callback}, {call, put, select}){...},  
  //後面物件的，還有很多可以使用的，這些參數也可以使用上面 import 引入使用
}
```

### dva

dva 提供多个 effect 函数内部的處理函数，比较常用的是 call 和 put

* call：執行異步函数

* put：發出一个 Action，類似於 dispatch

```jsx
// call 異步執行
const response = yield call({
  type:'api_xxx',
  payload: payload
})

// reducer
yield put.resolve({
  type: 'removeData', // reducer 的
  payload: response,
});

// effect 使用自己或其他的 effect
yield put({type:'removeData', payload});

// all
const [a, b, c] = yield all([
  yield put({ type: 'reportSettingList/fetchGetIncomeTaxOverList' }),
  yield put({ type: 'fetchGetInfo', payload: { id: payload.id } }),
  (payload.tab == 'info') ? (yield put({ type: 'authorizedCountryList/fetchGetAuthorizedCountry', payload: { search: 'all' } })) : (null)
]);

// select，注意寫法要加 namespace 的名稱
const getPara = yield select((state) => (state.authorList.removeDataResult));
```
