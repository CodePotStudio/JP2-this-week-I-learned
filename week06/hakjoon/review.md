# 이번주 리뷰
<br>

##CSS Variable
상위 부모에 선언된 변수는 속해 있는 자식들에게 반영 가능<br>
최상위 부모 겪인 :root에서 css 변수를 주로 선언한다.
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
    h1 {
        padding : var(--side-padding);
        background: var(--black-color);
        color: var(--white-color); }
   ```   
##Responsive background
background 속성 값 활용, cover 속성을 통해 이미지를 반응형 같이 화면의 전체를 계속 채우게 설정할 수 있다.

   ```css
    :.box1{
    background-image : url("");
    background-repeat : no-repeat;
    background-position: center;
    background-size : cover;
}   
   ``` 
##Transform
xyz 값을 움직일 수 있고, 3D값, skew, scale, scale3D를 이용해서 할 수 있다.<br>
viewport 상 x축은 오른쪽으로 갈 수록 커지고, y축은 아래로 내려갈수록 커진다. - 같은 경우는 거꾸로 간다고 생각하면 된다.
   ```css
    .box2 {
    transform : translate(-50px, -20px)
}
   ```
- scale은 크게 만들 수 있다. : transform : scale(1.2);
- rotate / transform : rotate(45deg);
```css
    .box2 {
    transform : translate(-50px, -20px) scale(2) rotate(45deg);
}
   ```
##Transistion
hover 효과에 transition을 입히는 경우
transition을 통해 무엇을? 얼마나? 어떻게?를 통해 적용한다.
```css
    .box2 : hover {
    background-color: crimson;
    transition : background-color 300ms linear;
}
   ```
또는 transition : all 2s ease;를 통해 해당하는 모든 property에 적용한다를 의미할 수 있다.
- cubic-beizer를 통해 linear, ease, ease-in등 transition에 대한 variable들을 customizing할 수 있다.
<br>ex) transition : all 2s cubic-bezier(0.47, 0 ,1, -0.06);

##참고 사이트
https://developer.mozilla.org/en-US/docs/Web/CSS/transition
https://cubic-bezier.com/#.06,.79,.89,.45

# 튜터에게 궁금한 점
궁금한점 작성 공간!