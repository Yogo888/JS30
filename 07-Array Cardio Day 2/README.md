# JS30 Day7 – Array Cardio Day 2

1、Array.prototype.some()
---
只要其中一個條件符合就回傳 `true` 並結束

```js
// 是否有人年滿 19 歲，(new Date).getFullYear() 取得當前日期的年份
const isAdult = people.some(person => ((new Date).getFullYear()) - person.year >=19 );
console.log(isAdult);
```

2、Array.prototype.every()
---
必須完全符合條件，才會回傳 `true`，其中有一筆不符合就會回傳 `false`

```js
// 是否都年滿 19 歲
const allAdults = people.every(person => ((new Date).getFullYear()) - person.year >=19 );
console.log(allAdults);
```

3、Array.prototype.find()
---
回傳第一筆為 `true` 的值

```js
// 找尋 id=823423 的評論
const commentID = comments.find(comment => comment.id === 823423);
//回傳 {text: "Super good", id: 823423}
console.log(commentID);
```

3、findIndex() & splice()
---
`findIndex()` 回傳第一筆符合條件的元素索引位置，如果沒有符合的將返回-1

```js
// 找出需要的元素索引
const index = comments.findIndex(comment => comment.id === 823423);
// 回傳 1
console.log(index);

// 使用 splice() 刪除該索引的資料
// comments.splice(index, 1);

// 使用 slice() 拆開，略過 index
const newComments = [
  // 從索引 0 的位置開始，index結束(不包含index)
  ...comments.slice(0, index),
  // 從 index + 1 後所有元素
  ...comments.slice(index + 1)
];
```
`splice(start,deleteCount,item1,...,itemX)` 藉由刪除既有元素並／或加入新元素來改變一個陣列的內容 [MDN詳解](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
> `start` 添加/刪除的起點
`deleteCount` 欲刪除的原陣列元素數量，如果為 0 表示不刪除元素
`item1,...` 從`start` 開始，要加入到陣列的元素

```js
var myFish = ['angel', 'clown', 'trumpet', 'sturgeon'];
// 從索引 0 的位置開始，刪除 2 個元素並插入「parrot」、「anemone」和「blue」
var removed = myFish.splice(0, 2, 'parrot', 'anemone', 'blue');
```
> myFish 為 ['parrot', 'anemone', 'blue', 'trumpet', 'sturgeon'] 
removed 為 ['angel', 'clown']
