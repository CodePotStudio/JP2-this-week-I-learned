# 이번주 리뷰
<br>
리뷰 작성 공간!!!


## nomad 트위터클론

대표적인 기능

1. 로그인
2. 실시간처리(업데이트포함)
3. 프로필
4. 삭제
5. 이메일 인증, 회원가입,로그인, 구글,깃헙 인증 , 실시간처리, 트윗,파일업로드 등.. 
트윗수정,트윗삭제 등등..

> 제일 놀라운것 백엔드코드 작성하지 않는것!!

CSS작업하는데에 시간이 제일 많이 필요

이모든게 5분도안걸리고

결국 CSS가 제일 시간을 잡아먹을것이다.

firebase로 할수있는것이 매우 믿기지 않을것이다.

백엔드 구현이없다는 점에서 매우 최고!!

## 알아야할 내용

HTML
CSS
GITHUB
(카카오클론코딩)

React Fundamental
(ReactJS로 영화 웹 서비스 만들기)

React
React JS
(초보를 위한 React JS)

React 컴포넌트를 만드는 새로운 방법

state를 관리하는방법

React Hooks
(실전형 리액트 Hooks 10개)

지금 내가 알고있는 내용으로 충분할까? 싶긴하지만

도전!

## Firebase 란

firebase로 할수 있는 것들

firebase는 처음에 데이터베이스였다.

하지만 이후에 구글에 인수되었고

그리고나서 구글에 의해 확장되었다.

지금의 firebase는 백엔드기능들을 포괄하고

그 그기능들을 제공 해주는것이다.


### firebase로 좀더 나은 apps을 만들수있다.

- cloud Firestore = 데이터베이스 관련 코드없이 데이터베이스를 사용하게 해준다. (ios,android,web)

- Firebase ML = Machine Learning을 할수있다. (ios,android)

- cloud function = serverless function의 기능을 제공 AWS의 Lambda와 비슷

- cloud storage = AWS의 S3와 비슷한것이다. 기본적으로는 업로드의 기능을 해준다.

- hosting = 나의 assets들을 배포하려 하거나, react Application을 배포하고자 한다면 Hosting 또한 사용해볼수 있다. (web을 위한 기능)

- Authentication = Firebase의 중요 포인트 => 이미 구현된 Authentication을 이용해서 __`인증`__ 을구현하면 10분 조차도 걸리지 않는다.

- Realtime Database = firebase의 오리지널 데이터베이스 = 사람들을 매료시키는이유 -> Realtime

- analytics (분석학,분석의) => 약간 통계 해준다는거 아닐까.. 그런기능도 사용가능 -> 구글이 인수하고 구글은 analytics 분야에서 뛰어나다. => dashboards, analytics, testing

    - Crashlytics => application 의 충돌 같은것을 볼수 있게 해준다. (web은 지원하지않고 , ios,android,unity만 지원)

    - Performance Monitoring = 나의 app의 성능을 보여주는 기능

    - Test Lab = > 나의 웹사이트를 각종 기기별로 테스트 할 수 있도록 해준다. (ios,android)

    - App Distribution => 나의 ios나 android의 버전 배포를 도와준다 (ios, android)

그 외에

business를 성장시키는 기능들도 많다.

google Analytics, Cloud Messaging, In-App Messaging, A/B Testing, Remote Config 등등 ..

AWS amplify 는 firebase와 매우비슷하다.
(AWS amplify의 장점은 GraphQL API , REST API를 제공한다는것)

하지만 firebase가 좀더 역사있고 많은사람들이 써왔다. (커뮤니티가 거대하다.)

AWS amplify는 비교적 최근에 나온것이며 , 거의 복붙 수준. (적은 코드, 적은 튜토리얼, 적은 질문)

또한 firebase는 google의 제품이다 이제는

그래서 구글의 문서방식인데 구글 문서가 깔끔하니 좋다?

### Firebase를 언제 사용하는가

firebase나 amplify를 회사에서의 실 프로젝트에서 쓰진않는다.

둘중 하나를 쓰는것은 google,amazon과 결혼하는정도로 밀접하게 의존하게된다는 의미아닐까.

amplify,firebase로 부터 벗어나는것이 큰 고통이 된다. (인증도 그들의 유저고, 데이터베이스도 그들의 데이터이다.)

좋을 수도있다.
많은사람들이 좋은아이디어,안좋은아이디어를 가지고있을수 있는데, 그런것을 가능한 빠르게 시작해볼수 있다. (서버,데이터베이스 만드는데에 시간과 돈을 쓰고싶지않다..) 이런데에 좋다.

나의 아이디어를 빠르게 테스트해볼수있다.
(본격적인 비즈니스의 용도라면 쓰지않을꺼같아.)
(비즈니스의 구상단계라면 ok => 테스트해보자)


### Firebase는 공짜가아니다.

대부분이 Free 이고

Authentication 은 무료로는 10000만명 까지 핸드폰 인증 가능

앵간하면 무료

cloud 1기가 무료 그이후 기가당  0.18$ 이다.

문서 쓰기, 문서 읽기, 문서 삭제 하루 2만,5만,2만 각각.

이후 10만당 얼마씩 추가결제 가능

storage 5기가 무료

이후 기가당 결제

용량을 자유룝게 줘버리면 빠르게 불어날수있으므로

트윗의 사진업로드 용량을 제한해줘야한다.

초기셋팅에 대해서 나오는데

`npm add create-react-app` 인가 로 설치하면 불필요한 것까지 같이

설치되는게 있다. (설치되는동안 github.com/new 로 새로운 레포지터리를 만들어주었다.)

vscode( 터미널에서 code로 실행하는 거 추가했는데 너무좋은거같다.)

실행하자마자 git remote add origin `깃헙레포지터리주소` 해주고

src 폴더에 App.js, index.js 만 남게 되고
(내부에 임포트되어있는 css파일이나 관련 문장도 같이 지워준다.)
(index.js에서 하단에 주석밑에 vital 어쩌구도 같이 날려줬다.)

이후 package.json 에서 scripts 부분에

"test" 부분을 날려줬다. (우리는 테스트를 하지않을것이다 라고했다.)


---

vscode 터미널에 
`git add .` 쳐주고  

`git commit -m '커밋메시지'`

`git push origin master`

---

여기까지가 react 셋팅이다.

이후 firebase 프로젝트 새로 생성하고,

약관은 동의하고 이후에 Analytics 는 체크해제 했다 (아직 하지말자 고했다.)

web으로 등록해주자 Firebase Hosting은 아직 하지말자고 (체크하지말고)

Register App!

하면 HTML 태그에 추가해서 사용할수있는 스크립트들이 보이는데

우리는 섹시한 개발자이므로(?) 이렇게 하지않고

 `npm install --save firebase`

설치되는동안 `var` 아까 register App 하고 나서 보여지는 script들 내부에 보면

`var` 

`var firebaseConfig = {` 여기서부터 ~~ `};` 까지 복사해놓고

빠르게 src 폴더 내부에  `firebase.js` 만들어주자.

const로 복붙해주고 밑에

`firebase.initializeApp(firebaseConfig);` 추가해주었다.

이후 firebase를 (아까 인스톨 했으므로 import 해줘야한다.)

`import * as firebase from "firebase/app";`


그리고 추가로 

`firebase.initializeApp(firebaseConfig);` 하지말고

export default 를 앞에 추가해서

`export default firebase.initializeApp(firebaseConfig);`

한다.

index.js 내부에서 `import firebase from "./firebase"` 해준다.

---

지금까지 한게 무엇인가??

1. 프로젝트를만들었다.

2. 기본적으로 Firebase web 형태이고

3. application도 만들었고

4. apiKey.. 등등 자동으로 생성해줬다.

5. Firebase 설치해줬고 파일하나 만들어서 initialization(초기설정)까지도 진행했다.
    - 나중에 Authentication,Analytics 등등 쓰고싶으면 import 해주면된다.
    [firebase홈페이지_나의JS에 node.js로 firebase설치하기](https://firebase.google.com/docs/web/setup?authuser=0#node.js-apps)

## key 보호하기

`.env` 파일을 만들어서 환경변수를 지정해준다. (root파일안에, `.gitignore`옆에 있어야한다.)

내부 형태는 `REACT_APP_이름 = 값` 의 작명 규칙을 사용해야한다.

추가로 `.gitignore`에 `.env` 를 추가해서 커밋되지않게 할수있다.

하지만 firebase는 클라이언트가 요청을 해야하기때문에

결국에 중요한 Key가 코드에 실릴수 밖에없다.

그래서 완벽한 보안수단이 아니다. 

> 그저 깃허브에 업로드하지 않기위함이다.

너무 key를 숨기는데 몰두하지 않아도된다.
- 다른 보안요소를 추가해줄 부분들이 있다.



## Router 셋팅

src/ 밑에 components , routes 두개의 폴더를 만든다.

app.js는 components 에 넣고

`index.js`에서 import 경로를

`import App from "./components/App"` 으로 수정해준다.


라우터는 4개정도 만들예정

1. Authentication 부분이다.
    - Auth.js
        - ```jsx
            import React from "react";

            export default ()=> <span>Auth</span>
            ```

2. Home.js

3. Profile.js

4. EditProfile.js

이후 react-router-dom

을 인스톨해준다

`npm i react-router-dom`

components 폴더 아래에 Router.js 를 생성하고

```jsx

import React from "react";
import { HashRouter as Router, Route, Switch } from "react-router-dom";

```

중간에 실행해봣는데

```

Failed to compile.
./src/firebase.js
Attempted import error: 'initializeApp' is not exported from 'firebase/app' (imported as 'firebase').

```

오류가 발생해서 어떻게 해결해야할지 막막하다 .

> 해결방법

```
8.0.0 이전

import * as firebase from 'firebase/app'
8.0.0 이후

import firebase from 'firebase/app'

```


firebase 버전이 올라가면서 생긴 문제인거같다.


이어서

Router.js 에서

Switch해서 인증(로그인)여부에 따라서 라우트를 다르게 해줄것이다.

>functional component

기본적으로 const ()=> 로 시작해서 함수를 변수에 담아서

export 시켜주는식으로 컴포넌트를 계속 사용하는거같다.

컨셉은 인증이됬는지 안됬는지를 flag로써 useState 훅을 이용해서

true false 를 이용해서 로그인페이지를 보여줄지 , home 페이지를 보여줄지를

router.js 가 정해준다.

## firebase 인증 사용하기

먼저 Router.js 에있던 state를 app.js로 옮겨서 props 로 넘겨줄것이다

(왜냐하면 중요 데이터기때문에 혹은 라우팅 이후에도 계속 필요로 하는 데이터이기 때문에 ?)

application이 (App.js) 모든 로직들을 다루고 있다.

App 에서 주된 html 외에도 footer 같은것을 달려면

일단 <div>나 <> 프레그먼츠로 감싸야 한다 (return안에는 하나의 태그만 보여야한다.)

```jsx

<>
    <AppRouter isLoggedIn={isLoggedIn}>
        <footer> &copy; {new Date().getFullYear()} Nwitter</footer>
    </AppRouter>
</>

```

먼저 firebase의 auth 기능을 쓰려면 (다른 라이브러리나 프레임워크도 마찬가지로) documentation 을 잘 읽어보고 써야한다.

import를 뭘 해야한다던가 등등..

`firebase.js` 에서 `import "firebase/auth"`

`App.js` 에서 `import firebase from "../firebase"` ..은 상대경로이다.

이것을 해결해주는건가 ? 절대경로로써 바꿔쓸수있게 도와주는 .. `jsconfig.json`에 

```json

{
    "compilerOptions":{
        "baseUrl" : "src"
    },
    "include":["src"]
}

```

이것을 추가해주는데 "./Router" 이런식으로 최대

리뷰를 작성하면서 어느정도 정리가 되었는데 ./ 를쓰던것은 현재위치를 잡을때 사용하는데 내가 vs코드로 불러왔을때 가장 최상단 문서를 기준으로 한것? (혹은 create-react-app 했을때 기준 최상위 문서)

그것을 위에 작성한 jsconfig.json 으로 root 를 바꿔주는거같다.

앞으로 상호간 import할때는 src폴더를 최상위로잡고 사용할수있다.

추가로 firebase.js 는 이름이 겹칠꺼같다 auth 를 임포트할때 라이브러리 이름이였기때문에 그래서

내가만든 firebase는 fbase로 이름을 바꿔서 사용한다.

---

중간에 jsconfig로 인한 경로변경 이것저것 해주는 절차가 있엇다.

---

이후 Auth (객체?) 를 받아와야하는데

`const auth = fbase.auth()` 로 받아왔다.

이게 싫다면 fbase.js 에서 auth를 `authService`로 익스포트해주고

app.js에서 임포트해서 쓰면된다.

그렇게 authService의 매서드들을 보면 이것저것있고 , 공식문서를 보자.

먼저 console.log(authService.currentUser) 를 찍어보자.

그러면 둘중하나를 반환한다. `User` or `Null`

이것을 어디다 쓰냐 -> isLoggedIn 의 초기값으로 받아올수있다.


공식문서 잘 보면 User는 PhotoUrl 이나 등등.. 유저의 정보들을 가지고있다.

jsconfig.json으로 .(닷) 의 사용을 줄여서 경로가 좀더 보기좋게 바뀌고

fbase.js 에서 중요한 key 값들까지 export해주지않고 내가 자주사용하게될 authService만 익스포트해주는것도 좋은 멋진 방법이다.

원래 app.js에서 직접 auth를 호출해서 사용하면 자주 호출해야하는데

authService에서 익스포트해주면 한번만호출하고 익스포트해서 사용한다.


---





# 튜터에게 궁금한 점
궁금한점 작성 공간!

1. vscode 터미널에 `git add .` 쳐주고   이게무슨 명령인지 모르겠습니다.

2. package.json에서 script부분에 test를 날리면 무슨효과가 있나요?

3. index.js에서  

    ```jsx
    ReactDOM.render(
        <React.StrictMode>
            <App />
        </React.StrictMode>,
        document.getElementById('root')
    );
    ```

    를 제외한 하단문구를 날리면 어떤일이 생기나요?

4. jsconfig.json으로 src폴더를 기준으로 설정해버리면 나중에 public에서 무언가 이미지나 로고를 꺼내올때 어떻게 접근하나요??
