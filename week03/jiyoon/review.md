# 이번주 리뷰

# [React 리액트 기초부터 쇼핑몰 프로젝트까지]
## PART 1. 블로그 제작 & 기초 (완료)
## (9) props를 응용한 상세페이지 만들기
지난 강의까지에서는 버튼을 누르면 첫번째 글제목만 나오도록 하드코딩 했었다.     
이번에는 버튼을 누르면 해당 글제목이 나오도록 고치는 작업을 할 차례~!           
강의를 멈추면서 먼저 어떻게 고칠지 생각해보았다. 아마 state를 이용해서 인덱스 값을 변경해줘야겠다고 생각       
그래서 ```let [click,click변경] = useState(0);```이라는 state를 만들어줬고, component도 고쳤다.     
```jsx
{
    글제목.map(function(글,i){
        return (
          <div className="list">
          <h3 onClick={()=>{click변경(i)}}>{글}</h3>
          <p>12월 14일 발행</p>
          <hr/>
          </div>
        )
    })
}
```
> 나는 상단에서 글이라는 parameter하나로 click변경(글)이라고 했는데, 돌아가지 않아서..?         
왜일까 생각했는데 바보같은 생각이었다.. 글은 글제목 state 배열의 값들인데!           

그리고 하단에 Modal 함수도 변경해주었다.    
```jsx
function Modal(props){ //부모에게 전달받은 props가 여기에!
  return(
    <div className="modal">
      <h2>{props.글제목[props.click]}</h2>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
```
이렇게 하고나니깐, 코드가 안돌아가서 강의를 보니깐 위에 component에서 click이라는 부모의 state를 쓰는데,            
값을 넘기지 않아서 생긴 문제였다..! ```<Modal 글제목={글제목} click={click}></Modal>```라고 고쳐주었더니 완성       

<br>

## (10) input 다루기1 : 사용자가 입력한 글을 변수에 저장하는 법
사이트에서는 입력값을 받는 경우가 생긴다. 이 값을 state에 저장하려면 자바스크립트 문법을 이용하면 된다.        
state에 저장하는 이유는 보통 사용자가 입력한 데이터는 중요한 데이터이기 때문이라고 한다.        
```jsx
let [입력값, 입력값변경] = useState('');
...
<input onChange={ (e) => {입력값변경(e.target.value)}}/>  
```
위와 같이 입력값을 처리해주면 되는데, 여기서 onChange는 input 박스의 변화가 생기면 처리하는 이벤트 핸들러이다.       
```e.target```은 자바스크립트 문법으로 지금 이벤트가 동작하는 html요소, 이벤트가 발생한 DOM요소이다.        
```.value```는 input에 입력한 값을 의미하게 된다. (자바스크립트 복습해야겠다...아니 공부해야겠다.. )        

* 여기서 map이라는 반복문을 사용하면 warning이 뜨는데, key={}라는 속성을 쓰지 않아서 그렇다구 한다.     
```key={i}```를 map 반복문에 적어주면 된다고 한다.      

<br>

## (11) input 다루기2 : 블로그 글발행 기능 만들기
이번에는 input box에 작성하고 저장버튼을 누르면 첫번째로 글이 추가되도록 구현하는 강의였다.     
강의에서 혼자해보라고 해서 혼자해보았는데 성공했다~! 소소하지만 기분이 좋다.    
나는 우선 input에 넣은 값을 저장할 ```let [새글, 새글변경] = useState('');```라는 state를 생성해줬다.       
다음으로 버튼을 클릭하면 글을 저장할 함수를 만들어줬는데, 나중에 해설안을 보니 onClick안에 넣어주긴 했던데 상관 없을 듯하다..       
```jsx
function 글저장(새로운글){
    var newArray = [...글제목];
    newArray.unshift(새로운글);
    글제목변경(newArray);
}
```
그리고 input과 button에 각각 아래와 같이 완성
```jsx
<div className="publish">
    <input onChange={(e)=>{새글변경(e.target.value)}}/> 
    <button onClick={()=>{글저장(새글)}}>저장</button>
</div>
```
<br>

## (11) class를 이용한 옛날 React 문법
현재 강의에서 소개하고 있는 문법은 react의 신문법으로 class를 잉요한 옛날 react 문법을 간단히 알려주는 부분이었다.      
강의 중에 궁금한게 생겨서 전에 구글링할때 해당 문법을 본적이 있어서, 나중에 배우는건가 싶었는데?            
```jsx
class Profile extends React.Component{
  constructor(){
    super();
    this.state = {name : "YOU", age : 24}
  }

  changeNmae(){
    this.setState({name:'YOO'})
  }

  render(){
    return(
      <div>
        <h3>프로필</h3>
        <p>저는 {this.state.name}입니다.</p>
        <button onClick={this.changeNmae.bind(this)}>버튼</button>
      </div>
    )
  }
}
```
위에는 버튼 클릭시에 state의 name 값을 변경해주는 코드이다.     
간단히 정리하자면,          
- class는 데이터 또는 함수를 보관하며, 여러개의 데이터나 함수를 한 곳에 보관하려고 만든 문법이다.         
- extends React.Componet는 컴포넌트 성질을 상속받겠다는 것이다.      
- Constructor는 class의 변수나 초기값을 저장하는 곳이라, 여기 안에서 state를 정의하면 된다.   
- useState와 달리 class안에서 선언은 this.state로 , 변경은 this.setState를 이용한다.        
- this.setState는 state변경함수와 완전히 같지 않다. state변경함수는 대체를 하지만, setState는 대체가 아닌 변경할 state만 넣어서 사용한다.           
- class에서 this가 굉장히 중요하다. this에 민감하기 때문에 .bind(this)와 같은 코드를 쓰거나 함수를 arrow로

결론 : 현재 react 최신 react function 문법에 비해 class는 사용하기 복잡하므로 function 문법을 사용하라고 한다.    

<br>

## PART 2. 쇼핑몰 프로젝트
## (1) 프로젝트 생성 
- 새로운 쇼핑몰 만들기를 위한 프로젝트 생성 : 터미널에서 ```npx create-react-app shop```
- yarn을 설치하면 npx에 비해서 빠르고 안정적이게 할 수 있다.        
- bootstrap을 리액트에 맞게 변환한 React Bootstrap을 설치하고 index.html에 CSS 파일을 넣어준다.

<br>
리뷰 작성 공간!!!

## (2) 쇼핑몰 레이아웃 디자인
- bootstrap을 이용해서 navbar와 jumbotron과 같은 component를 사용한다. 이때 주의할 점은 상단에 아래와 같은 코드를 작성!
```jsx
import {Navbar,NavDropdown,Nav,Jumbotron,Button} from 'react-bootstrap';
```
사용되는 모든 component들을 import 해줘야 한다.     
- className을 이용하여 css에서 배경의 이미지를 변경하려고 한다면, ```background-image:url(./해당이미지.jpg)```      
> 전에는 public 폴더안에 이미지 파일 첨부가 가능했으나, 현재는 src파일에 이미지를 넣어야 한다!

<br>

## (3) import / export 사용해보기 ~ (4) 상품목록 Component화, 반복문
- export default란 긴 코드를 별도 파일로 만들어서 쓸 수 있게 하는 것으로 변수명, 함수명, 자료형 전부 배출 가능하다. 파일마다 키워드 하나만 사용 가능하다.       
- export default말고 여러 변수를 보내고 싶다면 export {}을 사용하면 된다.   
- import에서 export default한 파일을 불러올 수 있는데, ```import 지정하는변수명 from './date.js'```로 사용      
- import에서도 export{{}로 보낸 변수들을 import {}을 이용해서 가져다 쓸 수 있다.        

강의 마지막에 여태 진행한 쇼핑몰 코드들을 component로 만들고 데이터 바인딩한뒤에 반복문을 이용하라고 하셨다.    
나는 index를 위해서 state를 선언하고 아래와 같이 코드를 작성했는데,,,, 따로 index변경(i)도 사용해서..?      
Too many re-renders. React limits the number of renders to prevent an infinite loop 오류가 뜨고,        
나중에 다음 강의의 해설을 보니 굳이 그럴 필요가 없다는 것을 깨달았다 ㅎㅎ
```jsx
function Product(props){
  return(
    <div className="col-md-4">
      <img src ={'https://codingapple1.github.io/shop/shoes'+(props.index+1)+'.jpg'} width="100%"/>
      <h4>{props.shoes[props.index].title}</h4>
      <p>{props.shoes[props.index].content} & 가격</p>
    </div>
  )
}
```  
map 반복문에서 두번째 파라미터를 이용하면 된다는 것,,,! 어렵게 돌아가느라 애먹었다ㅜㅜ          
아직 처음이라 이렇게 바보짓을 하는거겠지 
```jsx
{
    shoes.map((a,i)=>{
        return(
            <Product shoes={shoes[i]} i={i} />
        )
    })
}   
...
function Product(props){
  return(
    <div className="col-md-4">
      <img src ={'https://codingapple1.github.io/shop/shoes'+(props.i+1)+'.jpg'} width="100%"/>
      <h4>{props.shoes.title}</h4>
      <p>{props.shoes.content} & 가격</p>
    </div>
  )
```

<br>

## (5) React Router 1 : 셋팅과 기본 라우팅          
**설치 및 셋팅**      
여러 페이지를 만들고 싶다면 Router를 사용해야 한다. ```npx install react-router-dom```을 통해서 설치    
그 다음에 ```index.js```에 ```import {BrowserRouter} from 'react-router-dom'```을 상단에 작성한다.      
그 후에 ```<App/>```을 ```<BrowserRouter>```로 감싸주면 된다.       
여기서! BrowserRouter말고 HashRouter도 있다고 한다. 이 둘의 차이점은 #이다.     
HashRouter는 실수로 서버에게 요청하지 않게 안전하게 #을 붙여준다. 서버 셋팅만 잘한다면 BrowserRouter를 쓰면 된다고 한다.    

<br>

**라우팅**              
1. 라우팅 하기 위해서는 ```App.js```에 Route를 import 해준다.       
2. 라우팅을 할 곳에 ```<Route></Route>``` 작성해준다.(라우터 라우터 하니깐 Router로 태그 작성했던,,,)       
3. ```<Route path="path작성">보여줄 HTML</Route>```을 적어준다.         
> 여기서 리액트 라우터는 매칭되면 모두 보여주는 속성을 가지고 있다. 그래서 ```/detail```의 path에서 ```/```의 경우도 보여준다.      
> 이를 막기위해서는 exact를 path앞에 작성해주면 된다.       

안에 코드들은 이전 작성한 코드들을 path에 맞게 보여줄걸 골라서 넣어주면 된다.               

여기서 ```React-Router```의 특징이 있는데, 지금 다른 HTML파일을 보여주는 것이 아니라 안에를 갈아치우고 있다는 것이다.       
이것이 웹앱의 특징이라고 한다.      

<br>



# 튜터에게 궁금한 점
궁금한점 작성 공간!
1.  map 반복문에서 key={}가 개발시에 필수적인가요? 이걸 이용해서 무언가를 하는 경우도 있나요?           
2. class 문법을 자세히 알아야 할까요? 요즘은 대부분 function 문법으로만 사용되는건가요?     
3. BrowserRouter보다 HashRouter가 안전해서 많이 쓰일까요?           
4. wakeTime이 Goal에서 전날 기준까지 나오는 점과 이게 vscode에서 md파일을 작성하다보니 이 시간까지 들어가더라구요!      
저는 우선 이번주에 md 파일은 약 2시간 30분은 작성 시간이긴 합니다..! 그래서 Goal말고 우선 Last 7days로 캡쳐했어요..!