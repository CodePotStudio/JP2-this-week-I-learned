# 이번주 리뷰
<br>



## Velog 블로그 시작

기본적으로 블로그에 하나씩 TIL 을 작성해서


.. 링크 첨부 해두겠씁니다!

(아직 있는게없는 벨로그입니다.)[https://velog.io/@gatsukichi]
## 계정 생성 기능 다시보기

전체적인 흐름 훑어보기

1. 로그인 상태는 (state변수는) 기본적으로false 이다.
2. onSubmit 함수는 form에서 submit (버튼역할하는태그) 를 눌렀을때 발생하는 함수이다.

3. 이때 async를 걸고 이벤트를 인자로하는 Arrow펑션을 잡는다. 

4. 내부에서 preventDefault 를 걸어서 form태그에 onSubmit의 기본적인 행동인 페이지를 새로고치는(이동시키는) 기능을 수동으로 제어하기 위해서 정지시킨다.

5. 이후 try , catch로 에러를 잡아낼것이며

6. try안에서 if문으로 계정 상태가 true,false인지에 따라서 다르게 동작하게 코딩한다.

7. 내부에서 await로 firebase authService의 각 매소드 (이메일,패스워드 받아서 유저생성하는것  / 이메일 패스워드 받아서 로그인 확인하는것) 으로부터의 응답을 기다린다.

8. 받고나면 아직 로그인 되었다는것을 보여줄수는 없다.

9. 대신 firebase 관리 페이지에서 사용자가 등록된것을 볼수있다.

이러한 흐름이다.
(참고로 로그인? 관련된 쿠키가 브라우저 저장소 어딘가에 들어있다.)
## 이제 해줘야하는 일

persistance  : 지속성

setPersistence 매서드를 사용해줘야한다.
- 나의 사용자들을 어떻게 기억할것인가? 를 정해준다.

리액트네이티브의 앱과 브라우저에서의 디폴트값은 `Local` 이다.

setPersistence에서

local : 브라우저를 닫더라도 사용자의 정보를 기억하고있다.

session : 탭이 열려있는동안에 사용자의 정보를 기억하고있다.

none : 유저정보를 기억하고있지 않는다.

로컬에 저장된 유저정보 위치
IndexedDB -> firebaseLocalStorageDB - 사용자주소 -> firebaseLocalStorage

## login 시키기

### 로그인상태를 확인하지못했던이유 ( currentUser를 받아오는데에 시간이 필요하다)

제목과 마찬가지로 기본적으로 console.log와

```jsx
console.log(authService.currentUser); // null 찍힘
setInterval(()=>{ //2초뒤에 찍어보면 값이 찍힘
    console.log(authService.currentUser);
}, 2000)
```

이렇게 확인해본결과 너무 빨리 유저의 데이터를 확인했던거같다. - (내생각은 그럼 await 해주면 되는거아닌가 ? )

영상을 이어서 보도록하자. 어떤식으로 문제를 풀어갈지

첫째 모든 값들 이 들어온지 확인해주는 state를 하나 만들고 디폴트로 false를 준다. 이를 init ,setInit 이라고 하겠다.

두번째로 useEffect 훅을 사용할것이며

마운트가 완료되면 실행되는 조건으로 무엇을 주면좋을까

이때 js SDK 가  필요하다.

문서를 보면 onAuthStateChanged 라는 매서드가 있다

즉 인증상태가 변했는가? 를 확인해주는 옵저버 역할을 한다.

로그아웃할때, 계정을 생성할때도 트리거로써 사용할수있다.

```jsx

useEffect(()=>{
    authService.onAuthStateChanged((user)=> console.log)
}, [])

```

해보면

마운트이후 옵저버를 띄우고

값이변하면 그거 바로 콘솔로그로 띠워줘

해서 **뙇** 하고 나타난다.

여기서 옵저버는 계속해서 변할때마다 반응하는데

hook 자체는 한번만 실행되지 않는가 ??

음 로그아웃했을때의 코드는 그때 다시 짜겠지 일단

넘어가도록 해야겠다.

여기까지 문제없이 되는가 싶더니

일단 첫번째로 분명 firebase auth관리 페이지에 가면 내가 등록한 이메일이 존재한다.

하지만 결과는 이미존재하는 이메일이라고 뜬다.

예상해볼수있는 버그는

Create Account 버튼이 로그인은 안돼고 그저 계정생성만 해주는 것이다..

아까 계정등록안된다고 

기본값 False 인 스테이트를 true로 함부로 바꿧다가..

걸린 버그같다.

아까 바꾼값은 처음 접속하면 기본적으로 계정생성하세요 를 정해주는 boolean 이였다.

~~당연히 false가 맞다. 그래서 그 값과 연결된 if문이 당연히 오작동 했던것으로 보인다.~~

> 아니고 아직 newAccount와 Login 을 토글해주는 기능을 만들지 않았다.

불편한점은 한글입력과 영문입력이 다르게 들어가서

영어로 된 비밀번호에 한글비밀번호가 들어가게되면

비밀번호가 잘못되었다고 결과가 돌아온다.

> 훅에 대한 이해가 부족함을 느꼈다.

일단.. 이어서 듣고 훅을 복습해야겠다 ㅠㅠ

### 추가기능으로 로그인이 안될때 에러메시지 표시하기

비밀번호가 6글자 이하이면 에러메시지를 화면에 띠워줘야하고..

어떠한 에러가 발생했을때 firebase에서 날리는 에러메시지가 있다

그거 그대로 화면에 띠워주면된다.

const [error,setError] = useState(""); 먼저 빈공백으로 유즈스테이츠 만들어주고


catch(error) 로가서

setError(error.message); 해주고

html의 어딘가에 error 를 써주면 된다.

에러가발생하면 스테이츠가 변경될것이고

그러면 재 렌더링이 될테니

에러르 보여줄수있다. (나는 alert 생각하긴했는데.. 크롬사용자로써 alert 뜨면 좀 불편하긴하더라 ..)


> state의 이전값은 (스테이트이름은 임의로 지은것) `setMyboolean((prev)=>{ !prev })`로 써 스테이트변경함수에 콜백함수를 주고 그인자로 prev를해주고 변경값을 (아마 boolean 타입이라서 쓰는것일듯) 약간의 인과관계를 줄수있다. 아무래도 단순히 `setMyboolean(!myboolean)` 이렇게하는거랑 사실 무슨차이지 싶긴하다..

로그인 기능 완료!! 

확실히 하나의 기능을 만들때 분명이 로그인이면 매우 어렵고

백엔드에서 많은 절차를 거치고

또 스파르타때를 생각해도 로그인은 엄청 어려우니 나중에 하세요 했을만큼 어려웠을꺼라고 생각한다

하지만 역시 firebase 는 이러한 로그인기능을 매우 쉽게 구현한게 맞다..

인증도 내가 따로 서버를 만들고 어떠한 일련에 절차를 만든것도 아니며..

관리또한 firebase내에서 모두 지원한다.

써보니까 `최고`다.


## 소셜 로그인 기능

사용할거같은 기능 

1. signInWithPopup //팝업창으로 인증시킨다는것 ( 각 소셜서비스의 팝업이 뜨지 않을까 예상)
2. signInWithRedirect // 리다이렉트 시켜주는데에 필요한 매서드로 보이는데..

- 두개를 같이 쓰는건 아니라고 한다.

- ~~signInWithRedirect 를 써서 해보도록 하자.~~
    - 만들어야할 function 들이 너무 많아서 거르고
    - 여기서는 pop-up 으로 한다.


---

continue google , github 버튼에

각각 name 을 google, github 로 지정해주고

함수를 하나 만들것인데

```jsx

const onSocialClick = (event)=>{
    const {
        target : {name},
    } = event;
    if(name==="google"){

    }else if(name==="github"){

    }
}

```
대략적으로 이러한 그림으로 버튼 클릭했을때 어떤 버튼인지에 따라서

내부 if문으로 기능이 분리된다.

provider 라는것을 만들것이다.

그게뭐지? 제공자 ?

결국 니꼬도 하다가 , 효율좋게 firebase를 임포트해서 필요한 기능만 익스포트해서 사용 하려고 했는데

실패했다. 그냥

`export const firebaseInstance = firebase`

로 firebase에서 제공하는 전체 객체를 통째로 인스턴스로 익스포트 시켜서 사용하는것을 볼수있다.


그래서 각 Provider를 구글과 깃허브 각각 다르게 If문 내부에서 선언해준다.

즉 google로 인증하기 누르면 구글 Provider를 받아오고

github로 인증하기 누르면 깃헙 provider를 받아온다.


그리고 popup 매서드를 사용할것인다.

await 해줘야한다.

당연히 감싸고있는 내부 함수는 async 해주자.

(거기에 provider을 인자로.)

`await authService.signInWithPopup(provider);`

`let data = await authService.signInWithPopup(provider);`

하고 console.log(data) 했을 뿐인데..

잘된다..

구글인증 , 깃헙인증 모두 잘된다. 나이스~~!!

## 로그아웃 기능 만들기

하지만 먼저 Home의 모양새를 먼저 좀 바꿔주자.

tweet을 쓸 수 있는 형태가 되어야 한다.

추가로 네비게이션 도 만들어줘야하므로

components/Navigation.js 를 만들어주자.

```jsx

import React from "react";

const Navigation = () => <nav>lalala</nav>

export default Navigation;

```

이후 Router.js 내부에 Router컴포넌트 최상단에
{isLoggedIn && <Navigation />}

해주는것인데 이거 어디서 많이봤다.

&&의 문법인데 그자리에 무엇이 남는지 정해주는식이였던거같다.

### &&과 || 의 단락평가인가??

exp1    exp2   (앞)표현식 1과 (뒤를)2라고 칭하겠다
truthy && truthy  // 앞뒤 둘다 참값이면 표현식2(뒤에값)을 리턴한다.(남긴다)

false && falsy // 는 뒤에 false를 리턴하고
falsy && false // 는 앞에 falsy한 값을 리턴한다.

살짝 어떤 로직인지 감이잘 오지않는다..

&&은 둘다 true여야 true인 로직이다. 그래서

중간에 t && f  , f && t 는 false를 남긴다.

이제 주로 사용할만한 로직은

truthy & truthy 하면 오른쪽값까지 확인하니까 오른쪽을 남기는거고

truthy || truthy하면 왼쪽값이 확인되면 뒤에값을 볼필요도없으니 왼쪽값이 남는것이다. 일단 이거만 기억하자. 나머지는 크게?? 그때그때 찾아보는것으로.

## useHistory

프로파일 페이지에서 로그아웃 시켯더니 잘되는데

아직 url 이 profile에 있게된다.


라우트단계에서 리다이렉트 시키는방법도 있지만

Profile.js 에서 로그아웃버튼을 눌렀을때 훅을 걸어서 뒤로가기 시킬수도있다.

그게 바로  useHistory 이다.

```jsx

const history = useHistory();

//사용할 위치
history.push("/");

```


# 튜터에게 궁금한 점
궁금한점 작성 공간!

1. (스테이트이름은 임의로 지은것)  
`setMyboolean((prev)=>{ !prev })`  
`setMyboolean(!myboolean)`  
두가지 방법에 차이점이 있을까요? 문법적으로는 밑에 가 훨씬 쉬운것 아닌가요 ??