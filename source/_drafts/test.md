---
title: 測試
tags: 測試
categories: 測試
---
前端為何要寫測試，益處是什麼，可以解決什麼問題


### 為何要寫測試?
維護、重構時，改動其他部分不小心更動到某個數值，導致結果錯誤。(改A壞B的情況)
因此如果有寫測試，就可以安心的改動，因為只要有錯就會顯示。

很多公司耗用大量人力、金錢進行網站維護

### 寫測試的時機:
目標:保護程式
因此不是所有元件都需要寫測試，首先需要評估這段程式的重要性
ex: 必須很強迫限制參數類型，不能有誤傳的狀況

因為寫測試也是需要時間來開發，但如果花1.5~2倍的時間開發，未來長期下來可以減少不只2倍