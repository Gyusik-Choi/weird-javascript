

# var, let, const의 전역 선언에 따른 window 프로퍼티 포함 여부 차이

```javascript
var a = 1
console.log(window.a) // 1
```

```javascript
let a = 1
console.log(window.a) // undefined
```

```javascript
const a = 1
console.log(window.a) // undefined
```

"전역객체는 전역스코프를 갖는 전역변수를 프로퍼티로 소유한다."

자바스크립트를 공부할때 많이 참고하게 되는 poiemaweb님의 this 글의 일부다.

<br>

```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    console.log("foo's this: ",  this);  // obj
    function bar(a, b) {
      console.log("bar's this: ",  this); // obj
      console.log("bar's this.value: ", this.value); // 100
      console.log("bar's arguments: ", arguments); // 1, 2
    }
    bar.bind(obj)(1, 2);
  }
};

obj.foo();
```



```javascript
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    console.log("foo's this: ",  this);  // obj
    function bar(a, b) {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // 1
      console.log("bar's arguments: ", arguments); // 1, 2
    }
	bar(1, 2)
  }
};

obj.foo();
```

위의 첫번째에서 두번째로 바꾸면서 this를 공부하다가 아래의 코드를 통해서 이번 글의 주제를 생각하게 됐다.

<br>

```javascript
const value = 1;

var obj = {
  value: 100,
  foo: function() {
    console.log("foo's this: ",  this);  // obj
    function bar(a, b) {
      console.log("bar's this: ",  this); // window
      console.log("bar's this.value: ", this.value); // undefined
      console.log("bar's arguments: ", arguments); // 1, 2
    }
	bar(1, 2)
  }
};

obj.foo();
```

전역의 value 변수를 var에서 const로 바꾸었는데 obj객체의 메소드인 foo의 내부 함수 bar에서 this.value는 undefined로 나온다.

전역객체인 window는 전역스코프에서 var로 선언한 변수만 자신의 프로퍼티로 받아들인다. 이제 맨 상단의 세개 코드를 이해할 수 있을 것이다.

<br>

전역객체란? 

- 모든 객체의 유일한 최상위 객체

<br>

참고

https://poiemaweb.com/js-this