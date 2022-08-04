---
title: TypeScript2
tags: TypeScript
categories: JavaScript
---
#### as unknown 斷言
API 抓取回來的資料 JavaScript 無法先推導類型，所以透過 unknown 事先定義
<!--more-->
##### 固定資料
使用 as 連接狀態
```
// 1.先寫 type 定義類型。
type Data = {
  id: number,
  name: string,
  completed: boolean
}

// 2.抓資料
async function getData() {
  const res = await fetch('https://xxx.xxx');
  const data = await res.json() as Data;  // 3.這邊用 as 連接
  const data2 = await res.json() as Data;  // 3.這邊用 as 連接
}
```

##### 動態資料
使用 as unknown as
公式： const data = data1 as unknown as Data
解釋：假設 data1 不知道資料什麼狀態，先用 as unknown 轉換成"不知道什麼狀態"，最後再用 as Data 斷言成希望的類型


```
// 1.同上：先寫 type 定義類型。
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

<!-- ---------------------------------------
#### class
public 公開(預設)
private 私有:實際上還是會跑
protected 受保護

......待補

.....泛型

1.19.27
1.44.17泛型 -->

---------------------------------------
#### utility
[Utility Types - 右邊欄位很多方法](https://www.typescriptlang.org/docs/handbook/utility-types.html)

- Record<Keys, Type>
宣告2種類型變成物件
record 在不指定內容下宣告物件

- Pick<Type, Keys>
跟上面 Record 相反，主要是塞選出東西來

- Omit<Type, Keys>
過濾