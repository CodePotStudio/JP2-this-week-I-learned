# 이번주 리뷰

<br>
1. history.push()로 페이지 이동시 props 넘겨주기
routing으로 페이지에서 다른 페이지로 이동 할 때 props로 넘기는 방법.
(예를 들면 현재 페이지에서 다음 페이지로)

redux를 사용해도 되지만, 굳이 상태 관리가 필요하지 않은 데이터를 넘기기 위해 사용함.

'''
history.push({ pathname: "/url", state: { key: value } })

'''
value = history.location.state.key

---

2. react-router Prompt로 routing 제어하기

페이지 이동 시 때로는 Confirm 과 같은 창을 통해 페이지 이동을 막고 제어할 수 있음.

브라우저에서 뒤로가기 뿐만 아니라 페이지 이동을 막는 것이 필요한 경우가 많다.
이를 해결하기 위한 방법으로 네비게이션 가드(Navigation Guard) 라고 불린다.

<Prompt when={canNavigate} message="Are you sure you want to leave?" />

라우터 이동이 발생하면, Confirm 창이 뜨고, 사용자 선택에 따라 결정될 수 있다.
when 인자는 단순히 boolean 값이고, 이 값을 통해 네비게이션 여부를 제어하면 된다.

'''
const App = ({ history }) => {
const [whenState, updateWhenState] = useState(true);
return (
<div className="App">
<RouteLeavingGuard
when={whenState}
navigate={path => {
history.push(path);
}}
shouldBlockNavigation={location => {
if (whenState) {
// if (location.pathname === 'signup') {
// return true
// }
return true;
}
return false;
}}
yes="yes"
no="no"
content="Are you sure you want to leave?"
/>
<div className="drawer-list">
<ul>
<li>
<NavLink to="/home" activeClassName="is-active">
Home
</NavLink>
</li>
<li>
<NavLink to="/about" activeClassName="is-active">
About
</NavLink>
</li>
</ul>
<Switch>
<Route path="/home" exact component={Home} />
<Route path="/about" component={About} />
</Switch>
</div>
</div>
);
};

export default withRouter(App);

# 튜터에게 궁금한 점

질문은 아니고요.
기초 강의 때 주로 사용되는 HTTP 상태 코드에 대해서 다뤄봐도 좋을 것 같습니다.
참고 : https://developer.mozilla.org/ko/docs/Web/HTTP/Status
