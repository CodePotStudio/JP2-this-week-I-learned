# 이번주 리뷰

![redux](https://user-images.githubusercontent.com/50645183/105139663-e1884600-5b39-11eb-81f1-e041e6aebe2b.PNG)

## Keywords

### 액션(Action)

> 상태에 어떠한 변화가 필요하게 될 땐, 우리는 액션이란 것을 발생시킨다.

```jsx
{
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
```

### 액션 생성함수

> 파라미터를 받아와 액션 객체 형태로 만들어주는, 액션을 만드는 함수

- 리덕스를 사용 할 때 액션 생성함수를 사용하는것이 필수적이진 않다. 액션을 발생 시킬 때마다 직접 액션 객체를 작성할수도 있다.

```jsx
export function addTodo(data) {
  return {
    type: "ADD_TODO",
    data,
  };
}

// 화살표 함수로도 만들 수 있다.
export const changeInput = (text) => ({
  type: "CHANGE_INPUT",
  text,
});
```

### 리듀서(Reducer)

> 변화를 일으키는 함수. 두가지의 파라미터를 받아온다.

```jsx
function reducer(state, action) {
  // 상태 업데이트 로직
  return alteredState;
}
```

```jsx
function counter(state, action) {
  switch (action.type) {
    case "INCREASE":
      return state + 1;
    case "DECREASE":
      return state - 1;
    default:
      return state;
  }
}
```

### 스토어 (Store)

> 리덕스에서는 한 애플리케이션당 하나의 스토어를 만들게 된다. 스토어 안에는, 현재의 앱 상태와, 리듀서가 들어가있고, 추가적으로 몇가지 내장 함수들이 있다.

### 디스패치(dispatch)

> 액션을 발생 시키는 것. 파라미터로 action을 전달

```jsx
const dispatch = useDispatch();
const onCreate = (text) => dispatch(addTodo(text)); // addTodo(text)가 action
```

### 구독(subscribe)

> 원래는 `subscrbie`함수를 통해, 예전에는 `connect`를 사용했으나 요즘은 `useSelector`를 활용해 리덕스의 상태값을 조회하는 것

```jsx
const { number, diff } = useSelector((state) => ({
  // 이런식으로 하면 상태가 바뀌지 않아도 전체가 리랜더링
  number: state.counter.number,
  diff: state.counter.diff,
}));
```

```jsx
const number = useSelector((state) => state.counter.number); // useSelector를 여러번 사용해 바뀐 상태의 부분만 리랜더링
const diff = useSelector((state) => state.counter.diff);
```

## Fetch

> 브라우저에 내장된 `fetch()`함수는 비동기 HTTP 요청을 하기 위해 사용한다. fetch() 기본은 GET이다.

- 사용법 : Promise 타입의 객체를 반환, 반환된 객체는, API 호출이 성공했을 경우에는 응답(response) 객체를 resolve하고, 실패했을 경우에는 예외(error) 객체를 reject한다.

```js
fetch(url, options)
   .then(res => res.json()) // 요청이 성공할 경우 then에서 response 객체를 받아 처리
   .then(res => { // data를 응답 받은 후의 로직 })
  .catch((error) => console.log("error:", error)) // catch에서는 error 처리
```

### GET

> 원격 API에 있는 데이터를 가져올 때 쓰이는 GET 방식의 HTTP 통신의 경우

```js
const endpoint = `${API_URL}movie/popular?api_key=${API_KEY}&lanuage=en-US&page=1`;

fetch(endpoint)
  .then((response) => response.json())
  .then((response) => {
    console.log(response);
    // 요청이 성공했을 때 작업들
  });
```

### POST

> POST인 경우에는 fetch() 함수에 method 정보를 인자로 넘겨주어야 한다.

```js
const endpoint = "https://api.google.com/user";

fetch(endpoint, {
  method: "post",
  body: JSON.stringify({
    // body는 JSON형태로 보내기 위해 JSON.stringfy() 함수에 객체를 인자로 전달하여 JSON형태로 변환한다.
    name: "yeri",
    batch: 1,
  }),
})
  .then((res) => res.json())
  .then((res) => {
    if (res.success) {
      alert("저장 완료");
    }
  });
```

- 참고 : https://yeri-kim.github.io/posts/fetch/

<br>
리뷰 작성 공간!!!

# 튜터에게 궁금한 점

궁금한점 작성 공간!

1. 하단의 코드에서 `...state`를 deep copy해주고 사용하고 있는데, 따로 `a = ...state` 이런식으로 하지 않고 저렇게 바로 사용할 수 있는 건가요 ??

```jsx
function reducer(state = initaiState, action) {
    switch (action.type) {
    case INCREASE:
      return {
        ...state,
        counter: state.counter + 1,
      };
```

2. useEffect 훅을 사용할 때 API 정보를 이용하려고 할 때, axios를 사용하는 것과 fetch를 사용하는 것의 차이점이 궁금합니다 ! 그냥 axios가 더 편한 거라고 보면 되는건가요 ??

3. 아직 Redux 미들웨어까지는 섭렵하지는 못했지만 요즘은 Context API와 Hook들을 사용해 만드는 것이 Redux를 쓰는 것보다 늘어나고 있다는 글도 본 것 같은데 대략적인 차이점을 한번 짚어주시면 감사하겠습니다 !

4. Redux에서 구독을 할 때, `connect`는 store가 갱신될 때마다 전체가 리렌더링 될 수 있으므로 `useSelector` 를 활용해서 따로 처리해주는 식으로 요즘 많이 사용한다고 하던데요 ,, 그럼 `subsrcibe()`는 단순히 store에 연결해주는 함수인건가요? `subsrcibe()`에 대한 정보가 헷갈리네요 ,, 제가 이해하기엔 subscribe는 store에 직접적으로 연결하는 것이고, `useSelector`, `connct` 등이 실제로 상태에 구독하는데 많이 쓰는데 ,, `useSelector`를 쓰는 것이 요즘 대세이다? 이렇게 이해한 게 맞을까요?

<hr>
- 코드 자동 완성 해주는 확장 때문에 md파일이 좀 이상하게 저장되네요 ,, 범인이 어떤 확장파일인지 못찾아내겠네요 ,,
- Redux 미들웨어 쪽도 보면서 이번주부터는 이제 직접 만들어보며 Redux의 필요성을 느껴봐야할 거 같습니다. 아직까지는 오히려 더 복잡해지는게 아닌가 생각이 드네요 ,, 직접 경험해야 느낄 것 같습니다 !
