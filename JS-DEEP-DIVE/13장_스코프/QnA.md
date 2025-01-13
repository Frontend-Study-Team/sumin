## 13장 스코프

### 1. 각 코드에서 wrapper를 호출했을 때 나오는 값?

```js
var name = 'a'

function log() {
  console.log(name)
}

function wrapper() {
  name = 'b'
  log()
}

wrapper() // b

// 전역변수 name값 수정
```

```js
var name = 'a'

function log() {
  console.log(name)
}

function wrapper() {
  // var 키워드로 선언
  var name = 'b'
  log()
}

wrapper() // a

// wrapper 함수의 지역 변수를 선언 (별개의 변수)
```

<br>

### 2. 다음 코드를 실행했을 때 나오는 값?

```js
var x = 1000

function foo() {
  var x = 10
  bar()
}

function bar() {
  console.log(x)
}

foo() // 1000
bar() // 1000
```

- 함수의 렉시컬 스코프(정적 스코프)에 의하여 둘 다 1000이 출력됩니다.
- 함수는 정의된 시점에서의 스코프를 상위 스코프로 기억하기 때문입니다.

```js
var name = 'Global'

function outer() {
  var name = 'Outer'

  function inner() {
    console.log(name)
  }

  return inner
}

var myFunc = outer()
myFunc() // Outer
```

- 렉시컬 스코프에 따라 `inner` 함수는 `outer` 함수의 스코프를 참조하기 때문

<br>

### 3. 다음 코드를 실행했을 때 나오는 결과?

```js
function test1() {
  if (true) {
    var x = 1
  }
  console.log(x) // ? → 1
}

function test2() {
  if (true) {
    let y = 1
  }
  console.log(y) // ? → ReferenceError
}

test1()
test2()
```

- `var` → 함수 레벨 스코프
  - 블록 {}을 무시하고 변수가 함수 전체에 걸쳐 접근 가능
- `let` → 블록 레벨 스코프
  - 변수가 선언된 블록 {} 내에서만 접근 가능
- `let`은 **TDZ(Temporal Dead Zone)** 때문에 선언 전에 변수를 접근할 경우 `ReferenceError`를 발생시킴

<br>

### 4. 다음 코드를 실행했을 때 나오는 결과?

```js
var a = '전역 변수'

function outer() {
  var b = '외부 함수 변수'

  function inner() {
    var c = '내부 함수 변수'
    console.log(a) // 출력: ?
    console.log(b) // 출력: ?
    console.log(c) // 출력: ?
  }

  inner()
}

outer()
```

> 함수 스코프(Function Scope)

- var로 선언된 변수는 함수 내부에서만 유효함.
- outer 내부에서 선언된 b는 outer 외부에서 접근할 수 없음.

> 클로저(Closure)

- inner 함수는 outer 함수의 변수 b에 접근 가능함.
- inner 함수가 실행될 때, outer 함수의 스코프는 살아있으며, 이를 클로저라고 함.

> 전역 변수(Global Variable)

- var a는 전역에 선언되어 모든 함수에서 접근 가능함.

<br>

### 5. 다음 코드를 실행했을 때 나오는 결과?

```js
console.log(a) // undefined
var a = 10
console.log(a) // 10
```

```js
let count = 0

function increment() {
  count += 1
}

function resetCount() {
  let count = 0
  console.log(count)
}

increment() // 1
resetCount() // 0
console.log(count) // 1
```
