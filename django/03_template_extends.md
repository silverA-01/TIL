# Template 상속(inheritance)
## URL 하드코딩
직접 문자열로 고정하는 형태 - 상대경로 <-> 절대경로 URL 설정(CONF)를 가지고 만든 경로 - url이 바뀌어도 name에 할당된 경로를 찾기 때문에 더 유연하다.

<!-- 인스턴스 네임스페이스가 지정되지 않으면 기본적으로 포함된 URLconf의 애플리케이션 네임스페이스가 사용됩니다. 이는 해당 네임스페이스의 기본 인스턴스이기도 함을 의미합니다. -->

## 기본 틀 html 생성의 필요성
더 효과적으로 html 문서를 관리하기 위해서는, **html 문서에서 공통적으로 사용되는 부분을 기본 틀 html 문서로 정의**해주고, 다르게 작성할 부분만 따로 각 APP의 html로서 작성해줘야 한다. 

각 APP의 html 문서마다 공통적으로 사용되는 부분을 반복해서 작성하는 일은 매우 비효율적이고, 수정할 때 번거롭기 때문이다. 만약 기본 틀 html을 활용한다면 공통적으로 사용되는 부분을 수정하고 싶을 때, 일일히 html 문서들에 대해서 바꾸지 않고 기본틀로 정의한 html 문서만 수정하면 되는 편리함이 있다.

기본 틀로 사용할 Template 파일(html 문서)를 생성하고 이를 기본 템플릿으로 사용하는 법을 알아보자.

## 기본틀로 사용할 Template 파일 생성
### 1. `base.html` 생성
프로젝트 폴더(`00_INTRO`) 에서 `templates` 하위 폴더를 생성하고, 그 안에 템플릿 파일의 기본 틀이 되는 `base.html` 문서를 생성한다.
- 프로젝트에서 생성한 APP이 공통적으로 사용할 기본 틀인 html 문서이기 때문에, 특정한 APP 폴더 내부가 아닌 프로젝트 폴더에서 `templates` 폴더를 생성했다.
-  장고에서는 `templates` 폴더 내부에 있는 html 문서를 조회하기 때문에,  `templates` 폴더 내부에 html 문서를 생성한다.
-  `base`라는 html 이름은 임의로 정한 것이기 때문에 다른 이름으로 설정해도 괜찮다. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>
```
- 위 코드는 html 문서로서 브라우저에 보여지기 위해 기본적인 세팅만 되어 있고, `body` 태그 안에 아무 코드도 작성하지 않았기 때문에 빈 페이지로 나올 것이다.

### 2. DTL을 사용해서 `body`에 구멍을 뚫어주기
`block`을 사용해 하위 템플릿(html 문서)이 기본 틀을 상속받을 수 있게 한다.
기본 틀로 사용되는 부분 외에 개별적으로 들어갈 내용을 넣기 위해 `body`에서 DTL Template 태그를 활용해 `block`

추후 각 APP에서 작성될 html은 기본 틀로 작성된 코드를 제외하고 `{% block content %}`, `{% endblock content %}` 태그 사이에 작성될 부분만 작성해주면 된다.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    {% block content %}

    {% endblock content %}
</body>
</html>
```

## 2. `settings.py`의 `Template`에 등록
`DIRS`

## 3.  `base.html` 에서 DTL을 활용
### 1. `{% extends '<상속받을html파일명>.html' %}`

### 2. `{% block content %}` ~ `{% endblock content %}`