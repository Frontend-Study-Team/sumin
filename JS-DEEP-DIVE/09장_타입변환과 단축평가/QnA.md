### 9장 타입변환과 단축평가

<br>

Q. 아래 코드에서 각 줄의 출력값과 그 이유를 설명해주세요

```js
'CAT' && 'DOG' // 'DOG'
'CAT' || 'DOG' // 'CAT'

false && 'DOG' // false
true || 'DOG' // true
```

<br>

---

<br>

```js
let x = null

console.log(typeof x) // object
console.log(x === null) // true
```

<br>
