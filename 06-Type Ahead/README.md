# JS30 Day6 – Ajax Type Ahead

Fetch API
---
利用 `fetch()` 向後端取得 api 資料，回傳 `Promise`
> `fetch()`是新的api，有[瀏覽器相容性問題](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API#Browser_compatibility)

```js
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

// 建立空陣列 將 JSON 資料存入
const cities = [];

// 利用 fetch 取得 promise 物件
fetch(endpoint)
  // 用 then 進行之後的動作，將 promise 的資料轉換成 JSON 格式，所接收的資料會傳到下一個 then 接收
  .then(blob => blob.json())
  // push 將資料逐一加入 cities 陣列中 
  .then(data => cities.push(...data));

```
> `...data` 將資料逐一加入的意思

RegExp 正規表達式
---
利用`RegExp`來尋找`city`與`state`的屬性中含有關鍵字的資料

```js
// 透過 findMatches() 取得特定資料
function findMatches(wordToMatch, cities) {
  return cities.filter(place => {
    // 確定城市或州是否與搜索到的內容匹配，`g` 尋找整份文件，`i` 代表不區分大小寫
    const regex = new RegExp(wordToMatch, 'gi');
    return place.city.match(regex) || place.state.match(regex)
  });
}
```

建立 `keyup` 及 `change` 監聽事件，並觸發 `displayMatehes` 的查找事件

```js
function displayMatches(){

}

const searchInput = document.querySelector('.search');
const suggestions = document.querySelector('.suggestions');

searchInput.addEventListener('change', displayMatches);
searchInput.addEventListener('keyup', displayMatches);
```

```js
function displayMatches() {
  const matchArray = findMatches(this.value, cities);
  // 使用 map 回傳一個新陣列
  const html = matchArray.map(place => {
    const regex = new RegExp(this.value, 'gi');
    const cityName = place.city.replace(regex, `<span class="hl">${this.value}</span>`);
    const stateName = place.state.replace(regex, `<span class="hl">${this.value}</span>`);
    return `
      <li>
        <span class="name">${cityName}, ${stateName}</span>
        <span class="population">${numberWithCommas(place.population)}</span>
      </li>
    `;
    //使用 join 把陣列轉為字串
  }).join('');
  suggestions.innerHTML = html;
}
```
> [`.join()`](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 將陣列所有的元素連接合併成一個字串，並回傳

人數的百進位逗點處理
```js
function numberWithCommas(x) {
  // \B(?=...) 尋找符合條件的字串，?= 篩選條件為(\d{3})+(?!\d)
  // (\d{3}) 代表每三個數字為一組，\d 是數字的意思，{} 代表字元出現次數
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
}

function displayMatches(){
  ...
  <span class="population">${numberWithCommas(place.population)}</span>
}
```