# 이번주 리뷰
<br>

## Tweet 작성 form 과 데이터베이스 셋업

```jsx

const Home = ()=>  {
    const [nweet, setNweet] = useState("");
    const onSubmit = (event)=>{
        event.preventDefault();
    }
    const onChange = (event) =>{
        const { 
            target:{value},
        } = event;
        setNweet(value);
    }
    return (
    <div>
        <form onSubmit={onSubmit}>
            <input type="text" onChange={onChange} placeholder="What's on your mind" maxLength={120} />
            <input type="submit" value="Nweet"/>
        </form>
    </div>
    );
    
}

```
기본적으로 Home에서 이제 트윗 기능을 만들어보려고한다.

form 태그를 써서,  preventDefault 주고 ,

스테이트를 사용해서 value 를 받아와서 저장해주고있다.

이후 데이터베이스 셋팅을 하는데

cloud firestore 로 들어간다

[https://console.firebase.google.com/u/0/project/nwitter-702be/firestore/data~2F]

이후 데이터베이스 하나를만들것인데, 보안규칙에 대해서는 나중에 한번더 언급할것이며 , test모드로 일단 데이터베이스를 생성할것이다.


## 트위팅을 해보기

Cloud Firestore의 데이터베이스는 NoSQL database이다.

그래서 상당히 유연하고, 사용하기 쉽다. 규칙들도 많이없고

대신에 규칙들이 적어서 제한되는부분이조금있다.

(사용하려면 일단 firebase/firestore 임포트 해줘야한다.)
(추가로 export const dbService = firebase.firestore();로 내가부를때 저렇게 사용하기로 익스포트 시킨다.)

NoSQL의 한가지 특징은 Collection이라고 불리는것을 갖고있다.

그리고 Document라고 하는것도 존재한다.

Collection은 기본적으로 폴더와 같다.

Document는 여러분 컴퓨터애 있는 문서같은것이다. doc문서, text같은..

하나의 데이터베이스 -> collection들을 가지고있다.

그리고 각 collection은 document들을 가지고 있다.


> Cloud Firestore 에서 Start a Collection 을 눌러서 시작해보자

nweets (트윗들)을 컬렉션으로 하나 만들어주자.

(document id 는 auto로 unique하게 만들어주는거같다.)

collection은 document들이 모여서 생기는것이다.

트윗들이 모이는 컬렉선이 만들어진것이다.

그러면 이제 뭐 필요하다면 예를들어 DM 그렇다면 DM collection이 있으면 되는것이다.


---

> submit 할때마다 document를 생성해줘야한다.

Javascript- firebase.firestore 문서를 들어가서 보면

firestore의 레퍼런스들.. 그리고 각 method 들을 눌러서 볼수있다.
(collecton레퍼런스를 얻게되는데 인자로 컬렉션패스를 줘야한다.)
우리가 필요로하는것은

결과적으로는

```jsx

const onSubmit = (event)=>{
        event.preventDefault();
        dbService.collection("nweets").add({
            nweet,
            createdAt:Date.now(),
        })
        setNweet("");
    }

```

이런 코드가 되는데, nweets 컬렉션(없으면 새로만들겠지?) 에 추가한다 document를 그거는 객체형식인데 -> nweet 이게 뭐냐면

원래는 `nweet : nweet` 이렇게 된다. 하나는 db에 저장될 key의 이름이고
value는 state선언한 유저가 입력한 트윗내용이 담긴다는 의미를

shorthand property로 해결했다. 언제 생성되는날짜인지도 추가해줬다.

이후 스테이트를 빈 문자열로 초기화해주면

onSubmit (엔터만 쳐도 적용이되던데 이게 form태그를 써서그런가) 아마도..

함수가 실행되면 자동으로 빈문자열로바뀐다.

비동기 처리가되고 ~~(문서상으로는 프로미스 리턴한다고 되있는데 딱히 다른 처리는 안한거같다.)~~

관리자페이지에 가보면 db에 추가된것을 볼수있다. ( 뿌듯 )


역시 강의를 끝까지 듣다보니 바로 프로미스를 async로 받아주는모습이 보인다.


```jsx

const onSubmit = async (event)=>{
        event.preventDefault();
        await dbService.collection("nweets").add({
            nweet,
            createdAt:Date.now(),
        })
        setNweet("");
    }

```

결과적으로 이런모양의 onSubmit이 만들어지고

심지어 관리 db페이지는 실시간으로 업데이트되는것을 알수있었다.

async await 이후에 form내부가 비워지지 않길레 뭐지하고 소스코드를보니까

조금달라진점이 있었다.

```jsx

return (
    <div>
        <form onSubmit={onSubmit}>
            <input type="text" value={nweet} onChange={onChange} placeholder="What's on your mind" maxLength={120} />
            <input type="submit" value="Nweet"/>
        </form>
    </div>
    );

```

인풋의 받아오는값에 nweet으로 받아주는부분이 있는데

내가 state로 setNweet으로 빈문자열로 강제변경하면 form내부의 공간도 빈문자열로 갱신될것이다. (당연히 async await 이후에 있었으니 await이 처리되고 순차적일것이다. 즉 약간 시간걸리는걸 느낀다. db에 반영되는 시간같은 느낌인거같다.)

## DB에서 트윗 정보들 얻어오기

```jsx

 const [nweets, setNweets] = useState([]);
    const getNweets = async ()=> {
        const dbNweets = await dbService.collection("nweets").get();
        console.log(dbNweets);
    }
    useEffect(()=>{
        getNweets();
    }, [])


```
먼저 async를 주기위해서 getNweets() 함수로 따로 분리해서 어싱크 시켜놓았다.

이후 useEffect훅에서 사용하기 위함이다.

내부에서는 `await` 해서 `dbService.collection("nweets").get();` 했고 await 주기전엔 콘솔로그에 Promise가 찍혔는데

await을 주고나니까 t 라고하는 이상한 객체가 찍혔다 그래서

문서를 확인했더니

Promise : QuerySnapshot < T > 라는것을 리턴한다.

이것은 많은 정보를 가지고있는데

properties로

docs , metadata, size, empty, forEach()


```jsx

const getNweets = async ()=> {
        const dbNweets = await dbService.collection("nweets").get();
        dbNweets.forEach((document)=>console.log(document.data()));
    }

```

forEach매서드를통해서 각 document의 data들을 찍어보겠다

> data()는 메소드이다.

정상적으로 잘찍힌다!!

---

```jsx

dbNweets.forEach((document)=>{
            const nweetObject ={
                ...document.data(),
                id : document.id,
            };
            setNweets((prev)=> [nweetObject, ...prev]);
        });

```

여기보면 많은것들이 보인다.

파헤쳐보자.

forEach 각각 반복문 돌릴것이다. document는 dbNweets인 뭐 QuerySnapshot? 뭐 그런형태에 내부적으로 document들이 존재하는데 그거로 반복문들 돌린다.

거기서 새로운 객체를 만들것인데

...document.data() 해서  ES6문법인 spread attribute 문법이고

밑에 setNweets는 useState의 변경함수인데. 그함수는 저렇게 콜백내부에

prev를 줘서 이전상태를 가져올수있다.

즉 저런식으로 자주사용이 된다고하는데 (spread operator도 보인다 ...)

> 이전값에 누적을 시켜야하는경우 저런식의 코드작성이 기본인거같다.

```jsx

<div>
    {nweets.map(nweet => <div key={nweet.id}>
        <h4> { nweet.nweet}</h4>
    </div>)}
</div>

```
이렇게 트윗들을 html로 찍어주니 그럴듯 해졌다.

아쉬운건 트윗하고 실시간으로 변경되는것? 아직 좀 아쉬운거같다.

새 글을 입력하고 새값을 받아왔을때 재렌더링되게 하면 되지않을까 ?

서브밋 내부에서 트윗전체내용값을 []로 한번초기화해주고

다시 getNweet()를 호출해줌으로써 다시 db에서 자료를 긁어오게끔 해주는식으로 작성하니 해결은되었다.

## 실시간으로 해보고 , 작성자 추가하기

```jsx

const getNweets = async ()=> {
        const dbNweets = await dbService.collection("nweets").get();
        dbNweets.forEach((document)=>{
            const nweetObject ={
                ...document.data(),
                id : document.id,
            };
            setNweets((prev)=> [nweetObject, ...prev]);
        });
    }

```

이방식은 약간 구식이다.. forEach를 사용해서하는것인데.


```jsx

useEffect(()=>{
        dbService.collection("nweets").onSnapshot((snapshot)=>{
            const nweetArray = snapshot.docs.map(doc => ({
                id:doc.id,
                ...doc.data(),
            }))
            console.log(nweetArray)
        })
    }, [])

```

이렇게 훅에 dbService에서 컬렉션하나를 선택하면 거기에 있는메소드로 기가막힌게있다.

db의 변경점이 감지가되면 (listener) 그 snapshot을 찍어준다. 근데 이 때 그 쿼리객체가

`dbService.collection("nweets").get()`했을때 받아오는 객체와 같다.

그래서 이런식의 접근이 좀더 맞는거같다.

사용자가 트윗을 보낼때, 혹은 재렌더링될때마다 Db를 긁어오는 쓸대없는지 하지말고

db가 변경되었다는 리스너를통해서 확실하게 변했을때 (CRUD) 그때만 db를 갔다오면 더 효율적일꺼같다는 생각이든다.


이제 유저정보를 가져올것인데

먼저 우리는 유저에 관련된 행위를(?) authentication 때에 다뤘엇다.

그리고 항상 모든 컴포넌트의 최상단에 app.js가 있다.

그러면 즉 app.js에서는 로그인이 되었는지 확인후 라우터로 보내는 것을 해준다.

이때 우리는 로그인될때의 그 user값을 state로 따로 가지고 props를 통해서 계속 들고있다면 로그인된 유저를 기억할수있다.

props를 두번만 사용하면 되기때문에

app.js -> Router.js -> Home.js

이렇게 넘어간다.

그렇게 받아온 userObj는 onSubmit 할때 uid로 접근하면

firebase에서 각각의 유저에게 unique하게 준 uid를 db에 같이 저장할수있게 한다.

아직 해결되지 않은문제로는

db에서 값을 뽑아왔는데

트위터는 보통 시간순이다.

하지만 html로 보내서 map돌아서 찍어낸 그값은

시간순이아니라서 트윗된 목록을 보는게 불편하다.

아마 다음엔 그런문제를 개선하지 않을까 생각해본다.

(분명 메소드중에 sort라던가 시간순으로 불러온다던가, 혹은뭐 어렵지않게 map을 이용해서 내가 시간순으로 어떻게든 정렬해서 array만들어서 map으로 div 찍어준다면 해결될일이긴 하다.)


## 중간에 잠깐 공부한

### 1. filter()

    내부에 콜백함수가 들어간다.

    그 인자로 첫번째는 우리가 반복돌리게될 순차자료형의 하나하나의 요소가 나오게된다.

    예를들어보자.

    ```js
    let array = [1,2,3,"a","b",true];
    ```

    이 있다면 


    ```js
    let array = [1,2,3,"a","b",true];
    array.filter(function(i){
        //반복의 의미로 I를 사용했지만 이름보다는 몇번째 파라미터이냐가좀 더 중요하다.
        
    })

    ```
    
    그리고 filter의 콜백함수에는 boolean 한 값을 리턴해서

    원하는 조건의 값들만 추스려(?)내서 새로운 배열을만들어 준다.(immutable 하다는 뜻)

    ```js
    let array = [1,2,3,"a","b",true];
    let result = array.filter((i)=>{
        return typeof i === 'number'
    })
    console.log(result) // [1,2,3]
    ```
    처음에 콜백함수 내부에서 if문으로 돌렸는데

    결국 return true, false이기때문에 저런식으로 작성하는일이 더 많아진거같다.

    arrow펑션도 처음배울때와달리 손에 익어 잘 쓸수있는거같다.

    생략할수있는것도 뭐뭐 있는지 알지만 아직 쓸수있는데로 쓰고있다..

    parameter가 하나면 보낼때 소괄호 생략가능

    함수body에 return문 하나밖에 없다면 body를 감싸는 중괄호 생략가능
    (거기에 return도 생략가능)



### 2. map()
    맵은 보통 특정 행동을 시킨다.

    즉 [1,2,3] 이런배열이 있다면 모든배열 요소에 2씩 곱하기 를 해줘

    ```js
    let array = [1,3,4];
    let result = array.map(i=>i*2);
    console.log(result) // [2,6,8]

    ```
    마찬가지로 이뮤터블하다.
### 3. reduce()
    리듀스는 약간이 각 요소간의 이동할때 상관관계가있는 조건으로 반복문을 돌려야할때 쓰면 좋은거같다.

    첫번째요소에서 무언가 비교,혹은추출,혹은변경,혹은누적 된 어떤것이 이후의 검사할 요소와 상관관계가 있는가? 이후 절차에 영향을끼치는가?

    그렇다면 reduce를 쓰는게 맞다.

    ```js
    let array = [1,3,4];
    let result = array.reduce((acc,cur,index,arr)=>acc+cur);
    console.log(result) // 8

    ```

    모든항을 더해주었다.

    acc는 누산기 누적되는값이다. 초기값은 지정해주지않으면 reduce사용되어지는 0번째 인덱스의 자료를 가질것이다.

    초기값을 주면 cur(currentValue) 현재 보고있는값이 0번인덱스부터 볼것이고,

    초기값을 주지않으면 1번인덱스부터 비교하게된다. (초기값안주면 자동 0번인덱스 값이니까) 0과1 비교? 누산 > 누산값 과 인덱스2번 비교->누산 -> 누산값 과 인덱스3번 비교 ... 이런방식이다.

    각 순회할때의 index가 3번째 파라미터이며

    reduce를 도는 연속된 자료형 자체가 arr로 4번째인자로 받는다.

    주로 acc,cur를 주로 쓰게되는거같다.

    

# 튜터에게 궁금한 점
궁금한점 작성 공간!

1. form 태그를 계속 쓰는게 보이는데, 장단점이 좀 궁금한거같아요 button들과 form태그 쓰임새가 많이다를까요?

2. 함수들을 파라미터로받고 그함수들을 서로 체이닝 걸어서 마지막에 함수의 체인이 완성된 그 함수를.. 리턴해주고싶은데 방법이 있을까요?

```js

  function square(num) {
    return num * num;
  }
  function add5(num) {
    return num + 5;
  }
  function mul3(num) {
    return num * 3;
  }
  function isOdd(num) {
    return num % 2 !== 0;
  }


let sumFunc = 내가만든함수(square,add5,mul3,isOdd);
sumFunc(4) // 4를제곱하고 , +5되고 *3되고 , 그값이 홀수인지 판별 이런순서. 이런게 될까요 ?
```

이런게 될까요 ?? 흠 ..