### 3차원 배열 - 배열 리터럴 vs new Array, Array.from

[프로그래머스의 자물쇠와 열쇠 문제](https://school.programmers.co.kr/learn/courses/30/lessons/60059)를 풀이하다가 3차원 배열에서 배열 리터럴과 Array.from, new Array 간의 차이를 발견할 수 있었다.

배열 리터럴과 달리 나머지 두 방식은 값이 복사되는 현상이 발생했다.

```javascript
const arr = [[[-1, -1], [-1, -1], [-1, -1]], [[-1, -1], [-1, -1], [-1, -1]], [[-1, -1], [-1, -1], [-1, -1]]];
const arr = new Array(3).fill(0).map(v => new Array(3).fill([-1, -1]));
const arr = Array.from(Array(3).fill(0), () => new Array(3).fill([-1, -1]));

arr[0][0][1] = 1;
console.log(arr);
```

<br>

배열 리터럴

```javascript
// 배열 리터럴
[
  [ [ -1, 1 ], [ -1, -1 ], [ -1, -1 ] ],
  [ [ -1, -1 ], [ -1, -1 ], [ -1, -1 ] ],
  [ [ -1, -1 ], [ -1, -1 ], [ -1, -1 ] ]
]
```

<br>

new Array 와 Array.from

```javascript
// new Array 와 Array.from
// 배열 리터럴과 달리 
// [0][0][1] 만 바뀌는게 아니라 나머지 [0][1][1], [0][2][1] 의 값도 바뀐다...
[
  [ [ -1, 1 ], [ -1, 1 ], [ -1, 1 ] ],
  [ [ -1, -1 ], [ -1, -1 ], [ -1, -1 ] ],
  [ [ -1, -1 ], [ -1, -1 ], [ -1, -1 ] ]
]
```

<br>

배열의 길이가 유동적인 경우에는 배열 리터럴도 3차원 배열을 만들 수 없다. 

[프로그래머스의 자물쇠와 열쇠 문제](https://school.programmers.co.kr/learn/courses/30/lessons/60059) 에서는 1차원 배열을 생성한 후에 1차원 배열의 길이만큼 for 문을 돌면서 빈 배열을 넣어서 2차원 배열을 만들었다. 그리고 3차원 배열을 만들어주기 위해 2차원 배열의 길이만큼 for 문을 돌면서 원하는 배열의 값을 넣어서 3차원 배열을 생성하는 방식을 사용했다.

이에 대한 자세한 풀이는 [깃헙](https://github.com/Gyusik-Choi/Algorithm/blob/master/ThisIsCodingTest/%EC%9D%B4%EA%B2%83%EC%9D%B4%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4_12%EC%9E%A5_%EC%9E%90%EB%AC%BC%EC%87%A0%EC%99%80%EC%97%B4%EC%87%A0.js) 에서 확인할 수 있다.

```javascript
const arr = new Array(length);
for (let y = 0; y < length; y++) {
  arr[y] = [];
  for (let x = 0; x < length; x++) {
    arr[y].push([-1, -1]);
  }
}
```

