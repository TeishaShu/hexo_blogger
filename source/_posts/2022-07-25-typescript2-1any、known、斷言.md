---
title: TypeScript2- any、unknown、斷言
tags: TypeScript
categories: JavaScript
---
### any
1. 代表: 任何類型，放什麼類型都不會出錯 (ex: string、number....)
2. 注意! 使用等於關閉 TS 類型檢測，因此盡量少用，或是 debug 時用。
3. 定義變數時，沒有設定型別時 TS 自動判斷為 any。

### unknown
1. 未知類型: 安全版的 any，可以接受任何型別資料，但不能直接賦值給其他變數。不確定時使用.不要用any
2. 使用情境: 開發時不知道型別時使用。(ex: API 抓取回來的資料無法先推導類型，透過 unknown 先定義)
<!--more-->
```
let aaa:unknown;
let bbb:string;

bbb = aaa; //b會有紅字

if(typeof aaaa ==="string"){ //解法一: 判斷式
  bbb = aaa; 
}

bbb = aaa as string; //解法二: 斷言.語法1(下面內容)
bbb = <string>aaaa; //解法二: 斷言.語法2(下面內容)
```

- type A = string & unknown
  ```
  type A = string & (string | number | void | ....);
  ```

  A 的型別是 string 。

- type B = string | unknown
  ```
  type B = string | (string | number | void | boolean ...);
  ```
  B 的型別是 unknown。

### 斷言
鐵口直斷，告訴變數實際的類型。(可以手動指定一個值的型別)
語法2種:
1. 「變數 as 型別」，使用 as 固定資料的型別
2. 「<型別>變數」
```
// A.先寫 type 定義類型。
type Data = {
  id: number,
  name: string,
  completed: boolean
}

// B.抓資料
async function getData() {
  const res = await fetch('https://xxx.xxx');
  const data = await res.json() as Data;  // 語法1: 用 as 連接
}
```

### 動態資料
使用 as unknown as
公式： const data = data1 as unknown as Data
解釋：假設 data1 不知道資料什麼狀態，先用 as unknown 轉換成"不知道什麼狀態"，最後再用 as Data 斷言成希望的類型

```
// 1.先寫 type 定義類型。
type Data = {
  id: number,
  name: string,
  completed: boolean
}

// 2.同上：抓資料
async function getData() {
  const res = await fetch('https://xxx.xxx');
  const data = await res.json() as unknown as Data;  // 3.這邊差異 as unknown as
}
```
