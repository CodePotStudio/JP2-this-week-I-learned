# 이번주 리뷰

<br>
1. React 강의 OT : 왜 리액트가 필요한가

Web app : 모바일앱과 비슷한 사용감 (SNS- instargram, facebook, NAVER VIBE, Flipkart 등의 웹사이트)

Web app의 주요 라이브러리 : React/Angular/Vue (React가 사용자가 가장 많음)

Web app의 장점:

1. 모바일앱으로 발행이 쉬움
2. 앱처럼 뛰어난 UX
3. 그냥 웹사이트보다 비즈니스적 강점(고객 구매 결제량 증가)

---

2. 리액트 React 설치와 개발환경 셋팅 (2020 ver)
   ㅁ 셋팅
   Node.js 설치 ( https://nodejs.org/ )
   VS Code 설치 ( https://code.visualstudio.com/ )
   작업 폴더 생성
   VS Code로 작업 폴더 오픈
   VS Code로 앱 생성 : VS Code Terminal 에서 'npx create-react-app blog' 입력
   VS Code 앱 폴더 오픈
   코딩 시작

ㅁ Node.js 왜 필요한가?
create-react-app 라이브러리 때문 - npx, npm 사용하며, Node.js 설치시 같이 설치 됨.
(https://create-react-app.dev/docs/getting-started/)

ㅁ html은 어디에?
./public/index.html <- ./src/index.js <- ./src/App.js

ㅁ 작업폴더 구조
./node_modules/ : 라이브러리 설치되는 폴더
./public/ : static 폴더와 유사(build시 코드를 압축하지 않아서, 백업용으로도 활용)
./src/ : 코딩
./package.json : 설치한 라이브러리 목록(npm으로 설치할 때 자동으로 기록 됨)

---

3. JSX를 이용해 HTML 페이지 제작해보는건 처음이겠죠
ㅁ 태그에 class를 주고 싶으면?
<div className="클래스명">

ㅁ 리액트가 HTML코딩보다 편리한 이유?
리액트에서 데이터 바인딩 쉽게 할 수 있다 - { }의 활용

- 변수/함수 활용
let 변수(함수)명 = 데이터;
<div>
  { 변수(함수)명 }
</div>

- 이미지 넣는 방법
  import logo from './logo.svg';
  <img src={ logo } />

- style 넣는 방법 - 텍스트가 아닌 { Object }로 넣어야 함
<div style={{ color : 'blue', fontSize : '30px' }}>
  개발 Blog
</div>
** font-size의 '-'는 못 쓴다. (마이너스로 쓰이는 기호로 오류가 발생할 수 있음)
** camelCase로 속성명을 작성

---

4. 중요한 데이터는 변수말고 state로 만들랬죠
   ㅁ 데이터는 변수, state에 넣음
   let [a,setA] = useState('data'); // ['data',data 수정 함수]

state는 변수 대신 쓰는 데이터 저장 공간
useState()를 사용함
문자, 숫자, array, object 다 저장 가능

state를 사용하는 이유 : 웹이 App처럼 동작하게 만들고 싶어서

- 변수와 달리 state의 데이터가 바뀌면 새로고침 없이 html이 자동으로 다시 렌더링 됨

- 자주 바뀌는 중요한 데이터는 변수 말고 state로 저장해서 사용

ㅁ활용법
let [text, setText] = useState(['남자 코트 추천', '강남 우동 맛집', '맛집 기행']);

<div>{ text[1] }</div> // 강남 우동 맛집

---

5. 버튼에 기능개발을 해보자 & state변경하는 법
   ㅁ 컴파일 warnings 안보는 방법
   코드 젤 위에 /_ eslint-disable _/ 삽입

ㅁ 이벤트
<span onClick={ ( ) => { } }>...</span>

- ( ) => { } : 함수()

ㅁ state의 값은 state 변경 함수를 사용해서 수정해야 자동으로 다시 렌더링이 됨
let [a,setA] = useState('변경 전'); // a의 값은 '변경 전'
setA('변경 후'); // a의 값은 '변경 후'

---

6. 숙제 해설 : 블로그 글 수정버튼 만들기
   reference data type
   state 값은 immutable data이기 때문에 직접 수정하면 안되고, 변경 함수를 써야 함
   state 값을 복사할 때는 ...를 사용함 (spread operator)

---

7. Component : 많은 div들을 한 단어로 줄이고 싶은 충동이 들 때
   별도의 Component로 분리할 수 있다.

ㅁ Component 유의사항

1. 이름은 대문자로 시작
2. return( ) 안에 있는건 하나의 태그<></>로 묶여야 함 (fragment 태그)

ㅁ 어떤걸 Component로 만드는가?

1. 반복 출현하는 HTML 덩어리들
2. 자주 변경되는 HTML UI들 (자주 재렌더링이 필요한 부분)
3. 다른 페이지 만들 때

ㅁ Component 사용의 단점
다른 Component에서 만든 state 값을 사용하려면 props 문법을 이용해야 함

---

8. 클릭하면 동작하는 UI (모달창) 만드는 법

- 클릭하면 <Modal /> 등장하도록 하려면?
  > 여러분이 코드를 잘 짜시면 됩니다.

ㅁ JSX에서 if ( ) { }; 필요하면, 삼항연산자를 사용
1 > 0 ? console.log('맞아요') : console.log('틀려요')

ㅁ 모달창 열고 닫는 방법으로는 삼항연산자와 state에 상태 값을 저장해서 사용할 수 있음

---

9. map : 많은 div들을 반복문으로 줄이고 싶은 충동이 들 때
   ㅁ map( ) 사용
   let array = [1,2,3];
   let newArray = array.map(function(a){ return a \* 2 });

---

10. props : 자식이 부모의 state를 가져다쓰고 싶을 땐 말하고 쓰셔야합니다
    Component 간에 state 사용은 부모가 자식에게 props로 넘겨줘야 함

1) <자식Component props명={state명} />

- 보통 props명은 state명와 동일한 이름으로 함

2. 자식Component에서 props 파라미터 입력 후 사용

---

11. (UI 제작 패턴) props를 응용한 상세페이지 만들기
    ㅁ map( ) 사용
    let array = [1,2,3];
    let newArray = array.map(function(a, i){ return a \* 2 }); // i는 0부터 1씩 증가하는 변수

---

12. input 다루기 1 : 사용자가 입력한 글을 변수에 저장하는 법
    <input onChange={ (e) => { setState(e.target.value) } } />

---

13. input 다루기 2 : 블로그 글발행 기능 만들기
    array.unshift(a) // array의 맨 앞에 a 추가

ㅁ 변수를 안만들고 변수 자리에 함수를 넣는 것은 오류를 일으킬 수 있다. 내가 잘 모르니..

---

14. class를 이용한 옛날 옛적 React 문법

---

---

1. 쇼핑몰 프로젝트 : 프로젝트 생성 & Bootstrap 설치
   yarn 설치 ( https://classic.yarnpkg.com/ )
   npm install something은 yarn add something로 설치가 가능함

Bootstrap 이용하기 ( https://react-bootstrap.github.io/ )
부트스트랩 cdn 파일을 다운로드 받아서, ./public/ 폴더에 넣고 사용할 수 있음

---

2. 평화로운 쇼핑몰 레이아웃 디자인시간
   부트스트랩 사용 (Navbar, Jumbotron)
   className="mr-auto" 왼쪽 정렬 / "ml-auto" 오른쪽 정렬
   className="row" 가로 12등분
   className="col-4" 가로 12등분 중 4칸
   className="col-md-4" 가로 12등분 중 4칸 & 모바일(<740?px)에서 세로로 정렬 \*이건 orginal 부트스트랩

React용 부트스트랩 ( https://react-bootstrap.netlify.app/ ) 에서 검색해서 사용
import { Navbar, Nav, NavDropdown, Form, FormControl, Button } from 'react-bootstrap';

---

3. 코드가 넘나 길어진다면 import / export 사용해보기;

---

4. 숙제 해설 : 상품목록 Component화 + 반복문 \*코드 참고하기 좋은 강의
   <img src={ 'https://.../shoes' + 변수 + '.jpg' }

\*props로 넘긴 index 사용
<img src={ 'https://.../shoes' + (props.i + 1) + '.jpg' }

---

5. React Router 1 : 셋팅과 기본 라우팅
   React Router 사용
   설치: yarn add react-router-dom

./src/index.js에 import { BrowserRouter } from 'react-router-dom'; \*라이브러리는 경로없이 이름만 넣어 사용(from '')
ㅁ App 감싸기
<BrowserRouter>
<App />
</BrowserRouter>

HashRouter / BrowserRouter 차이점:
HashRouter는 좀 더 안정적으로 라우팅 할 수 있게 도와줌

> url에 #이 붙는데, # 뒤의 내용은 서버로 전달이 안되므로 엉뚱한 요청을 피할 수 있고,
> 라우팅은 #뒤의 내용을 리액트가 처리 해 줌.
> 서버에 잘 못된 요청을 했을 경우, 서버가 404 에러를 낼 수도 있고. 등등
> BrowserRouter 사용하여 서버와 통신 할 경우, 서버에서 서버 라우팅 방지하는 API를 작성해둬야함
> (리액트에게 라우팅을 담당하도록 설정해주세요.)

App.js에 import { Link, Route, Switch } from 'react-router-dom';

<Route path="/" exact>
  <div>메인페이지에요</div>
</Route>
<Route path="/detail">
  <div>디테일페이지에요</div>
</Route>
<Route path="/어쩌구" component={ Modal }></Route> // HTML 말고 컴포넌트를 보여줄 때

---

6. React Router 2 : Link, Switch, history 기능
   component는 대문자로 시작, 파일명도.

<Link to="/">Home</Link>
<Link to="/detail">Detail</Link>

ㅁ커스텀 버튼
import { useHistory } from 'react-router-dom';
const history = useHistory();
onClick={ () => { history.push('/') } }

ㅁ 택1
<Switch>
<Route path="/"></Route>
<Route path="/detail"></Route>
<Route path="/:id"></Route>
</Switch>

---

7. React Router 3 : URL 파라미터로 상세페이지 100개 만들기
   <Route path="/detail/:id">
   <Detail shoes={ shoes[0] } />
   </Route>

/detail/:id/:id2 도 가능
import { useParams } from 'react-router-dom';
const { id, id2, id3 } = useParams();

ㅁ props에서 id 찾기
const product = props.shoes.find((item) => { return item.id == id }); // .find(item => item.id == id);
{ product.title }

---

8. styled-components를 이용한 class없는 CSS스타일링
   component가 많아지면, CSS 스타일링이 어려워진다.
   ex. component내에 class가 중복되어 스타일링 오류 발생 등.
   so. className 선언 없이 컴포넌트에 CSS를 직접 장착

설치: yarn add styled-components

import styled from 'styled-components';

let 박스 = styled.div` padding: 20px;`;
let 제목 = styled.dib` font-size: 25px; color: ${ props => props.색상 };`;
<박스>
<제목 색상={'red'}>Detail</제목> // <제목 색상="red">
</박스>

---

9. 아니면 CSS대신 SASS를 쓰자 (SASS 문법 10분 총정리)
   설치: yarn add node-sass ( yarn add node-sass@4.14.1 )
   ㅁ 변수 사용 가능
   something.scss
   $메인칼라: #ff0000;
   .red {
   color: $메인칼라;
   }

ㅁ @import 파일경로 \*모든페이지에 필요한 CSS reset
body {
margin: 0;
}
div {
box-sizing: border-box;
}

ㅁ 셀렉터 대신 쓰는 nesting문법
// div.container h4 {
// color: blue;
// }
// div.container p {
// color: green;
// }

div.container {
h4 {
color: blue;
}
p {
color: green;
}
}

ㅁ @extend 가능
ㅁ @mixin, @include 가능

---

10. Lifecycle Hook (옛날사람) useEffect (요즘사람)
    ㅁ console warning 발생
    <Nav.Link><Link to="/">Home</Link></Nav.Link>
    -> <Nav.Link as={Link} to="/">Home</Nav.Link>

ㅁ Lifecycle Hook
class Detail2 extends React.Component {
componentDidMount(){
//Detail2 컴포넌트가 Mount 되고나서 실행할 코드
}
componentWillUnmount(){
//Detail2 컴포넌트가 Unmount 되기전에 실행할 코드
}
}

ㅁ useEffect
import React, { useEffect } from 'react';
컴포넌트가 mount / update 될 때
특정 코드를 실행할 수 있음
useEffect(() => {
let timer = setTimeout(() => { setAlert(false) }, 2000)
});

컴포넌트가 사라질 때 코드를 실행시킬 수도 있음
useEffect(() => {
return ( ) => { 실행할코드~ }
});

---

11. useEffect 숙제 풀이 & 나머지 기능
    ㅁ 컴포넌트가 mount / update 될 때 && alert, inputData, number1, number2 값이 바뀌었을 때 작동.
    useEffect(() => {
    let timer = setTimeout(() => { setAlert(false) }, 2000)
    }, [alert, inputData, number1, number2]);

}, [ ]); // 조건이 없을 땐, mount 될 때만 실행. (update 때는 실행 x)

setTimeout의 경우, 버그 나올 수 있다.
ex. 2000ms 후 실행인데, 시간 도달 전에 뒤로가기로 나갔을 때라던가.. 등
그래서 unmount 함수를 넣어줘야 한다.
useEffect(( ) => {
let timer = setTimeout(() => { setAlert(false) }, 2000)
return ( ) => { clearTimeout(timer) }
},[alert]);

---

12. 리액트에서의 Ajax 요청방법 & Ajax는 무엇인가
    Aajax 서버에 새로고침없이 요청을 할 수 있게 도와줌

요청 구분:
GET 요청 : 특정 페이지/자료 읽기, url입력
POST 요청 : 로그인/회원가입/글쓰기/검색 등, 정보를 입력하여 전송

사용법

1. jQuery 설치해서 $.ajax() 쓰든가
2. axios 설치해서 axios.get() 쓰든가 (vue, react 많이 씀, ie 9/11 지원)
3. 자바스크립트 fetch() 쓰든가 (최신 JS, 최신 브라우저만 지원)

axios 설치 : yarn add axios
import axios from 'axios';
axios.get('https://....json').then(( ) => { 성공하면 실행코드 }).catch(( ) => { 실패하면 실행 });
cf. fetch('https://....json').then(( ) => { 성공하면 실행코드 }).catch(( ) => { 실패하면 실행 });
fetch는 json을 object로 자동 변환해주진 않는다.

---

13. 리액트에서의 Ajax 요청방법 2 & 숙제풀이
    ㅁ state 수정
    .then(response => { setShoes([...shoes, ...response.data]) })

ㅁ 더보기 버튼을 2회 이상 누르는 작동
변수나 state로 버튼 누른 횟수를 저장하고, 횟수에 맞춰 새로운 URL로 데이터를 요청
/data2.json
/data3.json
/data4.json

ㅁPOST요청
axois.post('서버url', { id : 'a1234', pw : 1234 });

ㅁ페이지 로드하면서 ajax 요청은?
useEffect(( ) => {
axios.get('https://....json').then(( ) => { }).catch(( ) => { });
}, [ ]);

---

14. Component를 3개 중첩해서 만들면 state 전달은 어떻게 하죠?
    ㅁprops로 state를 보내라
    <Detail shoes={ shoes } stock={ stock } />
    function Detail(props){
    return ( <Info stock={ props.stock } /> )
    }
    function Info(props){
    return ( <p>재고 : { props.stock[0] }</p> )
    }

ㅁ 하위 컴포넌트가 상위 컴포넌트 state를 변경하려면.
상위 컴포넌트가 props로 보내준 state 변경함수를 사용하라

---

---

1. 만든 리액트 사이트 build & Github Pages로 배포해보기
   yarn build
   github.com에 New Repository 생성
   Repository name에 아이디.github.io 입력
   파일 업로드
   https://아이디.github.io

---

2. 컴포넌트 많을 때 props 쓰기 싫으면 Context API 쓰셈
   하위 컴포넌트들이 props없이 부모의 state 값을 사용할 수 있음.

export const contextStock = React.createContext();

<contextStock.Provider value={ stock }>
<컴포넌트>
</contextStock.Provider>

import { contextStock } from '../App.js';
const stock = useContext(contextStock);
{ stock }

const a = React.createContext()는 범위(또는 그룹)를 생성하는 것
const b = React.createContext()
그래서 여러개를 사용 할 수 있음

ㅁ Redux 라는 라이브러리 :
모든 컴포넌트 파일들이 같은 값을 공유 할 수 있는 저장 공간 생성 가능 + state 데이터 관리 기능

- 이걸 쓰라

---

3. Tab 만들기와 리액트에서의 애니메이션 (react-transition-group)
   react부트스트랩의 탭 활용
   https://react-bootstrap.netlify.app/components/navs/#base-nav
   Tabs

className="mt-5" margin-top : 5

ㅁ애니메이션 CSS 쉽게 부착하기(CSS Transition)
설치 : yarn add react-transition-group

import { CSSTransition } from 'react-transition-group';

<CSSTransition in={ true } classNames="" timeout={ 500 }> // in={ true } : 작동 스위치. true면 작동함, classNames="wow" : className아니다. Names다. 애니메이션 이름임, timeout={ 500 }: 500ms
<TabContent activeTab={ activeTab } />
</CSSTransition>

SCC에선
.wow-enter { // 애니메이션 시작 때 적용할 CSS
opacity: 0;
}
.wow-enter-active { // 애니메이션 동작 때 적용할 CSS
opacity: 1;
transition: all 500ms;
}

---

4. 세계최고로 쉬운 Redux 1 : props 싫으면 쓰세요

설치 : yarn add redux react-redux

index.js에
import { Provider } from 'react-redux';
import { createStore } from 'redux';

let store = createStore(() => { return [{ id : 0, name : '멋진신발', quan : 2 }] });

<Provider store={ store }>
<App />
</Provider>

컴포넌트에서
import { connect } from 'react-redux';

function mapStateToProps(state){
return {
state : state
}
}

function Cart(props) {
return { props.state }
}

export default connect(mapStateToProps)(Cart)

<Provider>로 감싸면 state 공유

사용 이유:

1. props 안쓰려고. (Context API 와 유사)
   복잡한 props 전송이 필요없이, 컴포넌트가 직접 꺼내 쓸 수 있다.

---

5. 세계최고로 쉬운 Redux 2 : reducer/dispatch로 데이터 수정하는 법
   사용 이유:

2) state 데이터 관리 가능

store 만들 때 state 데이터의 수정방법을 미리 정의해서 수정에 사용(reducer)

index.js에서 다시.
let initialState = [
{ id : 0, name : '멋진신발', quan : 2 },
{ id : 1, name : '멋진신발2', quan : 1 }
]

function reducer(state = initialState, action){
if ( action.type === 'QUAN_INCREASE' ){
let newState = [...state];
newState[0].quan++;
return newState
} else {
return state
}
};

let store = createStore(reducer)

컴포넌트에서
<button onClick={() => { props.dispatch({ type: 'QUAN_INCREASE' }) }}>+</button>

- app에서 state 값 수정에 오류가 발생하면, dispatch({ type: '액션' })을 찾아보면 쉽게 확인 할 수 있다.

---

6. 세계최고로 쉬운 Redux 3 : state와 reducer가 더 필요하면

import { combineReducers } from 'redux';

let store = createStore(combineReducers({reducer,reducer2}));

function mapStateToProps(state){
console.log(state);
return {
state : state.reducer,
stateAlert : state.reducer2
}
}

- 개별 컴포넌트 안에서만 쓰는 데이터는 redux 쓰지않고, useState 써라.

---

7. 세계최고로 쉬운 Redux 4 : dispatch할 때 데이터 실어보낼 수 있음

<button onClick={() => { props.dispatch({ type: 'QUAN_INCREASE', payload: { name : 'kim' } }) }}>+</button>

- if 문이 길어지면 switch문 사용
  function reducer(state = initialStateCart, action){
  if ( action.type === 'QUAN_INCREASE' ){
  let newState = [...state];
  newState.push(action.payload);
  return newState

- 리액트 강의가 이해하기 쉽고 매우 좋습니다!!

# 튜터에게 궁금한 점

라우팅 운영 방법에 대한 궁금증.
스파르타에서 실습했었던,
파이썬에서 라우트 관리하는게 나은지, 리액트 라우터로 관리하는게 나은지 궁금합니다.
