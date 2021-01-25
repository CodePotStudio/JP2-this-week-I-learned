# 이번주 리뷰
<br>

###navbar 동적 제어
- 페이지 스크롤 시 navbar의 backgroundcolor, padding 변경하기
```javascript
const navbar = document.querySelector('#navbar')
const navbarHeight = navbar.getBoundingClientRect().height;

document.addEventListener('scroll', () => {
    console.log(window.scrollY)
    console.log(`navbarHeight : ${navbarHeight}`)
    if (window.scrollY > navbarHeight) {
        navbar.classList.add('navbar--dark');
    } else {
        navbar.classList.remove('navbar--dark');
    }
});
   ```
queryselector API를 통해 navbar id를 navbar 변수에 저장한다.
navbar section의 height를 구하기 위해 getboundingclientrect() 함수를 사용한다.
이벤트 리스너를 통해 scroll 이벤트 시 window.scrollY api의 리턴 값이 navbarheight보다<br>
크게 되면 그 이후 부터는 navbar section에 dark 클래스를 추가한다.

- navbar menu 클릭 시 스크롤 구현
```javascript
const navbarMenu = document.querySelector('.navbar__menu');
document.addEventListener('click', (event) => {
    const target = event.target;
    const link = target.dataset.link;
    if (link == null) {
        return;
    }
    console.log(event.target.dataset.link);
    const scrollTo = document.querySelector(link);
    scrollTo.scrollIntoView({behavior: 'smooth'});
});
   ```
queryselector api를 통해 navbar__menu의 속성 값을 변수에 저장한다.<br>
각 navbar의 menu li 태그에 data 필드를 추가로 달고 그 값은 menu 클릭 시 이동할 섹션의 id로 할당한다<br>
eventlistener를 추가하여 click 이벤트 발생 시 event target의 dataset에 걸어두었던 link를 파싱하여
link 변수에 저장하고, 그 link의 값이 존재할 시 scrollintoview api를 통해 link값인 section으로 스크롤을 이동시킨다.
+behavior 키를 smooth value값을 할당하여 스크롤 속도 제어

# 튜터에게 궁금한 점
궁금한점 작성 공간!