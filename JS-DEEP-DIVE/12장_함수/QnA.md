### 12장 함수

<br>

Q. 자바스크립트에서 원시 값과 객체는 메모리에 어떻게 저장되며, 가비지 컬렉션은 각각에 대해 어떻게 작동는지?

```js
function outer() {
  const x = 10
  return function inner() {
    console.log(x)
  }
}

const innerFunc = outer()
innerFunc() // ?
```

A. `innerFunc();`는 `10`을 출력한다. `inner` 함수는 자신이 생성될 당시의 렉시컬 환경을 [[Environment]] 내부 프로퍼티로 기억한다. 따라서 `outer` 함수의 실행 컨텍스트가 종료되어도 `inner` 함수는 변수 `x`에 접근할 수 있어 `10`을 출력한다.

<br>

---

<br>

Q. 결과값은?

```js
const person = {
  name: 'Alice',
  sayHello: function () {
    console.log(`Hello, ${this.name}!`)
  },
  arrowHello: () => {
    console.log(`Hello, ${this.name}!`)
  },
}

person.sayHello() // Hello, Alice!
person.arrowHello() // Hello, undefined!
```

> 일반 함수 (function)

- 호출 시점에 따라 this가 동적으로 결정
- 객체의 메서드로 호출되면, this는 해당 객체를 참조
- sayHello는 일반 함수로 정의되어 있으며, 객체의 메서드로 호출 <br>
  JavaScript에서 일반 함수의 this는 호출 컨텍스트에 따라 동적으로 바인딩 <br>
  person.sayHello() 호출 시, this는 person 객체를 참조

<br>

> 화살표 함수 (=>)

- this는 정의된 위치의 상위 스코프에서 결정
- 일반적으로 전역 스코프나 함수 스코프의 this를 참조
- arrowHello는 화살표 함수로 정의 <br>
  화살표 함수는 자신의 this를 가지지 않고, 선언 당시의 상위 스코프의 this를 사용 <br>
  여기서 arrowHello가 정의된 상위 스코프는 전역 스코프이므로, this는 전역 객체를 참조 <br>
  this.name는 전역 객체에서 찾지만, 전역 객체에는 name 속성이 없으므로 undefined가 출력

<br>

---

<br>

Q. 결과값은?

```js
;(function () {
  var a = 5
  console.log(a) // 5
})()

console.log(typeof a) // undefined
```

- IIFE가 종료된 이후 변수 a는 함수 스코프를 벗어나기 때문에 더 이상 존재 ❌
- 전역에서 a를 참조하려고 하면 a가 정의되지 않았으므로 typeof a는 `"undefined"`를 반환
- 참고: typeof는 참조되지 않는 변수에 대해 에러를 던지지 않고 `"undefined"`를 반환

<br>

---

Q. 결과값은?

```js
const obj = {
  value: 100,
  method: function () {
    setTimeout(() => {
      console.log(this.value)
    }, 100)
  },
}

obj.method() // 100
```

- setTimeout 내부의 console.log(this.value);는 100을 출력. 화살표 함수는 자신을 감싸는 외부 함수의 this를 상속받음. 따라서 setTimeout의 콜백 함수인 화살표 함수 내부의 this는 method 함수의 this와 같으며, 이는 obj를 가리킴. 따라서 this.value는 obj.value인 100을 출력.
