# 이번주 리뷰
<br>


## Login form 만들기

### Authentication sign-in method

먼저 로그인시 인증에 사용할 절차들은 firebase console 페이지에 들어가서

셋팅해줍니다. 

이메일+비밀번호를 이용해서 인증할것이고

구글 -> 서포트 이메일 (뭔지 잘모르겠는다.)

깃허브도 연결해서 인증할수있다. 사전에 app신청이 필요하다.

1. 깃허브이동
2. settings
3. developer settings
4. OAuth apps -> Register a new application
5. firebase깃허브 인증 밑에보면 URL이 하나있는데 그거 복사해서
6. OAuth apps 셋팅에서 Homepage URL 과 callback URL 에 둘다 사용할것이다.
7. 이때 원본이 `https://nwitter-702be.firebaseapp.com/__/auth/handler`라면
    - 홈페이지URL : `https://nwitter-702be.firebaseapp.com/`
    - callback URL : `https://nwitter-702be.firebaseapp.com/__/auth/handler` 
    이렇게 사용했다.
8. 그러면 Client ID 와 Client Secret을 주는데 이것을 firebase setting 창에 복붙해준다.

---

Auth.js를 일단 Arrow Function에서 return을 쓸수있게끔 중괄호를 쳐주고 해서 return 부( html태그 들어감 ) 위에는 변수와 state를 쓸수있게끔 수정을좀 해주고.

email,pw 를 state로 받게 셋팅하고 
onChange() 어떤 event(변화) 발생시 해당 html태그의 name을 들고와서 그게 email,password인지 확인하고 그 input란의 값인 value를 가져와서 setEmail , setPassword 인 state변경함수에 집어넣어서 state값을 수정한다. (이때 재 렌더링 된다.)


onSubmit() <- 이거는 아직 기능구현 안했다 (아마 다음장?) 아닌가 ?

### Creating Account

먼저 firebase 문서에 가서 EmailAuthProvider를 보도록하자.

Creating Account 하다가

Promise 를 리턴하는 Auth 의 매서드를 사용했는데

이때 nomad는 async와 await 을 사용했다.

```jsx

const onSubmit = async (event) => {
        event.preventDefault();
        try{
            let data;
            if(newAccount){
                data = await authService.createUserWithEmailAndPassword(
                    email,password
                )
            } else {
                data = await authService.signInWithEmailAndPassword(
                    email,password
                );
            }
            console.log(data);
        } catch(error){
            console.log(error);
        }
        
    }

```

이런 구문인데

try catch로 오류를 잡아내게끔 해주고

내부에서 새로운 계정인지 확인하는 조건을 돌려줍니다.

이때 data를 authService에서 받아오는데
(authService는 fbase에서 익스포트되어서 auth.js로 임포트되어있다.)

authService의 내장함수인 createUserWithEmailAndPassword()와
signInWithEmailAndPassword()을 이용하는데 파라미터로 email과 password (state로 기록되어있던) 값을 같이 보내준다. 그리고

이때 해당 메서드들은 프로미스를 리턴해주므로 await 으로 받는다.

내가 막상 작성해놓고 봐도

promise라서 await으로 받는다? async 로한다?

지난주에 배운것인데 복습할필요성이 ... 너무느껴진다

아무래도 문서를 다시 뒤져보거나

튜터님깨 promise까진 이해가되는거같은데

async await이랑 뭔가 머리속에 따로 노는거같습니다. 하고 질문해야겟다.

await은 기다린다. 비동기처리를 뭔가 동기처럼 해줘서 그 요청의 결과를 받을때까지 응답을 기다리는거로 직역할수있는데

반대로 async가 잘 이해가 안되는거같다.

기억으로는 async를 먼저 해야했던거같은데.

둘중 하나만 쓰는케이스는 없엇던가 항상 두개가 같이 사용되었던거같고

체이닝을 걸게된다면 쭉쭉 동기로 처리해야한다는것과

다중으로 await받을수있다는것 정도를 기억하고있는거같다.

야밤에 그냥 튜터님 미디움에 들어가보았다.

스크롤 조금내리니 이미 결론이 나와버린

Async (일반함수를 Promise를 return하는 함수로 바꾸기)

즉 항상 Promise로 마들어주기 어렵다 ? 번거롭다 그렇기때문에

내가 어떤 함수를 통째로 Promise 처럼 쓰고싶어

Async 그러면 리턴이 Promise이게 된다.

그러면 Await은 Promise가 이행될때까지 기다리자 이건데

Promise도 헷갈려서 문서를 더봤다..

Promise는 리턴이 두개야.

내가느낀건 그래, 근데 생김새는 콜백함수를 넣는데 파라미터로 resolve와 reject를 넣는다.

얘내는 어떻게보면 함수인데.

상태를 리턴한다고해야하나.

resolve("데이터들") 이렇게 보내면

resolve ( fulfilled ) 되었다. 그안에 데이터가 저렇게 찍힌다.

reject도 마찬가지 (rejected)

그럼 resolve되었을때 그값은 어떻게 접근해?

그래서 then을 쓰는것이다.

콜백함수로 받아서 첫번째인자로 response넣고

그걸 콘솔로그로 찍으면 값이 보일것이다.

이때 promise의 체이닝으로 또 콜백으로 만들어서 response를 받는 애로우펑션 만들어서 return 다른프로미스(response) 이렇게 해서 또 then으로 받는식으로 체인이 가능하다.

하지만 이방법은 결국 then을 계속 써야하고 내부에서 response로 받는 애로우펑션을 계속 써야한다는 불편함이 아직있는것이다.

그러면 ??

Async의 편리함

내가 아무 생각없이 크롬 개발자도구를 켜서 1을 리턴해주는 함수르 만들었다.

그냥 해보면 1이리턴된다.

Async를 붙여서 호출하면

fulfilled 되었다고 뜨며 프로미스가 리턴되고 그안에 1이 보인다.

await은?

이게 맞는지모르겟는데

그냥 이렇게 해서 직관적으로보니까 이해가 빠르게된다.

```js

function aa(){
    return 1;
}
//1
async function aa(){
    return 1;
}
aa()
// Promise {<fulfilled>: 1}__proto__: Promise[[PromiseState]]: "fulfilled"[[PromiseResult]]: 1

await aa();
// 1

```
결과가 딱 눈에 들어오는데 선언할때 async

사용할때 await 아닐까?

다시 쉽게 생각해서

내가 어떤 api 를 받아와서 그값으로 화면을 구성해야한다던가 그런게 필요한데

먼저 렌더링을하거나 그러면 안되고

그 값이 다 받아와질때까지 기다려야한다 그렇다면??

먼저 값을 받아오는 기능자체를 함수화 해야겠지 안에는 fetch 가 있을수도있고

ajax요청이 있을수도있고.

그렇다면 그 함수자체를 async 붙여버리고

나중에 그 함수콜을 할때

await으로 받으면 되는거아닐까 ??

사실 조금 걱정되는것은 ajax나 fetch 앞에 await을 붙여야 하는지.

fetch는 promise를 리턴한다고 했다. js 내장 함수라고 했으니까

그럼 async는 필요없을수 있겟구나.

함수가 막 진행되다가

fetch앞에 await을 만나면 일단 fetch가 요청이 완료되서 돌아올때까지 기다리지 않을까.

그럼 쉽게생각하면

- 공식문서나 이미 만들어진 기능중에 promise를 리턴하거나

- 혹은 내가 Promise를 미리 만들어놓은경우

에는 await만 사용해서 기다리게 할수있겟구나.

그럼 async는 그냥 함수의 리턴을 프로미스로 바꿔주는얘 ?

그렇게 생각하면 되나.

> - 혹은 내가 Promise를 미리 만들어놓은경우 이거를 

더 편하게 하기위해서 async를 쓴다고 생각하는게 맞나?

일단은 여기까지 이해했다고 보면될꺼같고

튜터님께 다른건 이해가 어느정도된거같은데 어싱크어웨잇만 한번만 부탁드려봐야겠다.



# 튜터에게 궁금한 점
궁금한점 작성 공간!

1. firebase에서 google인증 설정을 하게되면 프로젝트의 공개용 이름 과 프로젝트 지원이메일? 이런 란이 있는데 어떤것인지 잘모르겠습니다. 혹시 알수있을까요 ? (사진 별첨)

2. ```jsx
    const onChange = (event) => {
        console.log(event.target.name);
    }
    const onSubmit = (event) => {
        event.preventDefault();

    }
    ```
    이 두가지 Hook 의 기능에 대해서 잘모르겠습니다.!!
    (email,password 에대한 onChange function을 두개 만들기 싫어서 이렇게 했다고? 만 나옵니다.)

    - 추가 강의에서 나오네요.. 기본적으로 Log In 버튼을 누르면 새로고침이 되는데 ????? -> input태그와 type="submit" 이 만들어주는 콜라보.. email,password를 url에 담아서 보내준다 (GET요청처럼) 그럴때 원래 새로고침이되는데 이것을 방지하기위해서 preventDefault(); 를쓰면 이 기능이 기본값으로 실행되지 않게하겠다. 이기능은 내가 만들어서 쓸거다 이런느낌일까요?..

3. ```jsx
    const {
            target : { name, value},
        } = event;
    ```

    2번질문에서 event.target.name 으로 찍어봤엇는데

    저렇게 target : {name,value} 이렇게 열어두고
    event 에서 값을 가져오는것일까요??
    
    - 이해를 해보려고 노력해서 console.log로 event도찍어보고
    event.target 도 찍어보고 했는데
    event는 어떤 특정이벤트의 정보를 모두 포함한 객체가 찍히고
    event.target은 그중에 html태그가 찍히는데 여기서 내가 지정한 name은 한마디로 그 인풋태그의 이름인것이고 , value는 내부 값이 변할때마다 같이 따라서 변한다. 그래서 이프문으로 이벤트발생내부 타겟이뭐냐에 따라서 email,pw를 한번에 처리해주는 onChange function을 만들어서 사용한것으로 보인다. 아마도 ..?
