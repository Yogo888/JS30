# JS30 Day5 – Flex Panel Gallery

CSS Flex
---
將圖片依左右排序，並等寬排列

```css
/* 利用 flex 讓圖片垂直排列 */
.panels {
  display: flex;
}

.panel {
  /* 此空間的占比，等寬填滿全畫面 */
  flex: 1;
  /* 水平置中 */
  justify-content: center;
  /* 垂直置中 */
  align-items: center;
  /* 新的 flex 容器，將內容變成新的 flex item */
  display: flex;
  /* 縱向排列 */
  flex-direction: column;
}

.panel > * {
  display: flex;
  /* flex-grow 依照比例分配剩餘空間，預設為 0 */
  /* flex-shrink 空間不夠壓縮比例，預設值為 1，表示被壓縮比例相同，0 表示不壓縮 */
  /* flex-basis 默認尺寸，與 width 相似，但較優先；寬度 10px，flex-basis: 30px; 30px 會覆蓋過 10px*/
  flex: 1 0 auto;
  /* 文字調整置中 */
  justify-content: center;
  align-items: center;
}
```

> [Flex 詳細解說](https://ithelp.ithome.com.tw/articles/10208741)

e.propertyName 屬性名稱 
---
`includes()` 會判斷陣列是否包含特定的元素，並以此回傳 true 或 false


```js
function toggleActive(e) {

  // e.propertyName 獲取觸發 transitionend 的屬性名稱
  console.log(e.propertyName);
  
  // e.propertyName 有包含 flex 就加上 open-active
  if (e.propertyName.includes('flex')) {
    this.classList.toggle('open-active');
  }
  
  panels.forEach(panel => panel.addEventListener('transitionend', toggleActive));
}
```
