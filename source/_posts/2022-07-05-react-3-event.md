---
title: React(3) Event 事件
tags: React
categories: React
---
React 的事件是駝峰式的寫法，跟原生都是小寫的不同，這頁有更多比較紀錄。
[官方文件-事件相關](https://zh-hant.reactjs.org/docs/events.html)
<!-- more -->

- 注意大小寫：
  - 小駝峰：原生寫法都是小寫，JSX 中事件變成 onClick、onKeypress、onKeyUp、Oninput...
  - 目的：更好的兼容性、高效
  - 方式：改成小駝峰式是 React 自定義寫的，把原生 onclick 功能再加上事件會委託給最外層屬性(事件冒泡)
  ```
    class Demo extends React.Component{
      showData = (event)=>{
        console.log(event.target)
      }
      render(){
        return(
          <div> // onClick 事件會委託到這層 div 上，為了高效
            <button onClick={this.showData}>點擊</button>
          </div>
        )
      }
    }

    ReactDOM.render(<Demo />, document.getElementById('test1'))

    ------------------------------------------------------------------
    // 委外思考案例：下面不可能在每個 li 上放事件，而是放在 ul 外層上，為了更高效。
    <ul>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  ```

- 事件的 function 獨立出來，命名通常使用 handle 開頭
- render 畫面更新問題
下面程式說明：執行後畫面不會更新，只有資料更新 render 只跑一次，之後怎麼按 onClick 都只有數字增加而已，不會跑出 render 的字，因為 React 不知道需要幫我們更新畫面(需要使用 useState 這個 hook 後面會介紹)。
```
function handleClick(math) {
  math = math + 1;
  console.log(math)
}
// 也可以寫成箭頭函式
// const handleClick = (math) => { math = math + 1;}

const Content = (
  let math = 0;
  return(
    <div onClick={(math) => { handleClick(math)} >{{text}}</div>
    {/* 如果寫成下面這樣.會直接執行.因此外面要在一個 function */}
    {/* <div onClick={handleClick(math)} >{{text}}</div> */}
  );
);
ReactDOM.render(Content, document.getElementById('root'));
```
