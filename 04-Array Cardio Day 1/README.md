# JS30 Day4 – Array Cardio Day 1

1、Array.filter()
---
篩選出符合條件的選項，並回傳true的陣列

```js

//篩選1500~1599間的發明家
const fifteen = inventors.filter(function(inventor){
  if(inventor.year >= 1500 && inventor.year < 1600){
    return true;
  }
})

//簡化寫法
const fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));

console.table(fifteen);
```
> `console.table()`可將資料以表格方式呈現

2、Array.map()
---
依照條件重新組合一個新的陣列

```js
// 將last與first重新組合成一個陣列
const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);

console.table(fullNames);
```

3、Array.sort()
---
對陣列的所有元素進行排序，預設的排序順序是根據字串的 Unicode 編碼位置而定

```js
//依照生日由大至小排序，條件成立，回傳1；反之回傳-1
const ordered = inventors.sort(function(a, b){
  if(a.year > b.year) {
   return 1;
  } else {
     return -1;
  }
})

//簡化寫法
const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1);

console.table(ordered);
```

4、Array.reduce()
---
累加陣列中每項元素（由左至右）遞減，將陣列化為單一值

```js
//for迴圈寫法
var totalYears = 0;

for (var i = 0; i < inventors.length; i++) {
  totalYears += inventors[i].year
}

//reduce()寫法
const totalYears = inventors.reduce((total, inventor) => {
  return total + (inventor.passed - inventor.year);
}, 0);

console.log(totalYears);
```

5、利用 Array.sort() 依照年齡大小排序
---

```js
const oldest = inventors.sort(function(a, b){
  const lastGuy = a.passed - a.year;
  const nextGuy = b.passed - b.year;
  // if(lastGuy > nextGuy) {
  //   return -1;
  // } else {
  //   return 1;
  // }
  return lastGuy > nextGuy ? -1 : 1;
})

console.table(oldest);
```

6、列出所有'de'的路名
---
網址：[https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris](https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris)

```js
// 經由 querySelectorAll() 產生 NodeList
const category = document.querySelector('.mw-category');
// 使用Array方法,要將其轉成陣列
const links = Array.from(category.querySelectorAll('a'));
const de = links.map(link => link.textContent)
                .filter(streetName => streetName.includes('de'));
```

7、sort() & split() 人名排序
---
people 的 lastName 依照字母排序

```js
// 使用 split()
const alpha = people.sort((lastOne, nextOne) => {

// 拆開people['lastName, firstName'],取得lastName
const [aLast, aFirst] = lastOne.split(', ');
const [bLast, bfirst] = nextOne.split(', ');
  // 判斷順序
  return aLast > bLast ? 1 : -1;
});

console.log(alpha);
```

8、計算data內每個值的數量
---

```js
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
```

將預設值設為空物件 {}
```js
const transportation = data.reduce(function(obj, item) {
  
}, {});
```

將物件建立出來，並加 1
```js
const transportation = data.reduce(function(obj, item) {
  obj[item] = 0;
  obj[item]++;
  return obj;
}, {});
```

但遇到重複的資料時，不會累加。加上判斷式，重新將它設為 0 ，並累加次數

```js
if (!obj[item]) {
  obj[item] = 0;
}
```

```js
const transportation = data.reduce(function(obj, item) {
  // 加上判斷式，重新將它設為 0，並累加次數
  if (!obj[item]) {
    obj[item] = 0;
  }
  
  // 將物件建立出來，並加 1
  obj[item]++;
  return obj;
}, {});
    
console.log(transportation);
```
