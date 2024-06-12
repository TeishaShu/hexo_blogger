---
title: 計算機基礎(1) - Buffer 緩衝記憶體
tag: 計算機基礎
categories: 計算機基礎
---
固定一段長度的儲存空間，處理二進制資料(0、1組成的一段字)
- 特色:
  1. 大小是固定的無法被調整
  2. 每個元素 1bite(每個0、1)，8個字變成 1byte。
https://www.lhu.edu.tw/e_paper/94/lunghwa_paper_94018/cc.htm

### Buffer 種類
1. alloc
將記憶體的區段先清空在放資料
```
let buf = Buffer.alloc(10)
```

2. allocUnsafe 不安全
優點:比較快
缺點:不會先清空，空間複用，可能會被之前資料影響(所以名稱有 unsafe)
```
let buf = Buffer.allocUnsafe(100)
```

3. from
會把字轉換成2進制
```
let buf = Buffer.from("hello")
let buf_2 = Buffer.from([105, 111, 121])
console.log(buf_2.toString()) //utf-8
```

### 溢出
10進制最大數字255

