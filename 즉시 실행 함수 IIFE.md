# 즉시실행함수 IIFE

### IIFE(Immediately Invoked Function Expression)

```javascript
let a = (() => { console.log(1) })()
// 1
let a = (function() { console.log(1) })()
// 1
```

```javascript
let a = () => { console.log(1) }
// undefined
a()
// 1
```

위와 아래의 차이는 a를 곧장 실행하도록 만드는것과 따로 a를 a()로 호출해야 실행되는 것의 차이

