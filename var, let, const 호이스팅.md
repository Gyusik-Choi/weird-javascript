# var, let, const 호이스팅

### 변수 생성 3단계

선언 단계

- 실행 컨텍스트에 변수를 등록한다.
- **변수 선언문을 의미하는게 아니다.**

초기화 단계

- 실행 컨텍스트에 등록된 변수를 메모리에 할당한다.
- var, let 의 경우 이 단계에서 변수에 undefined 가 할당된다.
- var 의 경우 **변수 선언 단계**에서 초기화가 이루어진다.
  - 선언 단계와 초기화 단계가 동시에 발생한다.
- let 의 경우 **변수 선언문**에서 초기화가 이루어진다.
  - 선언 단계와 초기화 단계가 따로 발생한다.

할당 단계

- 변수 선언문에 작성한 값을 변수에 할당한다.

<br>

### 변수 선언문과 변수 할당문

```javascript
// 변수 선언문
var a;
let b;

// 변수 할당문
a = 1;
b = 1;

// 변수 선언문과 할당문이 함께 존재
const c = 1;
```

<br>

### TDZ

> [스코프의 시작 지점부터 초기화 시작 지점까지는 변수를 참조할 수 없다. 스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 ‘일시적 사각지대(Temporal Dead Zone; TDZ)’라고 부른다.](https://poiemaweb.com/es6-block-scope#13-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85)

변수 선언문 이전에 변수를 호출하면 var 는 undefined, let 과 const 는 reference error 가 발생한다.

let, const 는 변수 선언문 이전에 변수 접근하는 상황에선 아직 변수의 초기화가 수행되지 않았다. let, const 의 초기화는 변수 선언문에서 발생하며 메모리 할당이 이루어진다.

var, let 의 경우 할당 값 없이 변수 선언만 있는 경우 undefined 가 초기화 시점에 할당된다.

let, const 는 변수 선언문 이전에 변수 접근하면 메모리에 변수가 할당되지 않아서 tdz 에 놓인 상황이라 reference error 가 발생한다.

var, let, const 모두 자신이 포함된 스코프가 실행 컨텍스트에 올라가면 코드가 실행되기 전에 실행 컨텍스트에 등록된다. 다만 초기화 여부의 차이로 선언문 이전에 호출시 undefined, reference error 로 다른 양상을 보인다.

<br>

### var, let, const 키워드로 선언한 변수들 모두 호이스팅 된다

> [호이스팅(Hoisting)이란, var 선언문이나 function 선언문 등을 해당 스코프의 선두로 옮긴 것처럼 동작하는 특성을 말한다.](https://poiemaweb.com/es6-block-scope#13-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85)

#### reference error

let, const 모두 호이스팅이 일어나지 않는 것처럼 보이지만 실제로는 둘 다 호이스팅이 발생한다.

let, const 는 상위에 선언된 1을 출력할 것 같지만 실제로는 호이스팅으로 인해 블록 스코프에 선언된 a 에 접근하다보니 (초기화가 수행되지 않아서) reference error 가 발생한다.

<br>

```javascript
let a = 1;

{
  console.log(a);
  let a = 2;
}

// Uncaught ReferenceError: Cannot access 'a' before initialization
```

<br>

```javascript
const a = 1;

{
    console.log(a);
    const a = 2;
}

// Uncaught ReferenceError: Cannot access 'a' before initialization
```

<br>

<참고>

https://poiemaweb.com/es6-block-scope

모던 자바스크립트 deep dive (이웅모)

