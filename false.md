# false

[백준 2206](https://www.acmicpc.net/problem/2206) 문제를 풀다가 오류가 나서 디버깅을 통해 알게 됐다.

```python
a = [False]
print(a[0] == 0)
// True
```

<br>

```javascript
const a = [false]
console.log(a[0] === false)
// false
```

```javascript
const a = [false]
console.log(a[0] == false)
// true
```

파이썬에서는 False와 0을 갖게 다룰 수 있지만 자바스크립트에서는 다르다.

<br>

자바스크립트에서 물론 이런 것은 가능하다.

```javascript
let a = [0]
if (!a[0]) {
	console.log(0)
} else {
  console.log(1)
}
// 0
```



