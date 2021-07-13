---
title: RESTful API
tags: 
  - RESTful API
---
### 目的
一套設計規範來協議前後端的API，比較不用花時間猜怎麼使用，送出後會有狀態碼顯示。
<!--more-->
### 三種元件組成：
1. URL定位資源。(不同HTTP動詞有對應的URL寫法.寫在網址的最後面)
2. HTTP動詞描述操作：GET、POST、PUT、DELETE…(有很多種.常用的幾個)
3. Content Types 資源呈現方式：JSON、XML…。

| HTTP動詞 | 中文名稱    | 備註                                                 |
|----------|-------------|------------------------------------------------------|
| GET      | 獲取.讀取   | 從伺服器取出資料(一項或多項)。請求展示取得指定的資料 |
| POST     | 新增        | 在伺服器新增資料(用在新增的動作store)                |
| PUT      | 更新.替換   | 跟PATCH類似.一個                                     |
| DELETE   | 刪除        | destroy                                              |
| -        | -           | -                                                    |
| PATCH    | 更新.替換   | 跟PUT類似.選取的批次。                               |
| HEAD     | ----------- | 跟GET方法相同，但沒有回應主體（response body）       |
| OPTIONS  | ----------- | 描述指定資源的溝通方法                               |

每個資源都會有一個 url 位址，利用 url 去做一些事情會使用到 http 動詞

 → 一個檔案：變數{id}。多個檔案：陣列方式丟變數。

 → 加「?」是非必填，不用加參數。

- (思考)為何delete 不是對應 delete 而是 destroy?

請求request 和 操作actions 的指令不同，一開始設定時有分開不要一樣。

4種標準方法： GET、POST、PUT、DELETE

7種RESTful actions：index、new、create、edit、update、show、destroy

(使用destroy可以做批次刪除多個檔案)

[Why the Ruby on Rails action “destroy” is not named “delete”?](https://stackoverflow.com/questions/14730451/why-the-ruby-on-rails-action-destroy-is-not-named-delete)

---------------------------------------------------------------------------------------------

RESTful
一種api架構的標準.規範後的形式固定、可讀性強
根據 users 名詞和 http 動詞就可以操作這些資源
每個資源都會有一個 url 位址，利用 url 去做事情會使用到 http 動詞。

1.使每個url代表一個資源
2.客戶端和服務器之間，傳遞這種資源的某種表現層(分離的好處-單獨開發部互相干擾)
狀態有關
3.客戶端透過 4個http 動詞對服務氣資源操作(get、post、put、delete)

HTTP METHOD 用在什麼情況?
網頁使用時.需要透過 HTTP動詞跟伺服器取資料或送資料


HTTP METHOD  請求網址                          請求方式

得到資料
https://example.com/api/users     GET (獲取所有用戶信息) 
https://example.com/api/users/1   GET (獲取標識爲 1 用戶信息)  

新增
https://example.com/api/users     POST (添加新的用戶)

編輯、更新
https://example.com/api/users/1   PATCH (更新標識爲 1 用戶部分信息(批次))
https://example.com/api/users/1   PUT (更新標識爲 1 用戶部分信息(一筆資料))

刪除
https://example.com/api/users/1   DELETE (刪除標識爲 1 用戶信息)


HTTP 狀態碼也是有規律的

1**請求未成功；
2**請求成功、表示成功處理了請求的狀態代碼；
3**請求被重定向、表示要完成請求，需要進一步操作。通常，這些狀態代碼用來重定向；
4**請求錯誤這些狀態代碼表示請求可能出錯，妨礙了服務器的處理；
5**（服務器錯誤）這些狀態代碼表示服務器在嘗試處理請求時發生內部錯誤。這些錯誤可能是服務器本身的錯誤，而不是請求出錯。


CORS  是否可以跨網域撈取資料(開啟資料才能共享)
撈資料時有時會顯示 Access-Control-Allow-Origin  沒開啟(他擔心有資安問題
-如果真的需要撈但是被阻擋時:
a.把json格式的資料下載下來自己更新。
b.後端PHP、Node.js 的方式來撈取(透過自己寫的後端去撈資料，再渲染到自己的前端)
