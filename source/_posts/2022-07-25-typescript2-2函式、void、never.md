---
title: TypeScript2- 函式、void、never
tags: TypeScript
categories: JavaScript
---
void、never 主要使用在函式的返回值。
<!--more-->

### 函式
- TypeScript 中「=>」的左邊式輸入的型別需要用「()」括起來，右邊是返回值的型別
- 基本寫法
```
// a,b 變數加冒號是型態定義
function hello (a: string, b: boolean){
  return 123
}

// ()後寫的是回傳值的型態定義
function hello2 (a: string, b: boolean): number{
  return 123
}

// undefined (「?」非必填的變數，順序放在最後)
function hello3 (a: string, b: boolean, c?:number): number{

  //多寫個防呆.減少 ui、js 的 bug，是使用ts的好處
  if(c === undefined) return -1 

  return 123
}
```

- ES6 中「=>」是箭頭函式
```
// 函式
let myFun = function (x: number, y: number): number {
    return x + y;
};

// 另一種寫法: myFun 後先定義型別
let myFun: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

------------------------------------------------------
### void
表示: 空的，沒有返回值
```
function fn():void{
  return ; // 可以這樣寫
  return undefined; // 比較不會這樣寫，跟上一行一樣。
  return null; // 比較不會這樣寫，不會報錯。
}
```

### never
- 表示: 沒有值，永遠不會回傳結果。
- 出錯使用，連 undefined 也沒有
- 比較少使用
```
function fn():never{
  throw new Error("錯了!")
}
```