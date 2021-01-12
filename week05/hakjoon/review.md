#css
##box model

-   box-sizing : border box <br> 정해진 box size 안쪽에서 border, padding 처리
- box-sizing : content box <br> 정해진 box size 바깥쪽에서 border, padding 처리 (content box가 box size로 유진된다.)
<br> 대부분 border box 처리하여 box sizing을 한다.

##Absolute vs Static

box 기본 position은 static이다. 

-   relative : 원래 있던 자리(상대적)에서 설정한 위치 값(top, left, bottom, right 등등)에 따라 부모 기준으로 이동하게 된다.
- absolute : relative position 값을 가진 부모의 기준(절대적)에 따라 설정한 위치 갑 만큼 이동한다.

##Sticky vs Fixed

- position : sticky는 top, left등으로 설정한 값 기준으로 부모 뷰 안에서 스크롤을 통해 고정된다.
- position : fixed는 top, left등으로 설정한 값 기준으로 view port 기준으로 절대적 위치에 고정된다.

## BEM
Block Elementary Modifier, 컴포넌트 단위로 블록 레벨로 이름을 설정한다.
<br> class name rule : block_element-modifier
<br> ex) 카드 안 제목 element의 class : .cards__title
그런데 색깔이 블루가 존재 -> .cards__title--blue
# 튜터에게 궁금한 점
궁금한점 작성 공간!