---
title: TypeScript1
tags: TypeScript
categories: JavaScript
---
### 簡介
1. 加強版的 JavaScript，強化了 type 型別。可以了解變數的屬性是 string、number...。
2. 協助開發時更快的閱讀性、維護性(排除因為型別造成計算錯誤)。
3. 適用於前、後端開發(react、express)
<!--more-->

### 流程
1. 開發：
    - 副檔名：.ts、.tsx (搭配 react的JSX)
    - 設定檔：tsconfig.json
2. 編譯：tsc
3. 輸出：JavaScript

### 安裝環境
[ts官方](https://www.typescriptlang.org/)
```
// 全局安裝
npm install typescript -g

// 確認是否安裝好與版本
tsc -v
```

補充
```
// 改動後自動重新編譯
tsc --watch
```

--------------------------
### 流程
1. 建立檔案 index.ts
2. 實作
```
// 1.寫法：照原本定義方式，變數後面加「:型別」
let a: string = "name"

// 2.編譯：終端機上寫「tsc 檔案名稱」
tsc index.ts

// 3.完成後顯示一個js檔案，新檔案會轉換，回原本 ts 會顯示不能重複定義，那是偵測到編譯後的檔案才報錯
```

### tsconfig 設定檔
```
tsc --init
```

target 最後輸出版本的標準
rootDir 根目錄
outDir 輸出
inlineSourceMap 編譯出來的錯誤提示對應到 ts 中檔案位置

----------------------------
### 類型
ts 自動偵測.不用整個寫很完整知道
#### 基本型態
可以簡寫，ts會自動推類型。
```
// let str: string = "name";   原本寫法
let str1: string;
str1 = "name";

let num: number = 123;
let boo: boolean = true;
let n: null = null;
let un: undefined = undefined;

// any 任何類型.放什麼都不會出錯. debug 時候使用，謹慎使用
let ttt: any = 123;
```

#### 陣列
```
let arr: string[] = ['a', 'b'];
let arr2: string[][] = [['a', 'b']];

let tuple: [number, string, boolean] = [1, 'a', true];
let tuple2: [string, string][] = [['a', 'b']];
```

#### Enum 枚舉
使用狀況：api 的資料會改動代表不同意思，定義起來後續維護很清楚
```
// 假設情境：車子行駛狀態 (0未發動、1行進中、2發動引擎靜止中)

enum DriveStatus {
  NOT_STAR = 0,
  DRIVING = 1,
  STOP = 2
}

const status = DriveStatus.DRIVING
```

#### Union 一個變數多個型態
下面例子變數設定只能數字或字串
```
let ttt: number | string;
ttt = 1
ttt = "ttt"
ttt = true //顯示錯誤
```

--------------------------------------
#### 宣告類型：type、interface、object 

##### type
1. 定義類型.來重複使用
```
type A = number | string;
type B = boolean | string;

let a1: A  //照原本方式定義
a1 = 123
a1 = "name"

let b1: B
b1 = true
```

2. 不能重複宣告(比較：下面 interface 可以擴充)
3. 也可以使用 type 定義物件內容
```
type User = {
  name: string
  age: number
}

type User = {  // --->這邊顯示錯誤
  desc: string
}
```

##### interface
假設設定 User 的資料
- 可以擴充的類型。繼承原本有的內容再新增
(比較：上面 type 方式不能)
- 跟class繼承有些補充(下一頁內容)
- 可以使用 interface 定義物件內容
```
interface User{
  name: string;
  age: number;
}

// 可以擴充-重複定義
interface User{ 
  desc?: string  // 使用「?」表示可選類型，不是必填。
}

const obj: User = {
  name: "ttt",
  age: 123,
}
```

##### object 
假設設定 User 的資料
說明：type 用物件方式定義好後，之後使用這類型，「編譯器會提醒需要什麼資料」。實作上如果一開始寫空的，編譯器不會提示裡面需要什麼。
```
type User = { 
  name: string
  age:number
}
const obj: User = {} //這邊會提示需要什麼資料寫進去
```

--------------------------------------
#### function
##### 基本寫法
```
// (a,b) 裡面是變數的型態定義
function hello (a: string, b: boolean){
  return 123
}

// ()後寫的是回傳值的型態定義
function hello2 (a: string, b: boolean): number{
  return 123
}

// undefined (有 ? 的放在最後的順序)
function hello3 (a: string, b: boolean, c?:number){

  //多寫個防呆.減少 ui、js 的 bug，也是用ts的好處
  if(c === undefined) return -1 

  return 123
}
```

##### 泛型
- function、class 都可以用(class下一頁說明)
一個變數可能有不同類型，使用時才會知道他的類型
下圖寫法：<類型名稱>，後面()中把類型放進去
```
function print<T> (data: T) {
  console.log(data)
}

print<number>(123)
print<number>("ttt") //報錯
print<string>("ttt")
print<boolean>(true)
```
