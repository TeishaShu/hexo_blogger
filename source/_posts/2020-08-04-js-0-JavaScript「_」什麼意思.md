---
title: JavaScript 「_」 什麼意思?
tags: 
- JavaScript
- React
categories: JavaScript
---
練習 React 的過程中，看到一行這樣的程式
透過第一行建立新陣列，在透過下面的 map 把標籤<li>跑迴圈複製出來。過程中我發現 map 的第一個值「_」很奇怪
```
const lists = Array.from({length:3}); //[undefined, undefined, undefined]

ReactDOM.render(
  <ul>
    {lists.map((_, index) => (
      <li key="index">1</li>
    ))}
  </ul>
)

```

後來詢問一些人才知道這是代表「無意義」，拿「_」當沒用到的變數，如果用到 underscore.js (一個 JavaScript library )會打架，只是不太常用。

如果寫清楚一點可以命一個正常的變數名稱，只是不會使用到。
```
const lists = Array.from({length:3});
ReactDOM.render(
  <ul>
    {lists.map((listItem, index) => (
      <li key="index">1</li>
    ))}
  </ul>
)
```

在這邊因為不會用到這變數，所以才用「_」假裝不寫，因為在其他程式語言中有些可以像下面這樣省略不寫的，但是 js 一定要寫。
```
(,index)
```