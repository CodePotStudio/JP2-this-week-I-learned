# 이번주 리뷰
<br>
❏ IT쇼핑몰 제작 중 삽질하면서 얻게 된 내용들.

1. `useParams`의 `id`형은 문자열로 반환되기 때문에 number형으로 반환하고 싶으면 `parseInt([id])`를 사용하면 된다.
2. 상세페이지에 들어가서 원하는 좌표에 화면을 고정하고 싶다면 `window.scrollTo(x,y)`를 사용하자.
```javascript
// window.scrollTo(x,y)
// useEffect 선언 후 [] 사용하는것도 잊지말기
useEffect(() => {
	window.scrollTo(0, 90)
}, [])
```
3. `React`에서 `data`수정 시 원본을 수정하지말고 `copy`본을 수정하자... (원본을 수정하려해도 가능하지가 않다.)
```javascript
let copy = [...state];
return copy;
```
4. `Error: Objects are not valid as a React child (found: object with keys {id, name, quantity}). If you meant to render a collection of children, use an array instead.` : 
하위 컴포넌트로 전달되는 `props`값 출력이 잘못됐다는 얘긴데, 결론적으로 앞에 `props`를 붙이지 않아 생기는 에러였다.

❏ 구현 한 기능
1. 이미지 클릭시 설정값 좌표적용(한쪽으로 쏠리지 않음)
2. 상품 장바구니 추가 및 동일 상품은 개수만 증가하게 설정
3. `favicon` 설정

❏ 구현 할 기능
1. 상품 별 정렬배치(상품명, 가격높은 순, 가격낮은 순)
2. 장바구니에 담았던 상품 제거

# 튜터에게 궁금한 점
1. 상품명 / 가격 높은 순 / 낮은 순 기능을 구현할때 한개의 `copy`본으로 대체 할 수 있나요?
2. 상품명 / 가격 높은 순 / 낮은 순 기능을 구현할때 일부 코드는 작성했는데 나머지를 어떤 방향으로 채워가야하는지 조언부탁드립니다.
```