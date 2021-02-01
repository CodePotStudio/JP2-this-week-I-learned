# 이번주 리뷰

## 📍 저번 주 배운내용 복습

### ⚡️ CSS grid란
저번주에 배웠던 `flex`의 경우, 1차원은 행과 열로 `item`들을 효율적으로 배치 할 수 있다 그러나 1차원 이상의 차원에서 `item`들을 배치하고 싶다면 여러개의 `flex`를 조합해서 사용해야한다.

그래서 나온 기능이 `CSS grid`인데, 이는 작성하는 코드가 효율적이고 단순하게 작성가능하다는 점에서 유용하게 사용된다.

### ⚡️ Column과 Row 설정하기
`grid`의 `column`을 설정할 때는 `grid-template-columns` 속성을 주로 사용한다.

예를 들어, `grid-template-columns: 100px 200px 300px`를 적용하면 하나의 `row`에서 `100px, 200px, 300px`씩의 `column`을 만들고 `grid` 내부의 `item`을 다음과 같이 채우게 된다.

그리고 만약, `column`개수보다 좁게 선언하면 `row`가 추가되면서 `item`들이 넘어가게된다.

![](https://images.velog.io/images/abcd8637/post/9060617a-0d1c-422c-899d-9bfbc23845d1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2014.57.29.png)

만약, 한 줄로 만들고 싶다면 `item`개수만큼 `column`을 선언해주자
`grid-template-columns: 100px 200px 300px 300px 200px 100px;`

![](https://images.velog.io/images/abcd8637/post/9c1b5a13-f3fa-4362-92b1-96d7bc9c5cde/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.01.29.png)

`grid-template-columns`는 `px` 뿐만아니라 `%`, `rem`, `em` 같은 모든 사이즈 단위를 적용 할 수 있다. 
또한, `grid`만에서 사용하는 `fr`단위가 있는데 아주 유용한 단위이다.

`fr`을 알아보기 전에 현업에서는 `rem`과 `em`을 많이 사용하는데, 대체 어떤 점에서 많이 사용하는지 짧게 알아보자.

---

### 💡 rem과 em
em rem은 모두 길이가 유연한 가변 단위인데, 디자인에 설정된 폰트 크기에 따라 브라우저에 의해 픽셀값으로 변경된다. 

즉, `px`처럼 고정된 크기에만 머무는게 아니라 구성 요소의 크기를 늘리고 줄이는 게 가능해진다. 

이러한 유연성은 개발 중 만날 수 있는 다양한 상황에 대처가 훨씬 쉬워지고, 브라우저 사용자는 전체 사이트의 크기를 조절해 가며 읽기에 가장 적합한 환경을 손수 구성할 수도 있다.

`rem`은 페이지 최상위(root)요소, html 요소의 폰트크기가 기준이 되는 단위 즉, `최상위(root)의 폰트 크기 x rem` 값이라고 할 수 있다. 간단하게 예를 들어보자.
```javascript
<style>
html {
    font-size: 16px;
}

.card-box{
    font-size: 10rem;
}
</style>

<body>
<div class='card-box'>Hello</div>
</body>
```
라고 하면 `Hello`의 `font-size`는 `16 x 10`이 되어 `160px`이 된다.


`em`은 스타일을 지정한 요소의 폰트 크기를 곱한 값이다.
예를 들면,
```javascript
<style>
.temp-size{
    font-size: 18px
}
.card-box{
    font-size: 10em
}
</style>

<body>
<div class='temp-size'>
<div class='card-box'>Hello</div>
</div>
</body>
```
`Hello`의 `font-size`는 `18 x 10`이 되어 `180px`이 된다.


<a href ='https://webdesign.tutsplus.com/ko/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984'>Reference</a>

---

다시 본론으로 돌아와, `fr`에 대해서 배워보자.
`fr(fraction)`은 화면을 효과적으로 나눌 때 쓰는 단위인데, 컨테이너 내 공간 비율을 분수로 나타낸다. 즉, 화면 비율에 맞게 `item`을 설정 할 수 있다.

`fr`은 화면 비율을 `3등분` 할 때 쉽게 사용 할 수 있는데, 
전체가 `100%`이라고 할 때 `33.333%`으로 입력하는것보다 `1fr 1fr 1fr`로 입력하는것이 편할 것이다.

`grid-template-columns: 1fr 1fr 1fr;`인 화면

![](https://images.velog.io/images/abcd8637/post/8d872050-c46c-4016-a58f-c04a070e2b53/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.26.15.png)

또한, `grid-template-columns`뿐만아니라, `row`도 `fr`로 나타낼 수 있다.

### ⚡️ grid item을 효과적으로 배치하기
`grid`는 `flex`와 달리 `item`을 자기가 원하는 위치에 배치 할 수 있다.

다음과 같이 3개의 비율로 열을 나누고 크기가 `100px`인 3개의 `row`를 만들었다고 가정했다고 생각해보자.

![](https://images.velog.io/images/abcd8637/post/16ac8dd9-e0e5-40d3-916a-2371246576b6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.30.44.png)

이때, 1열을 `A`박스로만 채우고 2열부터 차례대로 나머지 박스를 채우고 싶을땐 어떻게 할 것인가?

그럴때는 `grid-column: 1 / 4`를 주면되는데, 이는 한 `row`에서 `1~4`번째까지의 `column`을 차지하라는 뜻이다.

![](https://images.velog.io/images/abcd8637/post/6150255f-5cb7-43e9-8dbe-d0dd2c6b7498/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.35.43.png)

그러면, `column`번호를 어떻게 나눌까?
다음과 같이 나눌 수 있다.

![](https://images.velog.io/images/abcd8637/post/2eb01990-482e-4b05-a40a-4d89884541b7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.37.45.png)

다음으로 만약, `row: 2~4, column: 1~4`까지 차지하는 `b`를 만들려면 어떻게 해야할까? 다음과 같이 할 수 있다.
```css
.b{
                grid-row: 2 / 4;
                grid-column: 1 / 4
            }
```
![](https://images.velog.io/images/abcd8637/post/c0a77cc5-a865-4c02-bcf7-244392a15563/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.40.40.png)

### ⚡️ 웹페이지 layout 구성하기
앞에서 배운내용을 토대로 응용하여 실제 웹페이지를 만들때도 사용 할 수 있다.

![](https://images.velog.io/images/abcd8637/post/cfdc42cd-fd00-4453-a2b6-efcbf19dc5c6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.52.50.png)

영역따라 구분하려면 어떻게 작성해야할까?
다음과 같이 작성하면 된다.

```css
.header {
            background-color: #3f29ef;
            grid-column: 1 / -1;
            grid-row: 1
        }

        .side-bar {
            background-color: #38dab0;
            grid-column: 1;
            grid-row: 2
        }

        .main {
            background-color: #fdc35a;
            grid-column: 2;
            grid-row: 2
        }

        .footer1{
            background-color: #e13338;
            grid-column: 1 / -1;
            grid-row: 3
        }
```

![](https://images.velog.io/images/abcd8637/post/60081640-ecaf-4a7c-86cb-26a47ef3445e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2015.57.18.png)

그런데 여기서 `1 / -1`은 무슨의미일까? 
`-1`은 마지막 컬럼을 뜻하며 `-2`가 되면 마지막에서 두번째 컬럼을 뜻한다.

또, 반응형 layout을 만들 때에도 `grid`가 사용된다.
지금까지 배웠던 `grid-template-column` 과 `grid-template-areas`에서 `media-query`을 더한다면 쉽게 구현 할 수 있다.

예를 들어, 화면이 600px 이하인 화면에서 `1 column`에 `상단: Header ` `가운데: Main` `우측: side-bar`, `하단: footer`을 배치하려면 다음과 같이 사용 할 수 있다.

```css
@media (max-width: 600px) {
            .container {
                grid-template-columns: 2fr;
                grid-template-areas:
                    "header"
                    "main side-bar"
                    "footer"
            }
        }
```

![](https://images.velog.io/images/abcd8637/post/86b9670f-0db6-4568-ae44-cd5df827a15f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-31%2016.08.59.png)

지금까지 `grid`를 배워봤는데, 저번주에 배웠던 `flex`를 이용하면 웹페이지의 기본적인 틀을 쉽게 만들 수 있을 것 같다.
또한, 웹페이지를 구축할 때 `item` 배치는 `mobile`에서 사용하는 작은 화면에서 `item`들을 배치하고 `pc`버전인 큰 화면으로 `item`을 추가하는 방향으로 진행한다면 어렵지 않게 만들 수 있다.

## 📍 이번 주 공부 한 내용
이번주에 `sort`코드를 `redux`화 해야하는데, 
전체적으로 감이 잘 오지 않아 서적에 나와있는 `redux` 를 공부해봤습니다.

### 리덕스 관련 코드 작성하기
리덕스를 사용할 때는 `액션 타입`, `액션 생성 함수`, `리듀서 코드`를 작성해야하는데 이 코드들을 각각 다른 파일에 작성하는 방법이 있고, 기능별로 묶어서 파일 하나에 작성하는 방법도 있다.

>1. 일반적인 구조: `actions`, `constants`, `reducers` 세 개의 디렉토리를 만들고 그 안에 기능별로 파일을 하나씩 만드는 방식, 코드를 종류에 따라 다른 파일에 작성하여 정리할 수 있어 편리하지만, 새로운 액션을 만들 때마다 세 종류의 파일을 모두 수정해야하기 때문에 불편하기도 하다. 리덕스 공식 문서에서도 사용되므로 가장 기본적이지만, 사용하기에 따라 불편할 수도 있는 방법이다.
>2. Ducks 패턴: `액션타입`, `액션 생성 함수`, `리듀서 함수`를 기능별로 묶어 하나에 몰아서 작성하는 방식이고 `Ducks` 패턴이라고 부른다. 리덕스를 사용하다 불편함을 느낀 개발자들이 주로 사용하는 방식이다.

### [ 실습 ] Counter redux를 만들어보자.

### ⚡️ 1. 액션 타입 정의하기
`counter.js`파일에 다음과 같이 작성하자
```javascript
// modules/counter.js
const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';
```

가장 먼저 해야하는 작업은 `액션 타입`을 정의하는 것인데, 액션 타입은 대문자로 정의하고 문자열 내용은 `모듈 이름 / 액션 이름`과 같은 형태로 작성한다. 문자열 안에 모듈 이름을 넣음으로써, 나중에 액션의 이름이 충돌되지 않게 하기 위함이다.

### ⚡️ 2. 액션 생성 함수 만들기
액션 타입을 정의한 이후에는 액션 생성 함수를 만들자

```javascript
// modules/counter.js
const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

export const increase = () => ({type: INCREASE})
export const decrease = () => ({type: DECREASE})
```

`export`를 선언함으로써 이 함수를 다른 파일에서 불러와 사용 할 수 있다.
   
### ⚡️ 3. 초기 상태 및 리듀서 함수 만들기
`counter`모듈의 초기 상태와 리듀서 함수를 만들어주자.

```javascript
// modules/counter.js
const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

export const increase = () => ({type: INCREASE})
export const decrease = () => ({type: DECREASE})

const initialState = {
    number: 0
}

function counter(state = initialState, action){
    switch(action.type){
        case INCREASE:
            return {
                number: state.number + 1
            }
        case DECREASE:
            return {
                number: state.number - 1
            }
        default:
            return state
    }
}

export default counter;
```
초기 상태에는 `number`값을 설정해주고, 리듀서 함수에는 현재 상태를 참조하여 새로운 객체를 생성해서 반환하는 코드를 작성했다.

### ⚡️ 4. 루트 리듀서 만들기
지금은 리듀서를 1개밖에 만들지 않았지만, 만약 2개 이상의 리듀서를 만들었다면, `combineReducers`함수를 이용하여 하나로 합쳐주어야한다.
예시를 들기위해 `todos`라는 리듀서를 한 개 더 만들었다고 가정해보자.

```javascript
// modules/index.js
import { combineReducers } from 'redux';
import counter from './counter';
import todos from './todos';

const rootReducer = combineReducers({
    counter,
    todos,
})

export default rootReducer;
```

### ⚡️ 5. 스토어 만들기
가장 먼저 스토어를 생성한다.
```javascript
// src/index.js

// 기타 코드 생략
import { createStore } from 'redux';
import rootReducer from './modules';

const store = createStore(rootReducer);

<Provider store={store}>
    <App />
<Provider>
```

### ⚡️ 6. CounterContainer 만들기
```javascript
// containers/CounterContainers.js

import React from 'react';
import Counter from '../components/Counter;

const CounterContainer = () => {
    return <Counter />
}

export default CounterContainer;
```

위 컴포넌트를 리덕스와 연동하려면 `react-redux`에서 제공하는 `connect`함수를 사용해야하는데,
사용방법은 다음과 같다. 
> `connect(mapStateToProps, mapDispatchToProps)(연동할 컴포넌트)`

`connect` 뒤에 사용된 함수들은 어떤 의미가 있는지 살펴보자.
>1. `mapStateToProps`: 리덕스 스토어 안의 상태를 컴포넌트의 `props`로 넘겨주기 위해 설정하는 함수
>2. `mapDispatchToProps`: 액션 생성함수를 컴포넌트의 `props`로 넘겨주기위해 설정하는 함수

이렇게 `connect` 함수를 호출하고 나면 또 다른 함수를 반환하는데, 반환된 함수에 컴포넌트를 `parameter`로 넣어주면 리덕스와 연동된 컴포넌트가 만들어진다.

```javascript
const makeContainer = connect(mapStateToProps, mapDispatchToProps)
makeContainer(타깃 컴포넌트)
```

이제 한번 `CounterContainer`에 적용해보자.
```javascript
// containers/CounterContainers.js

import React from 'react';
import { connect } from 'react-redux';
import Counter from '../components/Counter';
import { increase, decrease } from '../modules/counter';

const CounterContainer = ({ number, increase, decrease }) => {
    return (<Counter number={number} onIncrease={increase} onDecrease={decrease} />)
}

const mapStateToProps = state => ({
    number: state.counter.number,
})

const mapDispatchToProps = dispatch => ({
    increase: () => {
        dispatch(increase())
    },
    decrease: () => {
        dispatch(decrease())
    },
});

export default connect(
    mapStateToProps,
    mapDispatchToProps,
)(CounterContainer);
```
`mapStateToProps`, `mapDispatchToProps`에서 반환하는 객체 내부의 값들은 컴포넌트의 `props`로 전달된다.
>1. `mapStateToProps`는 `state`를 파라미터로 받아 오며, 이 값은 현재 스토어가 지니고 있는 상태를 가리킨다.
>2. `mapDispatchToProps`의 경우 `store`의 내장 함수 `dispatch`를 파라미터로 받아온다. 

이후 `App`에서 컴포넌트를 작성해주면 된다.
```javascript
// ... 기타 코드 생략
import CounterContainer from './containers/CounterContainer';

const App = () => {
    return(
        <div>
            <CounterContainer />
        </div>
    )
}

export default App;
```

### ⚡️ 7. 결과 확인하기
이후 `handleAction`, `immer`, `useSelector`, `useDispatch`등을 이용하여 응용 할 수 있다.


# 튜터에게 궁금한 점
`sort` 기능을 `redux`로 구현하려고 하는데 방향을 다음과 같이 잡으면 되는지 궁금합니다. 
<a href='https://github.com/YWTechIT/test_shop/pull/3/files'>깃허브 링크</a>