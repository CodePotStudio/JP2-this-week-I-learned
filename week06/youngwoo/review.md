# 이번주 리뷰
<br>

## 📍 저번 주 내용 복습
### ❏ promise란?
`Promise`는 javascript 비동기 처리에 사용되는 객체이다. 
여기서 비동기 처리는 `특정 코드의 실행이 완료 될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성`을 의미한다. 
(자바스크립트의 동작원리를 잘 모르겠다면 <a href='https://toycrane.medium.com/진짜-쉽게-알아보는-자바스크립트-동작-원리-c7fbdc44cc97'>링크</a>를 참고하자 )

### ❏ promise가 왜 필요할까?
`Promise`는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다. 
일반적으로 웹 애플리케이션을 구현 할 때 서버에서 데이터를 요청하고 받아오기 위해 `API`를 사용한다.
그런데, 데이터를 받아오기도 전에 마치 데이터를 다 받아온것처럼 화면에 표시하려고 하면 오류가 발생하거나 빈 화면이 뜬다. 이와 같은 문제를 해결하기 위한 방법 중 하나가 `Promise`이다.

### ❏ `Promise` 쉬운 예제
```javascript
function getData(){
    return new Promise(function(resolve, reject){
        $.get('https://jsonplaceholder.typicode.com/todos/1', function(response){
            if(response){
                resolve(response);
            }
            reject(new Error('Request is failed'));
        })
    })
}

getData().then(function(data) {
    console.log(data);
}).catch(function(err){
    console.error(err);
});
👉🏽 Promise {<pending>}
👉🏽 {userId: 1, id: 1, title: "delectus aut autem", completed: false}
```
서버에서 제대로 응답을 받아오면 `resolve()` 메서드를 호출하고, 응답이 없으면 `reject()`메서드를 호출하는 예제이다. 호출된 메서드에 따라 `then()`이나 `catch()`로 분기하여 응답 결과 또는 오류를 출력할 수 있다.

### ❏ `Promise Chaining` 
프로미스의 또 다른 특징은 여러 개의 프로미스를 연결하여 사용 할 수 있는데, 앞 예제에서
`then()` 메서드를 호출하고 나면 새로운 프로미스 객체가 반환된다. 따라서, 아래와 같이 사용가능하다.

```javascript
new Promise(function(resolve, reject){
  setTimeout(function() {
    resolve(1);
  }, 2000);
})
.then(function(result) {
  console.log(result); // 1
  return result + 10;
})
.then(function(result) {
  console.log(result); // 11
  return result + 20;
})
.then(function(result) {
  console.log(result); // 31
});
```
`resolve()`가 호출되면 
>1. `.then()` 로직으로 넘어가 결과값 1을 받아 10을 더하고 
>2. `11` 다음 `.then()`으로 넘기고 
>3. `20` 더한 값을 다음 `.then()`으로 넘긴다 
>4. 마지막 `.then()`에서 최종 결과 값 31을 출력한다.

### ❏ `Promise` Error 처리는 가급적 `catch()`를 사용하자
위의 `getData()` 함수의 프로미스에서 `resolve()` 메서드를 호출하여 정상적으로 로직을 처리했지만, `then()`의 첫 번째 콜백 함수 내부에서 오류가 나는 경우 오류를 제대로 잡아내지 못한다. 하지만, 같은 오류를 `catch()`로 처리하면 다른 결과가 나온다.

```javascript
// then()의 두 번째 인자로는 감지하지 못하는 오류
function getData() {
  return new Promise(function(resolve, reject) {
    resolve('hi');
  });
}

getData().then(function(result) {
  console.log(result);
  throw new Error("Error in then()"); // Uncaught (in promise) Error: Error in then()
}, function(err) {
  console.log('then error : ', err);
});

// catch()로 오류를 감지하는 코드
function getData() {
  return new Promise(function(resolve, reject) {
    resolve('hi');
  });
}

getData().then(function(result) {
  console.log(result); // hi
  throw new Error("Error in then()");
}).catch(function(err) {
  console.log('then error : ', err); // then error :  Error: Error in then()
});
```

## 📍 구현 한 기능
1. `<button>`을 누르면 상품들을 상품명, 가격 높은 순, 가격 낮은 순으로 정렬
  * `img` 도 같이 변경
  * `img` 클릭하면 해당 상품 상세페이지 이동
2. 장바구니에 추가된 상품 제거
<a href='https://github.com/YWTechIT/test_shop'>git_hub</a>

## 📍 구현 할 기능
1. `Node.js`를 이용한 `Login` 기능 구현
<a href='https://backend-intro.vlpt.us/'>참고 링크</a>

## 📍 삽질하며 얻은 기능
1. 빈 배열에 `push`로 추가된 데이터 중 원하는 데이터를 삭제하고 싶으면 `findIndex`로 해당 배열을 반환한 뒤 `splice`로 잘라주면된다.
```javascript
if (액션.type === '항목제거'){
    let copy = [...state];
    let idx = copy.findIndex((e) => e.id === 액션.payload);
    if (idx > -1) copy.splice(idx, 1);
    return copy;
}
```

## 백엔드 기초 다지기, 프로젝트 시작하기
<a href='https://github.com/YWTechIT/test_koa'>yw_github</a>

### ❏ 순서
>1. `Koa`를 이용하여 웹서버 만들기
>2. `Mongoose` 를 통한 `MongoDB` 연동 실습
>3. 회원가입 / 로그인 `API` 만들기

### 1. `Koa` 기본 사용법
`src` 디렉토리를 사용하여 `index.js` 파일을 만든다음에 내부에 다음 코드를 작성한다.
```javascript
const Koa = require('koa');
const app = new Koa();

app.use(ctx => {
    ctx.body = 'Hello Koa';
});

app.listen(4000, () => {
    console.log('ywShop server is listening to port 4000');
});
```

### ❏ 미들웨어란?
`Koa` 어플리케이션은 미들웨어의 배열로 구성되어있는데, 위 코드에서 `app.use`함수는 미들웨어를 어플리케이션에 등록을 해준다.
```javascript
app.use(ctx => {
    ctx.body = 'Hello Koa';
});
```

여기서 `ctx => {...}` 코드는 하나의 미들웨어가 된다.
`koa` 미들웨어함수에서는 두 가지의 파라미터를 받는데, 위 코드의 `ctx`와, `next`이다.

# 튜터에게 궁금한 점
1. 백엔드 대표 프레임워크 중 `Django`, `NodeJS`의 가장 큰 차이점과 둘 중 현업에서 많이 사용하는 프레임워크가 무엇인가요?