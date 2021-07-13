---
title: 網頁動畫、特效(2) - Gsap3 + Vue.js
categories: Gsap
tags: 
  - Gsap
  - Vue
  - 網頁特效
---
### 介紹
[GSAP3：專門處理動畫與特效的 JS 套件](https://hackmd.io/@chupai/SJStDfFV8#GSAP3)

### 安裝
[官方各種安裝方式](https://greensock.com/docs/v3/Installation?checked=core)
<!--more-->
1. npm 安裝
```
npm install gsap
```

2. 引入專案中
上面官方網站 npm 安裝的部分 
有些插件可以挑選.這次需要 ScrollTrigger (頁面滑到才動)
另外目前設定只有專案的首頁需要用到.所以在那 component 頁面打下面的指令引入 3行。
```
<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

export default {...}
</script>
```

### 使用方式
gsap 是使用 id 或 class 操作動畫。

#### 公式
```
gsap.method('selector', {});

// 使用例子 1
gsap.to(".a", {color: '#ccc', duration: 2});

// 使用例子 2
gasp.from (".a", {
  duration:3, x:"-50vw", rotation:-300, ease:"linear",
  scrollTrigger:{
    trigger:".a",
    markers:true
  }
})
```

#### 測試專案 gsap 是否安裝成功
(成功的話 #h1 出現在畫面中會右移)
```
<template>
  <div>
    <h1 id="h1">我是標題</h1>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
export default {
  mounted() {
    gsap.to("#h1", {x: 100, duration: 1});
  }
}
</script>
```

### ScrollTrigger 滾動觸發
[Introducing ScrollTrigger for GSAP](https://www.youtube.com/watch?v=X7IBa7vZjmo)

注意: scrollTrigger (要小寫s開頭).不然會顯示找不到這插件 !
```
gsap.to("#h1", { //要觸發的元素
  scrollTrigger:{ //頁面滑動觸發設定
    trigger: "#product1",  //要觸發的元素
    start: "top center", //第一個值:元素的開始位置，第二個值:畫面的位置
    end: "bottom 100px" // 同 start 用法
    marker: true, //顯示提示字.會顯示設定、物件的開始結束
    toggleActions: "restart none none none"  //切換動作
  },
  x: 400, //外部這是要改變的效果
  duration:2
});
```

#### start 可放的值
top、center、bottom、pixels、percentages(relative to top)

#### toggleActions 可以放4個值.依序跑

| 值        | 說明   |
|----------|------|
| play     | 只跑一次 |
| pause    | 暫停   |
| resume   | 繼續   |
| reverse  | 逆轉   |
| restart  | 重複跑  |
| reset    | 重置   |
| complete | 完成   |
| none     | 無    |
