---
title: Hexo 建立部落格(4) - NexT 美化
tags: Hexo
categories: Hexo
date: 2020-07-01 16:21:43
---

### 文章日期自己設定
原本日期是顯示檔案生成的時間，可以改成自己寫好的日期。

1. 文章的檔名前面加上日期
ex: 2020-01-01-oneBlog.md
<!--more-->
2. 在 _config.yml 檔案的 #Writing 下面的 # new_post_name: :title.md 改成
```
new_post_name: :year-:month-:day-:title.md
```

### 自定義 css
1. 在 themes/next/source/css 中建立 _mycss.styl 檔案放自己想要新增的。
2. 引入檔案，在 main.styl 中的最後加上下面程式碼。
```
@import "_mycss.styl";
```

### 大頭照設定
找到這個檔案 themes/next/source/images/avatar.gif
把自己的大頭蓋過去.可以改副檔名

到主題下的 _config.yml 改路徑
```
avatar:
  url: /images/avatar.jpg
```

### 推薦插件
#### 搜尋 search
1. 直接在終端機打下面的指令安裝
```
npm install hexo-generator-search --save
```

2. 在主題下的 _config.yml 中.下面 enable: false 改 true
```
local_search:
    enable: true
```

#### 留言板 disqus
照下面這安裝就可以呈現.只是不能在首頁看有沒有效果
[Hexo添加Disqus评论](https://www.jianshu.com/p/d68de067ea74)

#### sitemap
[hexo-generator-sitemap](https://github.com/hexojs/hexo-generator-sitemap)

### 推薦的網站
[Hexo-NexT 主题个性优化](https://guanqr.com/tech/website/hexo-theme-next-customization/)

### 修改的主題上傳到 github
這邊卡了一下，沒看過 github 上 themes 裡面資料夾會指到另一個地方
過程中感覺快把 git 弄壞了.後來有個感想是不要照網路上的亂弄
要懂自己在打什麼 XD ~ 之前都是先試在來理解

[Hexo Next 主题上传到Github中去以后无法点击查看文件？pull下来也是空白的？](https://www.zhihu.com/question/63962146)
[【狀況題】如何在 Git 裡刪除檔案或變更檔名？](https://gitbook.tw/chapters/using-git/rename-and-delete-file.html)

看很多文章後發現都有 git rm --cached 相關的指令

我的作法是
1. 把 next 裡面的 git 資料夾刪除
2. 下指令把遠端的指向拿掉
```
git rm --cached themes/next
```
3. 重新提交
```
git add .
git commit -m"delete"
git push
```
(完成)


如果過程中很卡一直在循環
可以還原一下
```
git add .
git git reset --hard HEAD
git status // 查看一下目前狀況
```

### 心得
整個弄下來花好幾天了，開始打算寫部落格或想換平台 Hexo 從來都不是首選，
因緣際會下對 git、markdown 更了解後，再加上想彈性一點的平台就想說來挑戰試試看，沒想到還弄得起來!!
過程中發現自己看文件的掌握比以前好很多，問題搜尋、關鍵字下得更準確不會查半天查不到，
此外在改樣式的過程中觀察到模板是怎麼設計程式和結構，讓我覺得很佩服!
蠻開心在過程中學到很多，也發現問題一定要解決不然做不同的專案都會卡一樣的東西。