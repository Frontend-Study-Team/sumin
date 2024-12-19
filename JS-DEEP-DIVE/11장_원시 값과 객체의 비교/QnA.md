### 11장 원시 값과 객체의 비교

<br>

Q. 얕은 복사를 하는 방법

- `Object.assign()`
- `...` 전개 연산자(Spread Operator)
- `slice()`

<br>

---

<br>

Q. 결과값은?

```js
const a = 1
let b = a

b = 2

console.log(a) //1
console.log(b) //2
```

```js
const a = { number: 1 }
let b = a

b.number = 2

console.log(a) // {number: 2}
console.log(b) // {number: 2}
```

<br>

---

<br>

Q. 결과값은?

```js
const array = [{ j: 'k' }, { l: 'm' }]
const shallowCopy = [...array]
console.log(array === shallowCopy) // false
console.log(array[0] === shallowCopy[0]) // true
```

- 얕은 복사는 최상위 수준에서만 새로운 객체를 생성
- 배열 안에 있는 객체나 배열은 여전히 원본 배열과 참조를 공유
