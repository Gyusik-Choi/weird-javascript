# arrow function syntax

nestjs 에서 jest 로 테스트코드를 작성하던 중에 화살표 함수 부분에서 의문점이 생겨서 확인한 내용을 간단하게 기록하려고 한다. 

```javascript
const mockARepository = async () => ({
  findOne: jest.fn(),
});
```

<br>

화살표 함수의 인자가 아니라 구현 부분에서 { } 바깥에 () 를 감싸주는게 잘 이해가 되지 않았다. ({ }) 이런 식으로 되어있는게 { } 와 어떤 차이가 있는지 궁금해졌다.

구현부에서 { } 는 return 을 기재해야 하고, ( ) 는 return 을 생략해도 된다. ({ }) 는 return 을 생략하되 객체 형태로 리턴할때 사용할 수 있다.

<br>

```javascript
const a = () => { return 1 };
const a = () => ( 1 );
const a = () => ({ 'a': 1 })
```

<br>

<참고>

https://stackoverflow.com/questions/49425755/arrow-functions-and-the-use-of-parentheses-or-or

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions