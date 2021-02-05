# 이번주 리뷰
<br>
## Docker + Express
- Why Docker
> 서버를 구축하는데 있어서 '안정성'은 굉장히 중요한 요소이다. 도커를 이용하면 서버를 날리는 실수를 막을 수 있다.
- 도커는 리눅스 컨테이너 방식과 다르게 일련의 기능을 완전히 독립된 소프트웨어 환경에서 동작하게 된다.
- 그래서 OS자원을 그대로 사용하므로 하이퍼 바이저가 가상환경을 위해 가상의 커널을 만드는 오버헤드가 거의 없다는 장점을 가지고 있다.


## Promise
>  자바스크립트 비동기 처리에 사용되는 객체
- 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다.

- 원래 코드 (ajax통신 예제)
```js
function getData(callbackFunc) {
  $.get('url 주소/products/1', function(response) {
    callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
  });
}

getData(function(tableData) {
  console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```

- Promise를 적용한 코드
```js
function getData(callback) {
  // new Promise() 추가
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function(tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
```

### resolve, reject
> ```new Promise()```의 콜백 함수 인자는 ```resolve```, ```reject```

```js
new Promise(function(resolve, reject) {
 // ...
});
``` 

- ```resolve```는 약속을 지킬 수 있는 상황이 되었을 때, 즉 **성공**했을 때 약속을 이행하고 결과 값을 외부로 ```return```하는 함수
- ```then()```을 이용하여 처리 결과 값을 받을 수 있다.
```js
function getData() {
  return new Promise(function(resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
  console.log(resolvedData); // 100
});
```

- ```reject```는 약속이 깨졌을 때, 즉 **실패** 상태에 결과 값을 ```return```
- 그리고, 실패 상태가 되면 실패한 이유(실패 처리의 결과 값)를 catch()로 받을 수 있다.
```js
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});
```
<hr>

### Promise 예제
```js
function sendResume(){
	// 이력서를 전송하는 수도 코드
	return true
}

const createPromiseSendResume = (isTimeToSendResume) => {
return new Promise((resolve, reject) => {
	// 12월을 체크하는 변수
	if(isTimeToSendResume){
		sendResume()
		resolve('이력서 전송 완료')
	}else{
		reject('아직 12월 1일이 되지 않았습니다.')
	}
})
}
```
```js
createPromiseSendResume(true) // Promise {<fulfilled>: "이력서 전송 완료"}
```
```js
createPromiseSendResume(false) // Promise {<rejected>: "아직 12월 1일이 되지 않았습니다."}
```

<hr>

```js
function prepareInterview(){
	// 면접을 준비하는 수도 코드
	return true
}
const createPromisePrepareInterview = () => {
	return new Promise((resolve, reject) => {
		prepareInterview()
		resolve('면접 준비 완료')
})
}
```
```js
createPromisePrepareInterview() // Promise {<fulfilled>: "면접 준비 완료"}
```
<hr>

- 이 2개의 ```Promise``` 예제의 연결
```js
function sendResume(){
	// 이력서를 전송하는 수도 코드
	return true
}

const createPromiseSendResume = (isTimeToSendResume) => {
  return new Promise((resolve, reject) => {
	// 12월을 체크하는 변수
	if(isTimeToSendResume){
		sendResume()
		resolve('이력서 전송 완료')
	}else{
		reject('아직 12월 1일이 되지 않았습니다.')
	}
})
}

function prepareInterview(){
	// 면접을 준비하는 수도 코드
	return true
}
  
// 이전의 작업이 끝났음을 받는 message 변수 추가
const createPromisePrepareInterview = (message) => {
  return new Promise((resolve, reject) => {
		prepareInterview()
    resolve(message + ' -> ' + '면접 준비 완료')
})
}

createPromiseSendResume(true).then(
  (response) => { return createPromisePrepareInterview(response)}
).then((response) => console.log(response)) // 이력서 전송 완료 -> 면접 준비 완료
```

## Async & Await

### 등장 배경
> async와 await는 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법으로 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와준다.

### Async
> ```async``` 함수는 Promise를 기반으로 하고 있으며, 좀 더 syncronous한 형식으로 promise를 사용할 수 있도록 도와준다.

- 원래 Promise 코드
```js
function fetchUser() {
  return new Promise((resolve, reject) => {
     // do network request in 10 secs ...
     resolve('woojerry');
  });  
}

const user = fetchUser();

user.then(console.log); // woojerry
```

- async 적용 코드

```js
async function fetchUser() { // 자동적으로 함수 안의 코드블럭이 자동으로 Promise로 바뀌게 된다.
   // do network request in 10 secs ...
     return 'woojerry'
}

const user = fetchUser();
user.then(console.log); // woojerry
```

### Await
> ```await```는 반드시 ```async``` 내에서만 사용이 가능하다.
- ```await```는 Promise를 기다리는 명령어이다. 즉, Promise가 완료될 때까지 기다렸다가 다음 코드를 실행한다.
- 원래 Promise 코드

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

function getApple() {
  return delay(1000)
  .then( () => 'apple');
}

function getBanana() {
  return delay(1000)
  .then( () => 'banana');
}

function pickFruits() {
  return getApple().then(apple => { 
    return getBanana().then(banana => `${apple} + ${banana}`);
  });
}  

pickFruits().then(console.log); // apple + banana
    
```
- async / await 적용 코드 

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return 'apple';
}

async function getBanana() {
  await delay(1000);
  return 'banana';
}

async function pickFruits() {
    const apple = await getApple();
    const banana = await getBanana();
    return `${apple} + ${banana}`;
}  

pickFruits().then(console.log); // apple + banana
```

- 하지만 이 경우에는 apple 따오고 나서 banana를 따온다. (2초 소요)
- apple과 banana를 받아오는 것은 다른 작업이므로 기다릴 필요없이 동시에 수행 가능하다.

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return 'apple';
}

async function getBanana() {
  await delay(1000);
  return 'banana';
}

async function pickFruits() {
  const applePromise = getApple(); // Promise를 만들면 바로 Promise가 실행이 된다.
  const bananaPromise = getBanana();
  const apple = await applePromise;
  const banana = await bananaPromise;
  return `${apple} + ${banana}`;
}

pickFruits().then(console.log); // apple + banana
```
- 이렇게 병렬처리를 해준 경우에는 1초 만에 결과가 나타난다.
- 하지만 이 코드는 깔끔하지 않다.

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return 'apple';
}

async function getBanana() {
  await delay(1000);
  return 'banana';
}

// Promise에서 제공하는 all API 활용하기
// Promise 배열을 전달하게 되면 모든 Promise를 병렬적으로 받을 때까지 모아준다.

function pickAllFruits() {
  return Promise.all([getApple(), getBanana()]).then(fruits =>
    fruits.join(' + ')
  );
}  
pickAllFruits().then(console.log); // apple + banana
```

- async, await만 사용해 나타내기 -> async, await로 한번 더 감싸주기
```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(1000);
  return 'apple';
}

async function getBanana() {
  await delay(1000);
  return 'banana';
}

function pickAllFruits() {
  return Promise.all([getApple(), getBanana()]).then(fruits =>
    fruits.join(' + ')
  );
}  

const printFruits = async () => { 
    result = await pickAllFruits();
    console.log(result)
};

printFruits(); // apple + banana
```





# 튜터에게 궁금한 점
궁금한점 작성 공간!