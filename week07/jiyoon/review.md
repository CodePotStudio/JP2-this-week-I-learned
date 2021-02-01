# 이번주 리뷰

# 벨로퍼트와 함께하는 모던 리액트
저번주에 이어서 리액트 입문 1장을 마저 공부하였다!

## 12. useRef 로 컴포넌트 안의 변수 만들기
useRef로 특정 DOM을 선택하는 것 이외에도 컴포넌트 안에서 조회 및 수정을 할 수 있는 변수를 관리할 수 있다고 한다.            
무슨 말인지 단번에 와닿지 않아서 여러번 봤던 것 같다.           
useRef로 관리하는 변수들은 값이 바뀐다고 해서 state처럼 리렌더링이 되지 않는다고 한다.          
useRef에서의 current가 인자로 넘어온 초기값을 할당받는데, 이 속성이 값을 변경해도 재랜더링 되지 않고 랜더링되도 속성값이 유실되지 않는다고 한다.       
아래 코드를 검색하다가 보고 이해했다! 세상에 똑똑한 사람들이 많아서 공부하기 편해졌다,,,              
정말 콘솔창을 보니 useRef로 관리되는 intervalId의 경우에 위의 특징을 모두 보여줬다.         
```jsx
import React, { useState, useRef } from "react"

function ManualCounter() {
  const [count, setCount] = useState(0)
  const intervalId = useRef(null)
  console.log(`랜더링... count: ${count}`)

  const startCounter = () => {
    intervalId.current = setInterval(() => setCount((count) => count + 1), 1000)
    console.log(`시작... intervalId: ${intervalId.current}`)
  }

  const stopCounter = () => {
    clearInterval(intervalId.current)
    console.log(`정지... intervalId: ${intervalId.current}`)
  }

  return (
    <>
      <p>자동 카운트: {count}</p>
      <button onClick={startCounter}>시작</button>
      <button onClick={stopCounter}>정지</button>
    </>
  )
}
```
> 코드 올려진 포스팅 주소(https://www.daleseo.com/react-hooks-use-ref/)             
             
<br>

## 13. 배열에 항목 추가~ 15. 배열에 항목 수정하기      
> 사실 이부분은 크게 새로운 내용보다는 자바스크립트 복습?!          

* 배열에 항목을 추가할때는 절대 원본을 손대면 안된다는 것! 불변성을 지켜줘야 한다.        
그래서 spread나 concat을 사용해서 새로운 배열을 만들어서 항목을 추가해줘야 한다.                    
<br>

* 배열에 항목을 삭제하는 경우애도 불변성을 지켜줘야 하는데, 삭제의 경우에 filter를 이용하면 조건을 만족하는 경우만 해서 새로운 배열을 만들어준다.
```jsx
const onRemove = id => {
    setUsers(users.filter(user => user.id !== id)); //id 값이 다른 애들로만 배열을 새로 만드는 것, 즉 id값이랑 일치하는 칭구를 삭제하는 것이다
  };
```
<br>

* 배열에 항목을 수정하는 경우애는 map을 이용하여 업데이트를 해주는 과정을 진행했다~!     
앞에 세 단계를 통해서 나온 결과물은 다음과 같다.            
```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: ''
  });
  const { username, email } = inputs;
  const onChange = e => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value
    });
  };
  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'JIYUN',
      email: 'JIYUN@gmail.com',
      active: true
    },
    {
      id: 2,
      username: 'HELLO',
      email: 'HELLO@example.com',
      active: false
    },
    {
      id: 3,
      username: 'WORLD',
      email: 'WORLD@example.com',
      active: false
    }
  ]);

  const nextId = useRef(4);
  const onCreate = () => {
    const user = {
      id: nextId.current,
      username,
      email
    };
    setUsers(users.concat(user));

    setInputs({
      username: '',
      email: ''
    });
    nextId.current += 1;
  };

  const onRemove = id => {
    setUsers(users.filter(user => user.id !== id));
  };
  const onToggle = id => {
    setUsers(
      users.map(user =>
        user.id === id ? { ...user, active: !user.active } : user
      )
    );
  };
  return (
    <>
      <CreateUser
        username={username}
        email={email}
        onChange={onChange}
        onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
    </>
  );
}

export default App;
```
그래도 예전에는 리액트 하시는 분들 코드 보면 도통 이해가 안갔는데, 이제는 이해하고 넘어가서 좋다 ㅎㅎ            
<br>

## 16. useEffect를 사용하여 마운트/언마운트/업데이트시 할 작업 설정하기         
useEffect Hook은 컴포넌트가 마운트/언마운트/업데이트 시에 해야할 작업을 처리할 수 있다.     
이 부분은 코딩애플에서 강의를 들을 때, 너무 간단하게 지나가서 벨로퍼트님 이 부분을 본적이 있어서 어렵지 않게 이해했다!          
다시 한번 정리하자면, useEffect는 첫번째 파라미터로 함수를 받고 두번째 파라미터로 deps를 받는다.            
이때 deps를 따로 주지 않는다면, 마운트시에만 useEffect에 있는 함수가 호출된다.      
그리고 함수는 반환을 할 수 있는데 이것을 cleanup함수라고 한다. 뒷정리를 위한 것인데,       
의도치 않는 결과를 낼 수 있기에 정리해주는 것이 좋다!(예를 들어서 setTimeout과 같은 것을 사용했다면, clearTimeout을 해주는 것이 좋음!)              
```jsx
useEffect(()=>{
        let timer = setTimeout(()=>{alert변경(false)},2000) ;
        console.log("안녕");
        return ()=>{clearTimeout(timer)} //뒷정리 해주기
    },[alert]);
```     
<br>

## 17. useMemo를 사용하여 연산한 값 재사용하기      
useMemo Hook은 성능 최적화와 관련된 훅으로, 내가 원하지 않는 애들까지 재렌더링이 되는 경우가 발생할 때 도움을 준다.   
이게 작은 토이 프로젝트 말고 컴포넌트가 크면 재랜더링 부담이 심해지기 때문에 이를 위해서 사용한다고 함!              

그런데 저번에 코딩 애플에서는 ```memo```를 했었는데..? 이건 ```useMemo```라서 이름이 바뀐건가 했는데?!  찾아보니            
차이점은 ```React.memo```는 HOC라는 컴포넌트를 인자로 받아 새로운 컴포넌트를 다시 return 해주는 함수로, 클래스형과 함수형 컴포넌트 모두 사용가능하다고 한다.          
```useMemo```는 hook으로 함수형 컴포넌트 안에서만 사용가능하다!         
기능은 둘다 변하지 않으면 리렌더링 되지 않고 이전에 기억된 결과를 반환하는 것이다.      


사용 방법은 ```import React, {useEffect, useMemo} from 'react';``` memo를 임포트 해주고,    
첫번째 파라미터에는 연산이 정의된 함수를 두 번째 파라미터에는 deps배열을 넣어준다!          
```jsx
  const count = useMemo(() => countActiveUsers(users), [users]);
  return (
    <>
      <CreateUser
        username={username}
        email={email}
        onChange={onChange}
        onCreate={onCreate}
      />
      <UserList users={users} onRemove={onRemove} onToggle={onToggle} />
      <div>활성사용자 수 : {count}</div>
    </>
  );
```
<br>

## 18. useCallback 을 사용하여 함수 재사용하기      
useCallback은 useMemo를 기반으로 만들어진 훅으로, 특정 함수를 재사용 하고 싶을 때 사용된다.     
props가 바뀌지 않았으면 virtual dom에서 조차 리렌더링을 시키지 않으려고 사용한다고 하는데...            
그저 끄덕이는 리액트 초보 ㅎㅎ          

아무튼 사용법은 useMemo와 같이 import해주고 재사용하고자 하는 함수에 useCallback으로 아래와 같이 감싸주면 된다.     
```jsx
const onToggle = id => {    //재사용하고자 하는 함수
  setUsers(
    users.map(user =>
      user.id === id ? { ...user, active: !user.active } : user
    )
  );
};
//
const onToggle = useCallback(   //이렇게 감사주면 된다!
    id => {
        setUsers(
        users.map(user =>
            user.id === id ? { ...user, active: !user.active } : user
        )
        );
    },
    [users]
);
```     
여기서 주의할 점은 함수 안에 변경되는 상태 또는 props가 있다면 꼭!! deps 배열안에 넣어줘야 한다고 한다.         
<br>

## 21. 커스텀 Hooks 만들기  
반복되는 로직들은 커스텀 훅을 만들어서 재사용할 수 있다고 한다..        
보통 커스텀 훅을 만들때는 use로 시작한다고 한다(오호랏)     
만드는 방법은 그냥 안에 useState나 useEffect와 같은 훅으로 기능 구현 해주고 반환해주면 된다.            
이 부분하면서 슬슬 코드가 길어지니깐 알았는데 헷갈려지고 이래서..ㅠㅠ 먼가 리액트는 조립하듯이 레고? 같아서 잠깐        
정신 놓으면 이게 무슨 코드였지 하고 헷갈린다. 익숙하지 않아서 그런 것 같다.. 아직 arrow와 낯가리는 중       
<br>

## 23. Immer를 사용한 더 쉬운 불변성 관리       
배열이나 객체를 직접 건들면 안되는 것과 그래서 배열은 spread이용해서 복사하고 수정도 map과 같은 함수를 이용한다는 것은 이제 잘 알고 있다      
그런데 앞에서 예제코드 하면서도 느꼈지만 아직은 더 친해져야 할 arrow 함수와 합쳐져서 앞에 말한 과정들이 굉장이 한 눈에 안들어온다..     
그런데 이것을 immer라는 라이브러리를 통해서 간단하게 구현할 수 있다고 한다!         
immer는 불변성 관리를 대신 해주는 친구인데, 우선 설치를 해주고 ```import produce from 'immer';```을 통해서 불러와줘야 한다.     
그리고 사용은 첫번째 파라미터에는 수정하고 싶은 상태, 두번째 파라미터는 업데이트 정의 함수를 넣어준다.      
```jsx
const nextState = produce(state, draft => {
  draft.number += 1;
});
```
이게 가능하다니...! 신기하다고 생각하고 마저 글을 보는데,,!    
성능적으로 immer를 사용하지 않은 코드가 더 좋고, 배열이 객체 깊은 곳에 위치하지 않는 경우에는 그냥 전에 했던 방식들이 낫다고 한다.      
<br>

이렇게 해서 1장 끝! 이제 투두리스트로 가즈아👏 👏 👏        
뭐라도 만들면서 직접 부딪혀봐야 내것이 될 것 같다 암튼 1장 끝..!    


<br>

# 튜터에게 궁금한 점
1. immer를 실제로 많이 사용하나요? 마지막쯤에 immer를 사용하면 느리다고 해서 궁금해졌습니다..!