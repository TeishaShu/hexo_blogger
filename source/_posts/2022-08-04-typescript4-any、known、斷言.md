---
title: TypeScript4- any、unknown、斷言
tags: TypeScript
categories: JavaScript
---
### any
1. 代表: 任何類型，放什麼類型都不會出錯 (ex: string、number....)
2. 注意‼️ 使用等於關閉 TS 類型檢測，因此盡量少用、不要用，或是 debug 時用。
3. 定義變數時，沒有設定型別時 TS 自動判斷為 any。

### unknown
1. 未知類型: 安全版的 any，可以接受任何型別資料，但不能直接賦值給其他變數。不確定時使用，但也盡量不要用，如果要用使用 unknown 不是 any
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
把變數轉換型別，可能原本型別有幾種後來想要轉換。
- 語法2種:
  1.「變數 as 型別」，使用 as 固定資料的型別
  2.「<型別>變數」

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
#### A. 使用 as unknown as
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

#### B. 比較寫法差異
型別寫在變數後 vs 使用 as
```
interface ErrorType {
  status: number;
}

const errorData = { status: 0, message: 'hello' }
const aaaError: ErrorType = errorData;
const bbbError = errorData as ErrorType;
```

上例中，aaaError 會出現紅字報錯，因為物件多了 message，bbbError 沒有顯示。

結論: 
型別寫在變數後比較嚴謹，使用 as 可能拿到的資料不太確定，因此只管有沒有滿足後來定義的條件，多餘的就不管。
因此 as 比較寬鬆不常用，實務上想拿 API 的確定某幾個欄位檢查使用。

#### C. 第三方套件輔助: Zod、Yup
當處理來自第三方的 API 資料，不是公司內部開發的而是各種平台，無法事先了解資料型態。這時可以使用 Zod、Yup 來幫助定義和驗證資料的型別。透過套件可以建立 schema，schema 是一種描述資料格式和數值的架構。可以讓我們先定義資料的型別和格式，並在需要時對資料進行驗證，確保資料的完整、正確性。對於處理來自第三方 API 的資料很重要，可以明確、更有效的處理資料。

```
const data = await api(...)

// good
// 使用 Zod, Yup
schema = zod.object({
  text: zod.string().length(2)
})
const parsedData: { text: string } = schema.parse(data)

// bad
const parsedData = data as { text: string }
```