---
title: react-router
tags: React
categories: React
---
寫 SPA 想要快速開發來寫頁面的切換就交給路由 Router 來決定路徑做什麼指定到哪裡。
[官網](https://reactrouter.com/)
[中文](https://react-guide.github.io/react-router-cn/)

有沒有#的網址
https://ithelp.ithome.com.tw/articles/10188245

#之後的那些參數都是給瀏覽器這邊看的而已。
```
import React from 'react';
import ReactDOM from 'react-dom';
import { Router, Route, Link, hashHistory } from 'react-router'

ReactDOM.render(
  (
    <Router history={hashHistory}>
      <Route path="/" component={App}>
        <Route path="about" component={About}/>
        <Route path="users/:userId" component={Users} />
      </Route>
    </Router>
  ),
  document.getElementById('root')
);
```

*用 HTML 的方式宣告哪個路徑要渲染哪個 Component。
只到哪裡回哪個組件