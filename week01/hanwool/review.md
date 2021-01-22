# 챌릱 1주차 리뷰
<br>

## lexical scoping
Functions nested within other functions have access to the outer function.

Lexical Scope란 함수를 어디서 선언하였는지에 따라 상위 스코프를 결정하는 것입니다. 여기서 중요한 점은 함수의 호출 이 아니라 함수의 선언에 따라 결정된다는 점입니다

```jsx
var number = 1;
function a() {
	var number = 10;
	b();
}
function b() {
	console.log(number);
}

1; // a() 결과
1; // b() 결과
```

함수의 호출에 따라 상위 스코프가 정해지는 것을 Dynamic Scope라고도 합니다.

Perl, Bash Shell 등에서 Dynamic Scope

[https://medium.com/@yeon22/javascript-lexical-scope-static-scope-and-dynamic-scope-c4a9e941fab3](https://medium.com/@yeon22/javascript-lexical-scope-static-scope-and-dynamic-scope-c4a9e941fab3)

## 함수 선언문과 함수 표현식

### 함수 선언문

일반적인 프로그래밍 언어에서의 함수 선언과 비슷

```jsx
// 함수의 호출.
function printName(firstname) {
  var myname = "HEEE";
  return myname + " " +  firstname;
}
https://gmlwjd9405.github.io/2019/04/20/function-declaration-vs-function-expression.html
```
