# 이번주 리뷰

<br>
Github에 써놓다가 저장을 안해놨더니 중간에 써놓은 게 날라가서 기억나는 부분을 포함해 다시 쓰게 됐네요 ,,
 
- 동기가 면접 때 React를 사용한 이유에 대해서 물어봤다고 했다. 그 순간 나는 이에 대해서 딱 정확히 대답하며 아는척 할 수 없었다.

## 리액트를 사용하는 이유

동적으로 UI 를 표현해야된다면 처리해야 할 이벤트도 다양해지고, 관리해야 할 상태값도 다양해지고, DOM 도 다양해지게 된다. 이렇게 변할 때마다 DOM을 어떻게 업데이트 해야할지 규칙을 정하는 것보다 이를 한번에 수행하는 Virtual DOM을 사용해 렌더링 해주는 것이 React이다.
Virtual DOM은 메모리에 가상으로 존재하는 DOM 으로서 그냥 JavaScript 객체이기 때문에 작동 성능이 실제로 브라우저에서 DOM 을 보여주는 것 보다 속도가 훨씬 빠르다.

## defaultProps

> 컴포넌트에 props 를 지정하지 않았을 때 기본적으로 사용 할 값을 설정하고 싶을 때 사용

```jsx
import React from "react";

function Hello({ color, name }) {
  // App.js
  return <div style={{ color }}>안녕하세요 {name}</div>;
}

Hello.defaultProps = {
  name: "이름없음",
};

export default Hello;
```

```jsx
import React from "react"; // Hello.js

function Hello(props) {
  return <div>안녕하세요 {props.name}</div>;
}

export default Hello;
```

![image](https://user-images.githubusercontent.com/50645183/102776120-8562c280-43d1-11eb-8064-49c5260a052c.png)

## props.children

> 값을 사용하는 곳에서 값을 정하는 것

```jsx
import React from "react"; // App.js
import Hello from "./Hello";
import Wrapper from "./Wrapper";

function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" />
      <Hello color="pink" />
    </Wrapper>
  );
}

export default App;
```

```jsx
import React from "react"; // Wrapper.js

function Wrapper({ children }) {
  const style = {
    border: "2px solid black",
    padding: "16px",
  };
  return <div style={style}>{children}</div>;
}

export default Wrapper;
```

## JS filter 내장함수

> 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환

```jsx
// 정수 배열에서 5의 배수인 정수만 모으기
var arr = [4, 15, 377, 395, 400, 1024, 3000];
var arr2 = arr.filter(function (n) {
  return n % 5 == 0;
});
console.log(arr2); // [15, 395, 400, 3000]
```

```jsx
//  3이 제외된 배열을 만들고 싶을 때,
array.filter((num) => num !== 3); // [1, 2, 4, 5]
```

# 튜터에게 궁금한 점

궁금한점 작성 공간!

- props.children에 대해서 정확한 쓰임새를 알고 싶습니다 !
