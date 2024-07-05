---
title: 資料庫(8) - E-R Model 延伸: Class
tags: 資料庫
categories: 資料庫
---
<!--more-->

### 類別 Class
一組個體的集合用類別表達之間的關係。
ex: Employee 可在分成 Sales、Manager、HR....。

#### 繼承
- Superclass 超類別: 上例的 Employee
- Subclass 子類別: 後面分成的。可以超多
子類別繼承超類別所有屬性。

#### Class 分成: 特殊化、一般化
##### 特殊化
一個個體可以被拆出更多小的、細部的個體，拆解過程是特殊化的程序
- 個體間的「差異性」，需要注意的比較多
- 圖形: 方形跟方形連接的中間線有很像 U 型的箭頭代表指向子類別。中間可能有「圈圈d」代表注意事項。
- 圈圈+英文字母: 特殊化關係的限制 (*一定要考慮!!)，旁邊會寫是「根據某特定屬性的欄位」來劃分
  分離、重疊會2選1出現，完整性會搭配其中1個。
- Disjoint Constraints 分離限制: 
  -子類別的個體不能重複(ex:車子會分成卡車、汽車，不可能同時)
  -符號: 圈圈d
- Overlap Constraints 重疊限制:
  -ex:員工.可能在業務、HR 同時2個。另外員工50人，業務、HR 總人數超過50人
  -符號: 圈圈o
- Completeness Constraints 完整性限制:
  1. 全部特殊化 Total specialization: 
      -Superclass 裡的資料全部可以分到子類別中。
      -圖案: Superclass 連接到圈圈d 是「雙線」。
  2. 部分特殊化 Partial specialization: 
      -部分資料無法分到子類別中
      -圖案: Superclass 連接到圈圈d 是「單線」。

##### 一般化
- 個體間的「共同性」，從下往上看。
ex: 有2個個體和他們的屬性，屬性相似性很高。這時需要找出他們的 Superclass，再把同屬性放在 Superclass 上，特殊化的逆向回推圖形
- 符號:圈圈u。表示一般化的聯集Union，共通屬性連結。
2個個體連到「圈圈u」，變成1條線連到 Superclass，箭頭像上的指到 Superclass。
- Completeness Category 完整性歸類:
  1. 全部歸類 Total: 
      -Superclass 裡的資料全部可以分到子類別中。
      -圖案: 圈圈u 連接到 Superclass 是「雙線」。
  2. 部分歸類 Partial: 
      -圖案: 圈圈u 連接到 Superclass 是「單線」。


<!-- 
影片: DBCh.03-E-R Model與延伸式E-R Model(07) 
 
#### 雞爪圖(魚尾圖) Crow's Foot Notation
(min, max)表示
差異在「關係型態」的表達方式。

- 符號表示: 在符號中「靠近菱形 min」，遠離 max。
  - 「->」橫線要匯聚到右轉折點: 多
  - 「|」: 1
  - 「O」: 0 
-->