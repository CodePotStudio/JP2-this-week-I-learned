# 이번주 리뷰

<br>
react-transition-group: react 애니메이션 라이브러리
공식문서: http://reactcommunity.org/react-transition-group/

개별 DOM에 애니메이션 거는 방법은 코딩애플 온라인 강의 3-3을 참고해서 CSSTransition을 사용하면 되고,
react 라우터를 이용한 페이지 전환 애니메이션을 사용하려면 아래 문서를 참고해서, TransitionGroup을 사용하면 된다.
https://stackoverflow.com/questions/45932263/page-sliding-animation-with-react-router-v4-and-react-transition-group-v2

TransitionGroup 사용 구조는 아래와 같다.
App.js
<TransitionGroup className="route__container">
<CSSTransition key={currentKey} timeout={1000} classNames={'route'}>
<Switch location={location}>
<Route path="/" exact component={Home} />
<Route path="/about" component={About} />
</Switch>
</CSSTransition>
</TransitionGroup>

App.scss
.route\_\_container {
width: 100%;
height: 100vh;
position: absolute;
top: 0px;
left: 0px;
}
.route-enter {
transform: translateX(100%);
}
.route-enter-active {
transform: translateX(0%);
}
.route-exit {
transform: translateX(0%);
}
.route-exit-active {
transform: translateX(100%);
}

페이지 전환 효과를 간단히 구현할 수 있는 라이브러리로 활용성이 높다.

# 튜터에게 궁금한 점

.
