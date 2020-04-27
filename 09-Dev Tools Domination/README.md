# JS30 Day9 – Dev Tools Domination

Dev tools
---
各種 console 用法


#### 1. 一般用法
```js
console.log('hello')` → hello
```


#### 2. %s 替換成指定參數
```js
console.log('Hello I am a %s string!', '💩');` → Hello I am a 💩 string! 
```


#### 3. 帶入css樣式
```js
console.log('%c I am some great text', 'font-size: 50px; background: red; text-shadow: 10px 10px 0 blue')`
```

#### 4. 警告圖示
```js
console.warn('OH NOOO');`
```

#### 5. 錯誤圖示
```js
console.error('Shit!');`
```

#### 6. 資訊圖示
```js
console.info('Crocodiles eat 3-4 people per year');
```


#### 7. 測試是否有錯誤，若第一參數為false，則輸出第二參數內容
```js
console.assert( 1 === 2 , 'This is false');
```

#### 8. 清除 console 畫面
```js
console.clear();
```

#### 9. 查看 DOM 元素所有屬性
```js
console.log(p);
console.dir(p);
```

#### 10. 群組化顯示
```javascript
const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];

dogs.forEach(dog => {
  console.groupCollapsed(`${dog.name}`);
  console.log(`This is ${dog.name}`);
  console.log(`${dog.name} is ${dog.age} years old`);
  console.log(`${dog.name} is ${dog.age * 7} dog years old`);
  console.groupEnd(`${dog.name}`);
});
```

#### 11. 計算 count() 輸出內容次數
```js
console.count('Wes'); 1
console.count('Wes'); 2
console.count('Steve'); 1
console.count('Steve'); 2
console.count('Wes'); 3
console.count('Steve'); 3
console.count('Wes'); 4
console.count('Steve'); 4
console.count('Steve'); 5
```

#### 12. 計算開始與結束的執行時間
```js
console.time('fetching data');
 fetch('https://api.github.com/users/wesbos')
  .then(data => data.json())
  .then(data => {
    console.timeEnd('fetching data');
    console.log(data);
});
```

#### 13. 把陣列輸出成 table 格式
```js
console.table(dogs);
```