---
title: TypeScript2-基本型別
tags: TypeScript
categories: JavaScript
---
### 型別推論
- TypeScript 會在沒指定型別時，自動推測出一個型別。
- 定義時沒有賦予值，不管之後有沒有賦予，都會被推斷成 any 型別，完全不被型別檢查。
```
let myLuckyNumber;
myLuckyNumber = 'one';
myLuckyNumber = 1;
```
<!--more-->

### 基本型態
可以簡寫，ts會自動推類型。
```
// let str: string = "name";   原本寫法
let str1: string;
str1 = "name";

let num: number = 123;
let boo: boolean = true;
let n: null = null;
let un: undefined = undefined;
let ttt: any = 123;
```

#### A. Null、Undefined
undefined、null 是所有型別的子型別，也可以獨立定義

獨立定義
```
let u: undefined = undefined;
let n: null = null;
```

子型別案例
```
// 不會報錯
let num: number = undefined; 

// 不會報錯
let u: undefined;
let num: number = u;
```

------------------------------------------------
#### B. 陣列
```
let arr: string[] = ['a', 'b'];
let arr2: string[][] = [['a', 'b']];

let tuple: [number, string, boolean] = [1, 'a', true];
let tuple2: [string, string][] = [['a', 'b']];
```

------------------------------------------------
#### C. Enum 枚舉
使用狀況：api 的資料會改動代表不同意思，定義起來後續維護很清楚
把所有情況列出來
```
// 假設情境：車子行駛狀態 (0未發動、1行進中、2發動引擎靜止中)
enum DriveStatus {
  NOT_STAR = 0,
  DRIVING = 1,
  STOP = 2
}

const status = DriveStatus.DRIVING
```

------------------------------------------------
#### D. Union 多個型態
一個變數有多個型態，下面例子中，變數設定只能數字或字串
```
let ttt: number | string;
ttt = 1
ttt = "ttt"
ttt = true //顯示錯誤
```
