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