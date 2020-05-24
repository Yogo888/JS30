# JS30 Day12 – Key Sequence Detection

輸入特定字串，出現特定圖片
---

#### 宣告空陣列 & 自訂特定字串
```javascript
// 儲存輸入按鍵的空陣列
const pressed = [];
const secretCode = 'yogo888';
```

#### 鍵盤 keyup 監聽事件
```javascript
window.addEventListener('keyup',(e) => {
  console.log(e.key);

  // 使用 .push() 將內容放進陣列中
  pressed.push(e.key);

  // 從陣列最後一個數過來，當 pressed.length 大於 secret.length 把第一個元素刪除
  pressed.splice(-secretCode.length - 1, pressed.length - secretCode.length);
  console.log(pressed);
})
```

#### 當 pressed 和 secretCode 內容相同時，出現特定圖片
```javascript
// 透過 .join() 把陣列轉成字串
// .includes() 判斷特定的元素是否出現在陣列，若有回傳 true
if (pressed.join('').includes(secretCode)){
  console.log('BOM BOM');
  
  // 觸發效果
  cornify_add();
}
```
