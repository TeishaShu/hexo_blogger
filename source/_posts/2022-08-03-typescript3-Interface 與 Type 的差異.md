---
title: TypeScript3-Interface 與 Type 的差異
tags: TypeScript
categories: JavaScript
---
TypeScript 中為型別命名有2種方式: 介面 ( interface ) 和型別 ( type ) 
這篇討論差異性
<!--more-->

### type
1. type 右邊可以進行任何運算
通常定義資料 ( 交集、聯集 )
```
type A = number;
type B = A & string;
type C = B | boolean;
```

2. 定義類型.來重複使用
```
type A = number | string;
type B = boolean | string;

let a1: A  //照原本方式定義
a1 = 123
a1 = "name"

let b1: B
b1 = true
```

3. 不能重複宣告
(比較：下面 interface 可以擴充)
```
type User = {
  name: string
  age: number
}

type User = {  // --->這邊顯示錯誤
  desc: string
}
```


### interface
常以 I 作為開頭

1. interface 右邊是固定型態
```
interface User{
  name: string;
  age: number;
}
```

2. 通常用來定義 object 型別

3. 可以重複宣告
重複定義後會變成條件壘加
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

上例說明: 假設設定 User 的資料
1.擴充的類型。繼承原本有的內容再新增 (比較：type 不能重複宣告)
2.跟 class 繼承有些補充
3.可以使用 interface 定義物件內容

#### Object 
假設設定 User 的資料
說明：type 用物件方式定義好後，之後使用這類型，「編譯器會提醒需要什麼資料」。實作上如果一開始寫空的，編譯器不會提示裡面需要什麼。
```
type User = { 
  name: string
  age:number
}
const obj: User = {} //這邊會提示需要什麼資料寫進去
```

### 比較 Interface 與 Type
Type: 靜態的資料格式.無法延展 ex: 像 Interface 使用 extends
```
interface AnimalType {
  feetNumber: number,
  eyeNumber: number,
}

interface DogType {
  name: string,
  weight: number,
  birth: string
}

interface MyDog extends AnimalType, DogType {
  nickname? : string
}
```

解釋上例:
想要時做出 MyDog 的介面時，除了它本身的屬性外，還要符合 AnimalType、DogType 這2者介面定義出來的屬性與功能，透過這種方式可以減少重複的部分，以增進彈性和複用性


```
type AnimalType {
  feetNumber: number,
  eyeNumber: number,
}

type DogType {
  name: string,
  weight: number,
  birth: string
}

type MyDog extends AnimalType, DogType {
  nickname? : string
}
```

解釋上例:
MyDog 的靜態資料格式是由 AnimalType、DogType 2者組成的。


### 結論
TypeScript 會一直更新，type、interface 原本有點差異(很多資料寫 interface 比較能擴展)，後來其實沒有差很多，實務開發上都可以。

累加屬性的程式寫法不同:

1. 「+」使用
type: A屬性+B屬性
interface: 有自己的屬性+A屬性+B屬性，屬性是堆疊全部都要符合

2. 擴展使用方式
```
interface Base {
  f: number;
}

interface AbcInterface extends Base {
  field: string;
}


type AbcType = Base & {
  field: string;
}
```
