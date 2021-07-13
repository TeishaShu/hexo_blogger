---
title: React 3基礎 - 陳述句(判斷式...)
tags: 
- JavaScript
- React
categories:
- JavaScript
- React
---

### JSX 中的判斷式
讓畫面元素消失的 3 種方法 js、class、style
#### js 方式
JSX 中 {} 內只能放「expressions 表達式」-有個值回應，statement 陳述句是呼叫不會有回應的值。
因此不能在 JSX 中使用 if...else..，需要換成使用[邏輯運算子 ||、&&](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Obsolete_Pages/Obsolete_Pages/Obsolete_Pages/%E9%81%8B%E7%AE%97%E5%AD%90/%E9%82%8F%E8%BC%AF%E9%81%8B%E7%AE%97%E5%AD%90)、[三元判斷式 ?:](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

邏輯運算子 ||、&& 判斷真假值
把 A、B 做比較，先判斷 A 值，不是 A、B 兩個值的比較
|| 前面是 false 就取後面的值
&& 前面是 true 就取後面的值

用在 JSX 中，因為要寫表達式無法使用 if
```
const { useState } = React;
const Content = () => {
  const [math, setMath] = useState(5);
  return (
    math > 0 && (<div>{{math}}</div>); // 大於0時顯示後面的數字資料，後面因為是一長串當變數所以括號起來
  );
}
ReactDOM.render(<Content />, document.getElementById("root"))
```

#### style 方式
使用 display: none; 或 visibility: hidden; 都是消失在畫面上。
display: none; 整個移除，如果位置很重要會影響其他的要用另一個。
visibility: hidden; 隱藏位置空間還在，開 f12 察看也還看的到。
```
const { useState } = React;
const Content = () => {
  const [math, setMath] = useState(5);
  return (
    <div style={{
      visibility: math <= 0 && 'hidden'
    }}>{{math}}</div>
  );
}
ReactDOM.render(<Content />, document.getElementById("root"))
```


#### 動態 class
先有個 class 的樣式
```
.v-hide{
  visibility: hidden;
}
```


```  
const { useState } = React;
const Content = () => {
  const [math, setMath] = useState(5);
  return (
    <div className={`color-red ${math <= 0 && 'v-hide' }`}>{{math}}</div> // 使用樣板字面值，裡面的變數前面要加$
  );
}
ReactDOM.render(<Content />, document.getElementById("root"))
```