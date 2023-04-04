## Quick shuffle

Yeah, it's not really "quick" in term of speed but the simplicity in code. 🙈

```js
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const shuffled = array.sort(() => 0.5 - Math.random());
```
