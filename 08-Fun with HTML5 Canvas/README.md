# JS30 Day8 – Fun with HTML5 Canvas

canvas 繪製功能
---

```html
<canvas id="draw" width="800" height="800"></canvas>
```

設定畫布內容
---

```js
const canvas = document.querySelector('#draw');
// 繪製的類型為 2D
const ctx = canvas.getContext('2d');

// 寬高撐滿至視窗大小
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

畫筆樣式設定
---

```js
// 顏色
ctx.strokeStyle = '#BADA55';
// 線條連結樣式
ctx.lineJoin = 'round';
// 線條頭尾樣式
ctx.lineCap = 'round';
// 線條寬度
ctx.lineWidth = 100;
// 類似 Photoshop 圖層混合效果
// ctx.globalCompositeOperation = 'multiply';
```

```js
// 判斷是否正在繪圖
let isDrawing = false;
// 起始點座標
let lastX = 0;
let lastY = 0;
// 預設初始顏色， hsl 顏色表示
let hue = 0;
// 判斷線條粗細大小
let direction = true;
```
> [其他筆觸參考](https://juejin.im/post/5c14ccea518825493b2a5f02)

繪製條件設定
---

```js
function draw(e) {
  // 判斷 isDrawing 是否為 true，為 false 則返回停止
  if (!isDrawing) return;
  
  // console.log(e);
  
  ctx.strokeStyle = `hsl(${hue}, 100%, 50%)`;
  // 開始新路徑
  ctx.beginPath();
  // 起始點
  ctx.moveTo(lastX, lastY);
  // 終點
  ctx.lineTo(e.offsetX, e.offsetY);
  ctx.stroke();
  // 更新每次起始與終點位置座標
  [lastX, lastY] = [e.offsetX, e.offsetY];

  // hue 代表顏色的度數 0~360
  hue++;
  // 超過 360 重設再從 0 開始
  if (hue >= 360) {
    hue = 0;
  }

  // 線條寬度大於 100 或 小於 1，則翻轉方向(細至粗、粗至細)
  if (ctx.lineWidth >= 100 || ctx.lineWidth <= 1) {
    direction = !direction;
  }
  
  // 如果為 ture，線寬增加，反之則減少
  if(direction) {
    ctx.lineWidth++;
  } else {
    ctx.lineWidth--;
  }
}
```
```js
canvas.addEventListener('mousedown', (e) => {
  // 開始繪圖
  isDrawing = true;
  // 更新位置座標
  [lastX, lastY] = [e.offsetX, e.offsetY];
});

canvas.addEventListener('mousemove', draw);
// 放開鼠標和移出畫布範圍時，不執行
canvas.addEventListener('mouseup', () => isDrawing = false);
canvas.addEventListener('mouseout', () => isDrawing = false);
```
