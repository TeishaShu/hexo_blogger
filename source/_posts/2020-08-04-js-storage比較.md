---
title: 存資料的方式比較 Cookie、LocalStorage、SessionStorage、Memory
tags: JavaScript
---
3種存資料的比較
位置：在瀏覽器-開發者工具-Application頁面中，左邊有 Storage 可以查看。
<!-- more -->

### Cookie
- 特性：(有些限制)
- 容量 4kb
- 每次 request 時都會帶上
- 比較適合重要的資料使用

-------------------------------------------------
### LocalStorage
- 特性：不重要但常用的資料存在用戶端.比較不安全
- 不會過期.需要手動清除
- 容量 5mb
- 每次 request 時不會帶上
- 格式：(value 的型態只有 string)
  ``` 
    key: value 
  ```

- 寫法 (如果非 string 型態，不管設置或取得都需要做轉換)
  ```jsx
    const name = 'Teisha';

    // 設置屬性
    localStorage.setItem('userName', name); 

    // 取得屬性
    localStorage.getItem('userName'); 

    // 刪除屬性
    localStorage.removeItem('userName');

    // 全部移除 (localStorage 不會自己過期，可以使用這方式一次全部清除)
    localStorage.clear();
  ```

-------------------------------------------------
### SessionStorage
- 特性：(分頁、瀏覽器關掉後會清除)
- 除了存活時間.其他都跟 localStorage 一樣
  ```jsx
    let value = 'abc'; 

    // 建立
    sessionStorage.setItem("key", value);

    // 取得
    sessionStorage.getItem('key');

    //刪除
    sessionStorage.removeItem("key");
  ```

value 只能是 string 格式，可以使用 JSON 轉換
  ```jsx
    let value = ['1', 'a'];
    let valueToString = JSON.stringify(value);
  ```

-------------------------------------------------
### Memory
每次頁面重整就會不見，存在記憶體

```
cache (EX:Taiwan area 台灣不同的地區名稱)
- data format: 資料需要轉成特定格式儲存
- last update time: 更新的時間需要紀錄上去再存
- API update time: 假如一周更新一次，需要比較時間來更新上去

// memory.ts
export const globalMemory = {
  abc: 'hello'
}

// Component.tsx
import { globalMemory } from 'memory.ts'
globalMemory.abc = 'hi'
```

-------------------------------------------------
暫存的使用情境:
想要省時間不要直打 API，要看需求狀況判斷 API 多久是要暫存的。
缺點是需要維護，資料會過期，沒有寫好會出現資料都沒有更新。

[參考：Day20 localStorage、sessionStorage](https://ithelp.ithome.com.tw/articles/10203525)