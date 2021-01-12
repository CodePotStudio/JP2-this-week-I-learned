# 이번주 리뷰

## PART 2. 쇼핑몰 프로젝트(완료)
## (6) React Router 2 : Link, Swithch, history 기능
**컴포넌트가 길어진다면 이를 따로 js파일로 만들어서 import 해줄 수 있다.**             
따로 파일을 만들어줄 때 중요한 점은 컴포넌트 생성시에, ```import React from 'react'``` 상단에!      
그리고 하단에 ```export default 컴포넌트명```을 해줘야 한다.        
컴포넌트가 길고 많아진다면 별도의 컴포넌트 파일을 만들어서 관리 한다고 한다. 

<br>

**Link 태그를 이용하면 페이지 이동하기**            
```<Link></Link>```를 이용하여 원하는 페이지로 이동할 수 있다.      
먼저 ```impoer  Link from 'react-router-dom```을 통해서 import를 해준다.            
그 다음에 ```<Link to="원하는 이동 경로"></Link>```를 해주면 된다. a태그와 유사하다.    
<br>

**useHistory()을 이용하여 페이지 이동하기?!**       
```useHistory```는 ```useState```와 비슷한것으로 방문 기록을 담는 오브젝트이다!         
보면서 이게 정말 신기했는데, 뒤로가기를 goBack 함수를 통해 정말 쉽고 간단하게 구현이 가능했다.      
```import {useHistory} from 'react-router-dom```을 이용해서 상단에 import를 우선 해준 뒤에,         
```let 내가정한변수  = useHistory();```를 통해서 방문기록을 담을 친구를 선언해준다!         
```jsx
<button className="btn btn-danger" onClick={()=>{
     history.goBack();
 }}>뒤로가기</button> 

<button className="btn btn-danger" onClick={()=>{
    history.push('/');
}}>홈이동</button> 
```
goBack함수를 통해서 뒤로가거나 push를 통해서 원하는 경로로 이동도 가능하다~!        
<br>

**Switch 컴포넌트를 통해서 하나의 Route만!**            
Route의 특징 중 하나가 바로 해당하는 모든 친구를 나타내준다는 것이었다.                 
그래서 이전 강의에서 ```<Route exact path="/">```와 같은 방법은 배웠다.         
Switch는 매치되는 라우트들을 모두 보여주는 것이 아닌 한번에 하나만 보여줄 수 있도록 하는 기능이다.      
<br>


## (7)React Router 3 : URL 파라미터로 상세페이지 100개 만들기
**state는 state를 필요로하는 컴포넌트 중 가장 최상위에 보관**       
컴포넌트들을 별도의 파일로 보관하다보면, props를 쓰는 귀찮음 없이 해당 컴포넌트에다가 state를 만들면 되지 않을까?       
가능은 하지만! 데이터는 항상 위에서 아래로 흘러야한다고 한다. 특히 중요한 데이터의 경우에는 App이 보관해야 한다.        
데이터가 위에서 아래로 흘러야 하는 이유는 잘못짜다가는 역방향으로 데이터를 전달해야할 수 있다....       
<br>

**여러 상세페이지와 같은 url을 만들때는 :id**       
상품들이 여러개가 존재하고 해당 상품마다 detail 페이지가 존재한다고 할 때, 이들을 일일히 Route하는 것은 말이 안된다.        
반복문을 쓸 수도 있겠지만, ```:id```라는 URL 파리미터 문법을 이용하면 된다.     
```:id```의 의미는 이 자리에 어느 문자가 오든 라우트 태그 안의 컴포넌트들을 보여주라는 것이다!      
id부분은 자류옵게 작명가능하며, 파라미터는 여러개 추가할 수 있다.          
 <br>

**:id에 입력한 값을 이용하여 데이터 바인딩은 useParams()**      
```import {useParams} from 'react-router-dom``` 을 데이터바인딩할 파일 상단에 import 해준다.        
```let {id} = uesParams();```을 보면 useParams함수는 url에 적힌 모든 파라미터를 {}안에 저장해주는 함수이다.     
이제 이 id를 이용해서 데이터 바인딩을 해주면 된다.      
여기서 간단한 숙제..? 로 내준 것이 있었는데, 바로 자료의 순서가 바뀌면 상세페이지가 문제생기는 것을 고치는 것이었다.
```jsx
function Detail(props) {

    let {id} = useParams();     //변수를 선언하자마자 파라미더 값을 저장해서 변수로
    let history = useHistory(); //방문 기록을 담는 오브젝트
    let findProduct = props.shoes.find(function(product) {  //javascript find()
        return product.id == id
    })

    return(
        <div className="container">
        <div className="row">
            <div className="col-md-6">
            <img src="https://codingapple1.github.io/shop/shoes1.jpg" width="100%" />
            </div>
            <div className="col-md-6 mt-4">
            <h4 className="pt-5">{findProduct.title}</h4>
            <p>{findProduct.content}</p>
            <p>{findProduct.price}</p>
            <button className="btn btn-danger">주문하기</button> 
            <button className="btn btn-danger" onClick={()=>{
                history.goBack();
            }}>뒤로가기</button> 
            </div>
        </div>
        </div>
    )
}
```
<br>

## (8) styled-components를 이용한 class없는 CSS스타일링     
class 없이 직접 컴포넌트 생성시에 스타일을 입힐 수 있는데, 이것이 바로 ```styled-component```이다.      
```npm install styled-components```을 통해서 라이브러리를 설치해야 사용가능하다.        
```jsx
    let 박스 = styled.div`
        padding:20px
    `;

    let 제목 = styled.h4`
        font-size : 25px;
        color : ${props => props.색상}
    `;
```
다음과 같이 사용하는데, styled.원하는태그 방식이다. backtick안에 원하는 스타일을 넣어주면 된다.     
보면서 오 편하겠다라고 생각하자마자,, 강사님이 css 잘못하는 사람들은 이걸 보면 편하다고 생각한다고 해서...ㅠㅠ      
호불호가 많이 갈리는 방식이라고는 하신다.       
두 번째 제목 컴포넌트처럼 props를 이용해서 스타일링도 가능하다.

<br>


## (9) CSS대신 SASS를 쓰자                           
CSS를 많이 작성해야 한다면 **SASS**를 쓰면 코드의 양이 줄고, 보다 프로그래밍적이라고 한다.     
웹에서는 CSS만 동작한다. SASS는 CSS Processor로 나중에 CSS로 컴파일해서 동작되는 원리이다.              
   우선 사용하려면, ```npm install node-sass@4.14.1```을 해줘야 한다.              
> 강의 보면서 다운 받으니 버전 문제 때문에 컴파일이 안돼서 다시 지웠다가 버전 명시해서 깔았다...
<br>            

SASS를 왜 사용하는지 더 구체적으로 알고 싶다면, 이들의 기능을 보면 된다.        
- 변수 사용 ($변수명 : 원하는 값;)
- import  (@import를 통해서 css간 파일 import)
- nesting (셀렉터를 안쪽에다가 작성할 수 있다.)
- mixin, include (mixin을 통하여 함수를 만들고 @include 함수명()을 통해서 원하는 css속성 사용)
- extend (@extend를 통해서 재사용이 용이하게)
```scss
@mixin 함수(){
    background-color: #eeeeee;
    padding: 20px;
    border-radius:5px;
    max-width: 500px;
    width: 100%;
    margin:auto;
}
.my-alert{
    @include 함수()
}
```
확실히 단순 css에 비해서 코드가 줄어들고, 재사용이 용이하다는 생각이 들었다..!!

<br>

## (10) Lifecycle Hook, useEffect ~ (11) useEffect 풀이 및 나머지 기능
**Life Cycle**  
컴포넌트들에게는 인생이 있다고 한다. 그것을 라이프 사이클이라고 하는데 생성-삭제-재랜더링이 될 수 있다는 것이다.    
컴포넌트의 라이프 사이클은 hook 때문에 알아야 한다. 훅이란건 컴포넌트 인생에 참견!      
<br>

**Lifecycle Hook**      
Hook을 class로 만든 컴포넌트에서 사용하는 방식, 아래와 같이 생겼다.              
```jsx
class Detail extends React.Component {
  componentDidMount(){
    //Detail 컴포넌트가 Mount 되고나서 실행할 코드
  }
  componentWillUnmount(){
    //Detail 컴포넌트가 Unmount 되기전에 실행할 코드
  }
}
```
여기서 코드에서 나온 두 훅이 가장 유용한 것이라고 한다.                 
<br>

**useEffect Hook**      
요즘 많이 사용하는 것은 uesEffect로 위에 방법에 비해서 짧다고 한다.
```jsx
import React, {useState, useEffect} from 'react'; //import 필수

function Detail(){

  useEffect(()=>{
    
  });
  useEffect(()=>{
    //순서대로 useEffect가 실행된다.
  });
  
  return (
    //
  )
}
```
useEffect눈 컴포넌트의 등장과 업데이트 되고나서 무조건 실행이 된다! 그래서 이걸 막을 수도 있도록 대괄호를 넣는다.           
>사실 이부분에서 생가보다 엄청 간단하게? 설명하셔서 먼가 거기서 오는 헷갈림이 있었다.     
그래서 벨로퍼트 리액트 그분꺼 찾아서 이 부분을 보니깐 훨씬 이해가 잘 갔던것 같다!           
문제는 이분껄 보니깐 앞에 부분도 정독해야겠다고 완전 들었다..!            <br>

벨로퍼트에서 본 것을 토대로 정리하자면 useEffect 사용시 첫번째 파라미터에는 함수가 두번째 파라미터에는 의존값이 들어있는 배열(deps)이 들어간다.           
앞서 말한 것처럼 대괄호, 즉 빈 deps를 넣는다면 컴포넌트가 처음 등장 할때 useEffect에 등록된 함수가 호출되게 된다.       
여기에 값을 넣는다면? 그 값이 변경될 때에도 호출되게 된다.      
<br>
그리고 강의에서 숙제를 기준으로 useEffect를 설명하는데, setTimeout()을 사용하는 부분에서 cleanup을 해주라고 하셨는데,       
그 이유는 useEffect에 대한 뒷정리를 위해서라고 한다. 만약에 이 안에서 꼬여서 잘못된 값이 저장된다면 의도치 않은 결과를 낼 수도 있으니깐!    
```jsx
    useEffect(()=>{
        let timer = setTimeout(()=>{alert변경(false)},2000) ;
        console.log("안녕");
        return ()=>{clearTimeout(timer)} //뒷정리 해주기
    },[alert]);
```     

<br>


## (12) 리액트에서의 Ajax 요청방법 & Ajax는 무엇인가 ~ (13) 리액트에서의 Ajax 요청방법 2 & 숙제풀이   
**Ajax는 서버에 새로고침 없이 요청을 할 수 있게 도와주는 자바스크립트 코드**        
GET 또는 POST 요청을 새로고침 없이 할 수 있게 해주는데, 리액트에서는 axios를 설치해서 보통 이용한다.        
그 이유는 fetch()도 문법이 같지만, axios는 JSON을 오브젝트로 자동 변환 해주기 때문이다.        
```jsx
 <button className="btn btn-primary" onClick = {()=>{
        axios.get('https://codingapple1.github.io/shop/data2.json') 
        .then((result)=>{
            console.log(result.data)
        })
        .catch(()=>{
            console.log('실패')
        }); //새로고침 없이 데이터를 가져온다.
  }}>더보기</button>       
```
axios에 get 요청은 위의 코드와 같이 ```axios.get```을 통해서 할 수 있다. 또한 then과 catch를 통해서 데이터 받아오는 것을        
성공, 실패 할때의 처리를 해줄 수도 있다.        
axios에 post 요청은 ```axios.post('서버 URL',{값})```을 통해서 할 수 있다.      
useEffect와 합쳐서 컴포넌트 로딩 또는 업데이트시에 ajax요처을 할 수 있다~!      

그리고 여기서 ```shoes변경([...shoes, ...result.data]); // 독립된 카피본이 생긴다.``` 코드가 나오는데,      
앞선 강의에서 절대 원본을 손대지 말고 카피본을 쓰라고 했는데, 그 부분을 이렇게 괄호를 벗겨서 사용할 수도 있다.              

<br>

## (13) Component를 3개 중첩해서 만들면 state 전달      
component안에 component가 있는 경우에 하위 컴포넌트들이 state를 쓰려고 하면 어떻게 해야할까?        
생각보다 단순했다. props를 이용해서 전송하고 또 props로 전송하면 된다.      

이렇기 때문에 하위 컴포넌트가 많아질 수록 props의 양이 많아지고, 복잡해진다고 한다.     

그렇기 때문에 3장에서 배울 redux를 쓴다고 하는데, 3장을 가지 못해서 반성 중,,,,     
그리고 벨로퍼트 앞부분을 다시 좀 읽어보고 redux 넘어가야겠다!!      


# 튜터에게 궁금한 점        
1.  Lifecycle Hook을 여전히 사용한다고 흘리듯이 말씀하시던데, 어느정도 알아둬야 하는 부분일까요? 설명을 너무 간단히 해서 궁금합니다.        
