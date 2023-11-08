## CSS 效果

```=CSS
.hand {
    width: 50%;
    height: 6px;
    background: black;
    position: absolute;
    top: 50%;

    /* TODO */
    transform-origin: right; /* 將 旋轉的起點 設定在 右端點 */
    transform: rotate(90deg); /* 旋轉 90 度，因為初始是一 */
    transition: all 1s; /* 轉場時間 */
    transition-timing-function: cubic-bezier(0.5, 2.56, 0.58, 1); /* 轉場效果 */
}
```

## 時間角度設定
1. 秒針角度
    秒 / 60 * 360
2. 分針角度
    分 / 60 * 360
3. 時針角度
    時 / 12 * 360
    
- `分針` 和 `時針` 的角度可以有更細緻的變化
1. 分針 + 秒轉分
    (分 / 60 * 360) + (秒 / 60 / 60 * 360)
2. 時針 + 分轉時
    (時 / 12 * 360) + (分 / 60 / 12 * 360)

## 旋轉 時、分、秒 針的角度
```=javascript
function rotatePointer(element, degree) {
    const offsetToZero = 90; // 預設是水平直線，所以需要加一個偏移角度
    degree += offsetToZero;
    element.style.transform = `rotate(${degree}deg)`; // 旋轉 element
}
```

## 補充
秒針從 59 秒 轉到 0 秒 會有閃現，這是因為是從 354 度 轉到 0 度是逆時針的原因，所以這時候要關閉轉場效果

```=javascript
function updatePointer(element, degree) {
    if (degree === 0) {
        // prevent counter clockwise from 354(deg) to 0(deg)
        removeTransitionDuration(element);
    } else {
        resetTransitionDuration(element);
    }
    rotatePointer(element, degree);
}
```

- helper functions
    ```=javascipt
    function removeTransitionDuration(element) {
        element.style.transitionDuration = "0s";
    }

    function resetTransitionDuration(element) {
        element.style.transitionDuration = "";
    }

    function rotatePointer(element, degree) {
        const offsetToZero = 90;
        degree += offsetToZero;
        element.style.transform = `rotate(${degree}deg)`;
    }
    ```