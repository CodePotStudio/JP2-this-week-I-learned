# 이번주 리뷰
<br>

## 쓸데없는 재렌더링을 막는 memo

잊지말자 useEffect 훅 <- 로드가 완료되었을때, 사라졌을때 사용가능

props 내용이 변경되면 내부 div등이 재렌더링된다.

사용하지않은 props의 내용이 바뀌어도 재렌더링한다? => 비효율적이다.

그래서 memo()를 사용한다.

props를 기억하겠다. memorize의 약자로 생각하면 좀더 기억하기 쉽다.


props가 변경이 안된 컴포넌트는 재렌더링 하지 말아주세요~

컴포넌트를 memo라는 함수() 로 감싸면 된다.

`react 에서 improt {memo}`


```jsx


function Parent(props){
    return (
        <div>
        <Child1 이름={props.이름}></Child1>
        <Child2 나이={props.나이}></Child2>
        </div>
    )
}

function Child1(){
    useEffect(()=>{console.log("렌더링됨1")})
    return <div>1111</div>
}

//function Child2(){
//    useEffect(()=>{console.log("렌더링됨2")})
//    return <div>2222</div>
//}

//여기서

let Child2 = memo(function(){
    useEffect(()=>{console.log("렌더링됨2")})
    return <div>2222</div>
})

//이런식으로 memo를 사용할수 있다.
```

> memo()의 단점
> 기존 props vs 바뀐 props    = 비교연산후
> 컴포넌트 업데이트할지 말지 결정함
> props가 양이 굉장히 많으면 사이트가 느려질수있다. 잘 판단.
> 컴포넌트 크기가 클때 잘 고려해볼것.


## PWA 10초만에 발행하기 ( 모바일앱 인척 사기치기 )

Progressive Web App

앱처럼 부드러운 사이트가 완성되었습니다.

가끔 PC든 모바일이든 => 앱을 설치하시겠습니까? 가 뜬다.

실제로 앱이랑 매우 동일하게 동작한다 

(실제로는 거의 바로가기만들기 수준.. 앱을발행한다.)

이런식으로 운영하는것은 외국에 많다.

원래 앱스토어에 들어가서 마케팅하면 비싸다.

웹방문 유도하고 마케팅하면 싸다.

2개의 파일이 필요 (파일 생성)

1. manifest.json

2. service-worker.js

create-react-app 만으로 파일생성이 되는 조건이 예전에는

build해주면 파일두개 모두 생성해줫는데 이제 manifest.json 파일만 생성해준다.

그래서 service-worker.js까지 자동으로 생성을 원한다면 프로젝트를 처음에 만들때

`npx create-react-app 프로젝트명 --template cra-template-pwa` 로 터미널에 입력해야한다.

프로젝트 다시만들어서 중요파일들 복사 붙여넣기해서 옮기는게 좋을듯.

시도해보았다.

yarn 을 사용하니까 명령어가 기억나지않아서 구글링

create-react-app 관련 레퍼런스에서 

`yarn create react-app my-app` 를보고

`yarn create react-app 프로젝트명 --template cra-template-pwa` 으로 실행해보았다.

어떤 패키지들을 설치했는지, 명령어들을 정리를 따로해놓지 않아서

깃허브 TWIL 하나하나 찾아보거나 구글링해봣던게 흠인거같다.

`package.json` 에서 어느정도 무엇이 깔린정도는 알수있지만..

다시 패키지를 설치하려니 좀 힘든??..

혹시 패키지 설치할때 `package.json` 내부에 설치된 패키지 밑에 주석으로

어떤 명령어로 설치했는지도 적어두면 나중에 편하지않을까??

(사실 이런 패키지 관리밑 버전관리 때문에 docker를 쓰는거아닐까..)

이후 `index.js` 파일 하단에

> `serviceWorkerRegistration.unregister();`  
> 을  
> `serviceWorkerRegistration.register();`  
>  
> 로 바꿔주면 끝.

`yarn build` 이후에

파일두개 생성되는것을 볼수있다.

웹서버에 올리면 리액트발행은 build폴더를 올리면된다.

1. `manifest.json`
    - 아이콘,이름,테마색상 (앱의 생김새 설정파일이다)
    - short_name : 어플아이콘 밑에 뜨는이름
    - name : 정식명칭
    - icon : os마다 필요로하는 아이콘 크기가 다를수있으니까 여러게 들어있다보통
    - start_url : 시작 url 처음 앱실행하면 나오는 주소
    - display : 상단바 제거하거나 등등.. 웹처럼 안보이게할수있다.
    - background_color : 킬(실행)때뜨는 배경 색 

2. `service-worker.js`
    - 앱은 마켓에서 설치해서 쓴다 => 모든 이미지,데이터 등등 하드에 저장된다. 앱의 동작방식 => 그걸 흉내내는거를 도와주는 파일

    - 웹앱 -> 서버로 보내는 데이터가있다. HTML/CSS/JS 를 보내고 하는데.

    - service-worker.js 가 있으면 중간에 가로챈다.

    - "너 이 이미지 이미 하드에있는데? " 중간에 가로채서

    - cache로 한다?


3. `precache-manifest`
    - 설치(캐싱)할 파일 목록들 이다.



### PWA 맞는지 확인하려면

크롬 - 개발자도구 - application 탭 들어가서

manifest 에서 보면 manifest.json에서 설정한것들이 잘 적용되어있는지 디버깅해볼수있다.

service Workers 로 보면 source에 service-worker.js 가 도와주고있는게 보인다.

cache 탭에 가보면 스토리지에 어떤 데이터들이 이미 다운되어있는지 볼수있다.

offline에서 사용가능하다. (프로그래시브앱들의 장점은 인터넷이안되도 잘 작동한다는것. )

크롬 디버깅창 -> Lighthouse 가서 카테고리 progressive Web App 해보면 점수로 평가를 해볼수있다.

workbox라는 라이브러리 덕분에 PWA 발행이 쉬운것이다.

세부설정을 바꾸고싶어.. 어쩌지

HTML은 캐싱하기싫어 -> precache-manifest를 수정해도 되지만..

1. node_modules 폴더 내부에
2. reasct-scripts 폴더 내부에
3. config 폴더
4. 그내부에 webpack.config.js 라는 파일을 열어보면
5. 밑에 ctrl+F 같은 단축키 써서 GenerateSW 부분을 건드리면된다.

workbox.js 라이브러리 참고해야한다. 
(exclude 같은곳에 정규식으로 index.html 같은거 추가해놓으면 캐싱을 하지않는 목록에 추가된다.)

## DB없이 데이터 저장하고싶으면 localStorage

장바구니에 추가를해도.. 자꾸 기본값으로 돌아간다, 새로고침이나, 브라우저 껏다키면.

그럼 어쩌지

state데이터를 기억하게 하려면

- 서버로 보내서 DB에 저장
- 브라우저 저장공간에 저장 (어딘데 크롬 개발자도구 - > application storage 에있다.) 
- key, value로 구분되어있다.

- session Storage는 브라우저 끄면 날라간다 (휘발성있음)

- local Storage : 순전히 텍스트만 저장가능  5MB 정도

- 최근본 상품 같은거 저장하면좋다. 

- localStorage 다루는문법은? 3개정도면 ok

    1. `localStorage.setItem('name','kim') // 자료 저장`
    2. `localStorage.getItem('name') // 자료 출력`
    3. `localStorage.removeItem('name') // 자료 삭제`

- sessionStorage 다루기?
    1. `sessionStorage.setItem('name','kim') // 자료 저장`
    2. `sessionStorage.getItem('name') // 자료 출력`
    3. `sessionStorage.removeItem('name') // 자료 삭제`


> localStorage에 object자료를 저장하려면 => 그냥넣으면 깨진다.

> object형자료를 강제로 문자로 바꾸면 깨진다 => `[object Object]`이렇게 됨

> 배열은? -> 문자로 그냥 다바뀜.. 

> 배열과 obj파일을 손실없이 저장하고싶다.

- 글자인척 하면된다. 그러면?

localStorage.setItem('obj', {name:'kim'})

localStorage.setItem('obj', "{"name":"kim"}")

전부다 "" 따옴표쳐서 JSON 만든다?

JSON.stringify() 내부에 오브젝트 넣으면 알아서 따옴표 쳐준다.

getItem을 쓰면

따옴표 쳐진 텍스트가 그대로 튀어나온다.

그래서 사용하려면

변수에 저장해서 양끝에있는 따옴표를제거하면되는데

따로 힘빼지말고 JSON.parse() 함수를 사용해서

양끝에 따옴표를 제거할수있다.

---

내가 짠 코드

```jsx
let recent_view = JSON.parse(localStorage.getItem("recent_view"));

//중략
    if(recent_view!==null){
        let temp_view = [...recent_view];
        if(temp_view.indexOf(id-0)==-1){
          temp_view.push(id-0);
          localStorage.setItem("recent_view",JSON.stringify(temp_view));
        }
      }else{
        let temp_view = [];
        temp_view.push(id-0);
        localStorage.setItem("recent_view",JSON.stringify(temp_view));
      }


```

Detail 컴포넌트 내부에서 let변수로 최근 접근한 id들을 모으는 자료형을 만드는데 기본적으로 로컬스토리지에서 가져온다. (콘솔로그 찍어본결과 없으면 null을 가져온다.)

지난번 사용했던 useEffect 내부에서 작성한 이프문인데

recent_view 변수가 null이 아니면 temp_view로 먼저 풀어서 선언해주고
만약 그값중에 현재 들어온 디테일페이지의 id 가 있는지? indexOf 매서드로 검사해준다. 없으면 -1을 리턴해주니까 없다면 추가를하는데
temp_view에 푸시 id 해주는데 
id가 문자형 자료로 되있어서 "0" 이런식으로 들어가게된다.

id-0을 해준이유는 숫자자료형으로 변환해주려고 쓴 잡기술이다.. +0해보려고했는데 문자자료+0 하면 "문자자료0" 이렇게 되다보니 -0 이 먼저 떠올랐다.

그리고 else로 로컬스토리지에 값이없으면 빈어레이 선언후 현재 값을 푸시해라. 이렇게 짰다.

set자료형을 생각안해본건 아니지만 조건문으로 해결하긴했는데

간결한 코드로 해결할수있다면 그게 더좋은 로직이지 않을까 싶긴하다.

해설 코드

```jsx

useEffect( ()=>{
  var arr = localStorage.getItem('watched');
  if( arr == null) { arr = []} else { arr = JSON.parse(arr) }
  
  arr.push(id);
  arr = new Set(arr);
  arr = [...arr];
  localStorage.setItem('watched', JSON.stringify(arr) );

}, [] );

```

유즈이펙트 내부에서 겟아이템 해서 리스트가져오고

값이없으면 빈어레이
있으면 JSON.parse해서 따옴표풀어서 가져온다.

그리고 푸시 id 해주고 new Set해주고 다시 풀어서 arr해주면

리스트에서 중복되는 값을 제거하는 로직으로 사용할수있다.

실제 강의자료에서는 ["0","1","2"] 이런식으로 담기는데

나같은경우는 [0,1,2]이런식으로 담기니까 좀더 가공하기 쉽지않을까생각한다..

---

~~https://react-sticky-box.codecks.io/~~

검색어로는 floating bar

side-panel 등등..

괜찮은 라이브러리를 찾아서 이것으로 해보려고한다..

불가능..

sticky side bar

flex.. 역시어렵고

side bar 구현에 실패한건가 싶긴하다 .. 좀더 도전해보겠지만 완성된 코드를 보이고싶은데 무섭다;;


# 튜터에게 궁금한 점
궁금한점 작성 공간!

1. 패키지 다시 설치하려니까 명령어가 하나도 기억이안나서 애먹었습니다 (프로젝트 재생성 복붙 과정) 이때 docker를 잘 다룰줄 알았다면 훨씬 쉽게 프로젝트하나를 복붙 할수 있었을까요 ?

2. 문자자료형 에서 -0으로 숫자자료형으로 바꾸는게 안좋은 습관일까요?

3. 사이드 메뉴 (퀵메뉴) 같은것을 구현해보려고하는데.. (localstorage를 배우고나서 써먹고싶어서) 어려워서.. npm도 찾아보고 bootstrap도 찾아보고 했는데 뭐 방법이 있을까요?? 차라리 어디 라이브러리 컴포넌트 따오지말고 직접 디자인 하는게 쉬웠을까요 ?

4. wakatime이 전날 기준이여서 이미지가.. 3시간 이하로나올때는 어떻게해야하나요? 이번주에 좀 몰아서 하다보니까 토,일,월 이렇게해서.. 지금 월요일 소모 시간까지 합쳐야 3시간이 넘는데 .. 12시넘어서 wakatime이미지만 올려도 될지..