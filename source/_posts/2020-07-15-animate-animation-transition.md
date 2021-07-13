---
title: 網頁動畫、特效(1) - Animation、Transition
categories: CSS
tags: 
  - CSS
  - 網頁特效
---
### 前言
製作網頁的動畫、特效以前是用 JavaScript、Flash，後來 css3 增加了一些屬性，變成開發時間可以縮短，透過 css 交給瀏覽器處理也比較不吃資源。
<!--more-->
要把效果做好有幾個關鍵字可以研究：
- 動畫：css Animation
- 過度、轉場：css Transition
- 變形：transform 2D、transform 3D
基本的有概念後就可以開始找範例解析試模仿寫看看。

這次紀錄研究 Animation、Transition 後，搭配 scrollmagic、gsap，
讓網頁使用起來多點效果不那麼死硬的過程，
transform 這次比較用不到所以先跳過。

------------------------------------------------------------
### CSS3 Animation
動畫也稱為影格動畫，可以設定比較細緻的效果。
動畫是直接執行的。

#### 語法簡寫順序
```
animation: [name 名稱] [duration 時間] | [timing-function 執行效果] | [delay 延遲] | [iteration-count 重複次數] | [direction 方向] | [fill-mode 播放前後模式] | [play-state 播放狀態];
```
要搭配關鍵影格 @keyframes 才可以用，畢竟沒有時間設定開始結束做什麼無法跑呀。

| 屬性                | 說明                     | 補充                                                                                             |
|-------------------|------------------------|------------------------------------------------------------------------------------------------|
| animation-name              | 名稱。@keyframes 後面的名稱  | @keyframes 搭配 from、to。                                                                  |
| animation-duration          | 執行時間\(s 秒或 ms 毫秒\)，預設0 |                                                                                                |
| animation-timing\-function  | 執行效果(速度曲線)                | [w3schools](https://www.w3schools.com/cssref/css3_pr_animation-timing-function.asp) |
| animation-delay             | 延遲(間隔多久後開始)，預設0                 |                                                                                                |
| animation-iteration\-count  | 重覆執行次數，預設 1            | infinite 無限次                                                                                   |
| animation-direction         | 執行方向。預設 normal           | reverse 反向、alternate 先正後反、alternate\-reverse先反後正                                               |
| animation-fill\-mode        | 播放前後模式，預設 none         | forwards、backwards、both                                                                        |
| animation-play\-state       | 播放或暫停狀態，預設 running     | paused 暫停                                                                                      |

#### @keyframes 關鍵影格設定方式
- 公式
```
@keyframes 動畫名稱 {
  時間1 {css 樣式}
  時間2 {css 樣式}
}
```
- 注意動畫名稱大小寫，不同大小寫是不同字。
```
// 下面2個是不同的動畫
@keyframes Abc{}
@keyframes ABC{}
```

- 設定時間有2種方式:
  1. from、to : 一開始和最後的效果( 0%、100% )
  ```
  @keyframes animate1 {
    from {background-color:red; margin-left:0;}
    to {background-color:black; margin-left:50px;}
  }
  ```
  2. 0-100% : 幾 % 時做什麼事
  ```
  @keyframes animate2 {
    0% {background-color:red; margin-left:0;}
    50% {background-color:blue; margin-left:100px;}
    100% {background-color:black; margin-left:50px;}
  }
  ```

#### 套用效果
<style>
  .animate123{
    width:50px;
    height:50px;
    animation: animate2 3s ease 1s infinite alternate;
    background-color:red;
    margin-bottom:10px;
  }
  @keyframes animate2 {
    0% {background-color:red; margin-left:0;}
    50% {background-color:blue; margin-left:100px;}
    100% {background-color:black; margin-left:50px;}
  }
</style>
<div class="animate123"></div>

```
div{
  width:50px;
  height:50px;
  animation: animate2 3s ease 1s infinite alternate;
  background-color:red;
}

@keyframes animate2 {
  0% {background-color:red; margin-left:0;}
  50% {background-color:blue; margin-left:100px;}
  100% {background-color:black; margin-left:50px;}
}
```

[完整解析 CSS 動畫](https://www.oxxostudio.tw/articles/201803/css-animation.html)

#### Animate.css
CSS3 Animate 有太多要設定，有人整理成一個 css 檔方便使用，只要會引用、使用就可以操作。
[Animate.css](https://animate.style/)

Vue.js中使用方式
[animate.css在vue项目中的使用](https://blog.csdn.net/qq_39009348/article/details/81144296)

操作流程:
1. 下載安裝
2. 在想要動畫的地方放 css，每個想要的特效前面都要加 ```animate__animated```。
```
<h1 class="title animate__animated animate__bounce">title</h1>
```
3. 如果希望可以調整的更多.有2種方式:
  a. 在設定的 css 上面寫 animation 就可以控制
  ```
  <style>
    .title{
      animation-duration: 2s;
    }
  </style>
  ```

  b. 也可以在原本的地方增加其他 css 屬性
  ```
  <h1 class="title animate__animated animate__bounce animate__faster">title</h1>
  ```
  | 效果 | 屬性名稱 | 成效                              |
  |----|------|---------------------------------|
  | 延遲 | animate__delay-2s<br>animate__delay-3s<br>animate__delay-4s<br>animate__delay-5s     | 2s<br>3s<br>4s<br>5s            |
  | 速度 | animate__slow<br>animate__slower<br>animate__fast<br>animate__faster      | 2s<br>3s<br>800ms<br>500ms      |
  | 重複 | animate__repeat-1<br>animate__repeat-2<br>animate__repeat-3<br>animate__infinite     | 1<br>2<br>3<br>infinite\(無限重複\) |


------------------------------------------------------------

### CSS3 Transition 語法
動畫效果需要觸發、只能跑一次，適合用在頁面轉場。
#### 語法簡寫順序
```
transition: [property 名稱] [duration 時間] [timing-function 特效] [delay 延遲] ;
```

| 屬性                         | 說明                    |
|------------------------------|------------------------|
| transition\-property         | 名稱 (放要變的class名稱) |
| transition\-duration         | 執行時間                |
| transition\-timing\-function | 執行的速度曲線                |
| transition\-delay            | 延遲，多久後執行 transition    |

#### transition-timing-function 漸變函式
動畫變換的速度

| 漸變函式          | 貝茲曲線                                      | 效果                          |
|---------------|-------------------------------------------|-----------------------------|
| ease          | cubic-bezier (0.25, 0.1, 0.25, 1.0) | 慢(剛起跑緩衝) > 快 > 慢(剎車感) |
| linear        | cubic-bezier (0.0, 0.0, 1.0, 1.0)   | 速度不變.平平的                   |
| ease-in      | cubic-bezier (0.42, 0, 1.0, 1.0)     | 慢(吃力的起床) > 快(快遲到了)   |
| ease-out     | cubic-bezier (0, 0, 0.58, 1.0)        | 快 > 慢(剎車感)                |
| ease-in-out | cubic-bezier (0.42, 0, 0.58, 1.0)    | 慢(吃力的起床) > 快 > 慢(剎車感)  |

想要其他的線性可以使用下面的網站自己調看看
4 個數字組成， 0~1 之間
[貝茲曲線](https://cubic-bezier.com/)

#### 套用效果
<style>
  .transition123{
    width:50px;
    height:50px;
    background-color:red;
    margin-bottom:10px;
  }
  .transition123:hover{
    background-color:blue;
    margin-left:30px;
    transition: background-color 3s;
    transition: margin-left 3s;
  }
</style>
(滑鼠請移到方塊上)
<div class="transition123"></div>

```
div{
  width:50px;
  height:50px;
  background-color:red;
  margin-bottom:10px;
}
div:hover{
  background-color:blue;
  margin-left:30px;
  transition: background-color 3s;
  transition: margin-left 3s;
}
//寫很多屬性時可以下面這樣
div:hover{
  background-color:blue;
  margin-left:30px;
  transition-property: background-color, margin-left;
  transition-duration: 3s, 1s;
}
``` 
[更多 Transition 的搭配使用](https://developer.mozilla.org/zh-TW/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

---------------------------------------------------------------------------------------------------------

### 比較 Animation、Transition 差異

| 屬性         | 特色差異                                                                     |
|------------|--------------------------------------------------------------------------|
| Animation  | 1. 網頁載入直接執行特效。<br>2. 可設定較細的動畫效果\(關鍵影格\.設定很多時間點\)                           |
| Transition | 1. 需要事件觸發才能執行特效。\(滑鼠、鍵盤事件\) <br>2. 只能設定一開始跟結束的效果中間無法。<br>3. 一次性無法重複 \(除非一直觸發才能重複\) |

他們簡寫的前 4 個順序一樣，但只要寫前面2個就可以跑了。

- animation: 
name duration timing-function delay 
iteration-count direction fill-mode play-state;

- transition: 
property duration timing-function delay;

