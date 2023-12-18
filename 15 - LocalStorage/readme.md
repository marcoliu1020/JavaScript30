## .className input + label:befor
```CSS
.plates input + label:before {
  content: "⬜️";
  margin-right: 10px;
}

.plates input:checked + label:before {
  content: "🌮";
}
```
它選擇了 .plates 類下的 input 元素後面直接跟著的 label 元素。

## FormData
```javascript
    const form = document.querySelector(".add-items");
    form.addEventListener("submit", addItem);

    function addItem(formEvent) {
        // on form submission, prevent default
        formEvent.preventDefault();

        // get value from selector
        // this: <form class="add-items">...</form>
        // const text1 = this.querySelector('input[name="item"]').value; // 123
        // const text2 = this.querySelector('[name="item"]').value; // 123

        // get value from FormData
        const formData = new FormData(formEvent.target);
        const text = formData.get("item"); // 123

        // clear input
        formEvent.target.reset(); // formEvent.target === <form class="add-items">...</form>
    }
```
- 2 種方式取得 form element 裡面 `<input>` 的值 
  - 1. `this.querySelector('[name="item"]').value`
      - `addItem()` 裡面的 `this` 是 `<form class="add-items">...</form>`，因為是用 `<form>` 綁定這個函式
  - 2. FormData
        ```javascript
        const formData = new FormData(formEvent.target);
        const text = formData.get("item"); // 123
        ```
    - this === formEvent.target


## Local Storage
儲存的是字串，不是物件
- 儲存
  - localStorage.setItem( key, string )
    - string = JSON.stringify( object )
- 讀取
  - result = localStorage.getItem(key)
    - result : string | null
    - object = JSON.parse(result)


## fetch data-index from `<input data-index='0' ... />`
```javascript
function toggleDone(e) {
    const isInput = e.target.matches("input");
    if (!isInput) return;

    const input = e.target;
    const index = input.dataset.index; // <input data-index='0' ... />
    items[index].done = !items[index].done; // toggle state

    updateListElement(items);
    updateItemsOnLocalStorage(items);
}
```
- `e.target.matches("input")` 只選取 `<input>` tag
- data-index 會在 `<input ... />.dataset.index` 