---
title: TypeScript2
tags: TypeScript
categories: JavaScript
---

<!-- ---------------------------------------
#### class
public 公開(預設)
private 私有:實際上還是會跑
protected 受保護

......待補

.....泛型

1.19.27
1.44.17泛型 -->
--------------------------------------
##### 泛型
在函式被執行時才能確定是什麼類型，看怎麼使用決定他的類型。
function、class 都可以用
下圖寫法：<類型名稱>，後面()中把類型放進去
```
function print<T> (data: T) {
  console.log(data)
}

print<number>(123) //使用成 number
print<number>("ttt") //報錯
print<string>("ttt") //使用成 string
print<boolean>(true) //使用成 boolean
```

2種泛型使用
```
function fn2<T, K>(a: T, b: K):T{
  console.log(b)
  return a;
}
fn2(111,"文字"); //可以寫這樣裡面知道泛型
fn2<number, string>(111,"文字"); //把型別放上去更明確
```

---------------------------------------
#### utility
[Utility Types - 右邊欄位很多方法](https://www.typescriptlang.org/docs/handbook/utility-types.html)

- Record<Keys, Type>
宣告2種類型變成物件
record 在不指定內容下宣告物件

https://zhuanlan.zhihu.com/p/356662885
Record 比較像是物件的使用，第一個放枚舉(哪些項目).像是key的腳色，第二個放value的型別。類似mapping

- Pick<Type, Keys>
跟上面 Record 相反，主要是塞選出東西來

- Omit<Type, Keys>
過濾




Partial
更新其中一欄位
https://ithelp.ithome.com.tw/articles/10273198?sc=hot