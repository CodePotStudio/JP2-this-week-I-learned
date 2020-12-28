# 이번주 리뷰
<br>

## 클론 코딩 : 유튜브 사이트 만들기 <br> (반응형, 모바일 우선)
- wireframe 제작 <br>
    1. 박스 단위로 구조를 잡는다
    2. 각 박스의 기능을 부여한다.
    3. 각 박스의 레이블링을 한다.
    
- css 팁 <br>
    1. root를 이용한 변수 설정을 통해 일관성을 부여한다.
    ```css
    :root {
        /*color*/
        --white-color : #fff;
        --black-color : black;
        --blue-color : blue;
        --red-color : red;
        --grey-dark-color : #909090;
        --grey-light-color : #e0e0e0;
    
        /*size*/
        --side-padding : 12px;
    
        /*font size*/
        --font-large: 18px;
        --font-medium: 14px;
        --font-small: 12px;
        --font-micro: 10px;
    }
    
    header{
        display: flex;
        justify-content: space-between;
        padding : var(--side-padding);
        background: var(--black-color);
        color: var(--white-color);
    }
    ```    
    2. flexbox, justifycontent, text-align, margin, padding 등을 통해<br>
    각 레이블링 된 박스의 요소들을 꾸며준다.
    3. class가 겹치지 않게 하시 위해 상위 태그 컴포넌트들을 타고 들어가서 해당 태그에 맵핑한다.
    4. line-clamp를 통해 반응형으로 동작 중 텍스트 라인을 제한할 수 있다. <br>
    제한된 텍스트라인을 넘을 시 토글 버튼을 통해 다음 라인을 활성화 시킨다.
    5. 반응형 동작을 위해 container들의 height,width는 % 단위로 설정하고 각 height, width에서 제한 값을 둔다.
    ex) 1000px



# 튜터에게 궁금한 점
궁금한점 작성 공간!

