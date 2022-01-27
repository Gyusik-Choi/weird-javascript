# 특이한 자바스크립트

## map

map 함수는 기존 배열을 수정하는게 아니라 새로운 객체를 생성한다.

```javascript
arr = ['1', '2', '3']
arr.map(v => Number(v))
arr[0] + arr[1] = 12
```

```javascript
arr = ['1', '2', '3']
newArr = arr.map(v => Number(v))
newArr[0] + newArr[1] = 3
```

새로운 객체를 생성하므로 새로운 변수로 map 함수의 결과물을 받아야 한다.

기존 객체가 변하는게 아니다.



또 한가지 특이점은

```javascript
arr = ['1', '2', '3']
arr.map(v => Number(v))
let num = Math.pow(arr[0] + arr[1], 2)
console.log(num)
// 144
```

문자열 12를 제곱한 것인데 정수 12를 제곱한 것처럼 숫자가 나온다.



참고 문제

https://www.acmicpc.net/problem/1002