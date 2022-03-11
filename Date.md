# Date

자바스크립트의 Date 객체를 통한 날짜 연산은 의도와 다른 결과가 나올 수 있어서 주의해야 한다.

자바스크립트의 Date 타입은 불변(immutable)이 아니라 변경 가능(mutable)하다. Date 객체에서 월을 1 더해주는 연산을 하여 새 변수에 담으면 연산한 대상 Date 객체도 변하게 된다.

```javascript
const a = new Date('2008-1-31');
const b = new Date(a.setMonth(a.getMonth() + 1));
console.log(a)
console.log(b);
// Sun Mar 02 2008 00:00:00 GMT+0900 (한국 표준시)
// Sun Mar 02 2008 00:00:00 GMT+0900 (한국 표준시)
```

<br>

결과가 조금 이상하게 느껴질 것이다. 1월 31일에서 한달을 더했으니 2월 마지막날(2008년은 윤년이라 2월 29일까지 존재)이 나와야 하는데 3월로 넘어가버렸다. 그리고 a도 함께 변경되었다.

연도 계산도 예상과 다르게 흘러갈 수 있다.

```javascript
const a = new Date('2020-2-29');
const b = new Date(a.setYear(a.getYear() + 1));
console.log(a)
console.log(b);
// Sat Mar 01 0121 00:00:00 GMT+0827 (한국 표준시)
// Sat Mar 01 0121 00:00:00 GMT+0827 (한국 표준시)
```

<br>

2021년 2월 28일을 기대했으나 3월로 넘어갔다.

<br>

월이 아니라 일을 더하는 경우에는 (제대로된 날짜를 대입했을 경우) 제대로 결과가 나온다.

```javascript
const a = new Date('2008-1-31');
const b = new Date(a.setDate(a.getDate() + 1));
console.log(a)
console.log(b);
// Fri Feb 01 2008 00:00:00 GMT+0900 (한국 표준시)
// Fri Feb 01 2008 00:00:00 GMT+0900 (한국 표준시)
```

<br>

그러나 존재하지 않는 날짜를 대입하면 Invalid Date 라는 결과가 나오므로 연산 자체가 되지 않을 수 있다.

```javascript
const a = new Date('2022-1-32');
const b = new Date(a.setDate(a.getDate() + 1));
console.log(b)
// Invalid Date
```

<br>

```javascript
const a = new Date('2022-1-32');
console.log(a)
// Invalid Date
```

<br>

<참고>

https://jojoldu.tistory.com/600

https://js-joda.github.io/js-joda/
