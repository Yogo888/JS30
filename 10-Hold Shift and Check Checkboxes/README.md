# JS30 Day10 – Hold Shift and Check Checkboxes

按住 Shift 鍵對核取方塊進行多個勾選
---

#### 取得所有 input type為 checkbox 的元素
```javascript
const checkboxes = document.querySelectorAll('.inbox input[type=checkbox]')
```

#### 紀錄最後一個點擊打勾的 input
```javascript
let lastChecked;
```
> 之後值會變動，所以使用 let 而不是 const



#### 設定 handleCheck() 方法，處理勾選  input 時的動作
```javascript
function handleCheck(e) {
  let inBetween = false;
  
  // 檢查是否按著 shift 點選以及當前 input 是否被勾選
  // this 為點擊當下的 input
  if (e.shiftKey && this.checked) {
  
    checkboxes.forEach(checkbox => {
      console.log(checkbox);
      
      // 最初勾選與最後勾選之間的 checkbox 
      if (checkbox === this || checkbox === lastChecked) {     
        inBetween = !inBetween;
        console.log('Starting to check them in between!');
      }
      
      // 當 inBetween 的值為 true 時，將 input 的 checked 改為 true ，進行勾選
      if (inBetween) {
        checkbox.checked = true;
      }
    });
  }
  
  // this 為當下點擊的 input
  lastChecked = this;
}

```
#### 監聽每個 input，在點擊後觸發 handleCheck() 方法
```javascript
checkboxes.forEach(checkbox => checkbox.addEventListener('click', handleCheck));