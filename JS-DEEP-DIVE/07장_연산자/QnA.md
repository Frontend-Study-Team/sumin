### 7장 연산자

<br>

```js
let x = 0
let result = x ? 'true' : x === 0 ? 'zero' : 'false'

console.log(result) // zero
```

- 0은 falsy
- 따라서 x가 false로 평가되어 첫 번째 삼항 연산자는 : 이후로 넘어감
