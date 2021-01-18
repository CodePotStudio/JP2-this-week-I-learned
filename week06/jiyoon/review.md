# 이번주 리뷰

# 벨로퍼트와 함께하는 모던 리액트       
지난번에 코딩애플의 강의를 리액트 강의를 완주했었다!    
강의 자체의 난이도는 어렵지 않았지만, 전체적인 흐름을 잡지 못한 것 같아서 복습겸 선택했다!      
쭉쭉 읽어나가면서 복습하는 것을 목표로 했다..!       
지난 강의에서 부족한 부분이나 다루지 않은 부분을 초점으로 정리해나가는걸로         

## 1장 
## 리액트는 어쩌다가 만들어졌을까?       
저번에도 리액트를 왜 쓰는지에 대한 이야기를 한적이 있었는데, 그것과 같은 맥락       
리액트를 쓰는 이유는 컴포넌트 단위로 재사용이 가능하며, jsx을 통한 데이터 바인딩이 기존보다 편해진다.           
그리고 state가 변경되면 재랜더링 된다는 점도 있다. 여기까지는 내가 실제로 저번 강의를 들으면서 정말 편하다고 느꼈던 부분이었다.             
마지막으로 virtual dom을 사용한다는 것인데, virtual dom이 정확히 뭔지 왜 dom보다 좋은건지에 대한 정확한 이해를 하지 못하고 넘어갔었다...                      
그래서 (https://velopert.com/3236) 여기 글을 읽고 virtual dom에 대해서 잘 정리된거 같다?!(아마도)      
dom은 변화가 생기면 렌더트리를 재생성하고 그 과정에서 연산을 할 일이 많아지게 된다.     
virtual dom은 변화를 우선 가성의 dom에 먼저 적용하고 최종 결과를 실제 dom에 전달하기에 연산의 양이 줄고 성능 개선으로 이뤄지는 것이다.          
거기에 더불어 virtual dom은 최종 결과물 즉, 변화에 대한 정보를 관리 및 자동화 해준다는 장점이 있다.         
(리액트 diff 알고리즘과 virtual dom에 관한 글 : https://velog.io/@naamoonoo/리액트는-어떻게-작동할까-Diffing-3주차-회고)


## props를 통한 컴포넌트에게 값 전달    
1. defaultProps를 통하여 props의 default값을 지정할 수 있다.        
큰 내용은 아니지만 이런 방법도 있군아 했던 부분~        
```jsx
import React from 'react'

function Hello(props){
    return <div style={{color:props.color}}> Hello! {props.name}</div>
}

Hello.defaultProps ={
    name:'no name'
}

export default Hello
```    
2. props.children을 통해서 컴포넌트 태그 사이의 넣은 값을 조회 즉 보고자 할때 사용한다.     
```jsx
import Hello from './Hello'
import React from 'react'
import Wrapper from './Wrapper'
function App() {
  return(
    <Wrapper>
      <Hello name='react' color="red"/>
      <Hello color="pink"/>
    </Wrapper>
  )
}

export default App;
```
Wrapper라는 컴포넌트 안에 Hello라는 컴포넌트가 있는 상태에서 Wrapper에 children을 넘겨주어야 Hello 컴포넌트가 보이게 된다.
```jsx
import React from 'react'

function Wrapper({children}){
    const style = {
        border:'2px solid black',
        padding:'16px'
    };
    return(
        <div style={style}>
            {children}
        </div>
    )
}
export default Wrapper;
```
## 6. 조건부 렌더링~ 9. 여러 개의 input 상태관리하기      
조건문이 간단하다면 역시 삼항연산자나 &&연산자를 사용!  
비구조 할당과 spread연산이 나오는데, 순간 헷갈려서 다시 찾아봤었다.         
(참고: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

<br>


## 10. useRef 로 특정 DOM 선택하기
리액트 사용시에도 특정 dom을 직접 선택해야할때가 있다. 그때 사용하는 것이 바로 ref다.(크기 가져오거나 포커스 같은 거 맞출때)                 
함수형 컴포넌트에서 ref를 사용할 때, ```useRef```라는 훅 함수를 사용한다.       
방법은 useRef() 를 통하여 ref 객체를 만들고, 이를 우리가 건들고자하는 특정 dom에 ref 값으로 설정해주면 된다.        
```jsx
import React, { useState, useRef } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: ''
  });
  const nameInput = useRef();

  const { name, nickname } = inputs; 

  const onChange = e => {
    const { value, name } = e.target; 
    setInputs({
      ...inputs, 
      [name]: value 
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: ''
    });
    nameInput.current.focus();  //ref 객체의 current는 우리가 원하는 dom을 가르킨다.
  };

  return (
    <div>
      <input
        name="name"
        placeholder="이름"
        onChange={onChange}
        value={name}
        ref={nameInput} //건들고자 하는 dom에 ref 속성을
      />
      <input
        name="nickname"
        placeholder="닉네임"
        onChange={onChange}
        value={nickname}
      />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```
이 예제는 초기화 버튼을 누르면 첫번째 input 박스에 포커스가 가도록 하는 ref 예제였는데, 앞서 말한 것처럼            
```const nameInput = useRef();```로 ref 객체를 만들고 이를 input박스 안에 ref값을 설정해줬다.           
우선 저번 강의보다 이 강의안..? 이 훨 이해가 잘 갔다. 뭐 저번에 강의 들어서 그럴 수도 있지만,,ㅎㅎ          
뭔가 코딩 애플 들을때, 따라서 이 강의안들을 봤으면 좋았을 것 같다는 생각                
<br>

## 11. 배열 랜더링하기(key값이 필요한 이유)
동적인 배열을 렌더링 할 때는 map함수를 쓰는 것이 좋다.      
map은 배열 안의 각 원소를 변환할 수 있고, 그 결과로 새로운 배열이 만들어지기 때문이다.      
이전에 질문으로 key값이 왜 필요한지 여쭤봤었는데, 이젠 답할 수 있다!        
리액트가 변경된 사항을 확인하는데 있어서 필수적인데, 이는 리액트가 diff 알고리즘을 통해서 효율적으로 업데이트 하기 대문이다.       
그래서 식별을 위해서 고유한 key값이 있어야 한다.            
이번 강의안의 예제들을 보니 key값이 없으니 정말 비효율적으로 업데이트 하는군아를 느꼈다...!         
<br>

# 튜터에게 궁금한 점
이번에는 없습니다!