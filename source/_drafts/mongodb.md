---
title: MongoDB
tags: MongoDB
categories: MongoDB
---
資料庫 database
集合 collection: 很多變成1個 database，相同內容會放在1個 collection。
文件 document: 很多變成1個 collection

下面的資料結構是 BSON（binary JSON），一種 JSON-like 的格式。
很像物件是1個 document，下面名稱 list 是1個 collection，一個檔案是一個 database。
```
{
  "list": [
    {
      "_id" : ObjectId("5332889732"),
      "title" : "標題1",
    },
    {
      "_id" : ObjectId("9993288942"),
      "title" : "標題2",
    },
  ],
  "ageList": [
    {
      "_id" : ObjectId("5332889732"),
      "age" : "11",
    },
    {
      "_id" : ObjectId("9993288942"),
      "age" : "22",
    },
  ]
}
```
