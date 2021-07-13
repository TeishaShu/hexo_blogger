---
title: Hexo 建立部落格(2) - 創立部落格
tags: Hexo
categories: Hexo
---
### 為何選 Hexo 建部落格?
一開始是使用 google blogger 想要專注寫文章筆記，後來會 markdown 發現這很快能呈現有編排的樣子，
加上想把原本的文章重新整理，因此挑選時想找調整彈性比較大的部落格就挑到這個。
<!--more-->
優點:使用 markdown 用一些元素就可以把版面呈現很好、中文文件多(主要開發者是華人)
缺點:圖片連結需要另外用(可以搭配 Firebase )

----------------------------------------------------------------------

### 安裝並建立專案
- 安裝 git <!--kk 補連結-->
- 安裝 node.js <!--kk 補連結-->
- 安裝 hexo (步驟在下面) 

##### 1. 安裝hexo
```
npm install -g hexo-cli
```

##### 2. 建立專案資料夾
```
hexo init <folder>
cd <folder>
npm install
```
也可以建個資料夾後.在裡面打
```
hexo init
npm install
```

資料夾中會產生下面這些文件

<!--kk 放圖0.安裝hexo後ㄦ-->

    node_modules
    scaffolds 範例(可忽略)
    source 放文章(放在_post資料夾裡面)
    themes 安裝主題時用
    .gitignore 上傳 git 時忽略上傳的檔案
    package.json 套件管理

##### 3. 本地端瀏覽

在終端機下指令-本地端預覽( s 是 serve 的縮寫)
``` hexo
hexo s
```
會出現 http://localhost:4000/
打開後會出現下面這預設的部落格
<!--(放圖1.預設的部落格)-->

----------------------------------------------------------------------

### 部落格部屬到遠端 github 上

##### 1. 上傳整個專案
a. 建立 git 專案 <!--kk 補連結-->
b. 在 .gitignore 資料夾中寫
```
node_modules/
themes/
```
忽略上面 2 個資料夾.因為 node_modules 檔案太大，themes 等等要改主題所以先不要上傳
在專案的終端機打下面 git 指令 
不清楚可以查看 git 相關資料 <!--kk 補連結-->
```
git init
git add .
git commit -m"create project"
git remote add origin <url>
git push -u origin master
```

##### 2. 上傳 hexo 的部落格
a. 設定路徑
修改 _config.yml (網站配置文件)裡面的 deploy 
把檔案推到 gh-pages 這分支上
```
deploy:
  type: git
  branch: gh-pages
  repo: <儲存庫的路徑>

```

b. 打指令上傳遠端
```
// 上傳遠端.部署上去 (生成靜態網頁，並上傳遠端)
hexo d
```

如果上面指令無法的話.第一次上傳需要下面這個
```
// 生成靜態網頁.檔案會出現 public 資料夾
hexo g

// 第一次需要這樣.之後可以省略這步驟
npm install hexo-deployer-git --save

hexo d
```

c. 上傳後如果網頁整個跑版(需要檢查路徑)
1. 在 _config.yml 中
改相對路徑 true
```
relative_link:true
```

2. 如果是上傳到 github 上，因為網站是存在子目錄中，要設定 _config.yml 的 root (網站根目錄)
```
# URL
url: https://teishashu.github.io/
root: /blogger/
```

3. 重新上傳
```
hexo d
```

    需要等一下再刷新網頁