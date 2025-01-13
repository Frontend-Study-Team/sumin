## 14장 전역 변수의 문제점

### 1. 클로저를 사용한 모듈 패턴 문제

```js
const bankAccount = (function () {
  let balance = 1000
  return {
    deposit(amount) {
      balance += amount
      return balance
    },
    getBalance() {
      return balance
    },
  }
})()

console.log(bankAccount.deposit(500)) // ?
console.log(bankAccount.getBalance()) // ?
console.log(bankAccount.balance) //

// 1500
// 1500
// undefined → balance는 클로저 내부의 private 변수로 선언되어 외부에서 직접 접근 ❌
```

- `balance`는 즉시 실행 함수 내에서 `let`으로 선언된 private 변수
- `deposit`, `getBalance` 메서드는 클로저를 통해 해당 변수에 접근 가능
- `BankAccount.balance`는 외부에서 직접 접근할 수 없으므로 `undefined`를 반환

<br>

> 클로저: 클로저는 함수가 자신이 생성될 때의 스코프를 기억하고 있다가, 해당 스코프가 외부 환경에서 접근할 수 없게 된 후에도 그 기억을 유지하는 현상

- 함수가 생성될 당시의 외부 변수를 기억함
- 함수가 생성된 이후에도 그 외부 변수에 접근 가능
- 데이터를 은닉 하는데 사용됨

<br>

### 2. var let const 로 선언한 전역변수의 생명주기에 대해 각각 설명해주세요

- `var`로 선언된 전역 변수는 전역 객체에 바인딩되어 페이지가 종료될 때까지 존재하며, 메모리에 할당되고 해제됩니다.
- `let`으로 선언된 전역 변수는 전역 스코프 내에서만 유효하며, 페이지가 종료될 때까지 존재하지만 전역 객체에 바인딩되지 않습니다.
- `const`로 선언된 전역 변수는 let과 동일하게 전역 스코프 내에서만 유효하며, 재할당 불가능하지만 값은 변경할 수 있습니다.

<br>

### 3. 다음 코드의 실행 결과는?

```js
let a = 5
const b = 10

function test() {
  a = 20
  // b = 30;
  console.log(a, b)
}

test() // 20 10
```

```js
let a = 5
const b = 10

function test() {
  a = 20
  b = 30
  console.log(a, b)
}

test() // TypeError
```

- `let`은 재할당이 가능하므로 `a = 20`으로 값을 변경 가능
- `const`는 재할당 불가능하기 때문에 `b = 30`을 시도할 경우 `TypeError` <br>
  ⚠️ `const`로 선언된 객체, 배열의 속성이나 요소는 변경할 수 있지만, 변수 자체의 재할당은 불가능

<br>

### 4. 다음 코드의 실행 결과는?

```js
// module1.mjs 파일
export const foo = 'Hello'
```

```js
// module2.mjs 파일
import { foo } from './module1.mjs'
console.log(foo) // ?
```

> module1.mjs

- `export const foo = 'Hello';`
  - 여기서 `foo`라는 상수를 모듈 외부로 내보낸(`export`) 상태
  - 이제 다른 모듈에서 `foo`를 가져와 사용 가능.

> module2.mjs

- `import { foo } from './module1.mjs';`
  - 여기서 `module1.mjs`에서 내보낸 `foo`를 가져옴.
- `console.log(foo);`
  - 가져온 `foo`의 값인 `'Hello'`가 출력됨.

**[주의 사항]**

- 이 코드를 실행하려면 ES6 모듈을 지원하는 환경이 필요함.
- 파일 확장자는 `.mjs`로 작성해야 하며, 모듈 시스템이 활성화되어야 함.
- 경로는 상대 경로로 정확히 지정해야 함. 브라우저 환경에서는 파일 서버가 필요할 수 있음.

**[실행 결과]**

- 다음과 같이 실행하면 `'Hello'`가 출력.
