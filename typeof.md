## typeof

```javascript
typeof null
// "object"

const a = null
typeof a
// "object"
```

null 의 type 을 object 라고 인식한다. 자바스크립트 자체의 버그다. 

object 여부를 판단할때는 typeof 만으로는 판단해서는 안되고 null 이 아닌지도 체크해야 한다.

<br>

```javascript
const func = (obj) => {
  // null 이 아닌 object 타입인 경우
  if (typeof obj === "object" && obj !== null) {
    
  }
}
```



<br>

참고

코어자바스크립트