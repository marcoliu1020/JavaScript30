# canvas 畫圖

## 取得 canvas，並設定寬和高
```javascript=
const canvas = document.querySelector("#draw");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
```

## 取得 canvasContext，並設定基本參數
```javascript=
const canvasContext = canvas.getContext("2d");
canvasContext.lineWidth = 10;
canvasContext.lineCap = "round";
canvasContext.lineJoin = "round";
canvasContext.strokeStyle = "#bada55";
```

## 創立一個繪畫的抽象物件
```javascript=
const { startDrawing, exitDrawing, drawLinew } = new Draw(canvasContext);
```

```javascript=
function Draw(canvasContext) {
    let hue = 0;
    let lastPos = { x: 0, y: 0 };
    let isDrawing = false;
    let isLineWidthLarger = true;
    return { startDrawing, exitDrawing, drawLine };

    // helpers
    function startDrawing(e) {
        isDrawing = true;
        lastPos = [e.clientX, e.clientY];
    }
    function exitDrawing() {
        isDrawing = false;
    }
    function drawLine(e) {
        if (!isDrawing) return;
        // console.log(e);
        canvasContext.strokeStyle = `hsl(${hue}, 100%, 50%)`;
        canvasContext.beginPath();
        canvasContext.moveTo(lastPos.x, lastPos.y); // start from
        canvasContext.lineTo(e.clientX, e.clientY); // go to
        canvasContext.stroke();
        lastPos = { x: e.clientX, y: e.clientY };

        if (hue++ >= 360) hue = 0;
        if (canvasContext.lineWidth >= 100 || canvasContext.lineWidth <= 1) isLineWidthLarger = !isLineWidthLarger;
        if (isLineWidthLarger) canvasContext.lineWidth++;
        else canvasContext.lineWidth--;
    }
}
```

## 事件監聽使用者的滑鼠
```
canvas.addEventListener("mousemove", drawLinew);
canvas.addEventListener("mousedown", startDrawing);
canvas.addEventListener("mouseup", exitDrawing);
canvas.addEventListener("mouseout", exitDrawing);
```
- mousemove `滑鼠移動`
- mousedown `滑鼠按下左鍵`
- mouseup `滑鼠放開左鍵`
- mouseout `滑鼠離開繪畫區域` (`<canvas>`)