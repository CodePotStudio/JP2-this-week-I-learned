# 이번주 리뷰
<br>

## Node+Express 서버와 React 합치기

서버와 리액트를 합친다..

1. 서버 : 누가 어떤 주소로 접속하면 index.html을 보내주세요~ 하는역할

2. 리액트 : html을 예쁘게 만들어주는 도구일 뿐 웹앱이라고하고 SPA(single page application) 으로 만들어주는 도구 (모바일 앱처럼 부드럽게 동작한다.)

리액트로 개발을 마치면 => html파일 하나 나온다

서버에서 그걸 보내주세요 하고 작성하면 합치기 끝


server.js만들고

```jsx

const express = require('express');
const path = require('path');
const app = express();

const http = require('http').createServer(app);

http.listen(8080, function(){
    console.log('listening on 8080')
});

```

1. npm init 설치
2. npm install express

node server.js
(nodemon이 설치되있다?) nodemon server.js

public 폴더 만들어서 그 내부에 html 파일을 넣는다.

```jsx
//이게 필요할수도 있다 미들웨어 
// 내가 어떤 파일들을 서버에서 잘 보내고싶어
// static한 파일들이 어디있는지 기록해준다.

app.use( express.static( path.join(__dirname, 'public') ) )

app.get('/', function(요청,응답){
    응답.sendFile( path.join(__dirname,'public/main.html'))
})

```

---

따라해보는데 npm init 부터 설명이조금.. 부실해서

찾아봐야겠다.

node.js 설치하는 명령어 같은데 pakage name 은 그냥 프로젝트명 쓰면되고 그뒤로도 버전이라던가 등등 입력할수있게 터미널이 서포트해준다.

기본적으로 node, nodemon 등 궁금한게 많지만

node.js 의 범위인거같아서 깊이있게는 하면 안될꺼같다.

localhost:8080 갔더니

cannot GET 이렇게 나온다.

메인페이지 연결하는 방법등 연결해주고

`npx create-react-app 프로젝트이름`

리액트프로젝트가 하위폴더로 들어와진다.


리액트개발이 끝나면

`npm run build`

build 폴더가 하나 생성된다.

빌드폴더 내부에는 발행에 필요한 각종 파일들이 있다고 생각하면된다.

리액트폴더에서 개발하고 빌드했으면 그거를

server에서 내려주는식으로 하면

완성이다.

```jsx

//app.use( express.static(path.join(__dirname,'public')) );
//이거 대신에

app.use( express.static(path.join(__dirname,'react-project/build') ) );

app.get() 에 있던 요청도

'react-project/build/index.html'로 경로 수정해주면

```

이렇게 해서 발행시킨다. 누군가메인페이지로 접속하면


### 리액트 라우터를 사용하면 어떻게하지?

리액트가 더 잘한다 라우팅을

리액트 라우터를 쓰면 스무스하게 변경된다.

리액트를쓰면 서버의 역할이 축소된다.

서버의역힐 
1. ~~라우팅으로 페이지나누기~~
2. DB입출력

주소창으로 /about으로 들어가면 안됀다.

리액트로 라우팅하면 

app.get('*',function(요청,응답))...

이런식으로 해야 뒤에 어떤 문자가왔을때 잘 작동한다.

개발패턴


- 리액트
/list 페이지 접속시
잠깐 서버로 Ajax요청함 그럼 데이터 받아오기 기능
<list>컴포넌트같은거 보여주면된다.


- 서버
어떤놈이 Ajax요청 하면
DB에 있던 게시물 list데이터 보내줌

/ 로 들어오면 메인페이지
/react로 들어올때 리액트 페이지를 보여주려면

'/' , '/react' 이런식으로 app.get을 주면 되고 추가로

```jsx


app.use('/', express.static( path.join(__dirname, 'public')))


app.use('/react', express.static( path.join(__dirname, 'react-project/build')))



```


app.use 는 미들웨어라고한다.

내가 특정 요청과 응답 사이에 뭔가 코드를 수행하고싶다

그럼 그걸 미들웨어라고 칭한다.


근데 수행해보니 리액트페이지가 실행이 되지않는다.

리액트 폴더 내부에 들어가서

pakage.json 내부에 들어가서

homepage : '/react' 이런싣으로

해줘야

빌드해주고

하면 잘된다.


단점 ? 꼭 빌드를 한 10초동안 계속해야하나 ?

live 개발은 안돼나? proxy 라는게 있다. 검색 ㄲ


## 리액트강의를 마무리하며

제일 되새기기 좋은 문구는

>풀스택 개발에 관심있으시면 Node.js + Express 같은걸로 쉽게 서버기능까지 추가해볼 수도 있겠으며  

>다른걸 만들어보고 싶으면 타 사이트를 카피해보십시오. 저런 사이트를 리액트로 만들려면 어떻게 해야할지 생각해보고 구현해봅시다. 

앞으로 공부해야할것들? HTML5 이후에 추가된 웹개발 기본 기술들

- FileReader API
- 로컬스토리지
- Web worker
- Geolocation
- Canvas
- Drag & Drop
- fetch API
- CSS grid, flex 레이아웃 등등

리액트랑 JS문법 잘안다고 웹개발잘하는게아니라

항상 브라우저 기본기능과 API 를 잘알아야 실제 웹개발 잘하는 사람이된다고한다.

async await promise iterator 등등.. ES6 문법 (이전에 강의를통해 많이 이해는 하고있다고생각하지만..)

어싱크 어웨잇트는 너무 어렵다..

다른 툴들도 재미있다고한다.

angular : 기타 라이브러리 설치안해도 모든걸 내장기능으로 끝낼 수 있는 역사와 전통의 웹앱 라이브러리입니다.

Vue.js는 리액트랑 같은 기능을 제공한다. redux 어려운데 대신에 vuex 를 쓰는데 이게 100만배는 더 쉽다고한다.

아니면 React Native로 모바일 앱도 괜찮아보인다.

방향은 내가 정하는거겠지만...

리액트 는 얼마나 갈까, 리덕스때문에 개선된 리액트의 다음단계가 나올꺼같다고 하는느낌..

<details><summary>개발욕구를 자극하기 위한 리액트 예제 몇가지 보여드리면 </summary>

리액트로 만든 테트리스 https://chvin.github.io/react-tetris/ (spacebar, 방향키 이용)

간단한 영화정보 검색기 https://skempin.github.io/reactjs-tmdb-app/

파일 버전관리 툴인 git 문법 배우기 앱 https://learngitbranching.js.org/

iOS 스타일 계산기 https://codepen.io/mjijackson/full/xOzyGX

가짜 주식 트레이딩 앱 http://web-demo.adaptivecluster.com/

캘린더 UI http://clauderic.github.io/react-infinite-calendar/

스케치패드 http://svrcekmichal.github.io/react-sketchpad/ 

솔리테르 Solitaire 게임 http://pl12133.github.io/react-solitaire/

</details>


### 번외로 (최근 본 상품 같은 사이드 배너 스크롤바 따라다니는) 기능 구현


```css

.sideBanner{
  width: 20%;
  height: 25vh;
  position: -webkit-sticky;
  position: sticky;
  top: 100px;
}
.main {
  width: 78%;
  height: 150vh;
}
.wrapper{
  display: flex;
  justify-content: space-between;
}

```

이런느낌으로 구현했는데

sideBanner와 main을 포함하고있는 wrapper 라는 클래스가 있고

플렉스로 병렬해주고

사이드와 메인이 각가 20% 와 78% 로 나눠먹고

옆에 사이드바만따로 position: sticky로 따라다니게 할수있다.

디자인은 좀 하다가 안이뻐서 포기~

로컬스토리지에서 데이터 끌어오는건다 잘하는데

중간에 <더보기> 버튼으로 제어하는 GET API

받아오는게있는데 그때 변경된 state 를 받아와서

임시 ?명령어 이런느낌으로 로컬스토리지의 ID값과 비교해서 꺼내서 보여주는식?

이렇게했는데 중간에 값이 변경되고하면서 redux나 contextAPI로

땡겨서 써보려고했는데 , 하다가 막혀서 포기하고 수업을 마져 들었다.

확실히 배울땐 괜찮은데, 쓰려고하면 갑자기 머리속에 백지가 쫙 깔린다..



# 튜터에게 궁금한 점
궁금한점 작성 공간!