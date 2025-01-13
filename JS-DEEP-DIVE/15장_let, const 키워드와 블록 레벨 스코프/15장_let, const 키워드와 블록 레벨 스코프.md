## 15.1 `var` 변수로 선언한 변수의 문제점

### 1. 변수 중복 선언 허용

```tsx
var x = 1
var y = 1

var x = 100

var y // 초기화문이 없는 변수 선언문은 무시 (에러 ❌)

console.log(x) // 100
console.log(y) // 1
```

<br>

### 2. 함수 레벨 스코프

- `var` 키워드로 선언한 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정 <br>
  → 함수 외부에서 `var` 키워드로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수

```tsx
var x = 1

if (true) {
  // 전역 변수, x 변수 중복 선언
  var x = 10
}

console.log(x) // 10
```

<br>

### 3. 변수 호이스팅

- 변수 호이스팅에 의해 `var` 키워드로 선언한 변수는 변수 선언문 이전에 참조 가능

⚠️ 할당문 이전에 변수를 참조하면 언제나 `undefined` 반환

```tsx
// 1. 선언 단계: 이 시점에는 변수 호이스팅에 의해 이미 foo 변수 선언
// 2. 초기화 단계: 변수 foo는 undefined로 초기화
console.log(foo) // undefined

foo = 123

console.log(foo) // 123

// 변수 선언은 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 실행
var foo
```

<br>

## 15.2 `let` 키워드

### 변수 중복 선언 금지

- `let` 키워드로 이름이 같은 변수를 중복 선언하면 문법 에러(SyntaxError) 발생

```tsx
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언 허용 ⭕️
var foo = 123
var foo = 456

// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언 허용 ❌
let bar = 123
let bar = 456 // SyntaxError
```

<br>

### 블록 레벨 스코프

- `let` 키워드로 선언한 변수는 모든 코드 블록(함수, `if`문, `for`문, `while`문,` try-catch`문 등)을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다

```tsx
let foo = 1 // 전역 변수

{
  let foo = 2 // 지역 변수
  let bar = 3 // 지역 변수
}

console.log(foo) // 1
console.log(bar) // ReferenceError
```

⚠️ **함수도 코드 블록이므로 스코프를 만듦** → 함수 내의 코드 블록은 함수 레벨 스코프에 중첩

```tsx
let i = 10

function foo() {
  let i = 100

  for (let i = 1; i < 3; i++) {
    console.log(i) // 1 2
  }
  console.log(i) // 100
}

foo()

console.log(i) // 10
```

<br>

### 변수 호이스팅

- `var `키워드로 선언한 변수와 달리 let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것 처럼 동작 <br>
  → **자바스크립트는 모든 선언을 호이스팅**
- `let` 키워드로 선언한 변수는 선언 단계와 초기화 단계가 분리되어 진행 <br>
  → 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 선언 단계 먼저 실행 <br>
  → 초기화 단계는 변수 선언문에 도달했을 때 실행 (초기화 단계 이전에 변수에 접근하려 하면 참조 에러 발생)
- `let` 키워드로 선언한 변수는 스코프의 시작 지점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없다
- **일시적 사각지대(Temporal Dead Zone; TDZ)**: 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간

```tsx
// 런타임 이전에 선언 단계 실행, 아직 변수 초기화 ❌
// 초기화 이전의 일시적 사각지대에서는 변수 참조 ❌
console.log(foo) // ReferenceError

let foo // 변수 선언문에서 초기화 단계 실행
console.log(foo) // undefined

foo = 1 // 할당문에서 할당 단계 실행
console.log(foo) // 1
```

<br>

### 전역 객체와 `let`

- `var` 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 `window`의 프로퍼티가 된다. <br>
  → 전역 객체의 프로퍼티를 참조할 때 `window` 생략 가능

```jsx
var x = 1 // 전역 변수
y = 2 // 암묵적 전역
function foo() {} // 전역 함수

console.log(window.x) // 1 var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티
console.log(x) // 1 전역 객체 window의 프로퍼티는 전역 변수처럼 사용 가능

console.log(window.y) // 2 암묵적 전역은 전역 객체 window의 프로퍼티
console.log(y) // 2

console.log(window.foo) // foo() {} 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티
console.log(foo) // foo() {} 전역 객체 window의 프로퍼티는 전역 변수처럼 사용 가능
```

⚠️ `let` 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아님 → `window.foo`와 같이 접근 불가

- `let` 전역 변수는 보이지 않는 개념적인 블록 내에 존재

```jsx
let x = 1

// let, const 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아님
console.log(window.x) // undefined
console.log(x) // 1
```

<br>

## 15.3 `const` 키워드

### 1. 선언과 초기화

- `const` 키워드로 선언한 변수는 반드시 선언과 동실에 초기화해야 한다.
- `const` 키워드로 선언한 변수는 let 키워드로 선언한 변수와 마찬가지로 블록 레벨 스코프를 가지며, 변수 호이스팅이 발생하지 않는 것처럼 동작

```jsx
{
	// 변수 호이스팅이 발생하지 않는 것 처럼 동작
	console.log(foo); // ReferenceError
	const foo;
	console.log(foo); // 1
}

// 블록 레벨 스코프를 가짐
console.log(foo) // ReferenceError
```

<br>

### 2. 재할당 금지

- `const` 키워드로 선언한 변수는 재할당이 금지 된다.

<br>

### 3. 상수

- 상수: 재할당이 금지된 변수

  ```jsx
  // 세전 가격
  let preTaxPrice = 100

  // 세후 가격
  // 0.1의 의미를 명확히 알기 어렵기 때문에 가독성이 좋지 않음
  let afterTaxPrice = preTaxPrice + preTaxPrice * 0.1

  console.log(afterTaxPrice)
  ```

- 일반적으로 상수의 이름은 대문자로 선언
- 여러 단위로 이뤄진 경우에는 스네이크 케이스로 표현

  ```jsx
  const TAX_RATE = 0.1

  let preTaxPrice = 100

  let afterTaxPrice = preTaxPrice + preTaxPrice * TAX_RATE
  ```

<br>

### 4. const 키워드와 객체

- `const` 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경 가능

```jsx
const person = {
  name: 'Lee',
}

person.name = 'Kim'

console.log(person)
```

- `const` 키워드는 재할당을 금지할 뿐 ‘불변’을 의미하지 않음
  - 새로운 값을 재할당하는 것은 불가능하지만 프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경을 통해 객체를 변경하는 것은 가능 (객체가 변경되더라도 변수에 할당된 참조 값은 변경되지 않음)

<br>

## 15.4. var vs let vs const

- ES6을 사용한다면 `var` 키워드는 사용 ❌
- 재할당이 필요한 경우에 한정해 let키워드를 사용. (이 때 변수의 스코프는 최대한 좁게 만든다)
- 변경이 발생하지 않고 읽기 전용으로 사용하는(재할당이 필요 없는 상수) 원시 값과 객체에는 `const` 키워드 사용
