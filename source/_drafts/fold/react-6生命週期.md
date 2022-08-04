---
title: React 6- 生命週期
tags: 
- JavaScript
- React
categories:
- JavaScript
- React
---
   (這頁很讚- https://ithelp.ithome.com.tw/articles/10223344)
原始的方式

1. Mounting
  componentWillMount()
  componentDidMount()

2. Updating
  componentWillReceiveProps(object nextProps) 已載入元件收到新的參數時呼叫
  shouldComponentUpdate(object nextProps, object nextProps) 元件判斷是否重新渲染時呼叫，起始不會除非呼叫 forceUpdate()
  componentWillUpdate(object nextProps, object nextProps)
  componentDidUpdate(object nextProps, object nextProps)

3. Unmounting
  componentWillUnmount()


### useEffect
第二個參數是用來限定什麼參數改變時要觸發

#### 代替 componentDidMount 安装
第二參數為空值(array中是空的)
```
useEffect(()=> {
  // 想要 componentDidMount 的事情
},[])
```

#### 代替 componentDidUpdate 更新
某個參數會改變，想要偵測改變時更新畫面時使用
另外畫面一開始有偵測到想要使用的參數時也會 componentDidMount 進來。
```
useEffect(()=> {
  // 想要 componentDidUpdate、componentDidMount (重新觸發.更新、參數出現時運作)的事情
},[想要偵測的參數])
```

#### 代替 componentWillUnmount 卸载
跟安裝有點像
```
useEffect(() => {
    /* 放 componentDidMount 安裝的事情*/
    
    return (() => {
      /* 寫 componentWillUnmount  卸載的事情*/
    });
    
}, []); 
```

