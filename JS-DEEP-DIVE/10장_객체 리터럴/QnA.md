### 10장 객체 리터럴

<br>

Q. 결과값은?

```js
const obj = {
  var: 'var',
  function: 'function',
}

console.log(obj.var) // 1) ??
console.log(obj.function) // 2) ??
```

A. 1) var 2) function

<br>

---

<br>

Q. 자바스크립트 함수가 일급객체인데 일급객체가 뭘까?

1. 무명의 리터럴로 생성할 수 있다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있따.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

<br>

> 변수에 함수 할당

```js
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수 있다.
const add = function (num1, num2) {
  return num1, num2
}

// 2. 함수는 객체에 저장할 수 있다.
const calculater = { add }
```

<br>

> 함수에 인자로 전달

```js
// 3. 함수의 매개변수에 전달할 수 있다.
function sayHello() {
  return 'Hello, '
}

function greeting(message, name) {
  console.log(message() + name)
}

greeting(sayHello, 'JavaScript') // Hello, JavaScript!
```

<br>

> 함수 반환

```js
function helloWorld() {
  return () => {
    console.log('Hello, world!')
  }
}
```

<br>

---

<br>

Q. 결과값은?

```js
function test() {
  console.log('HelloWorld')
}

test.me = 'mozzi'
test.you = 'developer'

console.log(test.me) // mozzi
console.log(test.you) // developer
```

<br>

---

<br>

Q. `selectedOptions` 객체에서 `'Broker Service'`의 값을 가져오는 방법 ?

```ts
const [selectedOptions, setSelectedOptions] = useState<{ [key: string]: string }>({
  Group: '',
  'Broker Service': '',
  VPN: '',
  Role: '',
})
```

A. `selectedOptions["Broker Service"]`

- `"Broker Service"`는 공백이 포함된 문자열이기 때문에 점 표기법(.)을 사용할 수 없고 대괄호 표기법([])을 사용

<br>

---

<br>

Q. 결과값은?

```js
console.log({} === {}) // ??
```

A. `false`

- 객체는 생성할 때 마다 새로운 객체가 생성, 따라서 같은 객체인지 비교하고 싶다면 기존 객체를 변수에 저장해두어야함
- 객체의 값이 아니라 객체가 참조하는 메모리 주소를 비교
