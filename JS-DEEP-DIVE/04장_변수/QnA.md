### 4장 변수 Q & A

<br>

```js
console.log(divide(6, 2)) // 1) 결과는?

console.log(modulus(6, 2)) // 2) 결과는?

function divide(x, y) {
  return x / y
}

const modulus = (x, y) => x % y
```

1. 3
2. ReferenceError

- 화살표 함수는 변수 호이스팅만 발생하고, 함수의 정의는 호이스팅 ❌

<br>

---

### TDZ란?
