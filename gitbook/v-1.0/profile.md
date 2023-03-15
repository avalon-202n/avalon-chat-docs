# 🐶 Profile

{% swagger method="post" path="/profiles" baseUrl="" summary="프로필 생성" expanded="false" %}
{% swagger-description %}
회원 가입 이후 단 한번만 호출되는 프로필 생성
{% endswagger-description %}

{% swagger-parameter in="body" name="birthDate" required="true" type="String" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="AUTHORIZATION" type="String" required="true" %}
Bearer jjj.www.ttt
{% endswagger-parameter %}

{% swagger-parameter in="body" name="nickname" type="String" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="image" type="이미지" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="background" type="이미지" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="bio" type="String" %}
상태 메시지
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/profiles/{profileId}" baseUrl="" summary="프로필 상세 조회" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="AUTHORIZATION" type="String" required="true" %}
Bearer jjj.www.ttt
{% endswagger-parameter %}

{% swagger-parameter in="path" name="profileId" type="Integer" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
        "id" : 2,
        "nickname" : "haha",
        "bio":"haha 상메",
        "image": "haha/image/path/url", // “no profileImage" if null
        "backgroundImage" : "haha/bg/path/url", //“no backgroundImage" if null
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="patch" path="" baseUrl="" summary="프로필 수정" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="AUTHORIZATION" type="String" required="true" %}
Bearer jjj.www.ttt
{% endswagger-parameter %}

{% swagger-parameter in="body" name="nickname" type="String" required="false" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="bio" type="String" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="image" type="이미지" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="backgroundImage" type="이미지" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}

{% endswagger-response %}
{% endswagger %}
