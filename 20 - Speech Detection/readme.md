## Array.from()
https://medium.com/%E5%B0%8F%E9%83%AD-%E0%B9%80%E0%B8%88%E0%B8%99/%E8%8F%9C%E9%B3%A5%E5%B7%A5%E7%A8%8B%E5%B8%AB-array-from-%E6%96%B9%E6%B3%95%E4%BB%8B%E7%B4%B9-c00568852a44
```javascript
const a1 = new Array(5).fill([])
a1[0][0] = 1 // [ [1], [1], [1], [1], [1] ]

const a2 = Array.from({ length: 5} , () => [])
a2[0][0] = 1 // [ [1], [], [], [], [] ]

Array.from('marco') // ['m', 'a', 'r', 'c', 'o']
Array.from('marco', chr => chr.toUpperCase()) // ['M', 'A', 'R', 'C', 'O']

Array.from({ length: 5}, (num, i) => i) // [0,1,2,3,4]
```