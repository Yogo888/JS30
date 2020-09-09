# JS30 Day14 – JavaScript References VS Copying

### 基本型別：String、Number、Boolean 都是 Copy，互不影響已賦值的變數。

#### 傳值 (Call by Value)：age2 複製 age 建立新值。age 與 age2 是各自獨立，互不影響，所以當 `age = 200`，age2 仍是 100。

```javascript
let age = 100;
let age2 = age;
console.log(age, age2); // 100, 100
age = 200;
console.log(age, age2); // 200, 100
```
```javascript
let name = 'Wes';
let name2 = name;
console.log(name, name2); // Wes,  Wes
name = 'wesley';
console.log(name, name2); // Wesley, Wes
```

### 物件型別：Array 是 Reference，會互相改變
#### 傳址 (Call by Reference)：team 只是引用 players 並不是複製，所以 team 會跟著 players 改變。
```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team = players;
console.log(players, team);
// players → ['Wes','Sarah','Ryan','Poppy']
// team → ['Wes','Sarah','Ryan','Poppy']

team[3] = 'Lux';
console.log(players, team);
// players → ['Wes','Sarah','Ryan','Lux']
// team → ['Wes','Sarah','Ryan','Lux']
```

#### Array 複製方法
```javascript
// Array.prototype.slice()
const team2 = players.slice();
```
```javascript
// Array.prototype.concat()
const team3 = [].concat(players);
```
```javascript
// Spread syntax
const team4 = [...players];
team4[2] = 'heeeee';
console.log(team4); 
```
```javascript
// Array.from()
const team5 = Array.from(players);
```

#### Object 複製方法

```javascript
const person = {
  name: 'Wes Bos',
  age: 80
};
```
```javascript
// Object.assign()
const cap2 = Object.assign({}, person, { number: 99, age: 12 });
console.log(cap2);
```
```javascript
// JSON.parse() & JSON.stringify()
const wes = {
  name: 'Wes',
  age: 100,
  social: {
    twitter: '@wesbos',
    facebook: 'wesbos.developer'
  }
};

console.clear();
console.log(wes);

// Object.assign 只能淺拷貝一層
const dev = Object.assign({}, wes);

// 使用 JSON.stringify() 將 wes 轉換為字串，再透過 JSON.parse() 方式轉回 JSON 物件格式。
const dev2 = JSON.parse(JSON.stringify(wes));
```