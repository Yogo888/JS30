# JS30 Day13 – Slide in on Scroll

滾動視窗，圖片滑入滑出效果
---

#### debounce 限制一個時間內，只會被呼叫一次
```javascript
function debounce(func, wait = 20, immediate = true) {
  var timeout;
  return function() {
    var context = this, args = arguments;
    var later = function() {
      timeout = null;
      if (!immediate) func.apply(context, args);
    };
    var callNow = immediate && !timeout;
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
    if (callNow) func.apply(context, args);
  };
};
```

#### 設置動畫產生的位置
```javascript
const sliderImages = document.querySelectorAll('.slide-in');

function checkSlide() {
  sliderImages.forEach(sliderImage => {
  
    // 圖片一半的高度 → 頁面已滾動的距離 + 視窗高度 - 圖片高度 / 2
    const slideInAt = (window.scrollY + window.innerHeight) - sliderImage.height / 2;
    
    // 圖片底部位置 → 圖片至視窗頂端的距離 + 圖片的高度
    const imageBottom = sliderImage.offsetTop + sliderImage.height;
    
    // 超過圖片一半的高度時顯示 → 圖片一半的高度 > 圖片至視窗頂端的距離
    const isHalfShown = slideInAt > sliderImage.offsetTop;
    
    // 圖片底部位置未超過視窗頂端時 → 頁面已滾動的距離 < 圖片底部位置
    const isNotScrolledPast = window.scrollY < imageBottom;
    
    // 超過圖片的一半高度 以及 圖片底部位置未超過視窗頂端時 
    if (isHalfShown && isNotScrolledPast) { 
      // 加上 active 樣式
      sliderImage.classList.add('active');
    } else {
      // 當其中一個不成立時，則移除 active 樣式
      sliderImage.classList.remove('active');
    }
  });
}

// scroll 事件發生時，觸發 checkSlide()
window.addEventListener('scroll', debounce(checkSlide));
```
