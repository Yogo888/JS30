:root 建立 css 變數
---
`:root { --<varName>: <varValue>`

```css=
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 10px;
}

/* 使用變數 */
img {
  padding: var(--spacing);      
  background: var(--base);
  filter: blur(var(--blur));
}
```


利用JS 改變 css 變數的值
---

```js
// 使用 el.dataset 來取得 data-* 的值
// color不需要單位，所以使用||''
const suffix = this.dataset.sizing || '';

// document.documentElement取得根元素，setProperty修改樣式
document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
```
