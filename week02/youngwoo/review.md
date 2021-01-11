## 2주차 리뷰

1. JavaScript에서 자주 쓰이는 10가지 함수
2. 쇼핑몰 제작시 필요한 기본적인 기능들(Link, Switch, History, useEffect Hook, Ajax 등..)

## 1. JavaScript에서 자주 쓰이는 10가지 함수
### ✏️ 서론
`애플코딩` 강의를 듣다 혼자 예제문제를 푸는 과정에서 `JavaScript` 배열함수를 이용하는 문제가 나왔다.
쉬운 문제였었는데 솔루션을 찾지못하는 나를 보며 과연, 내가 알고 있는 배열함수는 몇개나 있을까? 하는 고민에 빠졌다.

`Youtube`에 관련영상을 찾아보니 `코드엘리`의 `모르면 후회하는 배열 함수 10가지` 영상을 봤다. 
나와 같은 <span style ='color:blue'>자린이(`JavaScript + 어린이`)</span>들에게 알맞는 난이도였고 영상을 보고 도움을 많이 받아 글을 남기려고 한다.

특히, 영상을 보기전에 배열함수를 이용하는 간단한 문제를 같이 첨부했는데, 꼭 풀어보길 권장한다.
혼자 고민하면서 문제를 푸니까 기억에 잘 남았다. 😄
하단의 코드는 `10가지 문제`를 축약해서 작성했다. 
본문에서 한 문제씩 풀어보자.

```Javascript
  // Q1. make a string out of an array
 
  // Q2. make an array out of a string
 
  // Q3. make this array look like this: [5, 4, 3, 2, 1]
 
  // Q4. make new array without the first two element
  
  // Q5. find a student with the score 90
 
  // Q6. make an array of enrolled students
 
  // Q7. make an array containing only the students' scores
  // result should be: [45, 80, 90, 66, 88]
 
  // Q8. check if there is a student with the score lower than 50
  
  // Q9. compute students' average score
 
  // Q10. make a string containing all the scores
 
  // Bonus! do Q10 sorted in ascending order
  // result should be: '45, 66, 80, 88, 90'
  
```

---

## ✏️ 본론

###  프로그래밍 언어를 공부 팁
문제풀기 앞서 엘리님이 알려주신 `💡 프로그래밍 언어를 공부 팁`이 있었는데, 

>
1. 궁금한 함수가 있으면, `API`가 정의된 라이브러리로 들어가기. (cmd + 함수클릭)
2. 라이브러리에서 `Parameter`는 무엇을 전달하는지, `return`되는 값은 무엇인지 확인하기.
3. `API`는 `Object`를 변형시키는 `API`인지, `Object`의 `State`는 변형시키는지 확인하기.
4. `?`: 함수 선언시 `Option`으로 선언가능한 구문


`Function API`가 정의된 라이브러리 모습<span style = 'color:blue'> (Feat. ~~영어공부의 중요성~~)</span>

![](https://images.velog.io/images/abcd8637/post/6b5bea1f-3dd9-44ac-8e8f-b1bbe3e3564c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-09%2021.22.37.png)

---

### 1. join( )
```javascript
// Q1. make a string out of an array
  const fruits = ['apple', 'banana', 'orange'];
```
  
단순히 `array`를 밖으로 꺼내라는 문제였기때문에, 
아무생각없이 `toString()` 함수를 사용했다.
하지만, `join()` 함수가 답이었다.
(`console.log()`는 제외하고 작성했다.)

>`let array = array.join();`
1. 배열에 있는 모든 값들을 더해 `string`으로 `return`시킨다. 
2. 내가 원하는 `문자열(separator)`을 추가 할 수 있다.

```javascript
let natos = ['alpha', 'bravo', 'charlie', 'delta'];

let nato1 = natos.join();
👉🏽 alpha,bravo,charlie,delta

let nato2 = natos.join('.');
👉🏽 alpha|bravo|charlie|delta

let nato3 = natos.join('|');
👉🏽 alpha.bravo.charlie.delta
```
---

### 2. split( )

```javascript
// Q2. make an array out of a string
  const fruits = '🍎, 🥝, 🍌, 🍒';
```

1번 문제와 반대로 이번에는 `string`을 `array`로 만들면 되는데, 
간단하게 `split()` 함수를 사용하면 풀 수 있다.
>`string.split( separator, limit )`
1. separator: 분할의 기준
2. limit: 최대 분할 개수

```javascript
const fruits = '🍎, 🥝, 🍌, 🍒';

let fruit = fruits.split();
👉🏽 ["🍎, 🥝, 🍌, 🍒"]

let fruit = fruits.split(',', 1);
👉🏽 ["🍎"]
```

---

### 3. reverse( )

```Javascript
// Q3. make this array look like this: [5, 4, 3, 2, 1]
  const array = [1, 2, 3, 4, 5];
```

배열을 뒤집는 함수는 `reverse()` 를 사용하면 된다.
그런데, `reverse()`는 원본의 배열까지 뒤집기 때문에 조건에 맞게 사용해야한다.

> `array.reverse()`

```javascript
let number = [1, 2, 3, 4, 5];
let reverseNumber = number.reverse();

console.log(reversNumber)
👉🏽 [5, 4, 3, 2, 1]
console.log(number)
👉🏽 [5, 4, 3, 2, 1]

let nato = ['alpha','bravo','charlie'];
let reverseNato = nato.reverse();

console.log(reveresNato)
👉🏽 ["charlie", "bravo", "alpha"]
console.log(nato)
👉🏽 ["charlie", "bravo", "alpha"]
```
---

### 4. splice( ), slice()

```Javascript
// Q4. make new array without the first two elements
  const array = [1, 2, 3, 4, 5];
```

배열을 추출하는 함수에는 크게 `splice()`와 `slice()`가 있다.
이 둘을 크게 나눠서 사용할 때는 `원본배열`이 바뀌는지 안 바뀌는지에 따라 사용할 수 있다.

---


### 4-1. slice()

원본배열은 수정되지 않는 함수는 `slice()` 함수이다.

>Array.prototype.slice( start[,end] )
Start(추출 시작점) 
1. undefined: 0부터 slice
2. 음수: 배열의 끝에서부터 길이를 설정한다. 
3. 배열의 길이와 같거나 큰 수: 빈 배열[ ]을 반환한다.

End(추출 종료점)
1. undefined: 배열의 끝까지 slice
2. 음수: 배열의 끝에서부터의 길이
3. 배열의 길이와 같거나 큰 수: 배열의 끝까지 추출

Return(반환 값)
1. 추출한 요소를 포함한 새로운 배열

모두 결과값은 같지만, `slice()` 함수의 특성을 이용한 다른 코드이다.
원본 배열이 수정되지 않음을 알 수 있다.

```javascript
let array = [1, 2, 3, 4, 5];

array.slice(-3)  
👉🏽 [3, 4, 5]

array.slice(2)
👉🏽 [3, 4, 5]

array.slice(2, 5)
👉🏽 [3, 4, 5]

// 원본배열 확인 코드
let array = [1, 2, 3, 4, 5];
let sliceArray = array.slice(-3)

console.log(array)
👉🏽 [1, 2, 3, 4, 5]
console.log(sliceArray)
👉🏽 [3, 4, 5]
```

---


### 4-2. splice()
`splice()` 함수는 `slice()`와 다르게 원본 배열 자체를 수정하는 특징을 가지고 있다.
원본은 함수를 실행하고 나머지(?)가 출력된다.

>Array.prototype.splice( start[,deleteCount[,item1[,item2[, ...]]]] )
Start(변경 시작점) 
1. 음수: 배열의 끝에서부터 길이를 설정한다. 
2. 배열의 길이보다 큰 수: 실제 시작 인덱스는 배열의 길이
3. 절대값이 배열의 길이보다 큰 경우: 0
   
deleteCount(제거할 요소의 수)
1. undefined / 값 > array.length: start부터 요소 제거만 수행
2. 음수: 어떤 요소도 제거되지 않음

item1, item2, ... (배열에 추가할 요소)
1. undefined: 요소 제거만 수행

Return(반환값)
1. 0: 빈 배열

```javascript
let array = [1, 2, 3, 4, 5];

array.splice(-3)  
👉🏽 [3, 4, 5]

array.splice(2)
👉🏽 []

array.splice(2, 5)
👉🏽 []

// 원본배열 확인 코드
let array = [1, 2, 3, 4, 5];
let spliceArray = array.splice(-3)

console.log(array)
👉🏽 [1, 2]
console.log(sliceArray)
👉🏽 [3, 4, 5]
```
---

### 5. find()

```javascript
// Q5. find a student with the score 90
class Student {
    constructor(name, age, enrolled, score) {
      this.name = name;
      this.age = age;
      this.enrolled = enrolled;
      this.score = score;
    }
  }
  const students = [
    new Student('A', 29, true, 45),
    new Student('B', 28, false, 80),
    new Student('C', 30, true, 90),
    new Student('D', 40, false, 66),
    new Student('E', 18, true, 88),
    new Student('F', 18, true, 90),
  ];
\
```

특정 조건에 맞는 학생 값을 뽑으려면 `find()` 함수를 사용해야한다.
`find()`함수는 조건에 맞는 값 중 첫번째 값을 리턴하는 함수다. 

만약, 배열의 값이 조건에 부합하여 `true`를 리턴하면, 그 이후의 배열값은 테스트되지 않는다.
만약, 배열의 값이 조건에 부합하지 않으면 `undefined`를 리턴한다.

실험을 위해 `const students` 에 `Score === 90` 2명인 학생을 추가했다. 

`find()`함수를 선언할때 2가지 방법이 있는데 `function()`을 선언하는경우와 
`arrowFunction(()=>{})`을 사용하는경우다. 나는 후자로 코드를 작성했다.

`arr.find(callback(element[, index[, array]])[, thisArg])`
> 1. element: 현재 처리중인 배열의 element
> 2. index?: 현재 처리중인 배열의 index
> 3. array?: `find()`가 호출된 배열

```javascript
let student = students.find((student) => student.score === 90);
console.log(student)

👉🏽 Student {name: "C", age: 30, enrolled: true, score: 90}

let student = students.find((student) => student.score === 10);
console.log(student);

👉🏽 undefined
```

---

### 6. filter()
`filter()` 함수는 해당 조건에 맞는 요소들을 모아 새로운 배열로 반환하는 함수이다.
위 `find()` 함수랑은 다르게 모든 값들을 출력해주는 함수다. 

`arr.filter(callback(element[, index[, array]])[, thisArg])`
> 1. element: 현재 처리중인 배열의 element
> 2. index?: 현재 처리중인 배열의 index
> 3. array?: `filter()`가 호출된 배열

```javascript
// Q6. make an array of enrolled students
let enrolledStudent = student.filter(student => student.enrolled === true);
console.log(enrolledStudent);

👉🏽 [Student, Student, Student, Student]
0: Student {name: "A", age: 29, enrolled: true, score: 45}
1: Student {name: "C", age: 30, enrolled: true, score: 90}
2: Student {name: "E", age: 18, enrolled: true, score: 88}
3: Student {name: "F", age: 18, enrolled: true, score: 90}
length: 4
```

---

### 7. map()
`map()`함수는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 모아 새로운 배열을 반환한다.
`filter()`랑은 다른점은 해당 조건에 대한 값만 출력해준다.

`map()` 함수는 `callback`함수를 각각의 요소에 대해 한번씩 순서대로 불러 함수의 반환값으로 새로운 배열을 만든다. 

> arr.map(callback(currentValue[ ,index [, array]]) [,thisArg])
1. currentValue: 현재 처리할 요소
2. index: 현재 처리할 index
3. array: map()을 호출한 배열

```javascript
// Q7. make an array containing only the students' scores
// result should be: [45, 80, 90, 66, 88]
let studentScore = students.map(element => element.score)
console.log(studentScore)
👉🏽 [45, 80, 90, 66, 88, 90]
```

---

### 8. some(), every()

---

### 8-1. some()
`some()`함수는 배열안에 조건식이 하나라도 들어있으면 `true`, 아니면 `false`를 반환해준다.
결과값에 `!`를 붙이면 반대가 된다.

쉽게 생각해 `OR` 조건을 떠올리면 된다.

>arr.some(function(currentValue, index, array), thisValue))
1. currentValue: 현재 처리할 요소
2. index: 현재 처리할 index
3. array: map()을 호출한 배열1. 
4. thisValue: 함수 내부에서 사용될 this의 값

```javascript
// Q8. check if there is a student with the score lower than 50

let someTrueScore = students.some(student => student.score < 50);
console.log(someTrueScore)
👉🏽 true

let someFalseScore = students.some(student => student.score > 100);
console.log(someFalseScore)
👉🏽 false
```

---

### 8-2 every()
`every()` 함수는 `some()`과 반대로 모든 조건식이 들어맞을때 `true` 하나라도 틀리면 `false`를 반환한다.

쉽게 생각해 `AND` 조건을 떠올리면 된다.

>arr.every(function(currentValue, index, array), thisValue))
1. currentValue: 현재 처리할 요소
2. index: 현재 처리할 index
3. array: map()을 호출한 배열1. 
4. thisValue: 함수 내부에서 사용될 this의 값

```javascript
// Q8. check if there is a student with the score lower than 50

let everyTrueScore = students.every(student => student.score > 100);
console.log(everyTrueScore)
👉🏽 true

let everyFalseScore = students.every(student => student.score < 50);
console.log(everyFalseScore)
👉🏽 false
```

---

### 9. reduce()
`reduce()`는 하나의 단일 값으로 줄이는 함수다. 
보통 계산할때 많이 쓰이는데 배열 하나하나를 돌면서 무언가 값을 누적할때 주로 사용한다.

>arr.reduce(function(accumulator, currentValue, currentIndex, array), initialValue)
1. accumulator: 이전 함수 리턴 값
2. currentValue: 현재 element 값
3. currentIndex?: 현재 element의 index 값
4. array?: 현재 엘리먼트가 속한 원본 배열 

중간에 값을 확인하고 싶어 console.log를 추가했다.

```javascript
// Q9. compute students' average score
// 1. Define array studentScore
// 2. calculate studentSum
// 3. studentSum / studentScore.length

let sumScore = students.reduce((prev, curr) => {
    return prev + curr.score 
})
👉🏽 459

let averageScore = students.reduce((prev, curr) => {
    return prev + curr.score / students.length
})
👉🏽 76.5
```

---

### 10. sort()  
`sort()` 함수는 보통 배열을 정렬할 때 사용하는 함수이다.
오름차순, 내림차순으로 출력할때 간편하게 사용할 수 있다.

기본적으로 숫자는 `sort()` -> `reverse()`를 사용하면 간편하게 오름차순 / 내림차순 기능구현이 가능하지만, 문자는 유니코드 값 순서대로 정렬되기때문에, 간단한 식을 추가한다.

a, b 두개의 element를 선언하고, 
리턴되는 값이 0보다 작을 경우 a가 b보다 앞에 오도록 정렬하고,
리턴되는 값이 0보다 클 경우 b가 a보다 앞에 오도록 정렬한다.
만약 0을 리턴하면, a와 b의 순서를 변경하지 않는다.

오름차순: `return a - b`
내림차순: `return b - a`

> arr.sort([compareFunction])
1. compareFunction: 정렬 순서를 정의하는 함수

```javascript
// Bonus! do Q10 sorted in ascending order
// result should be: '45, 66, 80, 88, 90'
let ascendScore = students.sort((a,b) => a.score - b.score)
let descendScore = students.sort((a,b) => b.score - a.score)
```

---

### bounus! map() + join()
마지막 문제는 `student.score`를 `string`으로 변환하는 문제였다.
앞서 사용한 `map()` 함수와 `join()` 함수를 사용하자.

```javascript
// Q10. make a string containing all the scores
// result should be: '45, 80, 90, 66, 88'
let studentScore = students.map(element => element.score)
👉🏽 [45, 80, 90, 66, 88, 90]
let stringScore = studentScore.join()
👉🏽 45,80,90,66,88,90
```
---
## ✏️ 결론

지금까지 자바스크립트에서 자주 사용되는 10가지 배열함수들을 알아보았다.
길게 작성한다고 영원히 기억하는것은 아니지만, 까먹을때마다 언제든지 내 벨로그에서 확인 할 수 있다는점이 좋아 남겨놓는다.

비록 기초 문법공부를 매일매일 열심히 하지는 않지만, 필요할때마다 시간을 내어 조금씩 공부해서 남겨놓는다면 내것이 되지 않을까?? 😆 😆

---

## 2. 쇼핑몰 제작시 필요한 기본적인 기능들 (Link, Switch, History, useEffect Hook, Ajax 등..)

### 📍 Routing: 페이지 나누기
`Routing` 을 통해 상세페이지를 만들 수 있다.
메인페이지는 `/`으로 접속 할 때, 상세페이지는 `/detail`로 접속하도록 코드를 작성해보자.

`React-router`는 각각의 페이지마다 다른 `HTML`을 보여주는것이 아니고, `HTML` 내부의 내용을 갈아치워서 다른 페이지처럼 흉내내는 특징을 가지고있다.

> 1. terminal - `npm install react-router-dom`을 설치한다
> 2. `index.html` 파일에 
> `import { BrowserRouter } from 'react-router-dom';` 
> `import { HashRouter } from 'react-router-dom';` 둘 중 필요한 `Router`의 코드 1줄을 작성한다.
> 3. `App.js`에 `import { Link, Route, Switch } from 'react-router-dom';` 를 작성한다.
> 4. 원하는 곳에 `<Router></Router>` 태그를 작성한다.
> 5. `<Route>` 안에 `path = 주소이름`을 적어준다.

```javascript
import { Link, Route, Switch } from 'react-router-dom';

function App(){
  return(
    <div>
      <Route exact path= '/'>
        <div>메인페이지입니다.</div>
      </Route>
      <Route path= '/detail'>
        <div>상세페이지입니다.</div>
      </Route>
    </div>
  )
}
```

`Route`안에 `Component`로 간단하게 작성도 가능하다.
```javascript
<Route path ='/' component={Card}> </Route>
<Route path ='/'> <Card /> </Route>
```
이렇게 상세페이지를 작성해봤는데, `/detail` 페이지로 접속하면 메인페이지와 상세페이지가 동시에 보여지는 경우가 있다. 정상적인 경우인데 `/detail`의 경로에 `/`가 포함되어있기때문에 동시에 렌더링을 해주기 때문이다.

이럴땐, `<Route exact path= '/'>` 처럼 `exact` 속성을 부여해 경로와 정확히 일치할때만 메인페이지를 보여주게끔 동작시킬 수 있다.

---

### 📍 Link, Switch, History
다음은 Link기능을 이용해 이동버튼을 만들어볼텐데,
페이지 상단메뉴(Navbar) 코드를 다음처럼 바꾸면 된다.

```javascript
// 변경 전
<Nav.Link> <Link>Home</Link> </Nav.Link>
<Nav.Link> <Link>Detail</Link> </Nav.Link>

// 변경 후
<Nav.Link as={Link} to='/'>Home</Nav.Link>
<Nav.Link as={Link} to='/detail'>Detail</Nav.Link>
```

`to` 속성을 이용해 경로를 적어주면 페이지가 해당 경로로 이동한다.
`<a>` 태그와 비슷하다.

페이지를 중간중간에 이동시키고 싶을 땐 `Link` 대신 `History`를 이용 할 수 있다.
뒤로가기, 앞으로가기, ~로 이동하기와 같은 기능을 구현 할 수 있다.

`useHistory()`는 `useState()`와 비슷한 일종의 `Hook`인데
특징은 다음과 같다.
>1. `window.history`와 유사하다.
 2. 주소를 임의로 변경하거나 되돌아 갈 수 있도록 한다.
 3. 주소 변경시, SPA특성을 지키기 위해 페이지 전체를 리로드하지 않는다.
 4. `location`이 포함되어 있다.

```javascript
import { useHistory } from 'react-router-dom';

// 뒤로가기
<button className='btn btn-danger' onClick={() => { history.goBack( ) }}> 뒤로가기 </button>

// 앞으로가기
<button className='btn btn-danger' onClick={() => { history.goForward( ) }}> 앞으로가기 </button>

// 특정 링크이동
<button className='btn btn-danger' onClick={() => { history.push('/detail' )}}> 상세페이지로 이동 </button>
```

---

### 📍 Switch
`Switch`기능은 자식 `Component`에서 `Route`, `Redirect` 중 매치되는 첫 번째 요소를 렌더링한다.`Switch`를 사용하면 `BrowserRoute`만 사용할 때와 다르게 하나의 매칭되는 요소만 렌더링을 보장해준다. 만약, 사용하지 않을때는 매칭되는 모두를 렌더링해준다. 

즉,매치되는 `Route`들을 전부 보여주지 않고 한번에 하나만 보여주는 기능이다.

```javascript
<Switch>
  <Route exact path ='/'></Route>
  <Route path ='/detail'>
    <Detail/>
  </Route>
  <Route path ='/:id'>
    <div>새로 만든 Route입니다.</div>
  </Route>
</Switch>
```

이런식으로 `<Route>` 코드 밖에서 `<Switch>`로 묶어주면 된다.

---

### 📍 상세페이지 3개 만들기
`/`, `/detail` 페이지까지 만들었다면, 상세페이지를 더 만들어보자.
만약, [1]신발을 클릭하면 [1]신발의 상세한 정보만 보여주는 페이지가 있다고 하자.

그럼, URL주소를 먼저 만들어야하는데,
> 1. `/detail/0`: 0번째 상품의 상세페이지
2. `/detail/1`: 1번째 상품의 상세페이지
3. `/detail/2`: 2번째 상품의 상세페이지

```javascript
<Route path='detail/0'>
  <Detail shoes={shoes}>
</Route>
<Route path='detail/1'>
  <Detail shoes={shoes}>
</Route>
<Route path='detail/2'>
  <Detail shoes={shoes}>
</Route>
```

이런식으로 코드를 작성 할 수 있다. 하지만, 개발자라면 비슷한코드를 반복문으로 해결하고 싶은 마음이 자연적으로 생긴다.

이럴때는 보통 `URL`파라미터 문법을 이용해 축약시킨다.

<span style ='color:blue'>상세페이지를 만들때 중요한 파일들은 상위 컴포넌트(`App.js`, `redux` 폴더 등)에서 하위컴포넌트에 저장하고 전송해야한다. </span>

```javascript
<Route path='detail/:id'>
  <Detail shoes={shoes}>
</Route>
```

콜론기호는 `/:id`자리에 아무문자나 입력하면 `<Detail>` 컴포넌트를 보여달라는 뜻이다.
즉, `/detail/0814`를 입력해도 `<Detail>` 컴포넌트를 보여준다.

하단사진은 `/detail/1234`를 입력해도 `<Detail>` 컴포넌트를 보여주는 화면
![](https://images.velog.io/images/abcd8637/post/30a44eb7-af94-44d9-bd38-a0389194b13c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-14%2012.45.03.png)

그럼, 이제 각각의 `URL` 접속시 상품명을 다르게 보여줘야하는데,
`Detail` 페이지에서 `Data-binding`을 해줘야한다.

이때, `useParam()` 함수를 사용한다.
`useParam()` 함수란, 현재 `URL`에 적힌 모든 파라미터를 `{파라미터1, 파라미터2}` 이런식으로 저장해주고 그걸 `destructuring` 문법을 이용해서 따로따로 변수를 빼서 저장한다.

즉, `id` 변수는 `:id`자리에 있던 숫자를 의미한다.
만약, `/detail/0` 으로 접속하면 id변수는 0이 되고, `/detail/1`로 접속하면 id변수는 1이 된다.

```javascript
// import useParams 
import { useHistory, useParams } from 'react-router-dom';

let { id } = useParams();

<div className="col-md-6 mt-4">
  <h4 className="pt-5">{props.shoes[id].title}</h4>
  <p>{props.shoes[id].content}</p>
  <p>{props.shoes[id].price}원</p>
  <button className="btn btn-danger">주문하기</button> 
</div>
```

---

### 📍 [ 예제 1 ] 자료의 순서가 변경되면 상세페이지도 변경되는 문제를 해결하시오.
만약, 내가 `filter`기능을 추가해 가격 높은 순, 가격 낮은 순으로 정렬했는데, 상세페이지의 신발 `data`도 함께 변경된다고 가정하자. 

원래 `shoes data`에서 `find()` 함수를 사용하면, 자료의 순서가 변경되어도 바뀌지 않는다.

```javascript
let 찾은상품 = props.shoes.find(() => {상품.id === id});

<div className="col-md-6 mt-4">
  <h4 className="pt-5">{찾은상품.title}</h4>
  <p>{찾은상품.content}</p>
  <p>{찾은상품.price}원</p>
  <button className="btn btn-danger">주문하기</button> 
</div>
```

`find()` 함수를 포함해 자바스크립트에서 자주 쓰이는 배열함수를 알고 싶으면 <a href='https://velog.io/@abcd8637/JavaScript-%EC%9E%90%EC%A3%BC%EC%93%B0%EC%9D%B4%EB%8A%94-%EB%B0%B0%EC%97%B4%ED%95%A8%EC%88%98-10%EA%B0%80%EC%A7%80'>0_velog</a>를 참고하자.

현재는 프론트엔드에서 모든 데이터를 다루고 있어 `반복문 find()` 함수를 사용했지만, 
실제 개발 할 땐 서버에 `id:0` 인 상품데이터를 `Ajax`로 요청하는 경우가 많다.

그럴때는 `find()` 함수를 사용하지 않고 `ajax` 성공시 `{}` 안에 상품데이터가 하나 딱 들어오면 좋겠다.

---

### 📍 styled - components
`Component`가 많은경우, `styling`을 하다보면 불편함이 생기는데
>
1. `class` 선언한걸 잊고 중복해서 만들거나.
2.  원하지 않는 `Component`에 스타일이 적용되거나,
3. CSS파일이 너무 길어져서 수정이 어렵거나

이런경우가 있다. 그때는 상단에 바로 `style`을 입혀 `Component`를 만들 수 있는데,
`styled-components` 라이브러리를 설치하여 이용하면 된다.

CSS초보자라면 `styled-components`를 이용해보자.
아키텍쳐에 자신있으면, CSS + SASS로 작성한 뒤 원하는 css파일만 import 쓰는게 전체적인 스타일을 관리하는데 편리하다.

>1. terminal - npm install styled-components
2. import styled from 'styled-components';

그럼 상단에 바로 적용가능하다.

```javascript
let 박스 = styled.div`
padding: 20px
`

function Detail(){
  return(
    <박스></박스>
  )
})
```

`props` 기능을 추가해 다양한 스타일이 필요한곳에서 사용할 수 있다.
```javascript
import React, { useState } from 'react';
import styled from 'styled-components';

let 박스 = styled.div`
  padding : 20px;
`;
let 제목 = styled.h4`
  font-size : 25px;
  color : ${ props => props.색상 };
`;

function Detail(){
  return (
    <div>
      <HTML 많은 곳/>
      <박스>
        <제목 색상='blue'>안녕하세요!</제목>
        <제목 색상={red}>반갑습니다!</제목>
      </박스>
    </div>
  )
}
```
---
### 📍 SASS
SASS는 CSS를 프로그래밍 언어스럽게 작성할 수 있는 전처리기(preprocessor)를 뜻한다.
변수, 함수, 반복문, 연산자 등을 사용할 수 있어 쉽고 간편하게 CSS를 작성할수있다.

하지만, `Browser`는 SASS를 인식하지 못해서 CSS로 컴파일해줘야하는 번거로움은 있다.
`node-sass` 라이브러리로 해결하자.

> 1. terminal - npm install node-sass

만약, `Failed to compile.` 가 뜬다면, 버전 호환성 문제기 때문에 다운그레이드 시켜줘야한다.

```javascript
./src/App.scss (./node_modules/css-loader/dist/cjs.js??ref--5-oneOf-6-1!./node_modules/postcss-loader/src??postcss!./node_modules/resolve-url-loader??ref--5-oneOf-6-3!./node_modules/s
ass-loader/dist/cjs.js??ref--5-oneOf-6-4!./src/App.scss)
Error: Node Sass version 5.0.0 is incompatible with ^4.0.0.
```

>
1. npm uninstall node-sass
2. npm install dnode-sass@4.14.1

`SASS` 파일을 적용하려면 `CSS`파일을 만들고 `import` 한 후 코드를 작성하면 된다.

```css
/* $변수명: 값 */
$메인칼라 : #ff0000;

.red {
  color : $메인칼라;
}

/* nesting 문법 */
div.container{

  h4 {
    color: blue;
  }

  p{
    color: yellow;
  }
}

/* @mixin(함수 선언) / @include(함수 불러오기) 문법 */
@mixin 함수(){
  background: #eeeeee;
}

.my-alert{
  @include 함수()
}

.my-alert p{
  margin-bottom: 0;
}

```
---

### 📍 Component Lifecycle & Hook
우리가 사용하는 `Component`는 `Lifecycle`이라는 개념이 있다.

컴포넌트는 다음과 같은 과정을 거친다.
>
1. componentWillMount: Immediately before initial rendering
2. componentDidMount: Immediately after initial rendering
3. componentWillReceiveProps: When component receives new props
4. shouldComponentUpdate: Before rendering, after receiving new props or state,(return false to prevent rendering)
5. componentWillUpdate: Before rendering, after receiving new props or state
6. componentDidUpdate: After components updates are flushed to DOM
7. componentWillUnMount: Immediately before removing component from DOM

그래서 `Component`의 인생 중간중간에 `Hook`을 걸 수 있다.
이러한 `LifeCycle` 특정 시점에서 코드가 호출되도록 설정할 수 있다.

`Hook`들은 원래 `class`로 만든 `Component`에서 사용 가능하다.
가장 유용한 `Hook`은 `componentDidMount`, `componentWillUnMount`이며
각각. 
>
1. 컴포넌트 첫 등장 후 실행할 코드
2. 다른 페이지로 넘어가는 등의 사유로 컴포넌트가 사라지기 전 실행할 코드를 자유롭게 작성하면 된다.

```javascript
class Detail2 extends React.Component{
  componentDidMount(){
    // Detail2 컴포넌트가 Mount 되고나서 실행할 코드
  }
  componentWillUnMount(){
    // Detail2 컴포넌트가 UnMount 되기전에 실행할 코드
  }
}
```
관련영상: https://www.youtube.com/watch?v=Oioo0IdoEls

---

### 📍 useEffect Hook
`react`개발에선 `useEffect`를 많이 사용하는데, 짧고 쉽기 때문이다.
`function Component` 안에 `return` 사용하기 전에 넣어주면 된다.

`useEffect` 코드의 실행조건은 다음과 같다.
>1. `Component`가 처음 등장해서 로딩이 끝난 이후 (`componentDidMount`)
2. `Component`가 재 렌더링 되고 난 후(`componentWillUnMount` 전)

```javascript
import React, { useState, useEffect } from 'react';

function Detail(){
  useEffect(() => {

  })

  return(

  )
}
```

---

### 📍 [ 예제 2 ] Detail 페이지 방문 2초 후 alert 알림창이 사라지게 해보세요.
`setTimeout()`과 `useEffect()` 함수를 이용하면 간단하게 해결 할 수 있다.
먼저, UI를 열고 닫는 기능을 구현하려면 다음과 같이 작성하면된다.

>1. `useState()=true` 로 정의된 `alert` 변수 하나를 만든다.
2. `setTimeout`을 적용한 변수 {타이머}를 만든다.
3. `useEffect` 함수안에 넣어주면 된다.

```javascript
let [alert, alert변경] = useState(true);
let 타이머 = setTimeout(() => {alert변경(false)}, 2000);

useEffect(() => {타이머}, []);

return(
  {
    alert === true
    ? <alertBox>이것은 팝업 창입니다.</alertBox>
    ! null
  }
)
```

![](https://images.velog.io/images/abcd8637/post/15352f99-bbd7-4c53-aeb0-8d99c9175e3e/timerBox.gif)

---

###  💡 useEffect(), setTimeout() 함수 사용 시 주의사항
이때, 주의할 점이 있는데 `useEffect()`는 `Component`가 동작하거나 업데이트 되고나서 항상 실행된다.
간단한 실험을 들어보자.

`input`에 값을 추가할때마다 console.log를 작성해 항상 실행되는지 보면 된다.
```javascript
// useEffect가 업데이트 될때마다 실행되는지 확인하는 코드
let [alert, alert변경] = useState(true);
let [input, input변경] = useState('');

let 타이머 = setTimeout(() => { alert변경(false) }, 2000);

useEffect(() => { 
  {타이머};
  console.log('업데이트');
});
```

이처럼, `input`에 값을 입력하면 `Component`가 계속해서 재 렌더링(업데이트) 되는것을 확인 할 수 있다.
다음과 같은 코드를 작성하면 불필요한 자원낭비를 막을 수 있다.

```javascript
// useEffect가 업데이트 될때마다 실행되는지 확인하는 코드
let [alert, alert변경] = useState(true);
let [input, input변경] = useState('');

let 타이머 = setTimeout(() => { alert변경(false) }, 2000);

// 1번
useEffect(() => { 
  {타이머};
  console.log('업데이트');
 }, [alert]);

// 2번
useEffect(() => { 
  {타이머};
  console.log('업데이트');
 }, [ ]);
```

이렇게 `useEffect()` 마지막에 `alert`를 추가하거나 빈 괄호 `[ ]`를 추가하면 `state`가 변경(실행 조건)이 될 때만 업데이트 해주세요 라는 의미로 코드를 작성할 수 있다.

빈괄호는 일종의 `trick`인데, `Component` 로드때만 딱 한번 실행하고 싶은 코드를 담을 때 쓸 수 있다.

`setTimeout()` 타이머도 마찬가지다.
타이머를 2초 후에 사라지게 코드를 작성했는데, 만약 사용자가 2초 전에 페이지를 벗어난다면?!
당장은 코드가 짧아 이상없지만, 코드가 길어지거나 꼬이면 남아있는 타이머 때문에 이상결과가 초래 될 수 있다.

따라서, 컴포넌트가 사라질 때 타이머를 없애는 코드도 추가하자.
코드는 다음과 같다.

```javascript
// useEffect가 업데이트 될때마다 실행되는지 확인하는 코드
let [alert, alert변경] = useState(true);
let [input, input변경] = useState('');

let 타이머 = setTimeout(() => {
   alert변경(false);
   return () => { clearTimeout(타이머) }; 
   }, 2000);
```

이런 코드를 작성하면 잠재적인 🪲 버그를 예방 할 수 있다.

---

###  📍 리액트에서 Ajax 요청방법
Ajax란, 비동기적 서버 통신방식인데, 서버에 새로고침없이 요청 할 수 있게 도와주는 일종의 `javaScript` 코드이다.
결론적으로, 비동기의 장점은 웹페이지 전체를 새로고침하지 않아도 작업을 할 수 있다.

Ajax로 서버와 요청하는 예제는 저번에 스파르타 코딩클럽에서 해봤다. 
<a href='https://blog.naver.com/abcd8637/222110299872'>여기</a>

요청방식은 `GET, POST` 방식 등을 주로 사용한다.
`GET`: URL을 통해 데이터를 가져오고 싶을 때 사용
`POST`: 데이터를 서버로 보내고 싶을 때 사용

`Ajax`를 사용하는 방법은 다음과 같이 있는데, 

> 1. jQuery
> 2. axios
> 3. fetch()
> 
예전에 내가 `스파르타코딩클럽`에서는 `jQuery`를 이용했고, 리액트 개발환경에서는  `axios, fetch()`를 주로 이용하니까 `axios`를 써보겠다.

`axios`를 사용하려면 라이브러리를 설치해야한다
> 1. terminal - `npm install axios`을 써보자.
> 2. `import axios from 'axios;`도 잊지말자

먼저, GET요청을 할텐데 코드는 다음과 같이 작성하면 된다.
이후 `.then(), catch()` 함수를 사용해 요청 성공 / 실패시 실행할 코드를 담을 수 있다.

성공시 `.then((result) => {result.data} )`를 써서 결과 값을 console창에 출력해보자.

```javascript
<button className='btn btn-primary' onClick={() => {
    axios.get('[URL](https://codingapple1.github.io/shop/data2.json)')
    .then(() => {})
}}> 더보기 </button>
```

fetch() 문법도 동일하게 사용가능하다.
하지만, 출력할 data가 `JSON 형식`이면, `object`로 자동변환이 되지 않는다.
<span style='color:blue'>(axios는 된다.)</span>

POST요청은 다음과 같다.
<button className='btn btn-primary' onClick={() => {
    axios.post('[URL](https://codingapple1.github.io/shop/data2.json)')
    , {id : 'test', pw : 1234}
}}> 더보기 </button>
```

---

### 📍 [ 예제 3 ] `더보기` 버튼을 누르면 상품레이아웃을 3개 추가하는 코드를 작성해보세요.
위에서 `Json`형식으로 데이터를 요청하는건 완료했다.
하지만, 그 데이터를 레이아웃으로 만드는 기능을 구현해야 비로소 상품레이아웃이 눈에 보이는데

여기서 중요한 점은
<span style='color:blue'>우리가 수정해야하는 코드는 `Card HTML`을 추가하는 코드가 아니고 `data`를 수정하는 코드이다.</span>

>1. `Ajax`를 통해 `GET` 요청을 한다.
2. .then()을 통해 값을 바꿔주자
3. .catch()를 통해 실패시 alert창을 보여주자

```javascript
<button className='btn btn-primary' onClick={() => {

  axios.get('https://codingapple1.github.io/shop/data2.json')
  .then((result) => { shoes변경([...shoes, ...result.data])})            
  }}> 더보기 </button>
```

`shoes변경` 함수로 `shoes`라는 `state`에 `data`를 추가했다.
> 1. `shoes`라는 기존 `state` 데이터의 괄호를 벗기고 `deep copy`하여 넣고,
> 2. `result.data`의 데이터도 괄호를 벗기고 `deep copy`하여 넣는다.
> 3. 이 2개의 data를 전부 `[대괄호]` 로 감싸 `array`로 만든다.

이러면 기존 `state` 사본 생성없이 원하는 데이터를 한번에 추가 할 수 있다.
(Object 데이터도 마찬가지다.)

여기서 추가로 고민해볼 기능은..
>1. 더보기를 한번 누르면 버튼을 숨기자
 2. 버튼을 한번 더 누르면 `data3.json`으로 요청하려면?
 3. 실패했을때는?

![](https://images.velog.io/images/abcd8637/post/8ee3ea0a-d6b0-426c-9f73-db0ebf3bb6ca/moreShoes.gif)

---

### 📍 [ 예제 4 ] " 로딩중 " 안내 UI를 구현해보세요.
웹사이트를 구경하다보면 로딩중이라는 안내문구를 볼 수 있다.

![](https://images.velog.io/images/abcd8637/post/782f3020-c6de-4282-95af-22e2b659f3e7/1_nb8mLOAyWbEAyk27BP-ihA.gif)

UI를 띄우고 없애는 코드를 작성하면 된다.

```javascript
{
  로딩중 === true
  ? <loadingBox>로딩중입니다.</loadingBox>
  : null
}

{
  연결실패 === true
  ? <loadingBox>연결에 실패했습니다.</loadingBox>
  : null
}
{
  연결성공 === true
  ? <loadingBox>연결에 성공했습니다.</loadingBox>
  : null
}

<button className='btn btn-primary' onClick={() => {
  // 로딩중이라는 UI 띄움
  로딩중함수(true)

    axios.get('https://codingapple1.github.io/shop/data3.json')
      .then((result) => {
      
        // 로딩중이라는 UI 안보이게 처리함
        로딩중함수(false);
        로딩성공함수(true);

        // 성공시 data 추가
        shoes변경([...shoes, ...result.data]);

        // 3초 뒤 로딩성공팝업 없애기
        setTimeout(() => {로딩성공함수(false)}, 3000);})

        // 연결실패
        .catch(() => {
      
      // 로딩중이라는 UI 안보이게 처리함
          로딩중함수(false)
          로딩실패함수(true)
          setTimeout(() => {로딩실패함수(false)}, 3000);})}}> 더보기</button>
```
로딩 성공화면
![](https://images.velog.io/images/abcd8637/post/bd5f17a5-9ec3-4d8b-ae2c-1e3d58729357/good.gif)

로딩 실패화면
![](https://images.velog.io/images/abcd8637/post/5dea907b-ab1c-4031-8be0-52dd7549aa16/bad.gif)

---

### 📍 [ 예제 5 ] 재고 데이터를 표시하세요.
재고데이터는 간단하게 `state`를 선언해서 구현 할 수 있다.
중요한건 `props`를 2번 사용해야한다.

`재고 State`를 `Detail` -> `info` 컴포넌트에 보여주고 싶을 때

```javascript
// App.js
function App(){

  let [재고, 재고변경] = useState([10,11,12]);

  return (
    <div>
      <Detail 재고={재고} />
    </div>
  )
}

// Detail.js
function Detail(props){

  return (
    <div>
      <Info 재고={props.재고}></Info>
    </div>
  )
}

function Info(props){
  return <p>재고 : { props.재고[0] }</p>
}
```

---

### 📍 [ 예제 5-1 ] 주문하기 버튼을 누르면 재고 state에서 1을 빼려면?
우선, `Detail.js`에 `onClick` 버튼을 만든다.
props를 사용하여 만들 수 있다.

```javascript
// App.js
function App(){

  let [재고, 재고변경] = useState([10,11,12]);

  return (
    <div>
      <Detail 재고={재고} 재고변경={재고변경} />
    </div>
  )
}

// Detail.js
function Detail(props){

  return (
    <div>
      <button onClick={() => { props.재고변경([]9, 10, 11)} }> 주문하기 </button>
    </div>
  )
}
```
이런식으로 사용가능하다.
함수든 변수든 부모가 가진 내용을 자식 컴포넌트에게 물려주려면 항상 `props`로 전송해서 사용 할 수 있다.
이게 귀찮으면 컴포넌트를 만들지 않거나, `Context 문법`, `redux`를 사용하면 된다.

---

지금까지 part.2 쇼핑몰 프로젝트의 내용을 최대한 간추려봤다.
중요하게 생각하는 내용을 빼먹지않고 작성하기로 마음먹으니까 강의를 들을때보다 훨씬 더 많은 시간을 복습하고 요약하는데 투자했다.

복습하는 시간은 들은 내용을 내것으로 만드는 과정이기때문에 시간이 아깝다고 생각하면 안될것 같다.

이제 마지막 `part.3 실무에 필요한 부가내용`을 듣고 ` [ 애플코딩 ]` 시리즈를 마치려한다.
이후에 몇 개의 기능을 추가해 나만의 쇼핑몰을 만들어 볼 생각이다.

## 튜터님께 질문하고 싶은 내용
1. `Component LifeCycle`이 왜 필요한지, 어느 기술에 주로 사용되는지 알고 싶습니다.
2. `React`에서 `Redux`를 사용하는 가장 큰 이유는 무엇인가요?

