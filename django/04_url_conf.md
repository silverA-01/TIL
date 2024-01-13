# URL Conf(설정)
## 동적 라우팅(Variable Routing)
Variable Routing이란 **URL 주소를 변수로 사용**하는 것을 의미한다. URL의 일부를 변수로 지정하여 view 함수의 인자로 넘길 수 있다.
변수 값에 따라 하나의 URL 경로에 여러 페이지를 연결 시킬 수 있다.

### 동적 라우팅 형식
```python
<데이터타입:변수>
```
`<>` 기호 사이에 변수명을 적어준다. 변수명은 사용자가 지정할 수 있다. 선택적으로 변수의 데이터타입을 앞에 작성하고 `:` 뒤에 데이터타입을 따르는 변수를 작성해준다. 
ex. `<int:number>`, `<str:name>`

- **Path converters** : URL path에 들어갈 수 있는 데이터 형식(타입)
  - `str` : `/`기호를 제외한 빈 문자열(`''`)을 포함한 문자열
  - `int` : 0 혹은 양의 정수
  - `slug` : ASCII 문자 인코딩에 해당하는 문자열, 숫자, 하이픈기호(`-`), 언더바기호(`_`)로 구성된 문자열을 지원
    - ex. ` building-your-1st-django-site.`
    - 슬러그(slug) : 조사나 전치사 등을 빼고 중요한 의미를 포함하는 단어만을 이용해 제목을 작성하는 방법. 띄어쓰기는 하이픈(`-`)으로 대체하고 쉼표나 마침표 등은 제거한다.
  - `uuid` : UUID 포맷
    - [파이썬에서 UUID](https://docs.python.org/3/library/uuid.html#uuid.UUID)
    - ex. `075194d3-6885-417e-a8a8-6c931e272f00`
  - path : `/`기호를 포함하는 URL 경로를 나타내는 문자열(빈 문자열X)
  
### 1. `home.urls`에서 동적 라우팅을 활용한 `path()` 추가
```python
from django.urls import path
from . import views

urlpatterns = [
  path('test/', views.test),
  path('', views.index),
  path('cube/<int:num>/', views.cube),
]
```
- 만약 `http://localhost:8000/home/cube/2/` URL이 요청되면 `http://localhost:8000/home/cube/<int:num>`이 적용되어 `num` 변수에 `2`라는 정수가 저장되고 `views.cube`가 실행된다.


### 2. `home.views`에서 추가한 `path()`에 대한 함수 정의
`home.views`에서 `cube` 함수를 정의해준다.
```python
from django.shortcuts import render
from django.http import HttpResponse

def test(request):
  return HttpResponse('Hello')

def index(request):
  return render(request, 'home/index.html')

def cube(request, num):
    answer = num * 3
    return render(request, 'var_routing/cube.html',
                  {'answer':answer, })
```
1. `def cube(request, num):` : 함수의 두 번째 인자로 `home.urls`에서 설정한 변수 `num`을 매개변수로 추가해준다.
2. `answer = num * 3` :  매개변수로 받은 `num`을 사용해 `answer` 변수는 `num`에 3을 곱한 값을 할당받도록 했다.
3. `return render(request, 'var_routing/cube.html', {'answer':answer, })`
   - `cube` 함수를 실행시 `var_routing/cube.html`이 렌더링되고, `cube.html`에서 변수로 `answer`를 사용할 수 있게 context에 넘겼다.

### 3. `cube.html`에서 변수 활용
`home` App 폴더에서 `templates/home/cube.html`을 생성한다. `cube.html`는 `03_template_inheritance.md`에서 설정해둔 기본 템플릿 `base.html`을 상속받아 사용하겠다.
```html
{% extends 'base.html' %}
{% block content %}
    <h1>{{ answer }}</h1>
{% endblock content %}
```
html 문서 `body`에 `<h1>{{ answer }}</h1>`로 context 받은 변수 `answer`를 넣어서, `num`에 3을 곱한 값이 페이지에 나오도록 할 것이다.

### 4. 서버실행 후 확인
서버를 실행해 브라우저에 `http://127.0.0.1:8000/home/cube/10/` URL을 요청하면 `http://localhost:8000/home/cube/<int:num>`이 적용되어 `num` 변수에 `10`라는 정수가 저장되고 `views.cube`가 실행된다. `cube` 함수에서 `answer = num * 3`라고 작성하였기 때문에 `answer`는 `10 * 3`이 계산된 `30`이 할당된다. `cube.html`에 `answer`이 변수로 사용될 수 있도록 context를 넘겨주어 작성했기 때문에 최종적으로 `answer`에 할당된 `30`이 렌더링된다.

![`home/cube/10/`URL 요청시 동적라우팅으로 렌더링되는 `cube.html`](./asset/django_var_routing_cube.PNG)

`http://127.0.0.1:8000/home/cube/300/` URL을 요청하면 변수 `num`에 `300`이 할당되어, 최종적으로 `900`이 렌더링된다.

![`home/cube/300/`URL 요청시 동적라우팅으로 렌더링되는 `cube.html`](./asset/django_var_routing_cube2.PNG)


## URL 별칭
### 1. URL 하드코딩
**URL 하드코딩**은 **URL을 직접 문자열로 고정하는 형태**이다.

위에서 정의한 `home.views`에서 `cube`함수에 변수 `num`을 context에 추가로 넘겨준다.
```python
def cube(request, num):
    answer = num * 3
    return render(request, 'var_routing/cube.html',
                  {'answer':answer, 'num':num, })
```

`cube.html`에서 `Cube`라는 문자열에 `a` 태그로 하이퍼링크를 연결했다. 연결되는 하이퍼링크는 `http://localhost:8000/home/cube/<int:num>/` URL이다. 이처럼 URL을 직접 문자열로 고정하는 형태를 URL 하드코딩이라고 한다.
- 동적라우팅으로 변수로 사용한 url의 변수 `num`은 `cube`함수에서 context로 넘겨서 `cube.html`에서 변수로 사용 가능하다. 아래와 같이 하이퍼링크에 들어갈 URL 경로에 `{{ num }}`으로 변수를 사용할 수 있다.
```html
{% extends "base.html" %}

{% block content %}
    <h1>{{ answer }}</h1>
    <h2>
        <a href="/home/cube/{{ num }}/">Cube</a>
    </h2>
{% endblock content %}
```
URL의 구조가 자주 변경된다면, 템플릿에서 사용하는 모든 URL들을 일일히 찾아가며 수정해야하는 번거러움이 있다. 예를 들어 `home.urls`에서 path에 설정된 `route`인 `'cube/<int:num>/'`를 `'cube2/<int:num>/'`로 수정하려면 `cube/`가 URL 경로로 설정된 html 문서의 내용을 모두 아래와 같이 수정해야 하는 것이다.
```html
{% extends "base.html" %}

{% block content %}
    <h1>{{ answer }}</h1>
    <h2>
        <a href="/home/cube2/{{ num }}/">Cube</a>
    </h2>
{% endblock content %}
```

이를 해결하기 위해서는, 해당 URL에 대한 실제 URL 문자열로 작성된 하드코딩대신 링크의 주소가 1:1로 매핑되어 있는 별칭을 사용해야 한다. URL의 구조가 바뀌어다 매핑된 별칭으로 URL 경로를 탐색하기 때문에 더 유연하다.

### 2. URL 별칭
URL 하드코딩 방식 대신에, URL 별칭을 사용하려면 URL 매핑에 name 속성을 부여하면 된다.

`home.urls`에서 다음과 같이 수정한다.
```python
from django.urls import path
from . import views

urlpatterns = [
  path('test/', views.test, name='test'),
  path('', views.index, name='index'),
  path('cube/<int:num>/', views.cube, name='cube'),
]
```
`http://localhost:8000/home/cube/2/`와 같은 URL에 대해 `cube`라는 별칭을 매핑한 것이다.

### 3. Template 에서 URL 별칭 사용
위 하드코딩에서 예시로 사용한 html에 대해 아래처럼 URL 별칭을 사용할 수 있다. URL 하드코딩으로 작성된 부분에 DTL(Django Template Language) 태그를 이용해 `{% url "<URL 별칭>" 변수 %}`을 넣어준다.
```html
{% extends "base.html" %}

{% block content %}
    <h1>{{ answer }}</h1>
    <h2>
        <a herf="{% url "cube" num %}">Cube</a>
    </h2>
{% endblock content %}
```
1. 하드코딩 되어 있던 `/home/cube/{{ num }}"`에 별칭을 사용한 `{% url "cube" %}`을 넣어준다. 
2. `{{ num }}`에서 활용된 `num`이라는 매개변수(parameter)는 별칭을 넣은 "cube" 뒤에 공백 문자(one space)과 함께 넣어, `{% url "cube" num %}`와 같이 작성한다.
3. 만약 `answer`이라는 매개변수를 추가로 URL에 받게된다면 공백 문자 이후에 덧 붙여주면 된다.
   - `{% url "cube" num answer %}`

최종적으로 하이퍼링크에 적어준 URL 경로인 `"{% url "cube" num %}"`는 `"/home/cube/{{ num }}/"`와 같은 `http://localhost:8000/home/cube/{{ num }}/` URL로 하이퍼링크가 연결된다.

## 3. URL 네임스페이스(namespace)
만약 Local App이 추가되었을 때, 서로 다른 앱에서 동일한 URL 별칭을 사용하면 중복이 발생할 것 이다. 장고에서는 Template과 마찬가지로 `settings.py`에 등록된 App 순서대로 URL 별칭에 해당하는 URL 경로를 탐색하기 때문이다.

때문에 각 Local App의 URL 네임스페이스를 의미하는 `app_name` 변수를 지정해야 한다.
   - 반드시 변수명은 `app_name`이어야 한다. 장고에서 URL 네임스페이스로서 찾는 변수명을 `app_name`으로 고정해두었기 때문이다.

### 1. `home.urls`에 `app_name` 추가
```python
from django.urls import path
from . import views

app_name = 'home'

urlpatterns = [
  path('test/', views.test, name='test'),
  path('', views.index, name='index'),
  path('cube/<int:num>/', views.cube, name='cube'),
]
```
1. `home` App의 URLConf인 `home.urls`에서 `app_name` 변수에 `'home'`이라는 네임스페이스를 추가했다.

2. App의 네임스페이스를 Template에서 사용한 URL 경로에 적용
`cube.html`에서 app_name에 할당한 URL 네임스페이스를 추가로 넣어준다. 형식은 `<URL네임스페이스>:<URL 별칭>`으로 작성한다. `<URL 별칭>`에 해당하는 `cube` 앞에 URL 네임스페이스인 `home`을 `:`와 함께 작성한다
```html
{% extends "base.html" %}

{% block content %}
    <h1>{{ answer }}</h1>
    <h2>
        <a herf="{% url "home:cube" num %}">Cube</a>
    </h2>
{% endblock content %}
```
3. 서버에서 URL 확인해보면 정상적으로 `cube.html`이 렌더링 되는 것을 확인할 수 있다.
   - 참고로 URL 네임스페이스를 할당한 후, URL 네임스페이스을 Template에 넣어주지 않으면 서버를 실행후 브라우저에서 URL 요청시 오류가 발생한다.