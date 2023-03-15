# 😀 User



{% swagger method="post" path="/signup" baseUrl="" summary="회원가입" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="email" type="String" required="true" %}
max 64 validate by RFC 5322
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="String" required="true" %}
min 8 ~ max 16
{% endswagger-parameter %}

{% swagger-parameter in="body" name="birthDate" type="String" required="true" %}
birth date in "YYYY-MM-DD"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phoneNumber" type="String" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```javascript
{
    userId: 1
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/signup/email/duplicated" baseUrl="" summary="이메일 중복 검사" %}
{% swagger-description %}
회원 가입 전 이메일 중복 확인
{% endswagger-description %}

{% swagger-parameter in="body" name="email" required="true" type="String" %}
max 64 validate by RFC 5322
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "duplicated" : true/false
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/signup/email/authenticate/send" baseUrl="" summary="이메일 인증번호 발송" %}
{% swagger-description %}
회원 가입 전 이메일 중복 확인
{% endswagger-description %}

{% swagger-parameter in="body" name="email" required="true" type="String" %}
max 64 validate by RFC 5322
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "duplicated" : true/false
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/signup/email/authenticate/check" baseUrl="" summary="이메일 인증번호 확인" %}
{% swagger-description %}
회원 가입 전 이메일 중복 확인
{% endswagger-description %}

{% swagger-parameter in="body" name="email" required="true" type="String" %}
max 64 validate by RFC 5322
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "duplicated" : true/false
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/signup/phonenumber/authenticate/send" baseUrl="" summary="핸드폰 인증번호 발송" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="phoneNumber" type="String" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/signup/phonenumber/authenticate/check" baseUrl="" summary="핸드폰 인증번호 확인" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="phoneNumber" type="String" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/login" baseUrl="" summary="로그인" %}
{% swagger-description %}
이메일 패스워드를 이용한 로그인, JWT Access, Refresh 토큰을 응답한다.
{% endswagger-description %}

{% swagger-parameter in="body" name="email" type="String" required="true" %}
max 64 validate by RFC 5322
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" type="String" %}
min 8 ~ max 16
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="LoginSuccess" %}
```json
{
    email: "hello@naver.com",
    accessToken: "jjj.www.ttt",
    refreshToken: "jjj.www.ttt"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="LoginFailure" %}
```json
{
    title: "LoginFailure"
    status : "400",
    detail : "이메일이나 패스워드가 올바르지 않습니다."
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="" baseUrl="" summary="TODO - 아이디 찾기" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

{% swagger method="get" path="" baseUrl="" summary="TODO - 패스워드 찾기" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

{% swagger method="get" path="" baseUrl="" summary="TODO - 패스워드 변경" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}
