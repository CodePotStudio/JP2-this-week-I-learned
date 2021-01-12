# 이번주 리뷰
## PART 3. 실무에 필요한 부가내용(끝!) - 진짜 끝
## (1) 컴포넌트가 많을 때 props 대신 context API            
컴포넌트 안에 컴포넌트가 많아진다면, props를 연달아서 사용해줘야 한다.          
이럴 때 보통 Redux나 Context를 사용한다고 함! 이를 이용하면 하위 컴포넌트에서 state값 공유가 가능하다.          

**Context문법으로 props없이 state 공유하는 단계**            
1. ```createContext()```라는 함수를 이용하여 context를 만든다. (ex : ```let 재고context = React.createContext();```)                
2. 공유를 원하는 컴포넌트들을 아까 만든 context를 사용해서 감싼다. (ex : ```<재고context.Provider value={공유할 state이름}```)              
3. state를 사용하고자 하는 곳에 useContext()를 이용해서 context를 불러오면 끝!          

> 하면서 이게 편한가? props보다 복잡하다는 생각을 했는데, 컴포넌트가 중첩이 많이 될 때 편하다고 한다...                     

만약에 다른 파일에 context를 써야 하는 경우에는, context 생성시에 export해주고 import 해주면 된당.  <br>
<br>
<br>

## (2) 리액트 애니메이션(react-transition-group)        
이번 강의에서는 탭을 만들고, 탭에 애니메이션을 주는 작업을 진행했다.            
탭을 만드는 작업에서는 부트스트랩을 사용하여, 탭 안에 내용이 바뀌도록 하는 것이여서 state를 사용해서 익숙하게~      
여기서 말씀하신 내용 중에 if-else문을 삼항 연산자를 이용하여 대체한다고 헸지만, 난해해지는 경우가 있어서        
그런 경우에는 따로 컴포넌트로 빼서 if-else 처리를 해주는 것이 좋다고 하셨다 👀 tab도 3개 이상인 경우가 많으니 아래 같이      
```jsx
function TabContent1(props){
    useEffect(()=>{
        props.스위치변경(true)
    });
    if(props.누른탭 === 0){
        return <div>0번째 탭입니다.</div>
    }else if(props.누른탭 === 1){
        return <div>1번째 탭입니다.</div>
    } else if (props.누른탭 === 2){
        return <div>2번째 탭입니다.</div>
    }
}
```
그 다음에 탭에 애니메이션을 붙여주는 넣어줬는데, ```react-transition-group```을 이용하면 간단한 애니메이션에 편히하다고 한다.       
사용 방법은 간단하다~!      
1. ```npm install react-transition-group```을 이용하여 라이브러리를 설치해준다.         
2. 애니메이션을 사용 할 파일에 ```import {CSSTransition} from react-transition-group;```
3. 적용할 부분을 <CSSTransition>으로 감싸주고, 해당 태그 안에 in, classNames, timeout 속성 넣기      
4. CSS파일에서 애니메이션 디자인 해주기(이때 앞에서 정한 className-enter는 컴포넌트 등장시 적용할 CSS이고, className-enter-active는 컴포넌트 등장중 적용할 CSS이다.)        
5. in={true}를 false로 했다가 원할 때 true로 바꿔주면 된다.     

> 여태 장고만 하다 react하면서 느낀건 react 잘하면 예쁜 페이지 만들 수 있겠다... 아직 나는 말하는 감자지만..🤒  

<br>
<br>

## (3) Redux 1 : props 싫으면 쓰세요    
> 드디어 리덕스,,                             

**redux 쓰는 이유 1 : props 전송 없이도 모든 컴포넌트들이 state를 사용할 수 있게 만들어준다.**      
앞에서 컴포넌트의 많아지면, props로 전송하는 것이 복잡해져 context와 더불어 redux를 쓴다고 했다.        
* 설치 : ```npm install redux react-redux```를 통해서 라이브러리 설치       
* 셋팅 : index.js에서 <Provider>를 import하고, state값을 공유하고자 하는 컴포넌트를 감싸준다.       
        그  다음에 state를 기존에 사용하던 useState가 아닌! createStore()함수를 이용하여 만들어준다.    
        ```let store = createStore(()=>{return[{id:0,name:'멋진신발',quan:2}]});```같은 형식으로!       
        마지막으로 <Provider>에 state를 props처럼 등록한다.         

* 사용 : store에 저장한 state를 쓰기 위해서는 state를 쓰고자 하는 파일 하단에 function을 만들어서, store안에 있는 state를 props로 만들어 준다.      
        그 다음에 export default connect(함수명)(파일명)을 해주면 된다!     
> store안에 있는 모든 state 데이터를 props로 등록하면, 데이터 바인딩이 쉬워진다.            

<br>
<br>

## (4) Redux 2 : reducer/dispatch로 데이터 수정하는 법          
redux 사용 시에 수정은 reducer라는 함수를 만들어서 수정 방법을 정의해놓고, dispatch()를 통하여 사용하게 된다.       
다소 복잡하다고 생각할 수 있으나, 프로젝트가 커진다면 state의 관리가 어려워진다고 한다.     
이 경우에 redux는 reducer와 dispatch만 검토해본다면, state 변화를 파악할 수 있기 때문에 state 관리가 용이하다고 말한다고 한다.              
지난 강의에서 배웠던 부분이 아래와 같이 해줌으로서, 이제 state의 값도 변경 가능하다.          
```jsx
let 초기값=[
  {id:0,name:'멋진신발',quan:2},
  {id:1,name:'멋진신발2',quan:1}
];

function reducer(state=초기값,액션){
  if (액션.type === '수량증가'){
    let copy = [...state];
    copy[0].quan++;
    return copy
  }else if(액션.type === '수량감소'){
    let copy = [...state];
    copy[0].quan--;
    return copy
  } else{
    return state
  }
}

let store = createStore(reducer);
```
reducer는 보통 state를 따로 만들어주고 그걸 default 파라미터 문법으로 집어넣고 수정 방법을 정의하여 만든다고 한다.          
위의 코드에서처럼 액션.type은 어떤 경우에 수정할 것인지 정하는데, 이를 html안의 dispatch를 통해서 reducer를 동작시킬 수 있다고 한다. 위와 같이 사용하면 된다..!         
```jsx
<Table responsive>
    <tr>
    <th>#</th>
    <th>상품명</th>
    <th>수량</th>
    <th>변경</th>
    </tr>
    { props.state.map((a,i)=>{
    return (
    <tr key={i}>
        <td>{a.id}</td>
        <td>{a.name}</td>
        <td>{a.quan}</td>
        <td><button onClick={()=>{ props.dispatch({type:'수량증가'})}}> + </button>
        <button onClick={()=>{ props.dispatch({type:'수량감소'})}}> - </button></td>
    </tr>
    )
    })  }
</Table>
```         
<br>
<br>

## (5) Redux 3 : state와 reducer가 더 필요하면      
reducer가 여러개 필요하다면, 관련 state와 reducer를 만들고, 이를 ```combineReducers()```안에 넣어서 createStore()에 넣어주면 된다!     
```jsx
let alert초기값 = true;

function reducer2(state = alert초기값, 액션){
  if (액션.type === 'alert닫기'){
    return false
  } else {
    return state
  }
}


let 초기값=[
  {id:0,name:'멋진신발',quan:2},
  {id:1,name:'멋진신발2',quan:1}
];

function reducer(state=초기값,액션){
  if (액션.type === '수량증가'){
    let copy = [...state];
    copy[0].quan++;
    return copy
  }else if(액션.type === '수량감소'){
    let copy = [...state];
    copy[0].quan--;
    return copy
  } else{
    return state
  }
}

let store = createStore(combineReducers({reducer,reducer2}));
```
위와 같이!!     
그리고 아까 사용하고자 한 곳에, 아래와 같이 작성을 했었는데 이 부분도 수정해줘야 한다.      
```jsx
function 함수명(state){
    return{
        state:state
    }
}

export default connect(함수명)(Cart)
```
state안에 여러개의 reducer가 합쳐서 들어가있으므로, 잘 골라줘야 한다.            
```jsx
function 함수명(state){
    return{
        state:state.reducer,
        alert열렸니:state.reducer2
    }
}

export default connect(함수명)(Cart)
```
강의 마지막에 redux 사용 시 주의해야할 점이, 굳이 redux까지 할 필요 없는 애들(다른 컴포넌트에는 쓰이지 않는 애들)은 useState()를 이용하라고 하셨다..! 컴포넌트들끼리 많이 공유하는 애들을 redux로,,,

정리하자면, 컴포넌트들끼리 자주 공유하는 애들은 redux를 이용한다. 이때 state당 reducer도 만들어주고 이들을 combineReducers를 해줘서 createStore에 넣어줘서 사용....     
> 뭔가 강의는 리덕스가 엄청 쉬운 것처럼 이야기 하는 느낌.. 근데 나는 뭔가 끄덕이고 있으나 공허한 느낌,,,

<br>
<br>

## (6) Redux 4 : dispatch할 때 데이터 실어보낼 수 있음
html에 있는 dispatch안에 내가 원하는 값을 태워서 reducer에서 쓸 수 있다~!       
즉, redux안의 state값을 바꿔주고 싶을 때, dispatch에 태워서 보낸 값으로 할 수 있다.     

방법은 ```props.dispatch({type : '항목추가', payload : {id : 2, name : '새로운상품', quan : 1} })```와 같이 태워보내면 된다!        
payload는 강사님이 화물이라는 뜻이 있어서 관습적으로 쓰고 있다고 이름은 data? 이런걸로 작명해도 된다고 함.      
그리고 reducer에서  액션.payload와 같이 쓸 수 있다.     
```jsx
function reducer(state=초기값,액션){
  if(액션.type === '항목추가'){
    let copy = [...state];
    copy.push(액션.payload); //바로 요렇게
    return copy
  }else if (액션.type === '수량증가'){
    let copy = [...state];
    copy[0].quan++;
    return copy
  }else if(액션.type === '수량감소'){
    let copy = [...state];
    copy[0].quan--;
    return copy
  } else{
    return state
  }
}
```
즉, 액션의 역할은 dispatch() 소괄호 안에 들어있던 모든게 들어있다고 생각하면 된다고 한다.       

## +a 강의들 몇 개 정리
1. 삼항 연산자와 &&연산자
```jsx
function Component() {
  return (
    <div>
      {
        1 === 1
        ? <p>참이면 보여줄 HTML</p>
        : null
      }
    </div>
  )
} 

function Component() {
  return (
    <div>
      {
        1 === 1 && <p>참이면 보여줄 HTML</p>
      }
    </div>
  )
}
```
삼항 연산자를 쓰는 경우에 &&를 통해서도 가능하다.       
&&연산자를 이용해서 왼쪽 조건식이 true이면 오른쪽이 남게 된다.     

2. 컴포넌트 import 할 때 lazy하게 임포트 하기       
App.js에는 많은 import가 존재하는대, 초기 접속속도가 굉장히 느려질 수 있다고 한다.      
이런 경우에 초기 메인 페이지에는 필요 없는 것들을 필요시에 임포트 해달라고 할 수 있다고 한다.       
react 라이브러리에서 lazy,Suspense를 import해오고, ```let Detail = lazy( ()=>{ return import('./Detail.js') } );```와 같이 lazy함수를 사용해서 임포트..!            
그리고 App.js에 해당하는 컴포넌트를 Suspense로 감싸주면 된다.           
Suspense안에 ```<Suspense fallback={ <div>로딩중입니다~!</div> }>```와 같이 해주면 컴포넌트 로딩 전까지 보이게할 HTML을 설정해줄 수 있다..!         

<br>

# 튜터에게 궁금한 점
1. redux 부분 강의를 듣던 중에 redux가 복잡해서 react recoil과 같은 라이브러리로 대체될 수 있다는 말과 슬랙을 보고 나서 이 부분이 궁금합니다..! 사실 강의 수준에서는 리덕스를 겉핥는 느낌이라 추가적으로 공부해야할 것 같다고 생각해서요..!         
2. 요즘 장고 프로젝트 하면서 계속 깃을 쓰다보니 진짜 실무에서 깃을 어떻게 쓰는지..? 궁금해요 ㅎㅎ
