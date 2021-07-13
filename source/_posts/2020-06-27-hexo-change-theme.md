---
title: Hexo 建立部落格(3) - 更換主題
tags: Hexo
categories: Hexo
---
### 前言
[Hexo Themes](https://hexo.io/themes/) 裡面有很多的版型可以選擇，
一開始的預設主題是 landscape，
查詢過程中發現目前最熱門、支援最多的是 [NexT](https://theme-next.iissnan.com/getting-started.html) 就來用用看!
<!--more-->
### 安裝主題
根據 [NexT](https://theme-next.iissnan.com/getting-started.html) 官方文件來安裝。

1. 下載 NexT Theme
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
下載完.查看themes裡面的資料夾是不是多個next的資料夾。

2. 在 _config.yml 檔案裡把 theme: landscape 改換主題
```
theme: next
```

3. 本地端預覽
``` 
hexo s
```
注意可能有暫存.如果沒更換可以用無痕開啟網頁。

### 版型調整
在 themes/next/layout 資料夾中的檔案.不同版型的檔案類型也不同.花一些時間了解他的邏輯 + 樣板語言就可以改 (其他詳細記錄在下一篇)

### 上傳到遠端
自動生成靜態網暫並上傳遠端
```
hexo d
```
注意上傳的網址路徑.錯誤會跑版.如果跑掉只要在網頁的 _config.yml 設定 root 。

我是用 github
如果靜態網頁是上傳到 master ，只要設定成
```
root: /
```

如果 master 是放資料，靜態網頁是在 gh-pages 上的話
```
root: /專案名稱/
```
記得這邊有時候還是要更新 master 的程式資料
