# this

this를 학습하면서 배운 내용들을 코드 위주로 정리해보려고 한다

```javascript
const obj1 = {
    name: 'abc',
    method: function() {
        console.log(this)
    },
    outer: {
        inner: function() {
            console.log(this)
        }
    }
}

console.log(this) // Window
obj1.method() // Object (-> obj1)
obj1.outer.inner() // Object (-> outer)
```

메소드의 this는 메소드를 감싸고 있는 객체를 바라본다

메소드의 this는 호출하는 함수 앞의 객체를 바라본다

- 메소드는 객체 안의 함수다
  - 메소드를 함수가 아닌 메소드로 호출하려면 해당하는 객체를 명시하고 함수를 호출해야 한다

<br>

```javascript
const obj1 = {
    outer: function() {
        const inner = function() {
            console.log(this) // Window
        }
        inner()
    }
}

obj1.outer()
```

outer 프로퍼티 inner 함수의 this는 전역객체를 바라본다.

<br>

```javascript
const obj1 = {
    outer: function() {
        const self = this
        const inner = function() {
            console.log(self)
        }
        inner()
    }
}

obj1.outer()
```

inner함수의 this가 obj1을 바라보도록 하기 위해서 outer 메소드 안에서 self 변수에 obj1을 바라보고 있는 this를 넣어준다. self를 통해서 inner 함수에서도 this가 obj1을 바라볼 수 있다.

<br>

```javascript
const func = function() {
    console.log(this)
}

const obj1 = {
    name: 'abc'
}

func.call(obj1)
```

call 메소드를 통해 func가 바라보는 this의 대상을 바꿔줄 수 있다.

call 메소드를 통해 func가 바라보는 this를 obj1 객체로 바꿔준다.

<br>

```javascript
const obj = {
    outer: function() {
        const inner = () => {
            console.log(this)
        }
        inner()
    }
}

obj.outer()
```

화살표 함수(arrow function)는 자신의 스코프 체인에서 가장 가까운 this를 바라보게 된다

<br>

```javascript
const car = {
    fuel: 100,
    power: 200,
    run: function() {
        const self = this
        const innerRun = function() {
            console.log(self.fuel * self.power)
        }
        innerRun()
    }
}

car.run()
```

run 메소드에서는 this가 car를 바라보고 있고 self 변수에 담아준다.

self를 통해 car의 프로퍼티에 접근할 수 있다.

<br>

```javascript
const car = {
    fuel: 100,
    power: 200,
    run: function() {
        const innerRun = function() {
            console.log(this.fuel * this.power)
        }
        // innerRun.bind(this)()
        // innerRun.call(this)
        innerRun.apply(this)
    }
}

car.run()
```

변수에 this를 담는 방식 외에도 apply, call, bind를 통해서 this를 메소드의 내부 함수에서도 car 객체를 바라보게 할 수 있다.

<br>

```javascript
const Func = function() {
    console.log(this) // Func {}
}

const funcChild = new Func()

const func = function() {
    console.log(this) // Window {~~~}
}

func()
```

생성자 함수를 new 연산자와 호출해서 인스턴스를 생성하면 this는 해당 생성자 함수를 나타낸다.

생성자 함수가 아닌 일반 함수를 호출하면 this는 전역객체를 나타낸다.

<br>

참고

코어자바스크립트

https://poiemaweb.com/js-this
