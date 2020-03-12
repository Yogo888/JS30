# JS30 Day2 – Js & Clock

transform
---
`transform-oragin` 時鐘的旋轉中心點

`transition` 指針走動的動態效果

`transition-timing-function: cubic-bezier`更改動畫曲線

```css
.hand {
  /* 更改旋轉中心點 */
  transform-origin: 100%;
  /* 更改指針角度 */
  transform: rotate(90deg);
  transition: all 0.05s;
  /* 更改動畫曲線 */
  transition-timing-function: cubic-bezier(0, 1.74, 0.36, 0.59);
}
```


setＤate 取得現在的時間
---

```js
// 取得時間函數
const now = new Date();
//透過 getSeconds() 取得'秒'的值
const seconds = now.getSeconds();
//透過 getMinutes() 取得'分'的值
const mins = now.getMinutes();
//透過 getHours() 取得'時'的值
const hour = now.getHours();
```

一圈 60 秒，`( seconds / 60 )` 獲得秒針在時鐘上的比例，比例乘`360`，得到指針對應數值

```js
// css已設定 transform: rotate(90deg)，+90 讓時針從12點鐘方向開始運作
const secondsDegrees = ((seconds / 60) * 360) + 90;
secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
```


setInterval() 定時器
---

`setInterval(function, mins)`會在間隔固定的時間不斷重複

```js
// 每秒運行一次
setInterval(setDate, 1000);
```


