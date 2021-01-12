# 이번주 리뷰

<br>

## 조건문

> JSX 안에서 if문은 여러가지가 있다.

1. 컴포넌트 안에서 쓰는 if/else
   > 이것은 Component안의 return() 안의 JSX내에서는 사용이 불가하다.

```jsx
function Component() {
  if (true) {
    return <p>참이면 보여줄 HTML</p>;
  } else {
    return null;
  }
}
```

2. 삼항연산자를 활용한 조건문

- jsx 안의 { }안에서 사용

```jsx
function Component() {
  return(
    <div>
    {
      modal === true // 조건문
      ? <Modal/> // ? 참일 때 실행할 코드
      : null // : else안에서 실행할 코드
    }
    </div>
```

- 삼항연산자 중첩 사용

```jsx
function Component() {
  return (
    <div>
      {1 === 1 ? (
        <p>참이면 보여줄 HTML</p>
      ) : 2 === 2 ? ( // else문
        <p>안녕</p> // else문 안의 if/else문
      ) : (
        <p>반갑</p>
      )}
    </div>
  );
}
```

3. &&연산자로 if역할 대신하기
   > JS의 &&연산자 활용

```jsx
function Component() {
  return (
    <div>
      {
        1 === 1 && <p>참이면 보여줄 HTML</p> // &&연산자는 falsy를 찾는 것
        // 왼쪽 조건식이 false면 오른쪽 HTML 보여주지 않는다.
      }
    </div>
  );
}
```

4. Object 자료형을 응용한 enum
   > object 자료형으로 HTML을 다 정리해 담고, 마지막으로 object뒤에 []대괄호를 붙여 key값이 현재상태인 자료 뽑기

```jsx
function Component() {
  var 현재상태 = "info"; // 현재상태의 값에 따라 보여지는 상태 다름.
  return (
    <div>
      {
        {
          info: <p>상품정보</p>,
          shipping: <p>배송관련</p>,
          refund: <p>환불약관</p>,
        }[현재상태] // 현재상태 변수 값에 따라 원하는 HTML보여주기
      }
    </div>
  );
}
```

```jsx
var 탭UI = {
  info: <p>상품정보</p>,
  shipping: <p>배송관련</p>,
  refund: <p>환불약관</p>,
};

function Component() {
  var 현재상태 = "info";
  return <div>{탭UI[현재상태]}</div>;
}
```

5. switch/case 조건문

```jsx
function reducer(state, 액션) {
  switch (액션.type) {
    case "수량증가":
      return 수량증가된state;
    case "수량감소":
      return 수량감소된state;
    default:
      return state;
  }
}
```

## lazy loading

> App.js에 import가 너무 많을 때, 메인페이지 방문시 모든 것을 import 해오면 사이트 초기 접속속도가 매우 느려질 수 있다. 그래서 그 Component가 필요할 때 import 해오도록 해주는 것

- 사용법 ex)Detail 컴포넌트로

1. `import {lazy, Suspense} from 'react';` import 해오기
2. `import Detail from './Detail.js';` -> `let Detail = lazy(() => { return import('./Detail.js'); });`
3. `<Suspense>`컴포넌트로 감싸주기
4. fallback 속성에는 ```원하는 컴포넌트 로딩 전까지 띄울 원하는 HTML을 적기

```jsx
<Suspense fallback={<div>로딩중입니다~!</div>}>
  <Detail />
</Suspense>
```

## React.memo

> React는 컴포넌트에 있는 props나 state가 변경되면 그것을 사용하는 HTML 전부 재렌더링된다. 그럴 때, props가 변경되지 않은 컴포넌트는 재렌더링 하지 않도록 하게 하는 것
> `import {memo} from 'react';`

- 원래 코드

  ```jsx
  function Child2() {
    useEffect(() => {
      console.log("렌더링됨2");
    });
    return <div>2222</div>;
  }
  ```

- memo 적용 코드

```jsx
let Child2 = memo(function () {
  // memo로 감싸진 컴포넌트는 재렌더링 되지 않는다.
  useEffect(() => {
    console.log("렌더링됨2");
  });
  return <div>2222</div>;
});
```

- 하지만 props가 매우 방대하고 큰 경우엔 오히려 손해일 수 있다. memo로 감싼 컴포넌트는 헛되게 재렌더링을 안시키려고 기존 props와 바뀐 props를 비교하는 연산이 추가로 진행된다. 그러므로props가 크고 복잡하면 이거 자체로도 부담이 될 수도 있다.

<hr>
### Express
> Server인 Express 기본 세팅
- server.js에 다음 코드 입력
```js
const express = require("express");
const path = require("path");
const app = express();

const http = require("http").createServer(app);
http.listen(8080, function () {
console.log("listening on 8080");
});

````

```js
// another ver.
const express = require("express"); // express 가져오기
const app = express(); // express앱 만들기
const port = 5000; // port번호

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

- 그 다음 터미널에 `npm init`
- `npm install express --save`
- `node server.js`로 서버 작동

```js
// HTML파일 보내는법
app.get("/", (req, res) => {
  // req는 요청 , res는 응답
  res.sendFile(path.join(__dirname, "public/index.html"));
});
```

```js
// 미들웨어로 HTML,CSS, img, js 파일들 담긴 곳 명시
app.use(express.static(path.join(__dirname, "public")));
```

<hr>

## Express + React

> React를 만들어 놨으면 React는 HTML파일 하나로 갈아끼우는 원페이지 앱이므로 index.html만 보내주게 세팅하면 된다 ?

- 같은 폴더 내에서 터미널을 하다 더 켜서 `npx create-react-app [프로젝트 명]` 을 입력하면 React프로젝트 생성
- React Project가 완성됐으면 터미널의 react project 디렉토리에서 `npm run build`를 하면 최종 HTML파일 생성

```js
app.use(express.static(path.join(__dirname, "react-project/bulild ")));
```

```js
app.get("/", (req, res) => {
  res.sendFile(path.join(__dirname, "public/main.html"));
});
```

### Router를 썼을 경우 ?

> React프로젝트 내에서 Routing 가능 -> Server의 역할 축소 -> 서버는 DB입출력으로

- 하지만 직접 `http://localhost:3000/`뒤에 예를들어 detail을 입력해 바로 들어가려고 하면 안된다.

```js
// 이렇게 *을 사용하면 해결된다. /detail로 들어가도 실제로 /deatil페이지가 라우팅된다.
app.get("*", (req, res) => {
  res.sendFile(path.join(__dirname, "public/main.html"));
});
```

### Express + React 개발 패턴

1. 예를 들어 /list로 접속시 list 내용의 HTML을 보여주려 할 때, list의 내용물들은 DB에 있을 것이다.
2. list페이지가 load되기 전에 useEffect등에서 Server에 Ajax요청을 한다.
3. Server에서는 React Ajax요청하는 코드도 작성해줘야하고 그럼 Server에서는 DB에 있던 list 데이터를 보내준다.

### `'/'`로 접속했을 때 react가 아닌 메인페이지 보여주는 법

```js
// 미들웨어에서 설정
app.use("/", express.static(path.join(__dirname, "public")));
app.use("react", express.static(path.join(__dirname, "react-project-build")));

app.get("/", (req, res) => {
  // req는 요청 , res는 응답
  res.sendFile(path.join(__dirname, "main.html")); // 메인페이지
});
app.get("/react", (req, res) => {
  // req는 요청 , res는 응답
  res.sendFile(path.join(__dirname, "react-project/build/index.html")); // 리액트 페이지
});
```

- 추가로 React프로젝트의 `package.json`에 가서 `"homparge" : "/react",`도 넣어 줘야한다.

### 매번 build를 해야하는가에 대해서는 proxy를 활용


## nodemon
> 서버 재실행 자동화 해주는 library
nodemon설치: terminal에서 ``` npm install nodemon``` or ```yarn add nodemon```
- global 설치: ``` npm install -g nodemon``` or ```yarn add global nodemon```
- nodemon 실행: ```nodemon server.js```
(만약 보안 오류 뜰 때: 1. powershell 관리자 권한으로 실행해 ```executionpolicy```를 입력했을 때 ```Restricted```로 나오면 문제가 있는 것.
2.```set-exectionpolicy unrestricted```입력 후 ```y``` 입력)


<hr>

# 튜터에게 궁금한 점

궁금한점 작성 공간!

1. PropTypes를 실제로 많이 쓰는건지 궁금합니다.
2. ",'의 차이에 대해 헷갈리는 것 같습니다.
3. non-blocking IO에 대해서 알려주시면 좋을 것 같습니다.
````
