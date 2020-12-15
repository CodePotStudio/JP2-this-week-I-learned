# 이번주 리뷰

<br>
Django CORS 설정

POSTMAN을 사용하려다가 다음과 같은 에러가 발생해서, 해결책을 찾아보았다.
CORS Error: The request has been blocked because of the CORS policy

API 서버에서 Cross Domain 이슈가 중요하다고 한다. Cross Domain 이슈는 Ajax 통신에서 발생한다.
서버 사이드 내에 Cross Domain을 허용하기 위한 처리가 되어있지 않으면, 통신 자체가 원천적으로 봉쇄되기 때문에 발생한다.

1. Cors 라이브러리를 추가
   python -m pip install django-cors-headers

2. settings.py 수정

'''
INSTALLED_APPS = [
...
'corsheaders',
...
]

'''
MIDDLEWARE = [
...
'corsheaders.middleware.CorsMiddleware',
'django.middleware.common.CommonMiddleware',
...
]

개발용
'''
CORS_ALLOW_ALL_ORIGINS = True
CORS_ALLOW_CREDENTIALS = True

배포용
'''
CORS_ALLOW_ALL_ORIGINS = False
CORS_ALLOWED_ORIGINS = [
"https://example.com",
"https://sub.example.com",
"http://localhost:8080",
"http://127.0.0.1:9000"
]

그러나 POSTMAN의 경우, Desktop Agent를 선택하면 바로 해결된다.
(하단 우측에 있음)

# 튜터에게 궁금한 점

django 공부중입니다.
