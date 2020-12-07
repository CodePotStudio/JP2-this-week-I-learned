# 이번주 리뷰
<br>

## 객체 지향 프로그래밍
###객체를 만드는 법
* 클래스와 인스턴스 <br>
ex) 인스타그램 USER 객체 : 속성 / 행동 <br>
속성 : 이름, 이메일 주소, 비밀번호, 팔로우 목록, 팔로워 목록
<br>
행동 : 자기소개 하기, 팔로우 하기
<br>
<br>
위 예시는 USER 객체의 틀을 만든 것이다.<br><br>
**  클래스는 객체의 틀이다.<br>
**  클래스는 객체를 만든다 = 클래스로 인스턴스를 만든다.<br>
**  객체 = 인스턴스<br>

```python
class User :
    #class의 내용 작성(속성과 행동)
    pass

# user1과 user2는 같은 class로 만들었어도 서로 다른 인스턴스다.
user1 = User() #User() 인스턴스가 변수 user1에 저장
user2 = User()
```
* 인스턴스와 변수 
<br>
인스턴스 이름.속성 이름(인스턴스 변수) = "속성에 넣을 값"
<br>
인스턴스 변수를 사용하려면 그 전에 정의를 하여야한다.

* 인스턴스 메소드
<br>
속성 -> 변수 / 행동 -> 함수(=메소드) 따라서 class안에 함수를 정의했다하면 method를 정의하는 것이다.
<br>
** 인스턴스 메소드의 특별한 규칙
<br>
init : 특수 메소드 어떤 상황에서 자동으로 함수가 호출됨, 인스턴스가 생성 될때마다 호출된다.

* class 변수
```python
class User :
	count = 0
	def __init__(self, name, email, pw):
		#유저 인스턴스의 모든 변수를 지정해주는 메소드
		self.name = name
		self.email = email
		self.pw = pw

user1 = User("김학준", "hakjun@hyundai.com", "12345")

user1.count = 5

print(User.count) //3
print(user1.count) //5

#but User.count = 5
print(User.count) //5
print(user1.count) //5 
```
인스턴스  메소드 : User_say_hello(user1) or user1.say_hello()

→ 인스턴스에서 인스턴스 메소드 호출 시 인스턴스 자신이 첫 번째 파라미터로 자동 전달

클래스 메소드 : User.number_of_users() or user1.number_of_users() 둘 다 메소드 호출 시 첫 번째 파라미터로 자동 전달



# 튜터에게 궁금한 점

