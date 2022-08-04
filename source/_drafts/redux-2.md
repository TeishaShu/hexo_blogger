---
title: redux 2
tags: 
- redux
- React
categories: React
---

[影片104]
- 連接ui、redux，透過connect。
connect 是容器連結 redux 資料。
```
import  CountUi from './components/CountUi'; //ui
import {connect} from 'react-redux'

export default connect()(CountUi)
```


```
import  CountUi from './components/CountUi'; // ui
import {increment, decrement} from '../redux/actions/count'; //引入 actions
import {connect} from 'react-redux'


export default connect(
  state => ({  // 映射狀態
    count: state.count,
    person:state.person
  }),
  { increment, decrement} // 操作狀態的方法
)(CountUi)  // ui
```
