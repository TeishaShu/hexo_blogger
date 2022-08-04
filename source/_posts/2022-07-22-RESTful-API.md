---
title: RESTful API
tags: RESTful API
---
目的：一套規範來協議前後端的 API 的呈現，不用花時間猜怎麼使用，看使用方式就能明白功能，並且送出後會有狀態碼顯示。
<!--more-->

### HTTP Method 
使用網頁需要透過 HTTP 動詞跟伺服器取資料或送資料，在有 RESTful API 前看到 API 傳送方式無法直接對應到實際功能比較混亂，規定後看 HTTP Method 就可以判斷功能。

#### 三種元件組成：
每個資源都會有一個 url 位址，利用 url 去做一些事情會使用到 http 動詞
1. URL 定位資源。(不同 HTTP 動詞有對應的 URL 寫法.寫在網址的最後面)
2. HTTP 動詞描述操作：GET、POST、PUT、DELETE…(有很多種.常用的幾個)
3. Content Types 資源呈現方式：JSON、XML…。

| HTTP 動詞| 中文名稱    | 備註                                                 |
|----------|-------------|------------------------------------------------------|
| GET      | 獲取.讀取   | 從伺服器取出資料(一項或多項)。請求展示取得指定的資料 |
| POST     | 新增        | 在伺服器新增資料(用在新增的動作store)                |
| PUT      | 更新.替換   | 跟PATCH類似.一個                                     |
| DELETE   | 刪除        | destroy 可以做批次刪除多個檔案                       |
| -        | -           | -                                                    |
| PATCH    | 更新.替換   | 跟PUT類似.選取的批次。                               |
| HEAD     | ----------- | 跟GET方法相同，但沒有回應主體（response body）       |
| OPTIONS  | ----------- | 描述指定資源的溝通方法                               |

- 補充：get、post傳送差異
    - get 傳送的是參數 params
    - post 傳送的是 data

#### HTTP 狀態碼也是有規律的
傳送完 API 後，會顯示狀態，大致的分類：
1** 請求未成功；
2** 請求成功、表示成功處理了請求的狀態代碼；
3** 請求被重定向、表示要完成請求，需要進一步操作。通常，這些狀態代碼用來重定向；
4** 請求錯誤這些狀態代碼表示請求可能出錯，妨礙了服務器的處理；
5** （服務器錯誤）這些狀態代碼表示服務器在嘗試處理請求時發生內部錯誤。這些錯誤可能是服務器本身的錯誤，而不是請求出錯。

---------------------------------------------------------------------------------
### RESTful API
一種 API 架構的標準，規範後的形式固定、可讀性強
根據 users 名詞和 http 動詞就可以操作這些資源
每個資源都會有一個 url 位址，利用 url 去做事情會使用到 http 動詞。

1. 使每個url代表一個資源
2. 客戶端和服務器之間，傳遞這種資源的某種表現層(分離的好處-單獨開發部互相干擾)
3. 客戶端透過 4 個 HTTP 動詞對服務氣資源操作
    - 4 種標準方法： GET、POST、PUT、DELETE
    - 7 種RESTful actions：index、new、create、edit、update、show、destroy

    - (補充：思考) 為何delete 不是對應 delete 而是 destroy?
請求request 和 操作actions 的指令不同，一開始設定時有分開不要一樣。
[Why the Ruby on Rails action “destroy” is not named “delete”?](https://stackoverflow.com/questions/14730451/why-the-ruby-on-rails-action-destroy-is-not-named-delete)

#### 範例：請求網址 & 請求方式
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