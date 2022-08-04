---
title: react-三屬性-state
tags: React
categories: React
---
異步使用 callback
```
const [count, setCount] = setState(0)
const add = () => {
  setCount(count+1)
  console.log(count) // 非同步，顯示原本的值.不是更新值
}

// 使用 callback
const add = () => {
  setCount(count+1)//...................要試一下
}
```

影片範例
```
import React, { Component } from 'react'
export default class Demo extends Component {
  state = {count:0}
  add = () => {
    const {count} = this.state
    this.setState({count: count+1})
    console.log(this.state.count) //顯示原本的值

    // 使用 callback
    this.setState({count: count+1}, () => {
      console.log(this.state.count) //透過回調可以看到最新的值
    })

    // 也可以這樣寫
    this.setState((state, props)=> {
      return {count: state.count+1}
    })

    // 簡寫
    this.setState(state => ({ count: state.count+1}) )

  }
}
```

