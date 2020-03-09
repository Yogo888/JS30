# JS30 Day1 – JavaScript Drum Kit

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
