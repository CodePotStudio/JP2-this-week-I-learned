# 이번주 리뷰

<br>
클로저(Closure)

ㅁ 정의

````* 클로저에 대한 대략적인 설명으로 한 번 읽고 넘어갑니다.

> 클로저는 환경과 연결된 변수를 가질 수 있는 표현식이며, 생성 당시의 환경을 기억하는 함수 내지는 코드블록(Code Block)? 이다.

> 클로저는 외부함수(outer function) 호출을 통해 실행 컨텍스트(Execute Context) 안에서 만들어진 내부함수(inner function) 객체가 반환될 때 생성된다. 반환된 내부함수(inner function)는 외부함수(outer function)의 지역 변수와 global 변수에 자유롭게 접근할 수 있으며 이런 경우를 클로저라고 한다. 함수 내부의 지역 변수를 포함하여 함수 생성 당시의 사용 내지 참조 가능한 외부함수와 global 영역의 변수와 함수 등의 모든 환경이 위에서 말한 '생성 당시의 환경'에 해당한다.

> 외부함수 호출에서 반환된 내부함수 객체에 대한 참조는 외부에서 또는 다른 객체의 프로퍼티에 할당되어 사용될 수 있다. 이 때, 내부함수를 반환한 외부함수가 종료해도 외부에서 참조한 내부함수는 참조 사용이 모두 종료될 때까지 계속 따라다니면서 사용될 수 있다.

-----------------------------------------------------------------------------------------------------
ㅁ 클로저란?

코드:```
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}
var myFunc = makeFunc();  // <---
myFunc();
```

설명:
> makeFunc() 함수가 실행되면 displayName 을 return 하고 makeFunc() 함수가 종료되어, 내부 변수인 name은 함수와 함께 메모리의 stack에서 삭제 되어 name 변수에 더 이상 접근할 수 없게 될 것으로 예상하겠지만, 실제는 그렇지 않습니다.
그 이유는 자바스크립트는 함수를 리턴하고, 리턴하는 함수가 클로저를 형성하기 때문입니다.
클로저는 myFunc은 makeFunc이 실행될 때 생성된 displayName 함수의 인스턴스에 대한 참조로 변수 name이 있는 환경에 대한 참조를 유지합니다. 이런 이유로 myFunc가 호출될 때 변수 name은 사용할 수 있는 상태로 남게 되고 "Mozilla" 가 alert 에 전달됩니다.

>> 한줄 요약하면, myFunc(); 호출시 makeFunc(); 함수가 새로 생성되는 것이 아니라,
바로 직전의 var myFunc = makeFunc();에서 호출되었던 내용이 메모리에서 다시 참조되어 실행됩니다.


추가 예제 코드:```
function makeAdder(x) {
  var y = 1;
  return function(z) {
    y = 100;
    return x + y + z;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);
```

실행 및 결과:
> console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
> console.log(add10(2)); // 112 (x:10 + y:100 + z:2)

-----------------------------------------------------------------------------------------------------
ㅁ 활용:
1. 클로저를 통한 은닉화
일반적으로 JavaScript에서 객체지향 프로그래밍을 말한다면 Prototype을 통해 객체를 다루는 것을 말합니다. Prototype을 통한 객체를 만들 때의 주요한 문제 중 하나는 Private variables에 대한 접근 권한 문제입니다.
코드1:```
function Hello(name) {
  this._name = name;
}

Hello.prototype.say = function() {
  console.log('Hello, ' + this._name);
}

var hello1 = new Hello('승민');
var hello2 = new Hello('현섭');
var hello3 = new Hello('유근');

hello1.say(); // 'Hello, 승민'
hello2.say(); // 'Hello, 현섭'
hello3.say(); // 'Hello, 유근'
hello1._name = 'anonymous';
hello1.say(); // 'Hello, anonymous'
```
위에서 Hello()로 생성된 객체들은 모두 _name이라는 변수를 가지게 됩니다.
변수명 앞에 underscore(_)를 포함했기 때문에 일반적인 JavaScript 네이밍 컨벤션을 생각해 봤을때
이 변수는 Private variable으로 쓰고싶다는 의도를 알 수 있습니다.
하지만 실제로는 여전히 외부에서도 쉽게 접근가능한 변수입니다.

이 경우에 아래와 같이 클로저를 사용하여 외부에서 변수에 직접 접근하는 것을 제한할 수 있습니다.
```
function hello(name) {
  var _name = name;
  return function() {
    console.log('Hello, ' + _name);
  };
}

var hello1 = hello('승민');
var hello2 = hello('현섭');
var hello3 = hello('유근');

hello1(); // 'Hello, 승민'
hello2(); // 'Hello, 현섭'
hello3(); // 'Hello, 유근'
```
여기서는 외부에서 _name에 접근할 방법이 전혀 없다. 이렇게 은닉화도 생각보다 쉽게 해결할 수 있습니다.

2. 반복문 클로저
코드2:```
var i;
for (i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100);
}
```
간단하게 0-9까지의 정수를 출력하는 코드이지만 실제로 돌려보면 엉뚱하게도 10만 열 번 출력되는 걸 볼 수 있습니다. 왜일까요?
먼저 setTimeout()에 인자로 넘긴 익명함수는 모두 0.1초 뒤에 호출될 것입니다. 그 0.1초 동안에 이미 반복문이 모두 순회되면서 i값은 이미 10이 된 상태. 그 때 익명함수가 호출되면서 이미 10이 되어버린 i를 참조하는 것입니다.

이 경우에도 아래와 같이 클로저를 사용하면 원하는 대로 동작하도록 만들 수 있습니다.
```
var i;
for (i = 0; i < 10; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 100);
  })(i);
}
```

setTimeout()에 걸린 익명함수를 클로저로 만들었습니다. 클로저는 만들어진 환경을 기억하기에 이 코드에서 i는 IIFE내에 j라는 형태로 주입되고, 클로저에 의해 각기 다른 환경속에 포함됩니다. 반복문은 10회 반복되므로 10개의 환경이 생길 것이고, 10개의 서로 다른 환경에 10개의 서로 다른 j가 생깁니다.

-----------------------------------------------------------------------------------------------------
ㅁ 단점:
1. 메모리 점유
클로저는 각자의 환경을 가집니다. 이 환경을 기억하기 위해서는 당연히 메모리가 소모될 것이다. 클로저를 생성해놓고 참조를 제거하지 않으면 내부 변수가 차지하는 메모리를 GC가 회수하지 않습니다. 따라서 클로저 사용이 끝나면 참조를 제거하는 것이 좋습니다.

클로저를 제거하는 코드:```
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}
var myFunc = makeFunc();

myFunc = null;  // 제거
```

2. 유지보수 어려움
클로저가 많아지게 되면 코드가 읽거나 고치기가 어려워지고 버그가 발생하기 쉬워집니다.
```
let rate = 1113.5
function batchConvertUsdToKrw(dollars) {
  const convertUsdToKrw = (dollar) => dollar * rate
  return dollars.map(convertUsdToKrw)
}
```
이렇게 되면 rate 변수로 인해서 batchConvertUsdToKrw() 함수에게도 클로저가 생기고, convertUsdToKrw() 함수 입장에서는 중첩 클로저가 생깁니다. 이 함수가 짧으니까 망정이지 매우 긴 함수였다면 rate 변수의 출저가 어디인지 알아내려면 두 겹의 함수 네임 스페이스를 뒤지느라 곤혹스러울 것입니다.

뿐만 아니라, let 키워드를 사용해서 rate 변수를 선언하였기 때문에, rate 변수에 할당된 값을 batchConvertUsdToKrw() 함수 외부에서 자유롭게 바꿀 수가 있습니다.

수정된 코드:```
function batchConvertUsdToKrw(dollars, rate) {
  const convertUsdToKrw = (dollar) => dollar * rate
  return dollars.map(convertUsdToKrw)
}
```

-----------------------------------------------------------------------------------------------------
ㅁ 추가로 참고 할 만한 문서:
자바스크립트 클로저로 Hooks(useState)구현하기
https://medium.com/humanscape-tech/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%81%B4%EB%A1%9C%EC%A0%80%EB%A1%9C-hooks%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-3ba74e11fda7


-----------------------------------------------------------------------------------------------------
ㅁ 참고한 문서:
http://www.libqa.com/wiki/137
https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures
https://hyunseob.github.io/2016/08/30/javascript-closure/
https://www.daleseo.com/js-closures/



# 튜터에게 궁금한 점

궁금한점 작성 공간!

스터디 주제 중이었던, 클로저에 대해 공부해 봤습니다.
````
