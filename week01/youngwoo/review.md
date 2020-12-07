# 12월 2주차 리뷰
<br>

## npm과 npx의 차이점
`React`를 처음 시작하면 `terminal`에서 `npx create-react-app shop`를 입력한다. 그리고 내가 작성한 코드가 잘 작동되는지 확인하려면 `terminal`에 
 `npm start`를 입력한다. 

종종 `npm start`를 치면 `error`가 날때가 있어서 `npx start`를 치는 경우도 있었고, 반대의 경우도 있었다.

이런일들을 겪으니까, 둘의 차이점이 뭐길래 하나는 실행되고 하나는 에러가나지?라는 생각이들었다.

그래서 알아보자. `npm`과 `npx`의 차이점

> npm: Node Package Manager(관리)

npm은 `Node.js`로 만들어진 `Package(module: 프로그램보다는 조금 작은 단위의 기능)`을 `Manage`해주는 툴이다. 즉, `Node.js`로 만들어진 모듈을 웹에서 받아 설치하고 관리해주는 프로그램이다.

또한, `버전관리`를 지원하고 우리 프로젝트가 어떤 버전의 의존성을 사용할지 지정 할 수 있다. 예를들어 패키지의 업데이트로 인하여 프로젝트가 오작동하는 경우를 방지 할 수 있고 그 외에도 우리가 원하는 버전의 패키지 의존성을 설치할 수 있다.

npm은 `Node.js`를 설치하면 내장(built in)되어 있기때문에 따로 설치할필요는 없다.

> npx: Node Package Execute(실행)

npx는 `npm` 레지스트리에 올라가 있는 패키지를 쉽게 설치하고 관리 할 수 있도록 도와주는 CLI도구이다.
  * CLI(Command Line Interface): 명령어 인터페이스, `terminal`을 통해 사용자와 컴퓨터가 상호 작용하는 방식
`npm`과 다르게 일일이 설치, 실행, 제거를 할 필요 없이 일회성으로 원하는 패키지를 `npm` 레지스트리에 접근해서 실행시키고 설치하는 실행도구이다.

<br>

## 배열에 원소를 추가하는 4가지 방법

[ 코딩애플 ] `React: part.1 기초부터 쇼핑몰 프로젝트까지` 강의를 듣다가 `props`, `map`, `input` 파트를 배우고 게시물을 작성할 때마다 새로 추가되는 코드를 작성해보라는 예제를 받았다.

그리고 다음과 같은 생각을 했다.

> 
1. `map` 반복문을 돌리고 있으니까 같은 `HTML`을 어떻게 생성하지? 보다는 `글제목` 변수에 어떻게 `입력값`을 넣어주지?라고 생각했다.
2. 원본 `state`는 수정하지 말고 생각해보자.

결국, 내가 쥐어짜낸 코드는 다음과 같았다.

```javascript
let [입력값, 입력값변경] = (['동탄맛집추천', '아이폰 12pro', '아메리카노')];

<input onChange={(e) => {입력값함수(e.target.value)} }></input>

<button onClick={() => {글제목변경([입력값, '동탄맛집추천', '아이폰 12pro', '아메리카노']);}}>게시물 추가</button>
    )}  
```
한개의 게시물만 추가하면 된다고해서 작성했는데 생각해보니까 게시물을 작성할때마다 4개로 고정된다면 뭐하러 게시물 작성기능을 만들까?라는 생각이 들었다.

스파르타코딩클럽에서 8주동안 웹개발종합반을 배우며 자바스크립트의 입문했다고 생각했지만, 기본적인 배열 다루는 방법을 몰랐던 내 자신이 부끄러웠다.

그래서 작성한다.

배열에 원소를 추가하는 4가지 방법
>
1. unshift(): 맨 앞에 원소를 추가하는 메소드
2. push(): 맨 뒤에 원소를 추가하는 메소드
3. shift(): 맨 앞에 원소를 제거하는 메소드
4. pop(): 맨 뒤에 원소를 제거하는 메소드

간단한 test를 해보자.
원본 `state`를 건들지 않고 `deep copy`하여 사용했다.

```javascript
let array = [1, 2, 3];
let newArray = [...array];

// unshift()
newArray.unshift(0);
console.log(newArray);
👉🏽 [0, 1, 2, 3]

// push()
newArray.push(4);
console.log(newArray);
👉🏽 [1, 2, 3, 4]

// shift()
newArray.shift();
console.log(newArray);
👉🏽 [2, 3]

// pop()
newArray.pop();
console.log(newArray);
👉🏽 [1, 2]
```

위와 마찬가지로 `blog`에 적용하면
```javascript
let [글제목, 글제목변경] = useState(['동탄맛집추천', '아이폰 12pro', '아메리카노']);
let [입력값, 입력값함수] = useState('');
```

`{ 글제목 }` 배열 맨 앞에 `{ 입력값 }` 이 들어가려면 `unshift()` 속성을 추가해주면 된다.

```javascript
function App(){
let [글제목, 글제목변경] = useState(['동탄맛집추천', '아이폰 12pro', '아메리카노']);
let [입력값, 입력값함수] = useState('');

 return( 
    <input onChange={(e) => {입력값함수(e.target.value)} }></input>
    
	<button onClick={() => {
    	let 뉴글제목 = [...글제목];
        뉴글제목.unshift(입력값);
      	글제목변경(뉴글제목);
    }}></button>
)}
```

## SPA(Single Page Application)
SPA란 한 개의 페이지로 이루어진 애플리케이션을 의미하는데, 화면의 `header`, `footer`, `sidebar` 등 다시 새로고침해도 변함이 없는 부분들은 그대로 유지한 채로 변경되는 부분의 데이터만 가져와서 수정하는 웹사이트를 말한다.

###  배경
기존에 사용자가 다른 페이지로 이동할때마다 서버로부터 새로운 `HTML`을 받아오고, 페이지를 로딩 할 때마다 서버에 리소르를 받아왔으나, `WEB`의 정보가 많아진 요즘에 사용하기에 비효율적이고 이를 보완하기위해 생겼다.

###  장점
주로, `React`의 라이브러리, 프레임워크를 사용하여 `View렌더링`은 사용자의 브라우저가 담당하고, 사용자가 인터렉션이 필요한 부분만 자바스크립트를 사용하여 업데이트를 해준다. 만약, 새로운 데이터가 필요하면 서버 `API`를 호출하여 필요한 데이터만 새로 불러와 어플리케이션에서 사용 할 수 있다.

### 단점
앱의 규모가 커지면 마찬가지로 자바스크립트의 파일도 같이 커지는데 이는, 페이지 로딩시 사용자가 실제로 방문하지 않을 수도 있는 페이지의 스크립트도 불러오기때문이다.

### 해결방법
`코드 스플리팅(Code Splitting)` 을 사용하면 트래픽과 로딩 속도를 개선 할 수 있다.

출처: https://codingbroker.tistory.com/72

## Routing: 페이지 나누기
`React`로 `SPA`를 구현한다는 것은, 해당 요청에 맞는 `Component`만 `Routing`하여 부분적으로 렌더링한다는 것을 의미한다.

`React`에서 `Routing` 관련 라이브러리는 크게 3가지가 있다.

1. React-router: WEB, APP을 합친 패키지
2. React-router-dom: WEB에 쓰이는 패키지
3. React-router-native: APP개발에 쓰이는 패키지

지금은 WEB을 개발 중이기때문에 `React-router-dom`을 사용 할 것이다.

`React-router-dom`에서는 `Router`를 2가지 기능으로 제공하고 있다.
>
1. BrowserRouter
2. HashRouter

### BrowserRouter
> www.domain.com/path

1. `BrowserRouter`는 보통 `Request`와 `Response`로 이루어지는 동적인 페이지를 제작할때 보편적으로 사용된다.
2. 불필요한 요청도 `Server`에 할 수 있기 때문에 서버단에서 라우팅을 방지하는 `API`를 작성하기도 한다.
3. 새로 고침을 하면 경로를 찾지 못해 에러가 날때도 있다.
4. 백엔드가 필요한 동적인 페이지에 주로 사용된다.


### HashRouter
> www.domain.com/#/path

1. `#` 이전의 경로에 대한 요청만 서버가 받아들인다.
2. `Routing`을 안전하게 할 수 있게 도와준다.
3. 백엔드가 필요하지 않은 정적인 페이지에서 주로 사용된다.

### 사용하기
1. `npm install react-router-dom`을 설치한다.
2. `App.js`페이지에 `import { BrowserRouter } from 'react-router-dom'`, `import { Link, Route, Switch } from 'react-router-dom'` 입력한다.
3. 원하는 곳에 `<Route path="/"></Route>` 코드입력과 경로설정까지 해준다.
4. `Component`를 사용하고 싶으면 `<Route path="/"  component={Card}></Route>` 나 `<Route path="/"> <Card/> </Route>`를 입력한다.

`React-Router`는 각각 페이지마다 다른 `HTML`파일을 보여주는것이 아니고, `index.html` 파일 하나로 내부의 내용을 갈아치워 다른 페이지처럼 흉내내는 것이다.

`/detail` 경로로 접속하면 `/detail`내용과 `/` 메인페이지 내용도 같이 보여주는데 이는 `/detail`에 `/` 경로도 포함되어있기 때문이다. 

그래서 메인페이지에 `exact path='/'`를 부여해 경로와 정확히 일치할때만 페이지를 보여주게 설정 할 수 있다.

<br>
# 튜터에게 궁금한 점

>
1. 효율적으로 코드스플리팅(`Code-Spitting`)은 어떻게 해야하나요?
2. SPA를 구현할 때 사용되는 대표적인 프레임워크 `React`, `Vue`, `Angular` 이들은 SPA를 구현한다는 목적은 같은데 왜 나눠서 사용하나요? 어떤 차이점이 있나요?