## slice vs splice

- slice : 不會更動原物件
    ```javascript
    nums = [1, 2, 3, 4, 5]
    const res = nums.slice(-2) // [4, 5]
    console.log(nums) // [1, 2, 3, 4, 5]
    ```

- splice : 會更動原物件
    ```javascript
    nums = [1, 2, 3, 4, 5]
    const res = nums.splice(-2) // [4, 5]
    console.log(nums) // [1, 2, 3]
    ```

- splice(0) 可以表示為清除陣列
    <br>
    因為從 index = 0 開始移出，並執行到最後一個