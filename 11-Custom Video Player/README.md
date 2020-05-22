# JS30 Day11 – Custom Video Player

自製影片播放控制功能
---

#### 取得所有 video 的 DOM 元素
```javascript
const video = document.querySelector('video');
const playToggle = document.querySelector('button.toggle');
const playSkip = document.querySelectorAll('.player__button[data-skip]');
const slider = document.querySelectorAll('.player__slider');
const progress = document.querySelector('.progress');
const progressFilled = document.querySelector('.progress__filled');
const fullScreen = document.querySelector('.full__screen');
```

#### 播放 & 暫停
```javascript
function togglePlay() {
  // video.paused 檢查影片是否暫停，若已暫停則播放
  
  // if (video.paused) {
  //   video.play();
  // } else {
  //   video.paused();
  // }
  
  // 三元運算子 – if else 的縮寫
  const method = video.paused ? 'play' : 'pause';
  video[method]();
}

video.addEventListener('click', togglePlay);
toggle.addEventListener('click', togglePlay);
```

#### 切換按鈕圖示
```javascript
function updateButton() {

  // 檢查 this.paused(影片) 是否暫停，更改 icon 樣式
  const icon = this.paused ? '►' : '❚ ❚';
  // console.log(icon);
  
  // 使用 toggle.textContent 更改 icon 內容
  toggle.textContent = icon;
}

video.addEventListener('play', updateButton);
video.addEventListener('pause', updateButton);
```

#### 快轉或倒帶
```javascript
function skip() {
  
  // 使用 parseFloat，將字串轉換為數字
  video.currentTime += parseFloat(this.dataset.skip);
  // 用 dataset.skip 取得設定好的 data-skip 數値
}

skipButtons.forEach(button => button.addEventListener('click', skip));
```

#### 控制音量 & 播放速度
```html
<input type="range" name="volume" class="player__slider" min="0" max="1" step="0.05" value="1">
<input type="range" name="playbackRate" class="player__slider" min="0.5" max="2" step="0.1" value="1">
```

```javascript
function handleRangeUpdate() {
  // 取得 DOM 元素的 name、value 的值
  video[this.name] = this.value;
}

ranges.forEach(range => range.addEventListener('change', handleRangeUpdate));
ranges.forEach(range => range.addEventListener('mouseover', handleRangeUpdate));
```

#### 點擊更改播放位置
```javascript
function handleProgress() {
  
  // 當前時間 / 全長 * 100 = 進度條比例位置
  const percent = (video.currentTime / video.duration) * 100;
  progressBar.style.flexBasis = `${percent}%`;
}

// timeupdate 在啟動播放後，才開始觸發
video.addEventListener('timeupdate', handleProgress);
```

#### 拖曳更改播放位置 
```javascript
function scrub(e) {

  // (滑鼠點擊的位置 / 全長) * 當前影片長度 以秒計算
  const scrubTime = (e.offsetX / progress.offsetWidth) * video.duration;
  video.currentTime = scrubTime;
}

let mousedown = false;
progress.addEventListener('click', scrub);
progress.addEventListener('mousemove', (e) => mousedown && scrub(e));
progress.addEventListener('mousedown', () => mousedown = true);
progress.addEventListener('mouseup', () => mousedown = false);
```