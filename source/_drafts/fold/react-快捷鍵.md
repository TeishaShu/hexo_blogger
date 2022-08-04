---
title: React 快捷鍵、代碼片段
tags: React
categories: React
---
快速生成一些固定使用的程式，不是快捷鍵實際上的名稱是代碼片段(代碼模板)。

### 使用前提
在 vscode 中插件都安裝好後可以使用這些
- ES7 React/Redux/GraphQL/React-Native snippets
寫 ES6、ES7、React、Redux、其他相關 React 技術都有提示。
這插件中詳細資料往下滑，在 Basic Methods 還有顯示很多快速使用的方式。


### rcc (react class component) 類組件
使用 class 組件，快速鍵是 rcc
```
import React, { Component } from 'react'

export default class index extends Component {
  render() {
    return (
      <div>
        
      </div>
    )
  }
}
```

### rfc (react function component) 函式組件
使用 function 組件
```
import React from 'react'

export default function index() {
  return (
    <div>
      
    </div>
  )
}
```