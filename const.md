# const

const로 선언한 변수를 다시 재선언하려고 하면 TypeError 발생한다.

```javascript
const fs = require('fs')
const input = fs.readFileSync('/dev/stdin').toString().trim().split('\n')
input = input.map(v => Number(v))

// TypeError: Assignment to constant variable.
```

백준 문제를 자바스크립트로 풀면서 TypeError가 발생한 원인이었다.

input을 const로 선언한 후에 다시 input을 선언하려고 해서 TypeError가 발생했다.

이를 막으려면

```javascript
const fs = require('fs')
const input = fs.readFileSync('/dev/stdin').toString().trim().split('\n').map(v => Number(v))
```

```javascript
const fs = require('fs')
let input = fs.readFileSync('/dev/stdin').toString().trim().split('\n')
input = input.map(v => Number(v))
```

```javascript
const fs = require('fs')
const input = fs.readFileSync('/dev/stdin').toString().trim().split('\n')
const nums = input.map(v => Number(v))
```

이런 방법들이 있다.

<br>

참고

https://www.acmicpc.net/problem/2108

https://jamesdreaming.tistory.com/176

https://mygumi.tistory.com/340