# 이번주 리뷰
<br>

# 벨로퍼트와 함께하는 모던 리액트       
이번주는 앞에 1장을 끝내고 todo list 부분을!      

todo list 컴포넌트 만들기 부분을 하다보니 styled components가 계속 나오는데,      

앞에 스타일링하기를 건너뛰고 온거라 다시 뒤로 돌아와서 공부했다 ㅎㅎ   
    

## styled-components     
js안에 css를 작성하는 CSS in JS관련 리액트 라이브러리 중에서 가장 인기 있는 것      

todo 앞부분 하면서 사용법이 template literal이랑 비슷하다고 느껴졌는데?   

역시나 설명 바로 앞부분에 내부적 작동이 비슷하다고 한다.      

전에 es6강의 들으면서 어렵다 느꼈는데, 생각하면 다 알짜배기 같이 리액트 하면서 떠올리는중!     

styled-components를 정확히 쓰는 이유? 기존 css와의 차이점에 대하여 궁금했는데  

클래스명과 html 요소를 기반으로 컴포넌트를 만들 필요가 없어져서 그렇다고 한다.      

그런데 전에 이 부분에 대해서 설명을 들었던 것 같아서,, 약간 복습과 정리의 중요성을 느껴서       

요즘 노션에다가 참고했던 글들과 정리한 내용 등을 목록별로 정리 중이다!        

(참고 : https://blog.nerdfactory.ai/2019/10/25/react-styled-components.html)

사용법은 ```import styled from 'styled-components';```을 상단에 적어준 후에,
```jsx
const Container = styled.div`
  background-color: lightgray;
  width: 100%;
  height: 100vh;
`;
```
와 같이 사용하는데! ```styled.div```를 보면 알수있듯이 해당 스타일링과 동시에 그 스타일을 가진 컴포넌트를 생성할 수 있다.       

그리고 props를 통하여 조건부 스타일링도 가능하다. 그래서 ```background: ${props => props.color || 'black'};```와 같은 코드를 짤 수 있다.        
<br>

## polished
CSS in JS에서 색상과 관련한 변화를 주는 유틸 함수를 쓸 수 있는 라이브러리       

```npm install or yarn add polished```로 설치 후에,     

```import { darken, lighten } from 'polished';```와 같이 사용하고자 하는 것을 import 해준다.        

그리고 아래와 같이 사용가능하다. 
```jsx
const StyledButton = styled.button`
  /* 공통 스타일 */
  display: inline-flex;
  outline: none;
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  ${props => {
    const selected = props.theme.palette[props.color];
    return css`
      background: ${selected};
      &:hover {
        background: ${lighten(0.1, selected)}; // polished 
      }
      &:active {
        background: ${darken(0.1, selected)};
      }
    `;
  }}

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;
```
위의 코드를 보면 rem이 많이 쓰이는데, 지난 수업이 생각나면서 페이지 최상위 요소에 기반하여 크기가 유연하게 결정된다는 점이 떠올랐다..!      

그리고 약간 샛길이지만 css 공부도 해야겠다는 생각이 드는게 먼가,,       
내가 혼자 뚝딱이면 보이는게 안예쁜데 예제들을 보면 간단한 기능이라도.. css만 잘해놓아도 보기 예쁘고 그래서!         
<br>

todo list는 context api를 통한 상태 관리 부분은 우선 끝내고 기능 구현하기를 ing..       



<br>    

# 튜터에게 궁금한 점
아직 투두리스트 기능 구현하기 부분을 하는 중이라,, 딱히 없습니다...!