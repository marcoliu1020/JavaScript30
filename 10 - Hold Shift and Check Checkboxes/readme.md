## document.querySelectorAll('.item input[type="checkbox"]')
```html
<div class="inbox">
    <div class="item">
        <input type="checkbox" />
        <p>This is an inbox layout.</p>
    </div>
    <div class="item">
        <input type="checkbox" />
        <p>Check one item</p>
    </div>
    ...
</div>
```
- 尋找 .item 下一層 input && type="checkbox" 的 element

## toggle status
```javascript
 function handleCheck(e) {
    // 沒有按住 shift 鍵，就不往下執行了
    if (!e.shiftKey) {
        lastChecked = this;
        return;
    }

    let isBetween = false;
    for (const box of checkboxes) {
        // toggle isBetween
        // 尋遍所有陣列，遇到當下的 input 或是 上一次按下的 input 就切換狀態
        if (box === this || box === lastChecked) isBetween = !isBetween;
        // skip
        // 如果是當下的 input 或是 上一次的 input 或是 不在中間的，就跳過
        if (box === this || box === lastChecked || !isBetween) continue;
        // toggle checked
        // 切換 input 狀態
        box.checked = !box.checked;
    }

    // 同步 上次的 input 為現在的狀態
    lastChecked.checked = this.checked; // sync status
    lastChecked = this;
}
```
