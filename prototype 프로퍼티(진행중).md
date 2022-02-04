# prototype 프로퍼티

> prototype 프로퍼티는 자신의 부모 역할을 하는 프로토타입 객체를 가리키는 [[Prototype]] 과 다르다

> 함수 객체만 가지고 있는 프로퍼티다

> 함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)를 가리킨다

<br>

### prototype 프로퍼티는 __ proto __ 가 아니다

__ proto __ 로 접근하는 것과 분리해서 생각해야 한다( __ proto __ 는 위에 언급한 [[Prototype]], 즉 프로토타입 객체를 의미한다).

말그대로 함수 객체의 고유한 프로퍼티라서 __ proto __로 접근하는 것과 달리 prototype 으로 접근한다.

<br>

### 생성자 함수의 프로토타입 객체([[Prototype]])는 Function.prototype

생성자 함수는 __ proto __ 로 접근하면 Function.prototype 에 접근할 수 있다. 

이는 Fuction의 prototype 프로퍼티에 접근할 수 있다는 의미다. 생성자 함수로 생성된 객체들이 __ proto __ 로 접근하면 이 생성자 함수의 prototype에 접근하게 된다.

```javascript
const Foo = function(name) {
    this.name = name;
}

const foo = new Foo('FOO');

console.log(Foo.__proto__)
// {}
console.log(foo.__proto__)
// {}
console.log(typeof Foo.__proto__)
// function
console.log(typeof foo.__proto__)
// object
console.log(Foo.__proto__ === Function.prototype)
// true
console.log(foo.__proto__ === Foo.prototype)
// true
```

<br>

자신을 통해 생성된 객체들이 __ proto __ 로 접근했을 때 부모 역할을 하는 객체(프로토타입 객체)를 갖게 된다.

쉽게 얘기하자면 생성자 함수는 Object.prototype, Function.prototype 처럼 자신도 ''부모'' 역할을 할 수 있게 된다는 의미를 갖는다.

```javascript
const arr = [1, 2, 3];
console.log(arr.__proto__ === Array.prototype);

Array.prototype.forEach.call(arr, (v, i) => console.log(v));
arr.__proto__.forEach.call(arr, (v, i) => console.log(v));
```

<br>

arr은 배열 객체로 arr.__ proto __ 를 통해 Array.prototype에 접근할 수 있다. 이처럼 생성자 함수 Parent가 있고로 만들어진 객체가 child 라면 child.__ proto __ 로 Parent.prototype 에 접근할 수 있다.

<br>

### prototype 프로퍼티는 스스로 프로토타입 객체가 되어 부모 역할을 할 준비를 한다

[모던 JavaScript 튜토리얼](https://ko.javascript.info/function-prototype) 에서 나온 내용을 빌리면

> 생성자 함수(`F`)의 프로토타입을 의미하는 `F.prototype`에서 `"prototype"`은 `F`에 정의된 일반 프로퍼티라는 점에 주의해 글을 읽어 주시기 바랍니다. `F.prototype`에서 `"prototype"`은 바로 앞에서 배운 '프로토타입’과 비슷하게 들리겠지만 이름만 같을 뿐 실제론 다른 우리가 익히 알고있는 일반적인 프로퍼티입니다.

<br>

여기까지 보았을때는 prototype 프로퍼티에 대해서 잘못 이해한건가 하는 생각이 순간 들었지만 바로 아래의 예시와 설명을 보면서 아님을 알았다.

```javascript
let animal = {
  eats: true
};

function Rabbit(name) {
  this.name = name;
}

Rabbit.prototype = animal;

let rabbit = new Rabbit("흰 토끼"); //  rabbit.__proto__ == animal

alert( rabbit.eats ); // true
```

> `Rabbit.prototype = animal`은 "`new Rabbit`을 호출해 만든 새로운 객체의 `[[Prototype]]`을 `animal`로 설정하라."는 것을 의미합니다.

<br>

__ proto __ 가 자신의 부모 역할을 하는 객체를 가리킨다면 prototype 프로퍼티는 __ proto __ 로 자신에게 접근할 객체의 부모 역할을 하게 된다.

<br>

### prototype 프로퍼티와 constructor 프로퍼티

생성자 함수 뿐만 아니라 기본적으로 함수는 prototype 프로퍼티를 갖게 된다. 이때 prototype 프로퍼티는 한 객체를 가리키는데, 이 객체의 프로퍼티는 constructor이며 프로퍼티의 값은 함수 자신이 된다.

```javascript
function Rabbit() {}

console.log(Rabbit.prototype.constructor === Rabbit);
// true
```

<br>

생성자 함수로서 새로운 객체를 만들게 되면 이 객체는 앞서 언급한 constructor 프로퍼티를 그대로 상속 받는다.

```javascript
function Rabbit() {}

const rabbit = new Rabbit();

console.log(rabbit.__proto__.constructor === Rabbit);
// true
```

<br>

### constructor 프로퍼티는 변할 수 있다

prototype 프로퍼티는 객체로서 값을 갖고 있는데, { jumps: true } 라는 객체를 할당해서 기존의 prototype 프로퍼티를 아예 바꿔버린다. 디폴트로 갖게 되는 constructor 프로퍼티가 사라지는 결과를 낳게 된다.

```javascript
function Rabbit() {}

Rabbit.prototype = {
  jumps: true
};

console.dir(Rabbit.prototype);
// 브라우저 콘솔에 찍어보면
// Object
//   jumps: true
//   [[Prototype]]: Object
```

<br>

위처럼 prototype 프로퍼티를 아예 새로 할당하는게 아니라 prototype 프로퍼티 객체 안에 새로운 프로퍼티를 추가하는 방식을 사용하면 constructor 프로퍼티를 유지하면서 jumps 라는 프로퍼티를 prototype 프로퍼티에 추가할 수 있다.

```javascript
function Rabbit() {}

Rabbit.prototype.jumps = true

console.dir(Rabbit.prototype);
// 브라우저 콘솔에 찍어보면
// Object
//   jumps: true
//   constructor: f Rabbit()
//   [[Prototype]]: Object
```

<br>

### 함수 객체만 갖는 prototype 프로퍼티는 값으로 생성자 함수로 사용될때 자신을 통해 생성된 객체의 부모 역할을 하는 객체를 갖는다

```javascript
prototype 프로퍼티 = { };
```

<br>

[poiemaweb의 이웅모님의 글](https://poiemaweb.com/js-prototype#42-%EC%83%9D%EC%84%B1%EC%9E%90-%ED%95%A8%EC%88%98%EB%A1%9C-%EC%83%9D%EC%84%B1%EB%90%9C-%EA%B0%9D%EC%B2%B4%EC%9D%98-%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85-%EC%B2%B4%EC%9D%B8) 에서는 prototype 프로퍼티를 아래와 같이 표현한다.

> **함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)를 가리킨다.**

이와 거의 갖지만 내가 이해한 바로는 '가리킨다' 보다 '갖는다'가 이해하기 더 편했다. 가리킨다 라는 문구가 [[Prototype]] 에서 가리킨다는 맥락과 섞여서 혼동하게 됐다(이웅모 님이 잘못 썼다는 의미가 절대로 아니라 내가 이 문구를 제대로 이해하지 못해서 혼동했다는 의미다).

[[Prototype]] 은 자신의 프로퍼티의 값 자체를 가리킨다기 보다는 자신의 부모 역할을 하는 객체의 prototype 프로퍼티의 값에 접근할 수 있게 된다. 반면에 prototype 프로퍼티는 자신의 프로퍼티의 값 자체를 가리킨다.

<br>

참고

https://poiemaweb.com/js-prototype

https://ko.javascript.info/function-prototype

