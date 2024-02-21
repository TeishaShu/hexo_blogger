---
title: TypeScript6-物件型別、陣列型別
tags: TypeScript
categories: JavaScript
---
### 物件型別
#### A.任意屬性
定義任意屬性是 any 彈性比較大。
```
interface Dog {
    name: string;
    age?: number; // 非必填
    [propName: string]: any;  // [任意屬性:名稱類型是 string]:任何類型
}

let ann: Dog = {
    name: 'Ann',
    color: 'white'
};
```

<!--more-->
注意: 如果定義任意屬性，所有屬性都必須是它型別的子集!
```
interface Dog {
    name: string;
    age?: number; // 非必填
    [propName: string]: string;  // 任意屬性
}

let ann: Dog = {
    name: 'Ann',
    age:3,
    color: 'white'
};
```

上例中，任意屬性定義是 string，但 age 屬性是 number 不是 string 所以報錯

#### B.唯獨屬性
只能在建立時被賦予值
```
interface Dog {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let ann: Dog = {
    id: 15453
    name: 'Ann',
    age:3,
    color: 'white'
};

ann.id = 12345; // 報錯:初始化後又被賦予值
```

### 陣列型別
1. 設定陣列裡面的型別
JS 中陣列裡面可以放任何類型，使用 TS 希望陣列裡面的類型都一樣
```
let arr: string[]; // 陣列中都是 string
arr = ["aaa", "bbb"];

let arr2: Array<number>; // 陣列泛型
arr2 = [1, 2, 3];

interface NumberArray{ //interface 的方式
    [index:number]: number;
}
let arr3: NumberArray = [2, 3, 4]
```

2. 設定陣列傳特定的類型
```
let arr4: [string, number];
arr4 = ["aaaa", 123]; //如果在當個位置寫不同型別，或是裡面不是2個值太多或太少都會顯示錯誤
```
