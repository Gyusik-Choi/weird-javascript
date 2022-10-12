# Vanilla JS 에서 Jest 기반의 테스트 환경 구축

NestJS 로 개발을 하면서 단위 테스트로 Jest 를 접하게 됐다. NestJS 에서는 Jest 기반 테스트 환경이 구축이 되어 있어서 테스트 환경 구축에 대해서 신경쓸게 별로 없었다. 일반 자바스크립트 파일 하나를 테스트 해보고 싶었는데 Jest 를 통해 테스트 하려니 환경 구축을 어떻게 해야할지 몰랐다.

<br>

### 파일 이름은 [테스트할 파일명].test.js

a.js 파일을 테스트 하려고 한다면 a.test.js 로 파일 이름을 생성한다.

<br>

### import/ export

babel 의 도움을 받아서 사용할 수 있다.

우선 babel 을 dev dependency 에 추가한다.

```
npm install -D @babel/core @babel/preset-env
```

<br>

babel.config.json 파일을 생성한다.

```json
{
  "presets": ["@babel/preset-env"]
}
```

<br>

### package.json - scripts

package.json 파일의 scripts 부분을 아래와 같이 작성하면 npm test 로 테스트를 실행할 수 있다.

```json
{
  "scripts": {
    "test": "jest"
  }
}
```

<br>

<참고>

https://poiemaweb.com/jest-esm