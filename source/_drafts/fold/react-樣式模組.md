---
title: React 樣式模組化
tags: React
categories: React
---
### 樣式模組化
*資料夾 src/components/Hello 有2個資料夾
一個 index.jsx，一個 index.module.css。(css 檔案名稱多寫 module 會模組化)
在 index.jsx 中引入 css檔案
```
import React,{Component} from 'react';
import hello from './index.module.css'; // 引入

export default class Hello extends  Component{
  render(){
    return <p className={hello.title}>您好!!!</p>   // 這邊使用 css 中寫的 title 樣式
  }
}
```

這不常用因為不常衝突，會名稱衝突可以這樣寫。