# forEach

forEach문에서 주의할 점은 return 으로 제어할 수 없다는 점이다.

```javascript
const findNumber = function(arr) {
  arr.forEach((number) => {
    if (number === 3) {
      return true
    }
  })
  return false
}
  
const arr = [1, 2, 3, 4, 5]
console.log(findNumber(arr))

// false
```

return으로 함수를 종료하려고 하더라도 forEach문은 끝까지 루프를 돌기 때문에  항상 리턴받는 값은 false가 된다.

<br>

그리고 break는 사용할 수 없다.

```javascript
const findNumber = function(arr) {
  arr.forEach((number) => {
    if (number === 3) {
			break
    }
  })
}
  
const arr = [1, 2, 3, 4, 5]
console.log(findNumber(arr))

// SyntaxError: Illegal break statement
```

<br>

또한 continue도 사용할 수 없다.

```javascript

const findNumber = function(arr) {
    arr.forEach((number) => {
      if (number === 3) {
        continue
      }
    })
  }
  
const arr = [1, 2, 3, 4, 5]
console.log(findNumber(arr))

// SyntaxError: Illegal continue statement: no surrounding iteration statement
```



참고

https://blog.fakecoding.com/archives/js-foreach-loop-statement/

