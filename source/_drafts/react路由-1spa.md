---
title: React 路由 1 - SPA
tags: 路由
categories: React
---
### SPA 網頁介紹
單頁網頁應用
single page application
只有一個頁面，只是局部更新，不會整頁刷新。

靠瀏覽器的路徑對應組件變化
==>path路徑(不看前面.只看後面)
url網址(從http開始到尾，所以不是這個)

### react-router
- 一個插件庫 library。
- 專門實現 SPA 網頁。
- Router 路由器，Route 路由
(路由器管理各個路由)
- 框架沒有要自己下載
[官方-比較新](https://reactrouter.com/)
[中文](https://react-router.docschina.org/)
官方現在分成2個類別:Web、Native，我們現在是用 web 開發。

### react-router-dom
1. 安裝(dom 前端特有的)
```
npm install react-router-dom
```

2. 在app.jsx中引入並使用
引入的組件要大寫開頭，因為是 component
注意：Link 中的 to 後面接要去的路徑(path)，盡量小寫，前面不要加點。
這邊路徑就有改變的效果了。
```
import React, {Component} from 'react'
import {Link} from 'react-router-dom'; //引入

export default class App extends Component{
  render() {
    return(
      <div>
        {/* 原生html中使用<a>跳轉 */}
        <a className="color-red" href="./product.html">Product</a>

        {/* react router */}
        <Link className="color-red" to="/product">Product</Link>
      </div>
    )
  }
}
```

3. 使用
- <\Router> 分2種：
使用路由時要選其中一個包起來(只能包一次.放在最外面)
-BrowserRouter
```
//在js中
const history = History.createBrowserHistory();
```

-HashRouter 錨點
下面範例使用換成這個會變成網址中間有個/#/後面接會換的hash，特色是換時不會發送給伺服器  
```
//在js中
const history = History.createHashHistory();
```

- 定義連結
把原本的<\a>換成<\Link>
- 標籤與路徑連結設定
<\Route path="..." component={大寫開頭}>

```
import React, {Component} from 'react'
import {Link, BrowserRouter, Route} from 'react-router-dom'

export default class App extends Component{
  render() {
    return(
      <div className="row">
        <BrowserRouter>
          <div className="col-6">
            {/* 編寫、定義路由連結 */}
              <Link className="color-red" to="/home">Home</Link>
              <Link className="color-red" to="/product">Product</Link>
          </div>
          <div className="col-6">
            {/* 註冊路由、展示區 */}
              <Route path="/home" component={Home}/>
              <Route path="/product" component={Product}/>
          </div>
        </BrowserRouter>
      </div>
    )
  }
}
```