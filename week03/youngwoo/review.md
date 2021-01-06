# 3주차 리뷰
## ✏️ 서론
`Part.2 쇼핑몰 프로젝트 강의`를 들으면서 쇼핑몰을 만드는데 기본적인 `Layout`과 `메인페이지, 상세페이지`를 만들면서 기본적인 틀을 다졌다.

그럼 이번에는 마지막 파트인 `Part.3 실무에 필요한 부가내용`에서 장바구니 기능, 데이터를 효율적으로 관리하는 라이브러리인 `Redux`, `Lazy loading` 등등을 배워보면서 어떤 방식으로 실무에 적용하면 도움이 되는지 알아보자.


---

## ✏️ 본론

## 📍 build & Github Pages 배포하기
우리가 지금까지 만들었던 사이트를 `Github`에 배포할때는 작업하던 `App.js`파일 그대로 업로드하는게 아니라 `build`파일을 생성한 다음 올려야한다.

왜냐하면, `브라우저`는 `HTML, CSS, JS` 3가지 언어만 해석 할 수 있기 때문이다. 따라서 우리가 사용한 `React`의 `state`, `JSX`는 알아들을 수 없다.

여기서 궁금한 점이 생겼는데, `빌드(build)` 와 `컴파일(Compile)`의 차이는 무엇일까?

---

### 💡 `빌드(build)` VS `컴파일(Compile)`
1. 컴파일(Compile): 개발자가 작성한 소스코드를 컴파일러(Compiler)를 통해 바이너리 코드로 변환하는 과정을 말한다. 즉, <span style='color:blue'>소스코드를 컴퓨터가 이해할 수 있는 기계어로 변환하는 작업을 말한다.</span>

2. 빌드(build): 소스코드 파일을 <span style='color:blue'>실행가능한 소프트웨어 산출물</span>로 만드는 일련의 과정을 말한다. 

빌드에서는 컴파일, 테스트, 배포 등 과정이 포함 될 수 있고, 빌드 과정을 도와주는 도구를 빌드 툴이라고 한다.

2-1. 빌드 툴(Build Tool): 일반적으로 빌드 툴이 제공하는 기능은 전처리(Processing), 컴파일(Compile), 패키징(Packaging), 테스팅(Testing), 배포(Distribution) 기능들이 있다.

출처: https://freezboi.tistory.com/39

---

먼저, `state`, `JSX`, `<Component>`, `props` 이런 문법들을 전통적인 `HTML, CSS, JS` 언어로 바꿔주는 `컴파일(Compile)` 작업을 거쳐야한다.

>
1. terminal - npm run build
2. build - `index.html`, `CSS`, `JS` 파일을 모두 서버에 올리자.

그럼 내가 설정한 링크를 통해 리액트 화면을 볼 수 있다.

![](https://images.velog.io/images/abcd8637/post/2d15b65f-6dcd-462a-bf1b-a77d01af46a0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-21%2009.35.31.png)

`React`, `Vue`로 만든 `Web-App`들은 첫 방문시 필요한 파일을 전부 로드하기 때문에 파일이 커진다면 로딩시간이 길어질 수 있다. 트래픽을 줄이고 싶다면 `Component`를 `Suspense, lazy` 라이브러리를 사용해서 해당페이지에 들어갈때만 코드를 불러오는 방식을 사용하자.

출처: <a href='https://reactjs.org/docs/code-splitting.html#route-based-code-splitting'>공식문서</a>

---

## 📍 Tab UI, react-transition-group
Tab UI는 버튼을 누르면 각각 해당하는 `<div>`를 보여주는 방식이다.
앞서, 만들었던 <a href='https://velog.io/@abcd8637/%EC%BD%94%EB%94%A9%EC%95%A0%ED%94%8C-React-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EA%B8%B0%EC%B4%88%EB%B6%80%ED%84%B0-%EC%87%BC%ED%95%91%EB%AA%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EA%B9%8C%EC%A7%80-part.1%EB%91%90%EB%B2%88%EC%A7%B8%EC%9D%B4%EC%95%BC%EA%B8%B0#%EC%98%88%EC%A0%9C-1-button%EC%9D%84-%EB%88%8C%EB%A0%80%EC%9D%84-%EB%95%8C-%EC%97%B4%EA%B3%A0-%EB%8B%AB%ED%9E%88%EB%8A%94-%EC%B0%BD%EC%9D%84-%EB%A7%8C%EB%93%A4%EC%96%B4%EB%B3%B4%EC%84%B8%EC%9A%94'>열고 닫히는 창을 만들기 편</a>을 참고하면 된다. 

![](https://images.velog.io/images/abcd8637/post/01d50ace-99ae-467b-9127-f7e0876e3099/motion.gif)

코드는 다음과 같다.

``` javascript
<CSSTransition in={스위치} classNames='wow' timeout={500}>
    <TabContent 누른탭={누른탭} 스위치변경={스위치변경} />
</CSSTransition>

function TabContent(props) {
    useEffect(() => {
        props.스위치변경(true);
    })

    if (props.누른탭 === 0) {
        return <div>0번째 상품입니다.</div>
    } else if (props.누른탭 === 1) {
        return <div>1번째 상품입니다.</div>
    } else {
        return <div>나머지 상품입니다.</div>
    }
} 
```
애니메이션 부여하는 라이브러리는 `react-transition-group`인데, 간단하게 구현할때 편하다.

> terminal - npm install react-transition-group
> import { CSSTransition } from 'react-transition-group';
> 원하는 컴포넌트에 `<CSSTransition>으로 감싼다.
> `in, classNames, timeout` 속성을 넣는다.

`in:` 스위치, `true` 일때 애니메이션을 적용한다.
`classNames:` 어떤 애니메이션을 적용할지 작명하는 부분
`timeout:` 작동시간

이후 `CSS`파일에서 속성을 부여해주면 된다.
```css
/* 애니메이션 시작 할 때 */ 
.wow-enter{
  opacity: 0;
}

/* 애니메이션 동작 할 때 */
.wow-enter-active{
  opacity: 1;
  transition: all 500ms;
}
```
탭의 버튼을 누를 때 작동해야하므로 `state`를 만들자.
최종 코드는 다음과 같다.

```javascript
let [스위치, 스위치변경] = useState(false);

<Nav className="mt-5" variant="tabs" defaultActiveKey="link-0">
    <Nav.Item>
        <Nav.Link eventKey="link-0" onClick={() => { 스위치변경(false); 누른탭변경(0); }}> 리뷰 </Nav.Link>
    </Nav.Item>
    <Nav.Item>
        <Nav.Link eventKey="link-1" onClick={() => { 스위치변경(false); 누른탭변경(1); }}> QnA </Nav.Link>
    </Nav.Item>
</Nav>

<CSSTransition in={스위치} classNames='wow' timeout={500}>
    <TabContent 누른탭={누른탭} 스위치변경={스위치변경} />
</CSSTransition>

function TabContent(props) {
    useEffect(() => {
        props.스위치변경(true);
    })

    if (props.누른탭 === 0) {
        return <div>0번째 상품입니다.</div>
    } else if (props.누른탭 === 1) {
        return <div>1번째 상품입니다.</div>
    } else {
        return <div>나머지 상품입니다.</div>
    }
} 
```

---

## 📍 props 전송: Context, Redux
이전에 `Component` 안에 `Component`를 사용한 적이 있었다. 
변수를 보내줄때 `props`를 사용했는데, 끔찍했다. 😖 😖

`props`를 연속으로 사용하기 싫다면 `redux`, `Context API`를 사용하면 `props` 전송 없이도 하위 컴포넌트끼리 `state`값을 동일하게 공유 할 수 있다. (중첩된 컴포넌트가 많이 없을때는 그냥 `props`를 사용하자.)

---

### 📍 Context 문법
먼저, 같은 `state` 값을 공유하고 싶으면 `context`부터 만들자. 
`createContext()`라는 함수를 이용하면 그 변수는 특별한 `Component`가 된다.

```javascript
// App.js
let 재고context = React.createContext();

function App(){
    let [재고, 재고변경] = useState([10, 11, 12]);

    return (
        HTML ~
    )
}
```

이후, `state` 값 공유를 원하는 컴포넌트를 전부 감싸고, `value = {state 이름}` 을 집어 넣으면 된다.

간단하게 예를 들어 `Card`에 `props` 문법없이 전송하고 싶다면 다음과 같은 코드를 작성하면 된다.

```javascript
import React, {useState, useContext} from 'react';

function App(){
    let 재고 = useContext(재고context);
    return(
        <재고context.Provider value={재고}>
            <div className="row">
                {
                  shoes.map(function (n, i) {
                    return (
                      <Card shoes={shoes[i]} i={i} key={i} />)
                  })
                }
            </div>
        </재고context.Provider>
    )
}

function Card(props) {

  let 재고 = useContext(재고context);

  return (
    HTML~
  )

```

이후 해당 컴포넌트 내에서 `useContext()` 훅을 이용해서 원하는 `context`를 불러와야한다.


그럼 `<범위 />` 안에 있는 <span style='color:blue'>모든 HTML & 컴포넌트는 재고 state를 이용 할 수 있다.</span> `props` 전송없이도!

---

### 📍 Redux 문법 1
Redux는 애플리케이션 상태를 관리하기위한 오픈 소스 JavaScript 라이브러리이다. 
사용자 인터페이스 구축을 위해 React 또는 Angular와 같은 라이브러리와 함께 가장 일반적으로 사용된다. 

쉽게말하면, <span style='color:blue'>props 전송 없이도 모든 컴포넌트가 `state`를 사용할 수 있게 만들어준다.</span>

리액트를 이용한 사이트에서는 `redux`를 설치해 사용하는 곳이 많다.

출처: <a href='https://www.google.com/search?sxsrf=ALeKk01-SwTagQkRCmVQ2_-rPwHK2sxbrg%3A1608515380296&source=hp&ei=NP_fX4qQEKSXr7wPsvitkAE&iflsig=AINFCbYAAAAAX-ANRHQfR1yR0qAjzmBHbW1OCiOAlnMU&q=redux&oq=redux&gs_lcp=CgZwc3ktYWIQAzIECCMQJzIFCAAQsQMyBwgAEBQQhwIyAggAMgIIADICCAAyAggAMgIIADIECAAQQzICCAA6BwgAELEDEEM6BggAEAoQQzoICAAQsQMQgwE6BggAEAoQEzoICAAQChAeEBM6CggAEAUQChAeEBNQkARY2hBgxRFoBXAAeACAAXOIAe8FkgEDMC43mAEAoAEBqgEHZ3dzLXdpeg&sclient=psy-ab&ved=0ahUKEwiK-uze-t3tAhWky4sBHTJ8CxIQ4dUDCAg&uact=5'> 구글 </a>

### ✏️ [ 예제 1 ] `redux`를 사용해 장바구니를 완성하세요.
장바구니 예제를 통해 `redux`를 사용해보자.

먼저, `Cart.js` 폴더를 생성하고 `Bootstrap table` 레이아웃을 하나 추가한다.

테이블에서 속성은 다음과 같다.
`tr`: 가로줄
`td / th`: 세로줄

먼저, 테이블에 넣을 데이터는 `Cart.js`에 있는게 아니라 `redux`를 이용해 보관해보자.

>1. terminal - npm install redux react-redux
* redux: data를 엄격하게 관리하는 기능
* react-redux: `redux`를 `react`에서 쓸 수 있게 도와주는 기능
  
>2. `index.js` 파일을 열고 다음과 같이 설정한다

```javascript
import { Provider } from 'react-redux';
import { createStore } from 'redux';

let store = createStore(() =>{ return [{id: 0, name : '멋진신발', quan : 2}] })

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
      <Provider store={store}>
        <App />
      </Provider>
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);
```
>2-1. import { Provider } from 'react-redux'; 을 상단에 넣고
>2-2. 공유하고 싶은 `state`를 원하는 `Component`로 감싸면 된다.
>3. `<App>` 컴포넌트와 그 안에있는 모든 `HTML`, 컴포넌트들은 전부 `state`를 `props` 없이 사용할 수 있다.
4. `redux`에서 `state`를 만드려면 `createStore()` 함수를 사용해야한다.
4-1. 콜백함수에는 내가 원하는 `state` 초기값을 뱉어내면 된다.
5. `<Provider>`에 만든 `state`를 `props` 처럼 사용하면 된다.

이렇게 만들었으면, 실제로 `state` 데이터를 꺼내보자.

`Cart.js`로 이동해서 `Bootstrap`을 이용해서 만든 `table`에 `dataBinding`을 해보자.
그냥 할 수는없고, `store` 안에 있는 데이터를 `props` 형태로 등록해야 사용 할 수 있다.

```javascript
// Cart.js
import { connect } from 'react-redux';

function Cart(){
    return()
}

function stateToProps(state) {
    return {
        // redux.store안에 있는 data를 가져와서 props로 변환해주는 함수
        // state 중에 name이라는 데이터가 있으면 상품명이라는 props로 변환
        // state를 props로 바꿔주기
        state: state
    }
}

export default connect(stateToProps)(Cart)
```

1. 장바구니 사용을 원하는 `Component.js` 파일 밑에 `function`을 만든다
이는 `store`안에 있는 `state`를 `props`로 만들어주는 역할인데, `return` 안에 `{ 원하는변수명 : state }`을 넣어주자. 그럼 모든 `state Data`가 `props`로 등록된다.

2. export default connect(stateToProps)(Cart)
`connect` 함수에 선언한 `Component`를 집어 넣는다. 그럼 `redux store` 에 있던 데이터가 `props` 된 채로 `export` 된다.

3. `Bootstrap`으로 만든 테이블에 data를 넣으려면 `Redux`에서 선언한 `state`를 넣어주면된다.

```javascript
<Table striped bordered hover variant="dark">
    <tr style={style}>
        <th>id</th>
        <th>상품명</th>
        <th>수량</th>
        <th>변경</th>
    </tr>

    {props.state.map(function (n, i) {
        return (
            <tr key={i}>
                <td>{n.id}</td>
                <td>{n.name}</td>
                <td>{n.quantity}</td>            
            </tr>
            )
                })}
</Table>

```

---

### 📍 Redux 문법 2 : reducer / dispatch
그럼, `data 저장`까지는 배웠는데 `data 수정`은 어떻게 할까??
`redux`에서 `data 수정`하려면 다음과 같은 순서를 밟는다.

>1. `reducer` 함수를 만들고 그곳에 데이터 수정하는 방법을 정의해놓는다.
>2. 원하는 곳에 `dispatch()` 함수를 사용해 `reducer`에 써진 대로 데이터를 수정한다.

---

### ✏️ [ 예제 2 ] `redux`를 사용해 장바구니 품목에 +/- 기능을 만들어보세요.
장바구니 화면에서 표의 행마다 +/- 버튼을 하나씩 만들어서 이걸 누르면 실제 품목데이터가 1씩 증가 / 감소하는 기능을 만들어보자.

`+ / -` 버튼을 누르면 `redux` 안에 있는 `state`를 수정해야한다.
그러기 위해서는 2가지 방법이 필요한데,

>1. `state` 데이터의 수정방법을 `reducer`로 정의해두고
>2. 데이터의 수정방법을 불러서 수정한다.

`reducer`는 `function` 안에
>1. `state` 초기값
>2. `state` 데이터 수정방법이 들어있는 함수.
라고 생각하면 편하다.

세팅방법은 다음과 같다.
```javascript
// 1번 방법
function reducer(){
    return [{id: 0, name: '멋진신발', quan: 2}]
}
let store = createStore(reducer);

// 2번 방법
let 기본state = [{id: 0, name: '멋진신발', quan: 2}];

function reducer(state = 기본state, 액션){
    return state
}
let store = createStore(reducer);
```
이렇게 만들면, `reducer`는 그냥 `state`를 뱉어내는 함수일뿐이다.
2번 방법은 `reducer`에 `default 파라미터 문법`으로 추가했는데

---

### 💡 default 파라미터 문법이란?
함수를 만들때, 실수 또는 의도적으로 파라미터 입력을 하지 않을 때 기본으로 가지는 파라미터를 부여하는 문법이다.
파라미터를 선언할 때 `=(등호)`로 입력하면 된다.

예를 들어, 매개변수가 선언됐지만, 호출 할때 값이 들어오지 않으면 초기값(undefined)이 들어온다.

```javascript
function test(a = 10, b = 20){
    console.log(a+b);
}

test(2);
👉🏽 22
```

위에서 함수를 호출할때 a = 2가 주어졌지만, b는 주어지지 않았다. 
따라서, b의 기본값인 20을 넣어 22가 출력되는것이 `default parameter`이다.

---

다시 본론으로 돌아와서 `reducer` 데이터 수정방법을 정의하자.
이런식으로 `state` 데이터 수정방법을 정의 할 수 있다.

```javascript
// index.js


let 기본state = [{id : 0, name : '멋진신발', quantity : 2}];

function reducer(state = 기본state, 액션){
  if (액션.type === '수량증가') {
    return 수량증가된새로운state
  } else {
    return state
  }
  
}
let store = createStore(reducer);
```

>1. `수량증가` 라는 `액션.type`을 만들었다.
>2. 만약, `수량증가` 라는 요청이 들어오면 `수량증가된새로운state`을 `return`하고
>3. 그렇지 않으면, 기존의 `state`를 반환한다는 코드이다.

다음으로 `reducer`를 구현할 페이지인 `Cart.js`에서 `dispatch()` 함수를 이용해 `reducer` 함수를 동작 시킬 수 있다.

```javascript
// Carts.js

<button onClick = {() => { props.dispatch({type: '수량증가'})}} > + </button>
```

이것이 우리가 `redux`를 사용하는 2번째 장점이다. 
<span style = 'color:blue'>데이터의 수정방법을 미리 정의 해 둘 수 있다.</span>

이제 실제로 `data`를 만져보자.
위에서 선언했던 `수량증가` 요청이 들어오면 `state` 첫째 아이템인 `quantity` 항목이 1 증가 / 감소 하게 만들면 된다. 
데이터는 `deep copy`를 이용하면된다.

```javascript
// index.js

let 기본state = [{id : 0, name : '멋진신발', quantity : 2}];

function reducer(state = 기본state, 액션){
  if (액션.type === '수량증가') {
    let copy = [...state];
    copy[액션.데이터].quantity++;
    return copy

  else if (액션.type === '수량감소') {
    let copy = [...state];
    copy[액션.데이터].quantity--;
    return copy
  } else {
    return state
  }
  
}
let store = createStore(reducer);

// Cart.js

<button onClick = {() => { props.dispatch({type: '수량증가'})}}> + </button>
<button onClick = {() => { props.dispatch({type: '수량감소'})}}> - </button>
```

작게 만든 사이트에서는 `redux`를 사용할 필요가 없지만, 
대규모 사이트에서는 데이터를 한 눈에, 한 곳에 관리할 수 있기때문에 `redux`가 쓰인다.
이때, `redux`를 만들어 `state` 수정하는 방법을 미리 정해놓으면 `redux` 안의 `reducer`만 잘 들여다보면 `state` 데이터가 어떻게 바뀌는지 알 수 있다. (`dispatch()` 부분도 살피자.)

---

### 📍 Redux 문법 3: state, reducer가 더 필요할 때
방금 만들었던 `Cart.js` 페이지에 조그만한 `alert UI` 하나를 추가해 열고 닫는 기능을 만들고 싶다. 이때 열고 닫히는 상태를 저장할 `state`가 하나 더 필요한데, `redux`에서 어떻게 만드는지 알아보자.

`HTML`

```javascript
function Cart(props){
  return (
    <div>
      <Table>table부분</Table>
      <div className="my-alert2">
        <p>지금 구매하시면 20% 할인</p>
        <button>닫기</button>
      </div>
    </div>
  )
}
```

이제, UI를 보여주고 안보여주는 `state`를 만들어야하는데, `reducer`를 하나 더 만들어보자.
`reducer`에는 `state 초기값` + `state` 수정하는 법을 넣으면 된다.
```javascript
// index.js

let alert 초기값 = true;

function reducer2(state = state초기값, 액션){
    return state
}

let store = createStore(combineReducers({ reducer, reducer2 }))
```

2개 이상의 `reducer`를 사용할때는 `combineReducers()` 함수를 사용해야하는데, 
모든 리듀서를 `object` 형식으로 담으면된다. 이때, 상단에 `import` 하고 사용하자.

이후 `Cart.js`에서 `redux`를 선언해주자.
```javascript
function stateToProps(state) {
    return { 
        state: state.reducer,
        alert: state.reducer2
    }
}
```

그럼, 닫기버튼을 누르면 UI가 사라지는 기능을 만들어보자.

```javascript
// index.js
function reducer2(state = alert초기값, 액션) {
  switch (액션.type) {
    case '알람닫기':
      return false;
    default:
      return state;
  }
}

// Cart.js
function Cart(props) {
    function 알람닫기() {
        return (() => { props.dispatch({ type: '알람닫기' }) })
    }

{ props.alert === true
    ? <Alert variant={'dark'}>
        <p>지금 구매 시 20% 할인</p>
        <button onClick={알람닫기()}>닫기</button>
        </Alert>
    : null
}

```

이렇게 알람 UI를 만들어봤는데,
결론적으로 <span style='color:blue'>작은 기능을 만들 때에는 `redux`를 쓰지 말자.</span>

이 `state` 데이터를 다른 컴포넌트에서 쓸 일이 없다면 간단하게 `useState()`로 `Cart` 컴포넌트 안에 간단하게 만들면 되겠다.

반면, 많은 컴포넌트들이 공유하는 값은 `redux store`안에 보관해서 코드 양을 줄이자.

---

### 📍 Redux 문법 4: dispatch할 때 데이터를 실어보내자.
요즘엔 `redux` 특유의 복잡함 때문에 미래에는 문법이 바뀌거나, 다른 라이브러리로 대체될 가능성이 높다고 하셨다. 

다른 라이브러리로  `react effector`, `react recoil` 가 있다고 하는데, 이게 왜 `redux`보다 간편하다고 하는지 나의 수준에서는 아직 이해하기 어렵다. 🥲 🥲

이번에는 신발 주문하기 버튼을 누르면 방금 만들었던 장바구니 페이지에 추가되는 기능개발을 해보자.
이렇게 생각할 수 있다.

>1. `redux`에서 데이터 수정하는 법을 만들고
>2. `dispatch()`를 통해 데이터를 함께 실어보내자

`redux`의 `항목추가`기능은 다음과 같이 만들 수 있다.

```javascript
// index.js
function reducer(state = 초기값, 액션) {
  if (액션.type === '항목추가') {
    let copy = [...state];
    copy.push(액션.payload);
    return copy    

// Cart.js
<button onClick={() => { 
    props.dispatch({ type: '항목추가', payload: {id: 2, name: '새로운 상품', quantity: 1};
    history.push('/cart');
}) }}> 주문하기 </button>
    
```

이제 버튼을 누르면 `항목추가` 요청을 `dispatch()` 하게 되고, 데이터를 실어 보낸다.
`reducer`에서는 해당 `data`를 `state`에 추가해준다.
`reducer(state, 액션)` 에서 `액션`이라는 파라미터는 그냥 `dispatch()` 소괄호 안에 들어있던 모든것이 들어있다. 그래서 `payload` 말고 여러가지 정보들을 함께 보낼 수 있다.

---

### 📍 리액트에서 자주쓰이는 if문 5가지 작성패턴 
1. 컴포넌트 안에서 쓰는 `if / else`

```javascript
// 1번
function Component(){
    if (true) {
        return HTML~
    } else {
        return null;
    }
}

// 2번
function Component(){
    if (true) {
        return HTML~
    } 
    return null;
}
```

컴포넌트에서 `JSX`를 조건부로 보여줄 때 사용하는 패턴이다.
주의 할 점은, `if문`은 `return()` 안의 `JSX` 내에서는 사용 불가능하다.

`else`와 중괄호를 하나 없애도 동일하다.
자바스크립트 `function` 안에서 `return` 키워드를 만나면 `return` 밑에 있는 코드는 더 이상 실행되지 않기때문이다. 
깔끔하게 코드를 작성하고 싶다면 생략하자.

2. JSX안에서 쓰는 삼항연산자(Ternary Operator)

```javascript
// 조건문
// ? 참일 때 실행 할 코드
// : 거짓일 때 실행 할 코드

function Component() {
    return(
        <div>
            {
                1 === 1
                ? <p> HTML~ </p>
                : null
            }
        </div>
    )
}

// 중첩사용
function Component() {
  return (
    <div>
      {
        1 === 1
        ? <p>참이면 보여줄 HTML</p>
        : ( 2 === 2 
            ? <p>안녕</p> 
            : <p>반갑</p> 
          )
      }
    </div>
  )
} 
```
JSX 내에서 if / else 대신 쓸 수 있는것이 장점이고, 조건을 간단히 주고 싶을 때 사용한다. 
중첩사용이 가능하다. 코드가 간결하게 보이기위해서는 중첩사용보다는 `return` 문 바깥에서 `if/ else`를 사용하고 변수로 저장하자.

3. && 연산자
&& 연산자는 좌항과 우항이 같으면 전체를 `true`로 바꿔달라는 의미다.

예를 들어, true / false 비교는 다음과 같은 결과가 나오지만, 
```javascript
true && true;
👉🏽 true

true && false;
👉🏽 false
```
자료형은 이와 다르게 true와 만나면 자료형이 반환되고, false와 만나면 false가 반환된다.
```javascript
true && 안녕;
👉🏽 안녕

false && 안녕;
👉🏽 false
```

이걸 `if문`에 적용하면 코드를 조금 더 간략하게 사용 할 수 있다.
```javascript
function Component() {
    return(
        <div>
            {
                1 === 1
                ? <p> HTML~ </p>
                : null
            }
        </div>
    )
}

function Component() {
    return(
        <div>
            {
                1 === 1 && <p> 참이면 보여줄 HTML~ </p>
            }
        </div>
    )
}
```
위 2개의 예제는 동일한 역할을 한다.
밑의 예제에서 왼쪽 조건식이 `true`면 오른쪽 `JSX`가 자리에 남고 `false`면 HTML로 렌더링하지 않는다.

4. Switch / case 조건문
`if문`이 여러개 달려있을 때 사용하면 코드와 괄호가 줄어 가독성이 좋아지는 문법이다.

```javascript
// 기존문법
function reducer(state, 액션){
  
  if (액션.type === '수량증가'){
    return 수량증가된state
  } else if (액션.type === '수량감소'){
    return 수량감소된state
  } else {
    return state
  }
}

// 동일문법
function reducer(state, 액션){
  
  switch (액션.type) {
    case '수량증가' :
      return 수량증가된state;
    case '수량감소' : 
      return 수량감소된state;
    default : 
      return state
  }
}
```

1. switch (검사 할 변수명){} 작성 후 
2. 그 안에 case 검사 할 변수명(if문)을 넣고
3. 일치하면 `case: ` 밑에 있는 코드를 실행한다.
4. `default: `는 `else`문과 동일하다.
   

5. Object 자료형을 응용한 enum
<span style='color:blue'>경우에 따라서 다른 HTML을 보여주고 싶은경우에 작성하면 편하다</span>

예를 들어, 쇼핑몰에 탭UI를 만들때 `state` 따라서 `<div>`를 보여준다고 하자.
`if문`으로 `state`를 검사해도 되지만, 이렇게 사용해도 된다.

```javascript
function Component(){
    let 현재상태 = 'info';
    return(
        <div>
            {
                {
                    info : <p> 상품정보 </p>
                    shipping : <p> 배송관련 </p>
                    refund : <p> 환불약관 </p>
                } [현재상태]
            }
        </div>
    )
}

let 탭UI = 
    {
        info : <p> 상품정보 </p>
        shipping : <p> 배송관련 </p>
        refund : <p> 환불약관 </p>
    }

function Component(){
    let 현재상태 = 'info';
    return(
        <div>
            {
                탭UI[현재상태]
            }
        </div>
    )
}
```
`object` 자료형으로 `HTML`을 정리해서 담고, 마지막 `object{}` 뒤에 대괄호를 붙여 <span style='color:blue'>key값이 현재상태인 자료를 뽑겠다.</span>라고 써놓는다.

---

### 📍 lazy loading / React devtools
홈페이지의 기능구현을 완성했다면 다음은 성능향상과 유지관리를 해야한다.
리액트 컴포넌트의 로딩속도를 향상시킬 수 있는 방법은 몇가지 존재하는데,
이번에는 3가지의 방법을 사용해 볼 것이다.
>
1. 익명함수 / 익명 object 쓰지 않기
2. 레이아웃에 애니메이션 주지 않기
3. 컴포넌트 `lazy loading` 하기

1. 함수나 오브젝트는 변수로 담자
리액트적인 개념은 아니고 메모리공간을 아낄 수 있는 JS 코딩 관습이다.
```javascript
let 스타일 = {color: 'red'};

function Cart(){
    return(
        <div style={ 스타일 }></div>
    )
}
```
이런식으로 컴포넌트 바깥에 있는 변수로 저장해서 사용하라는 얘기다.
이유는 <span style='color:blue'>컴포넌트가 재 렌더링될 때 변수에 저장되지 않은 이름없는 object, function 류의 자료형은 매번 새로운 메모리 영역을 할당해줘야하기 때문에 컴퓨터에 부하가 걸릴 수 있다.</span>
그걸 방지하기 위해 컴포넌트 바깥에 마련해두자. 

2. 애니메이션을 줄 때 레이아웃 변경 애니메이션은 자제하자.
리액트만 해당되는 것이 아닌 `CSS` 전반적인 코딩 관습이다.
`width`, `margin`, `padding`, `left right top bottom ` 과 같은 레이아웃을 JS나 `transition`을 이용해 레이아웃을 변경시키는것은 브라우저 입장에서 큰 부담이 된다.
CSS에서는 이러한 과정을 `Reflow`, `Repaint`라고 하는데 자세한 내용은 다음을 참고하자

출처: <a href ='https://boxfoxs.tistory.com/408'>브라우저 렌더링 과정 - Reflow, Repaint, 그리고 성능 최적화</a>

따라서, 애니메이션을 넣어도 성능에 큰 지장이 없게 만들고 싶으면 `transform`, `opacity` 같은 `CSS` 속성을 이용해 애니메이션을 주자.

3. 컴포넌트 `import` 할 때 `lazy import` 하는 법
`App.js`에서 지금까지 했던 코드를 살펴보면 `import`가 많은 것을 느낄 수 있다.
`Wep-App`의 특징인데, 관련된 모든 `component`를 `import` 하면 사이트 초기 접속속도가 굉장히 느려질 수 있다.

그래서, 해당 컴포넌트들이 필요할때만 `import`를 해달라는 코드를 작성할 수 있다.
```javascript
import React, { lazy, Suspense } from 'react';
let Detail = lazy (() => { return import('./Detail.js') });

render(
    <Suspense fallback={<div>로딩중이에요 :)</div>}>
        <Detail shoes={shoes} 재고={재고} 재고변경={재고변경} />
    </Suspense>
)
```

`fall back`을 사용해 로딩이 오래걸릴 때 안내문같은걸 띄워줄 수 있다.

---

React Dev Tools는 chrome 확장프로그램에서 설치 할 수 있다.
>1. props확인
1. `state` 상태 확인
2. 실시간 `state, props` 수정
3. 시계모양 버튼을 눌러 해당 컴포넌트 렌더링을 잠깐 정지해보기
4. 컴포넌트 렌더링 속도와 단계별 녹화

등등 개발할때 필요한 것들을 테스트 해볼 수 있다.

---
### 📍 필요없는 재 렌더링을 막는 memo
컴포넌트는 컴포넌트와 관련된 `state`, `props`가 변경되면 항상 자동으로 재 렌더링된다.
컴포넌트 안에 컴포넌트가 여러개 있을 때, 부모 컴포넌트의 `props` 내용이 일부 변경되면, 자식 컴포넌트들도 전부 재 렌더링된다.

`memo()`는 <span style='color:blue'>`props` 변경이 안된 컴포넌트는 재 렌더링 하고 싶지 않을 때 사용한다.</span>

```javascript
function Parent(props){
    return(
        <div>
            <Child1 이름={props.이름}></Child1>
            <Child2 나이={props.나이}></Child2>
        </div>)}

function Child1(props){
    useEffect(() => { console.log('렌더링됨1') } )
    return <div>1111</div>    
}

let Child2 = memo(function(){
    useEffect(() => { console.log('렌더링됨2') } )
    return <div>2222</div>    
});

```

이름을 존박1로 변경하면 `Child2`라는 존박과 관련없는 컴포넌트는 재 렌더링 되지 않는다.
컴포넌트가 너무 크거나 잦은 재 렌더링이 부담스러울 때 쓰는 방법 중 하나이다.

하지만, `memo`로 감싼 컴포넌트는 기존 `props`와 바뀐 `props`를 비교하는 연산이 추가로 진행되기때문에, `props`가 크고 복잡하면 자체로도 부담이 될 수 있다.

따라서, 상황에 맞게 평가하려면 `react dev tools`를 이용해 렌더링속도를 측정해보자.

---

## ✏️ 결론
지금까지 약 1달에 걸쳐 `[ 애플코딩 ] 리액트 기초부터 쇼핑몰 프로젝트까지!`를 완강했다.
많은 강의를 보고 언제 다 듣지~ 라는 생각을 했었는데, 막상 강의를 듣고나니까 더 듣고 싶다는 생각을 했다.

리액트의 리자도 모르던 나에게 애플코딩은 좋은 경험이었고, 강의의 수준이 어렵지 않아서 나처럼 리액트에 처음 입문하는 개발자, 혹은 쇼핑몰을 만들고 싶은데 몇 가지 기능들을 넣고 싶은데 방법을 모르는 사람들이 들으면 좋을 강의였다.

강의가 끝나고 2~3주정도 나만의 쇼핑몰을 만들어 볼 생각이다.
[ 스파르타코딩클럽 ]에서 만든 <a href = 'http://ywtech.shop/'> 지금뉴스! </a> 보다 발전된 모습으로 만들어야겠다.

쇼핑몰을 만들때 필요한 기능들은 강의를 여러번 듣는 것보다 내가 직접 코드를 짜며 구글링해가면서 만드는게 더 중요하다고 생각한다. 

2~3주 후에 프로젝트를 완성하고 나서 <a href='https://nomadcoders.co/nwitter'>노마드코더의 트위터클론코딩</a>을 들을 계획이다.

내가 만들 쇼핑몰의 제작 과정을 벨로그에 올려야겠다!

---

# 튜터에게 궁금한 점
1. `redux`를 대체하는 라이브러리로  `react effector`, `react recoil` 가 있다고 하는데, 이게 왜 `redux`보다 간편하다고 하는지 궁금합니다.
