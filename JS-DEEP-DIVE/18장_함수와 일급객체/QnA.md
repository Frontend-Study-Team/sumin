## 18장 let, const 키워드와 블록 레벨 스코프

### 1. 다음 코드의 결과는?

```js
function bar(x, y) {
  console.log(bar.length)
  console.log(arguments.length)
}

bar(1)
bar(1, 2, 3)
```

1. `bar(1)` 실행 시:

   ```perl
   함수 객체의 length: 2
   arguments 객체의 length: 1
   ```

2. `bar(1, 2, 3)` 실행 시:

   ```perl
   함수 객체의 length: 2
   arguments 객체의 length: 3
   ```

- **`bar.length`:** 함수가 선언될 때 정의된 **매개변수의 개수**만 표시
- **`arguments.length`:** 함수가 실제 호출될 때 **전달된 인자의 개수**를 표시

<br>

### 2. 다음 코드의 실행 결과는?

```js
function func(a, b, c) {
  return a + b + c
}

console.log(func.length) // 3
```

- 함수 객체의 `length` 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킴

```js
const func = function () {
  return 'test'
}

console.log(func.name) // func
```

- 함수 객체의 `name` 프로퍼티는 함수 이름을 나타냄

<br>

### 3. 맞는 것을 고르세요

```js
function add(x, y) {
  return x + y
}

const myAdd = add
console.log(myAdd(5, 3))
```

1. **add 함수는 myAdd에 할당되고, 이를 호출할 수 있다.** ⭕️

2. add 함수는 myAdd에 할당되면 더 이상 호출할 수 없다. ❌

3. add 함수는 인자로 전달할 수 없다. ❌

4. add 함수는 다른 함수에 할당되면 변경될 수 없다. ❌

```js
function memoizedAdd(x, y) {
  if (!memoizedAdd.cache) {
    memoizedAdd.cache = {}
  }

  const key = `${x},${y}`
  if (key in memoizedAdd.cache) {
    return memoizedAdd.cache[key]
  }

  const result = x + y
  memoizedAdd.cache[key] = result
  return result
}
```

1. **동일한 입력값에 대해 반복적인 계산을 방지한다.** ⭕️ <br>
   → `memoizedAdd` 함수는 캐시를 사용하여 동일한 입력값에 대해 반복적으로 계산하지 않고, 이미 계산된 값을 반환. `memoizedAdd.cache` 객체에 결과를 저장하여 동일한 `x`, `y` 값이 들어오면 계산을 하지 않고 바로 캐시된 값을 반환

2. x와 y의 값을 계속해서 더한다. ❌ <br>
   → `memoizedAdd` 함수는 `x`와 `y` 값을 더하는 것이 아니라, 그 값을 더한 결과를 저장하고 동일한 입력값이 들어오면 이미 계산된 결과를 반환

3. **memoizedAdd.cache는 함수의 반환값을 저장한다.** ⭕️ <br>
   → `memoizedAdd.cache`는 함수의 반환값(즉, `x + y`의 결과)을 저장 처음 계산된 결과는 `memoizedAdd.cache` 객체에 저장되며, 동일한 입력값에 대해 계산이 반복되지 않도록 함

4. memoizedAdd.cache는 함수의 인자값을 저장한다. ❌ <br>
   → `memoizedAdd.cache`는 인자값 자체를 저장하지 않고, 인자값을 기반으로 생성된 `key`를 사용하여 계산된 결과값을 저장
