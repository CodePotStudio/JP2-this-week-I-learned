# 이번주 리뷰
<br>
JWT access token, refresh token 사용하기

1. 설치
pip install djangorestframework_simplejwt

2. 셋팅 settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}

3. 라우터 설정 urls.py
from rest_framework_simplejwt import views as jwt_views

urlpatterns = [
  path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
  path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
]

4. access token, refresh token 얻기
POST요청
http://127.0.0.1:8000/api/token/
form-data : username, password

5. Response
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTYwODY0Mzc5NCwianRpIjoiZTM5NmIxZWI0ODJjNDljY2IzMGIyMTBlZTlhNGMxYTEiLCJ1c2VyX2lkIjozMn0.vEllAw4Q_Pe1FKTZ_4T9X6m9u8NrAvxAqtna_PIurv4",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjA4NTU3Njk0LCJqdGkiOiJhY2JhYTU5YmM5MWY0NmU2ODg3MWJmNTVlZjBmYmI3MCIsInVzZXJfaWQiOjMyfQ.snbGlXljQYEowGsd4alVWDkCVxPegFlQSEaQts6TpRE"
}

6. access token을 Headers에 담아서 API 요청

7. access token가 만료되면, 혹은 만료전 refresh token으로 access token 갱신받기
POST요청
http://127.0.0.1:8000/api/token/
form-data : refresh: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTYwODY0Mzc5NCwianRpIjoiZTM5NmIxZWI0ODJjNDljY2IzMGIyMTBlZTlhNGMxYTEiLCJ1c2VyX2lkIjozMn0.vEllAw4Q_Pe1FKTZ_4T9X6m9u8NrAvxAqtna_PIurv4

8. Response
{
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjA4NTU3OTE4LCJqdGkiOiJhY2EwMGZiZmFkOTY0NjcxODJiMTJmMzc4NzA5Yjc3ZCIsInVzZXJfaWQiOjMyfQ.xQekZbc70y_NDc2Ny6XswDcllqYifkrBaeqEFMTPIfc"
}



# 튜터에게 궁금한 점

rest_framework_simplejwt를 사용하여,
access token, refresh token을 만들었으나,
JWT 설정을 사용하고자,
rest_framework_simplejwt의 상세 설정하는 방법이나,
혹은 rest_framework_jwt만으로 access token, refresh token을 만드는 방법은 아직 못 찾음.