# 이번주 리뷰
<br>

###Transparent home
home 섹션의 높이를 변수에 저장하여 scroll 이벤트 발생 시 <br>
home 스타일의 투명도를 1에서 home높이에서 스크롤 y포인트 위치만큼의 비율에서
뺀 값으로 작성한다. 이 간단한 알고리즘을 통해 스크롤 시 화면 컨텐츠들의 투명도의 값을 크게 가져갈 수 있다.
```javascript
const home = document.querySelector('.home_container');
const homeHeigt = home.getBoundingClientRect().height;
document.addEventListener('scroll',()=> {
    home.style.opacity = 1 - window.scrollY / homeHeigt;
});
```    

# 튜터에게 궁금한 점
궁금한점 작성 공간!