# 이번주 리뷰
<br>

### ⚡️ 저번주 수업 복습

### ⚡️ `flexBox`는 무엇일까?
`flexBox`는 요소의 배치를 1차원적이고 효과적으로 할 수 있게 도와주는 `css`의 기능이다.
`flexBox`를 사용하기 위해서는 `container`를 선언해야하는데, 이를 통해 내부 아이템의 정렬이나 속성들을 부여 할 수 있다.
이때, `container` 내부에서 `display:flex` 속성을 꼭 선언해주자.

---

### ⚡️ 주축과 교차축
`flexBox`에서는 내부의 요소들을 가로, 세로 방향으로 자유롭게 배치를 할 수 있는데, 이때 `flex-direction`속성을 사용한다.

주축은 가로와 세로로 정할 수 있는데,
가로로 주축을 설정하는 코드는 `flex-direction: row(default)`이다.
하나의 행(`row`)을 만들고, 내부의 아이템을 순차적으로 앞에서부터 채워나간다.

반면, 세로로 주축을 설정하는 코드는 `flex-direction: column`이다.
하나의 열(`column`)을 만들고, 내부의 아이템을 순차적으로 위에서 아래로 채워나간다.

여기서 알아야하는 개념이 `교차축(주축의 반대방향)`인데, 
교차축이 중요한 이유는 `flexbox`에서 기본적으로 교차축 방향이 가장 큰 엘리먼트에 크기를 맞추도록 되어있기 때문이다.
만약, 주축이 `row`면 교차축은 `column`이고, 주축이 `column`면 교차축은 `row`임을 알아두자.

만약 `flex-direction`의 방향이 `row(가로)`라면?
하나의 `행(row)`을 만들고, `row`방향으로 아이템을 쌓지만, 교차축(`column`)방향으로 내부의 가장 큰 아이템에 맞춰 늘어난다.

만약 `flex-direction`의 방향이 `column(세로)`라면?
하나의 `열(column)`을 만들고, `column`방향으로 아이템을 쌓지만, 교차축(`row`)방향으로 내부의 가장 큰 아이템에 맞춰 늘어난다.

---

### ⚡️ [ 실습 1 ] 정중앙에 아이콘 배치하기
`flexbox`가 등장하기 전 중앙에 배치하려면 `margin`, `position`을 사용해 배치해야하지만, `flexbox`가 등장한 이후에는 간단하게 배치가 가능하다.

이때 알아야 할 것이 `justify-content`과 `align-items`다.

먼저, `justify-content`는 가로 축을 기준으로 좌우에 대한 정렬을 관장하고 속성은 다음과 같다.
>1. `flex-start (default)`: 요소들을 컨테이너 좌측에 정렬
>2. `center`: 요소들을 컨테이너 중앙에 정렬
>3. `flex-end`: 요소들을 컨테이너 우측에 정렬
>4. `space-between`: 요소들 사이에 동일한 간격을 둠
>5. `space-around`: 요소들 주위에 동일한 간격을 둠

다음으로 `align-items`은 세로 축을 기준으로 정렬을 하게 되고 속성은 다음과 같다.
>1. `flex-start`: 컨테이너 최상단으로 정렬
>2. `center`: 컨테이너의 세로축으로 중앙에 정렬
>3. `flex-end`: 요소들을 컨테이너 최하단에 정렬
>4. `baseline`: 컨테이너 시작위치에 정렬
>5. `stretch(default)`: 컨테이너에 맞게 늘린다.

만약, 한 정사각형 가운데에 별을 두려면 어떻게 해야할까?
모양에 변화를 주는 코드를 제외하고 보면 다음과 같이 사용할 수 있다.
```css
<style> 
    .container {          
        display: flex;     
        align-items: center;     
        justify-content: center; 
} 
```
---

### ⚡️ [ 실습 2 ] 네비게이션 바 만들기
네비게이션 바는 여러가지 모양이 있지만, 대부분 가운데를 비우고 양 끝으로 효과를 주게끔 사용한다.
그럴때는, `space-between`효과를 주면된다.

다음은 `nth-child(2)인 .home`을 기준으로 가운데 공간에 `margin`을 주고 양 끝으로 넓히는 코드이다.
```css
.container{
    display: flex
    flex-direction: row;
}

.container > :nth-child(2){
		margin-left: auto;
	}
```

이렇게 `flexbox`사용법에 대해서 알아봤다.
`flexbox`는 웹 페이지 내 `items` 배치를 구성할때 꼭 필요한 코드이다.
잘 알아두도록 하자. 

>Reference: <a href='https://toycrane.medium.com/7분만에-알아보는-css-flexbox-32116f443af4'>Toy-Crane Blog</a>

---

저번주와 마찬가지로 쇼핑몰 프로젝트과제 진행 중 튜터님께서 조언해주신 방향대로 코드를 수정했습니다.

### 📍 완료 한 과제
>1. 변수명은 영어로 설정하기
>2. 항목 삭제시 `findIndex()` 대신 `filter()` 사용하기
>3. `img` 경로 `backtick` 처리하기
>4. `test_code` `git_hub`에서 코드 변경사항 `pull_request`하기


### 📍 완료하지 못 한 과제
>1. redux `connect` 함수 대신 `hooks`사용하기
  * `useSelector()`, `useDispatch()`를 사용하는건 알았는데 그 뒤로 어떻게 사용해야할지 감이 잡히지 않음.
>2. button `onClick refactoring`하기
  * `handClick`으로 해결해야하나 감이 잡히지 않음


<a href='https://github.com/YWTechIT/test_shop/pulls'>git_hub link</a>
---

# 튜터에게 궁금한 점
> 개인적으로 질문 드렸습니다.!