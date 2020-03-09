# JS30 Day1 – JavaScript Drum Kit

練習頁面
---
<i class="fa fa-link fa-fw"></i> [Github](https://github.com/wesbos/JavaScript30)

addEventListener 指定元素添加事件
---
`keydown`按下按鍵，取得對應的鍵盤代碼`e.keyCode`，否則回傳`null`

```js
window.addEventListener('keydown',function(e){
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  // 如果沒有按到對應的按鍵，則停止此函式
  if (!audio) return;
  // 回到音效檔起始點 
  audio.currentTime = 0;
  //播放音效
  audio.play();
}
```

> es6 反引號`` – 透過反引號包住的內容，會保留所有的換行和空行。


element.classList.add( ) 添加指定 class
---

按下按鍵後，在該元素上添加指定`class`產生動態的效果

```js
window.addEventListener('keydown', function(e){
  // 取得按鍵對應的元素
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`); 
  // 加上 playing 樣式
  key.classList.add('playing');
})
```

`querySelectorAll`監聽每一個按鍵的事件，選出所有`.key`的元素，並回傳

```js
// 選出所有 .key 元素
const keys = document.querySelectorAll('.key');
// forEach 讀取 NodeList 為每一個元素加上 transitionend 事件，事件執行時會觸發 removeTransition
keys.forEach((key) => {key.addEventListener('transitionend', removeTransition)}); 
```

以`propertyName = transform`為指標，當`transform`結束後，`removeTransition`移除`playing`
```js
function removeTransition(e) {
  // 省略其他 propertyName 不是 transform 的物件
  if (e.propertyName !== 'transform') return;
  // 移除 playing 樣式
  this.classList.remove('playing');
}
```

> 1.監聽事件 [addEventListener(event, function)](https://www.runoob.com/jsref/met-element-addeventlistener.html)
> 2.按鍵事件 [keydown](https://medium.com/@yitailin/%E6%AF%94%E8%BC%83-keydown-keypress-keyup-%E7%9A%84%E5%B7%AE%E7%95%B0-4e873ba17e81)
> 3.透過 CSS 選擇元素 [querySelector、querySelectorAll](https://www.jianshu.com/p/9c3cb1ae03aa)
> 4.播放/指定播放秒數 element.play、element.currentTime
> 5.資料屬性 [data-* attribute](https://pjchender.blogspot.com/2017/01/html-5-data-attribute.html)
> 6.增加/移除CSS [element.classList.add( ), element.classList.remove( )](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/27430/)
> 7.動畫結束後所做的事件 - [transitionEnd](https://www.runoob.com/jsref/event-transitionend.html)
> 8.[forEach](https://www.hexschool.com/2017/09/01/2017-09-01-javascript-for/#Array-prototype-forEach)
> 9.若不符合則退出函式 [function( ){if(...) return}](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/return)
