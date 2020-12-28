# 이번주 리뷰<br>

# [React 리액트 기초부터 쇼핑몰 프로젝트까지]
## PART 1. 블로그 제작 & 기초 (14강중 10강 완료)
## (1) 리액트 설치와 개발환경 셋팅
- 터미널에서 ```npx create-react-app 프로젝트명```(여기서 npx는 리액트 셋팅 다된 boilerplate 만들기 쉽세 도와주는 라이브러리)            
- 해당 프로젝트를 열고 src 밑에 있는 ```App.js```가 메인 개발 파일이 된다.              
- 코드 짠걸 ```npm start```를 통해서 미리 볼 수 있다.               
- 프로젝트 파일에서 ```node_modules```는 라이브러리를 모은 폴더 / ```puvlic```은 static 파일 보관함 / ```src```는 소스코드 보관함


## (2) JSX를 이용한 HTML 페이지 제작                   
- ```App.js```에서 태그에 class를 주고 싶다면 ```<div className="클래스명">```을 이용한다. 기존에 class로 주던거라고 생각하면 됨!        
- 리액트의 데이터 바인딩은 ```{변수명, 함수}```을 통해서 한다. 데이터바인딩이 쉬워진다! 이 중괄호는 src, id, href 등 정말 다양하게 쓰일 수 있음     
- jsx에서 style 속성을 집어넣을 때, ```style={오브젝트 자료형으로 만든 스타일}```을 통해서 하는데, 우리가 알던 font-size와 같은 애들은 camelCase 형태로 속성명을 바꿔줘야 한다.
```jsx
import logo from './logo.svg';
import './App.css';

function App() {

  let posts = '리액트 시작!';

  return (
    <div className="App">
      <div className="black-nav">
        <div style={{color:"yellow", fontSize:'30px'}}>개발 Blog</div>
        <h4>{ posts }</h4>
    </div>
  );
}
export default App;
```

## (3) 중요한 데이터나 자주 바뀌는 데이터는 state로 
데이터는 변수나 **state**를 이용하여 담는다. 이때 state는 ```useState()```를 이용하여 만든다.                 
상단에 ```import React, {useState} from 'react'```을 통해 import해주고 사용 가능하다.           
```state```는 문자, 숫자, 배열, 오브젝트 모두 저장가능하다. 그리고 useState결과로 [state 데이터, state 데이터 변경함수]가 나온다.        
**Q. state를 이용해야 하는 이유는 무엇일까?**               
바로 state를 이용하여 담은 데이터에 변경이 일어나면? HTML이 자동으로 렌더링이 된다. 이는 웹앱에서 중요한 포인트                 
자주 바뀌는 데이터나, 중요한 데이터는 state로 해주자!


## (4) 버튼에 기능개발과 state 변경하는 법
버튼을 눌렀을 때 이벤트가 발생하는 것은 ```onClick```이라는 것을 알고 있다. react에서도 똑같다.         
```onClick={클릭될 때 실행할 함수}``` 또는 es6 문법을 이용하여 ```onClick={()=>{실행할 내용}}```하면 된다.
강의에서 버튼 클릭시에 해당 글제목 하나가 바뀌는 것을 각자 실습해보라고 하셨는데, 변경시에는 state 데이터 변경함수를 써야한다!      
특히 처음에는 나도 아무생각 없이 ```글제목변경(글제목[0]='겨울 과일 추천')```이라고 생각했었다.          
하지만 그렇게 하니깐 아예 글제목이라는 변수의 배열이 겨울 과일 추천이라는 글자로 바뀌는 것이었다. 아예 바꾸려면 아래와 같이 전체 배열을 다 적어줘야한다.     
그리고 state는 직접 건들지 않는것이 좋다고 한다. deep copy를 이용하여 복사 후에 손대도록! 복사해서 갈아치운다는 느낌으로 이해하면 된다고 한다.  
```jsx
function App() {

  let posts = '강남 고기 맛집';
  
  let [글제목,글제목변경] = useState(['겨울 음식 추천','겨울 옷차림 추천','감기 예방 과일 추천']);
  let  [따봉, 따봉변경] = useState(0)

  function 제목바꾸기(){
    var newArray = [...글제목];  //spread operator를 이용하여 deep copy를! 값 공유가 아닌 서로 독립적인 값을 가지는 복사
    newArray[0] = '겨울 과일 추천';
    글제목변경(newArray);
  }

  return (
    <div className="App">
      <div className="black-nav">
      <div style={{color:"gray", fontSize:'30px'}}>개발 Blog</div>
      </div>
      <button onClick={제목바꾸기}>버튼</button>
      <div className="list">
        <h3>{글제목[0]}<span onClick={()=>{따봉변경(따봉+1)}}> 👍🏻 </span>{따봉}</h3>
        <p>12월 14일 발행</p>
        <hr/>
      </div>
      <div className="list">
        <h3>{글제목[1]}</h3>
        <p>12월 14일 발행</p>
        <hr/>
      </div>
      <div className="list">
        <h3>{글제목[2]}</h3>
        <p>12월 14일 발행</p>
        <hr/>
      </div>
    </div>
  );
}

export default App;

```

## (5) Component : 많은 div들을 한 단어로 줄이고 싶을 때
react에서는 return 소괄호 안에  ```<div>```가 연달아 있을 수는 없다. 오직 하나의 html 태그만 시작하고 끝난다.               
여러개를 평행, 연속해서 쓰고 싶으면? 이들을 전체를 ```<div>```로 감싸줘야한다. App.js에서도 className이 App인 div로 전체가 감싸져있다.               

HTML이 길어지는 경우 복잡해보일 수 있다. 이를 줄여서 쓸 수 있는 방법이 ```Component``` 이다.                
만드는 법은 간단하게, App 밖에 함수를 만들고 안에 원하는 내용의 html을 넣고 사용하면 끝             
이름 같은 경우에는 대문자로 시작해야하며, 마찬가지로 return()에는 오직 하나의 태그로 감싸져있어야 한다!                 

Component를 사용하면 반복출현하는 html 코드나, 자주 변경되는 html ui 그리고 다른 페이지 만들 경우에 용이하다.       
하지만 state를 쓸 때 복잡해지고, 특히 상위 Component에서 만든 state를 쓰려면 props 문법을 이용해야 한다고 함.


## (6) 클릭하면 동작하는 UI 만드는 법
리액트에서 HTML UI를 조건에 따라 보여주고 싶다면 ```삼항 연산자```와 ```state``` 이용하면 된다.              
조건을 if문을 이용하면 되는 거 아닌가 싶을 수도 있지만, 리액트 중괄호 내에서는 if문을 사용할 수 없다고 한다.                    
``` 조건식 ? 참일 때 실행할 코드 : 거짓일 때 실행할 코드``` 형식으로 사용하는 자바스크립트 문법이다.                           
```state```는 조건에 맞게 변경함수를 이용하면 된다.       

이번 강의에서는 버튼을 클릭하면 modal창이 열리고 닫히는 것을 구현하라고 숙제를 냈는데, 소소하게 해보는 재미가 있는 것 같다! ㅎㅎ                
```jsx
let [modal, modal변경] = useState(false); //modal창을 켜고 닫는 스위치
//생략
<button onClick={()=>{modal변경(!modal)}}>버튼</button> //onClick에서 버튼이 눌리면 값을 반대로 바꾸도록 modal변경 함수를 사용한다.
      {
        modal === true
        ? <Modal/>
        : null //아무것도 남기고 싶지 않다. 빈 HTML을 의미한다.
      }
```

## (7) map : 많은 div들을 반복문으로 줄이고 싶을 때
앞서 했던 예제들에서 반복되는 div코드가 있었다. 이들을 줄이기 위해서 for문을 쓰면 되지 않을까? 싶었는데 이번 강의부분에서 나왔다.       
먼저 JSX에서 for 반복문을 직접 쓸 수는 없다고 한다. 앞에 if문이 안됐던 것처럼 중괄호 안에는 함수나 변수 같은 것만 입력이 가능하다.          
바로 이 때 ```map```함수를 이용하면 된다. map 함수는 es6 강의 때 했던 부분이라 이해하기 쉬웠다.     
다시 한 번 정리하자면, array안에 모든 자료에 대해 같은 작업을 각각 시켜주고 싶을 때 쓰는 함수이다.     
```arr.map(callback[, thisArg])``` //return이 필수적이다.       
아래와 같이 반복문을 사용하면 된다.    
```jsx
{
    글제목.map(function(a){ //a라는 parameter는 array안에 있던 하나하나의 데이터를 의미한다
    return (
        <div className="list">
            <h3>{a}</h3>
            <p>12월 14일 발행</p>
            <hr/>
        </div>
        )
    })
}
```
만약에 일반적인 for문을 쓰고 싶다면, 중괄호 안에 쓰일 수 없으니 따로 함수를 만들어서 써야 한다.     
여기서 div에 관한 내용들을 array 자료형에 보관하는 이유에 대해서 말씀해주셨는데,      
JSX에서는 array에 HTML 요소들이 담겨 있어도 잘 렌더링 시켜줘서 그렇다구 한다.       

## (8) props : 자식이 부모의 state를 가져다쓰고 싶을 땐 말하고 써야 한다.
현재 App이라는 컴포넌트 안에 Modal이라는 컴포넌트가 들어가 있다. 이들은 부모 자식 관계이다.     
자식이 부모에서 정의된 state를 쓰고 싶다면 props를 이용해야 한다.       
App의 자식 컴포넌트인 Modal이 App의 글제목이라는 state를 사용해 데이터 바인딩을 하려고 한다.            
아래와 같은 스텝으로 이뤄진다.              
1. <자식컴포넌트 전송할이름={state명}> (보통 state명과 전송할 이름을 똑같이 한다고 한다.)
2. 자식 컨포넌트 선언하는 function안에 파라미터를 하나 만들어 준다. {props라는 이름을 암묵적으로 사용}
3. props.전송할이름 으로 사용하면 된다.  

```jsx
{
    modal === true
    ? <Modal 글제목={글제목}></Modal>
    : null
}
//생략
function Modal(props){ //부모에게 전달받은 props가 여기에!
  return(
    <div className="modal">
      <h2>제목 {props.글제목[0]}</h2>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```

```props```에는 파라미터에 전송한 모든 props 데이터가 들어가있다.       
또 ```props```는 Immutable하다고 하는데, 이는 props는 받아오는 것만 할 뿐 수정할 수는 없어서 그런 것이다.       


# 튜터에게 궁금한 점
리액트에서는 그러면 for문은 잘 안쓰고 대부분 map을 이용해서 구현하나요?