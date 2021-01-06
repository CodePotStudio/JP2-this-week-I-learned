# 이번주 리뷰

<br>

### Reducer

> 현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해주는 함수

```jsx
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```

## useReducer

> 상태를 업데이트하고 관리할 때 `useState`를 사용하는 것과 같은 방법의 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리시킬 수 있는 Hook

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
// state는 컴포넌트에서 사용할 수 있는 상태
// dispatch는 action을 발생시키는 함수
// reducer는 reducer함수
// initialState는 초기 상태
```

- 예제

```jsx
import React, { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
}

function Counter() {
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: "INCREMENT" });
  };

  const onDecrease = () => {
    dispatch({ type: "DECREMENT" });
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

### useState vs useReducer

> 컴포넌트에서 관리하는 값이 딱 하나고, 그 값이 단순한 숫자, 문자열 또는 boolean 값이라면 확실히 useState 로 관리하는게 편리

- 컴포넌트에서 관리하는 값이 여러개가 되어서 상태의 구조가 복잡해진다면 useReducer로 관리하는 것이 편리. 결정은 편한대로 본인이 하면 된다.

## useRef

> JS에서 특정 DOM을 선택해야 하는 상황이 React에서도 발생할 때 사용

- React에서는 `ref`라는 것을 사용
- 함수형 컴포넌트에서 `ref`를 사용할 때는 `useRef` Hook 사용한다

```jsx
import React, { useState, useRef } from 'react'; // InputTest.js
                                                // 초기화 시 input 태그에 focus 잡히는 기능

function InputTest() {
  const [text, setText] = useState('');
  const nameInput = useRef(); // Ref 객체 생성

  const onChange = e => {
    setText(e.target.value)
  };

  const onRest = () => {
    setText('');
    nameInput.current.focus(); // Ref 객체의 current 값은 선택하고자 하는 DOM을 가리킨다.
                               // DOM API focus()호출해 포커싱한다.
  };

  return (
    <div>
      <input
        name="name"
        onChange={onChange}
        value={text}
        ref={nameInput}            // 선택하고 싶은 DOM에 속성으로 ref값을 설정
        />

        <button onClick={onReset}초기화</button>
        <div>
          <b>내용: </b>
          {text}
        </div>
       </div>
      );
     }

     export default InputTest;
```

- useRef로 Component 안의 변수 관리하기
- useRef Hook의 다른 기능으로 컴포넌트 안에서 조회 및 수정 가능한 변수를 관리할 수 있다.
- useRef로 변수를 관리해 그 변수가 업데이트 된다고 그 컴포넌트가 재렌더링이 되지 않으므로 재렌더링 할 필요가 없을 때 useRef로 관리하는게 효율적이다.
- 주로 id, key값을 관리할 때 사용한다.

```jsx
import React, { useRef } from 'react'; // App.js
import UserList from './userList';

function App() {
  const users = [
    {
      id: 1,
      username: 'woo',
      email: 'woojerry@naver.com'
    },
    {
      id: 2,
      username: 'pop',
      email: 'pop@gmail.com'
    }
  ];

  const nextId = useRef(3); // 배열의 고유값 변수로 nextID설정
                            // useRef() 파라미터로 다음 id가 될 숫자 4를 넣어준다.
  const onCreate = () => {
    // 배열에 새로운 항목 추가하는 로직

    nextId.current += 1;  .. 파라미터 값을 넣어주면 해당 값이 변수의 current값이 된다.
  };
  return <UserList users={users} />;
}
export default App;
```

참고 <https://xiubindev.tistory.com/98>

- 결국 벨로퍼트 Todolist를 참고하여 완성은 했습니다. 이렇게 보니 정말 쉬운 것이었네요 ,,  
  거의 후반부 기능은 다 이해하면서 따라한 느낌이지만
  Context API와 Reducer를 활용해 기능을 추가하는 부분에 대한 이해가 된 것 같습니다. 참고용으로 좋았던 것 같아요.

# 튜터에게 궁금한 점

- useRef에 대해 한번 더 알려주셨으면 좋을 것 같아요 !
  (저는 변수를 관리하는 것 때문에 접하게 되었지만 다른 기능으로 DOM을 선택할 때 사용하는 ,, 이런 것이 좀 생소하네요)
