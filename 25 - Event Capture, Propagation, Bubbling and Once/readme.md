## Capture
```html
<div class="one">
    <div class="two">
        <div class="three"></div>
    </div>
</div>

<script>
    const divs = document.querySelectorAll("div");

    for (const div of divs) {
        div.addEventListener("click", log, { capture: false });
    }

    function log(e) {
        console.log(this.classList.value);
    }
</script>
```

- { capture: false } : 這是預設狀態，事件會 bubble up 向上傳遞，當點擊 `<div class="three">` 會跑出 three -> two -> one
- { capture: true } : 當點擊 `<div class="three">` 會跑出 one -> two -> three，會從最外圍開始

## e.stopPropagation()
```javascript
function log(e) {
    e.stopPropagation() // 防止事件向上傳遞
    console.log(this.classList.value);
}
```
- e.stopPropagation() : 防止事件向上傳遞

## run once
```javascript
div.addEventListener("click", log, { once: true });
```
- 只觸發一次，就會執行 `div.removeEventListener("click", log);`