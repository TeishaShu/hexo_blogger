---
title: TypeScript1-安裝環境
tags: TypeScript
categories: JavaScript
---
1. 加強版的 JavaScript，強化了 type 型別。可以了解變數的屬性是 string、number...。
2. 協助開發時更快的閱讀性、維護性，減少因為型別造成的錯誤。
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

### 開發流程
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
#### 建立設定檔
```
tsc --init
```

#### A. include 
指定哪些檔案夾的 TS 文件需要被編譯
```
{
    "include": ["./src/**/*"]
}
```

#### B. files
類似 include 差別在是要寫所有要編譯的檔案，不是資料夾所以會寫很多。通常用在很小的專案上
```
{
    "files":["aaa.ts", "bbb.ts", "ccc.ts"]
}
```

路徑:「*」1個星表示任意文件，「**」2個星表示任意目錄。
第一個「.」跟目錄
上例說明: 跟目錄下的 -> src 目錄下的 -> 任意目錄下的 -> 任意文件。都會被編譯

#### C. exclude
有些文件不想被編譯
```
{
    "include": ["./src/**/*"],
    "exclude": ["./src/stop/**/*"]
}
```

上例說明: stop 目錄下的文件都不會被編譯
通常不需要改，通常預設值:["node_modules", "bower_components", "jspm_packages"]

#### D. extends
繼承.類似引入外部文件 
```
{
    "extends": "./configs/base"
}
```

#### E. compilerOptions (最重要)
決定編譯器如何編譯
不知道裡面怎麼填可以打標題: 後面寫錯誤的值，在終端機執行 tsc，會顯示可以輸入的值。
```
{
    "compilerOptions": {
        "target": "aaa",
    }
}

// 終端機執行 tsc 後，會顯示可以用的值
```

- rootDir 根目錄
- inlineSourceMap 編譯出來的錯誤提示對應到 ts 中檔案位置
- target: 決定 TS 最後輸出的 ES 版本
- module: 指定模組的規範
- lib: 使用哪些第三方的 library，通常不會改。
- outDir: 編譯後檔案放哪裡，通常放在 dist 資料夾裡。
- outFile: 將編譯後的程式合併成一個檔案。(下例中，會把所有不同的程式全部放在 dist 資料夾的 app.js 檔案中)
- allowJs: 要不要編譯 js 檔案 (預設是 false)。
- checkJs: 要不要檢查 js 語法 (預設是 false)。改成 true 會在 js 中在意型別
- removeComments: 程式中的注釋要不要被編譯過去。(true: 編譯不要注釋)
- noEmit: 編譯後不要產生文件(預設是 false)。(true: dist 裡面會空空的)，不常用.希望產生資料的方式不是透過 TS 可以關掉
- noEmitOnError: 有錯誤不要編譯後的文件(預設是 false，即使有錯都可以編譯)。(true: 更嚴格可以避免安全隱患)

##### 編譯、語法檢查相關項目
- strict: 所有嚴格檢查總開關，有設置下面檢查都不用另外設定
- alwaysStrict: 嚴格模式(預設是 false)，"編譯後"的文件是否是嚴格模式。等於每個頁面都用 "use strict"。
- noImplicitAny: 變數不允許預設 any 狀況。變數沒有定義型別下預設是 any。(使用any會關閉使用 ts 的效果，所以會想開啟檢查的效果)
- noImplicitThis: 不允許使用 this。是不是在嚴格模式、怎麼調用決定 this 是誰，設定 true 可以檢查出不明確 this，無法使用，指定 this 的型別是 Window 明確就可以用。
- strictNullChecks: 嚴格檢查空值
```
let box = document.getElementById("box");

// 不一定有 #box，這樣會錯誤
box.addEventListener("click",function(){
    alert("有 box")
})

//解法1
if(box!==null){
    box.addEventListener("click",function(){
        alert("有 box")
    })
}

//解法2: 如果有 box 在執行
box?.addEventListener("click",function(){
    alert("有 box")
})
```

下面只是展現寫法而已。
```
{
    "compilerOptions": {
        "target": "es2017",
        "module": "es2017", // common.js
        "lib": [],
        "outDir":　"./dist",
        "outFile": "./dist/app.js",
        "allowJs": false,
        "checkJs": false,
        "removeComments": false,
        "noEmit": false,
        "noEmitOnError": true,
        "alwayStrict": true,
        "noImplicitAny": true,
        "noImplicitThis": true,
        .....
    }
}
```