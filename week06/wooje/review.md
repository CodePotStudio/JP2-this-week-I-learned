# 이번주 리뷰

<br>

## Callback Function

> 다른 함수의 매개변수(파라미터)로 함수를 전달하고, 어떠한 이벤트가 발생한 후 매개변수로 전달한 함수가 다시 호출되는 것을 의미

- JS에서 비동기적 프로그래밍을 하기 위해 사용

```js
function print(callback) {
  callback();
}
```

```js
function fn_fakeAsync(callback) {
  calback();
}

console.log("------- fn_fakeAsync 호출 직전 -------");

fn_fakeAsync(function () {
  console.log("이게 비동기적으로 동작하길 바래");
});

console.log("------- fn_fakeAsync 호출 이후 -------");
```

- 결과

```js
------- fn_fakeAsync 호출 직전 -------
이게 비동기적으로 동작하길 바래
------- fn_fakeAsync 호출 이후 ------
```

## Babel

> 최신 JS 문법을 지원하지 않는 브라우저들을 위해서 최신 JS문법을 구형브라우저도에서 돌 수 있게 변환 시켜주는 것.

## Webpack

> 예전에는 웹사이트를 만들 때, JS파일 몇개와 CSS, HTML로 간단하게 만들었으나, 요즘은 여러 라이브러리 및 프레임워크의 등장으로 복잡하게 되버린 것들을 Bundle 시켜주는 것.

-> 원래 React App을 처음 실행하기 위해서는 Babel과 Webpack을 설정해줘야 했으나 create-react-app 명령어로 이를 하지 않고도 바로 시작할 수 있게끔 됐다.

## NPM

> NPM은 Node Package Manager의 줄임말로서 첫번째역할은 레지스트리 라이브러리들을 담는 역할이고, 두번째는 빌드를 하는 역할을 한다.

- `-g` 명령어를 넣어주면 글로벌로 다운 받아주는 것이고, 아니면 프로젝트 안에서만 받아지는 것이다.

## NPX

> 예전에는 `npm install -g create-react-app` 이렇게 React를 받았는데 이제는 npx를 활용할 수 있게 되었다. 그렇게 해서 Disk Space 낭비를 막고, 항상 최신 버전을 사용할 수 있게 되었다.

## 참고할만한 React 폴더 구조

```jsx
/components  -> 해당 페이지 관련
    /views -> Page들을 넣는 곳
    App.js -> Routing 관련 일처리
    Config.js -> 환경변수 같은 것들을 정하는 곳
/hoc -> Higher Order Component의 약자로 예를 들어 login이 안됐을 때 액션을 취해주는 컴포넌트들을 넣어두는 곳
/utils -> 여러 곳에서 사용되는 것들을 넣어두는 곳
```

# 튜터에게 궁금한 점

궁금한점 작성 공간!

- 이번에는 로그인 기능을 MongoDB의 mongoose를 활용해 express에서 만드는 것의 강의를 들었는데요 ,, 생각보다 많이 복잡해 이해하기가 매우 어려웠던 것 같습니다. 한번 더 정리하면서 봐야할 것 같아요 ,, 그래서 오히려 궁금한 게 없었네요 ,,
