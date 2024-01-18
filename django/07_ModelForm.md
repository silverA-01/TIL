# ModelForm - Form과 Model 응용
`05_form.md`에서 정리한 Form과 `06_model.md`에서 정리한 Model을 활용해 Form에 사용자가 입력한 데이터를 DB에 저장하도록 아래와 같이 설계해보자.

1. `01_INTRO` 프로젝트에서 `board` App 생성
2. `Article` 모델 클래스 정의
   1. `title` 컬럼 => `CharField(300)`
   2. `content` 컬럼 => `TextField()`
3. `Article` 모델 클래스 데이터 베이스에 반영
4. 사용자 데이터를 입력받아 `Article` 모델과 연동해 DB에 저장할 수 있는 `ArticleForm` ModelForm 생성
5. `Article` 모델에 대해 CRUD가 이루어질 수 있게 URL, View, Template 설정

## 1. Local App `board` 생성 및 등록
`01_INTRO` 프로젝트 경로에서 터미널에 아래 코드를 입력
```bash
$ python manage.py startapp board
```

`intro.settings`에 `board` App 등록
```python
INSTALLED_APPS = [
    # 장고 기본 Apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # 3rd Party Apps
    'django_extensions',

    # Local Apps
    'home',
    'form',
    'hospital',
    'board',
]
```

## 2. Model 생성
`board` App의 `Article` 모델을 생성한다. 즉 `board.models`에서 클래스 `Article`을 정의한다.
```python
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
```
`Article` 모델을 DB에 이주(migrate)시킨다.
```bash
$ python manage.py makemigrations board

$ python manage.py migrate board
```
위 코드를 실행하면 `db.sqlite3` 파일에 `board_article` 테이블이 생성된다.

## 3. ModelForm 생성
기존의 html 문서에서 `<form>` 으로 Form을 만들지 않고, `ModelForm`을 생성해 사용자 입력 데이터를 `Article` 모델과 연결해 DB에 데이터를 저장하겠다.

### 1. Form에 유효성 검사가 필요한 이유
`05_form.md`에서 `ping.html`에 `<form>` 태그를 만들어서 `<input>`, `<textarea>`와 같은 사용자 입력 HTML을 생성했다.

이를 Model에서 정의한 클래스를 활용해 DB에 사용자 입력 데이터를 저장할 수 있다.

하지만, 사용자 입력에는 다양한 가능성이 있기 때문에, **원하는 형태의 데이터를 받기 위해서는 입력에 대한 제한을 설정**해야 한다.

Model에서 `models.py` 모듈을 가져와 `CharField(min_length=2, max_length=100)`과 같이 사용자 입력 데이터에 대해 제한을 줄 수 있다. 생성한 Model에 맞게 html 문서에서 <form>을 `type` 속성이나 `required` 등을 통해  html에서 일차적으로 사용자 입력 데이터에 대한 조건을 걸러줄 수 있다.

하지만 이 방법은 서버를 실행해 해당 URL 페이지를 요청해 개발자 도구 `elemnet` 탭에서 조건에 대한 부분을 제거하면 조건에 맞지 않는 Form 제출할 수 있는 가능성이 있다. 예를들면 `min_length=2`에 대한 부분을 제거하고 아무 내용도 적지 않은 채로 Form을 제출할 수 있습니다. 이 때 문자열의 경우 빈 문자열을 데이터로 저장하지만, 정수/실수가 요구되는 입력창의 경우 오류가 발생한다.

그렇기 때문에 원하는 데이터를 받기 위해서는 사용자 입력 데이터인 Form이 원하는 조건을 제한하고 확인하는 **유효성 검사**가 필요하다.

Model에서는 유효성 검사를 하지 못하기 때문에 Local App에서 `form.py`를 생성해 `ModelForm`을 생성하여 유효성 검사를 할 수 있게 한다.

### 2. ModelForm의 역할
1. **검증 및 저장**
   - 사용자 입력 데이터에 대한 검증(Validation) 후 데이터를 저장(save)하는 역할도 수행한다.
   - 전제 조건 : Model의 `class Meta`에서 `fields`에 입력된 필드에 대해만 검증/저장한다.

2. **사용자 입력과 관련된 HTML 생성**
   - `<input>`, `<textarea>`와 같은 사용자 입력과 관련된 HTML을 자체적으로 생성할 수 있다. 즉, html 문서에서 `<form>` 내부에 들어갈 사용자 입력 관련 태그를 ModelForm으로 대체할 수 있다.


### 3. `Article` 모델과 연결할 ModelForm 생성
`board` App 폴더에서 `forms.py`를 생성한다. `board.forms` Article 모델과 연동될 ModelForm을 생성할 것이다.

#### 1. `ArticleForm` 생성
```python
from django import forms

class ArticleForm(forms.ModelForm):
    pass
```
클래스 `ArticleForm`을 생성하기 전에, 장고 내부에 있는 `forms.py` 모듈을 가져와 클래스 `ModelForm`을 상속해준다.


#### 2. `ArticleForm`의 `Meta` 클래스 생성
```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):

    class Meta:
        model = Article
        
        fields = ('title', 'content', )
```
1. 특정 모델과 `ModelForm`을 연결하기 위해서 `ArticleForm` 내부에 `class Meta:`를 작성해준다. 
   - `class Meta` : 파이썬의 metaclass에 대한 내용이 아니라, 장고에서만 사용되는 개념으로 `Meta`는 Metadata(메타데이터)를 의미한다. 메타데이터는 데이터에 대한 데이터로 `ArticleForm`에 대한 추가적인 정보를 나타낸다. 

2. `ModelForm`의 `Meta` 클래스는 클래스 변수로 `model`이 있어야 한다. `model`에 연결하고 싶은 `Article` 모델을 할당한다. 
   - 현재 `board.forms`에는 `Article` 모델이 없기 때문에 `from .models import Article`로 가져온다.
     - `.models` : 현재 경로에 있는 `models.py`, 즉 `board.models`를 의미한다.
3. `ModelForm`의 `Meta` 클래스는 클래스 변수로 `fields` 혹은 `exclude`가 있어야 한다. `Meta` 클래스의 `model`의 필드, 즉 모델에 매핑된 DB의 테이블의 필드(칼럼) 중 어떤 것을 검증 및 저장할지 지정해주는 것이다.
   - `ArticleForm`에 연결된 `Article` 모델이 매핑된 DB의 `board_article` 테이블의 필드에서 pk필드를 제외하면 `title`과 `content`가 있다. 
   - `fields`는 지정한 필드명을 리스트/튜플에 담고 지정한 필드명에 대해서만 검증/저장에 대해 반환한다.
     - `fields = '__all__'` : 모든 필드을 사용하고 싶으면 `'__all__'`을 할당하면 된다.
     - `fiedls = ('title', 'content', )` : 특정 필드만 지정하고 싶다면 리스트 혹은 튜플 형태로 넣어준다. 마지막에 `,`는 트레일링 콤마로 사용했다. `fiedls = ('title', 'content', )`는 `fiedls = [(]'title', 'content', ]`로 표현해도 같은 의미이다. 
       - 현재 모델에서 필드가 `title`, `content`밖에 없기 때문에 `fiedls = ('title', 'content', )`는 `fields = '__all__'`와 같은 의미이다. 추후 모델에 필드를 추가하여 migration하면 다른 의미가 될 것이다.
  
   - `exclude`는 지정한 필드명을 리스트/튜플에 담고 지정한 필드명에 대해서만 제외하고 나머지 필드명에 대해 검증/저장에 대해 반환한다.
     - `exclude = ('title', )` : `title` 필드만 제외하고 나머지 `content` 필드만 반환하는 필드로 지정해주는 것이다.


#### 3. `ArticleForm`의 사용자 입력할 부분 생성
`Article` 모델에서 DB에 저장될 컬럼을 `title`, `content`으로 만들었다. `ArticleForm`에도 사용자가 입력할 `<input>` 등을 `ArticleForm`의 클래스 변수로 만들 수 있다.
```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    title = forms.CharField(min_length=2, max_length=100)
    content = forms.CharField(min_length=2)
    
    class Meta:
        model = Article
        
        fields = ('title', 'content', )
```
- `ArticleForm`의 클래스 변수 `title`은 문자열 형태의 데이터 중 글자의 최소 길이가 2이고, 최대 길이가 100인 데이터만 받을 수 있도록 제한 조건을 설정했다.
  - `forms.CharField()` : `forms.py` 모듈에서 `CharField` 클래스는 사용자 입력창에 문자열 형태의 데이터를 받겠다는 의미이다. `CharField` 클래스의 속성(클래스 변수)을 이용해 사용자 입력을 제한할 수 있는 조건을 넣을 수 있다.
  - `max_length` : 문자열 글자의 최대 길이 지정
  - `min_length` : 문자열 글자의 최소 길이 지정

- `ArticleForm`의 클래스 변수 `content`은 문자열 형태의 데이터 중 글자의 최소 길이가 2인 데이터만 받을 수 있도록 제한 조건을 설정했다.

`ArticleForm`의 클래스 변수 `title`과 `content`는 연결된 `Article` 모델의 클래스 변수에 대해 유효성 검사를 하고 싶은 조건에 대해 다시 지정해주는 것이다.

`CharField` 외에도 정수를 받는 `IntegerField`, 소수를 받는 `FloatField`, 날짜에 대한 `DateField` 등 `forms.py` 모듈에서 다양한 클래스를 활용해 사용자 입력에 제한을 줄 수 있다.

참고로 html의 `<textarea>` 를 대신할 `TextField`는 없기 때문에 `content`에 대해 `CharField`를 사용했다.

## 4. ROOT URL `intro.urls` 포워딩
`intro.ulrs` 에서 `http://localhost:8000/board/` URL로 요청할 때 `board.urls`로 포워딩되도록 URL 경로를 설정한다.
```python
from django.contrib import admin
from django.urls import path
from django.urls import include, path


urlpatterns = [
    path('admin/', admin.site.urls),
    path('home/', include('home.urls')),
    path('form/', include('form.urls')),  
    path('board/', include('board.urls')),

]
```
## 5. `Article` 생성 - `board.urls` URL 경로 설정
`board.urls`에서 설계에 필요한 URL 경로를 설정한다.
```python
from django.urls import path
from . import views

app_name = 'board'

urlpatterns = [
    path('create_article/', views.create_article, name='create_article'),
    path('detail_article/', views.detail_article, name='detail_article'),
]
```
1. 필요한 `path`와 `views`를 가져온다.
2. `board` App URL 네임스페이스로 `'board'`를 매핑한다.
3. `/board/create_article/` URL로 요청할 때
   1. 'GET' 방식으로 요청시 : 사용자가 입력할 수 있는 `ArticleForm`이 담긴 `form.html`이 렌더링 사용자 입력 데이터를 제출시 `/board/create_article/` URL로 요청
   2. 'POST' 방식으로 요청시 : 사용자 입력 데이터가 유효성 검사에 통과하면(유효하면/조건에 맞으면) 입력 데이터를 `Article` 모델과 매핑된 DB에 저장하고 해당 `Article`의 상세페이지(`/board/detail_article/`)를 다시 요청(`redirect`)


### View Decorator(데코레이터)
데코레이터는 기존에 작성된 함수에 기능을 추가하고 싶을 때, 해당 함수를 수정하지 않고 기능을 추가해주는 함수이다. 장고는 다양한 HTTP 기능을 지원하기 위해 view함수에 적용할 수 있는 여러 데코레이터를 제공한다. 
```python
@<데코레이터명>
def <함수명>(request):
    pass
```
기능을 추가하고 싶은 기존에 작성된 함수 위에 `@`기호와 함께 데코레이터명을 작성해주면 데코레이터가 기능을 추가해준다.

`django.views.decorators.http`에서 데코레이터(decorators)는 요청된 request method에 대한 접근하도록 제한한다. 요청된 method가 아닐 경우 `405 Method Not Allowed` 에러를 응답한다.

HTTP request method는 'GET'과 'POST' 두 가지이다. 

1. `require_GET()` : 오직 'GET' 방식(method)
2. 


## 6. View - `create_article` 함수 정의
Form의 유효성 검사를 하기 위해 ModelForm을 사용해 `ArticleForm`을 생성했다. 

`board.views`에서 `create_article` 함수에 조건을 통해 두가지 기능을 수행하도록 만든다. 
1. 사용자가 입력하기 전 비어있는 `ArticleForm`를 담은 `form.html`을 렌더링하도록 응답한다. 
2. `ArticleForm`에 사용자가 데이터를 입력하여 제출했을 때, 사용자가 입력한 데이터가 조건에 맞는지 유효성 검사를 거쳐 유효한 Form만 DB에 저장하고, 해당 Form이 DB에 저장되는 `pk`값을 `article_pk`로 가져와 `'board/detail_article/<int:article_pk/>'`로 재요청(redirect)하도록 하자.

### 1. Model과 ModelForm 가져오기
생성한 `Article` Model과 `ArticleForm`을 가져온다.
```python
from django.shortcuts import render
from .models import Article
from .forms import ArticleForm
```
- `.models`는 현재 경로의 `models.py` 모듈을 의미한다. 즉 `board.models`이다.
- `.forms`는 현재 경로의 `forms.py` 모듈을 의미한다. 즉 `board.forms`이다.


### 2. HTTP request method 조건 달기 - GET
HTTP request method는 'GET'과 'POST' 두 가지이다. `if` 조건문으로 HTTP request method를 'GET'과 'POST'로 각각 조건을 설정해준다. 조건이 오는 순서는 바뀌어도 상관없지만, 보통 'POST' 방식을 먼저 조건으로 걸도록 작성한다.

```python
from django.shortcuts import render
from .models import Article
from .forms import ArticleForm

def create_article(request):
    if request.method == 'POST':
        pass
    elif request.method == 'GET':
        form = ArticleForm()
        return render('board/form.html', {'form': form, })
```
1. `http://localhost:8000/board/create_article/` URL을 주소창에 입력해 페이지로 이동하면 'GET' 방식으로 요청된다. 
2. 해당 URL 요청으로 `create_article` 함수가 실행되고, `elif request.method == 'GET':`에 대한 조건이 만족될 것이다. 
3. 이때 반환할 것은 사용자가 입력하기 전 비어있는 `ArticleForm`이 있는 `form.html`이다.
4. `form = ArticleForm()`으로 `ArticleForm`의 인스턴스로 `form`을 만들어준다.
5. HTTP request method를 'GET'일 때 `form`이 담긴 `form.html`이 렌더링 되도록 `render()` 함수를 사용한다. `form.html`에 `form`을 변수로 사용할 수 있도록 context로 넘겨준다.

## 7. Template - `form.html` 생성
1. `board/templates/board/form.html` 경로에 맞게 `form.html`을 생성한다. 기본 템플릿 `base.html`을 상속받는다.
```html
{% extends "base.html" %}

{% block content %}

{% endblock content %}
```

2. `<h1>`으로 `Article Form`이라고 제목을 만들어준다. `<form>`을 만든다.
```html
{% extends "base.html" %}

{% block content %}
<h1>Article Form</h1>
<form action="">
</form>
{% endblock content %}
```
3. `{{ form }}`  : `<form>` 안에 context로 넘긴 `form`을 DTL로 넣어준다. 사용자가 입력하기 전 비어있는 `ArticleForm`이 나올 것이다.
```html
{% extends "base.html" %}

{% block content %}
<h1>Article Form</h1>
<form action="">
    {{ form }}
</form>
{% endblock content %}
```
4. 사용자가 Form을 작성하고 제출하면 `board:create_article`로 요청한다. 즉, `'/board/create_article/'` URL로 요청하여 `create_article` 함수가 실행되도록 한다.
```html
{% extends "base.html" %}

{% block content %}
<h1>Article Form</h1>
<form action="board:create_article">
    {{ form }}
</form>
{% endblock content %}
```
5. `<form>`의 method는 POST로 한다. POST방식으로 넘겨야 사용자가 입력한 데이터에 대해 공개되지 않는다.
```html
{% extends "base.html" %}

{% block content %}
<h1>Article Form</h1>
<form action="board:create_article" method="POST">
    {{ form }}
</form>
{% endblock content %}
```

6. HTTP request method가 POST 방식이면 `csrf_token`이 보안상 필요하다. `<form>` 안에 DTL로 `csrf_token`을 넣어준다.
```html
{% extends "base.html" %}

{% block content %}
<h1>Article Form</h1>
<form action="board:create_article" method="POST">
    {% csrf_token %}
    {{ form }}
</form>
{% endblock content %}
```

## 8. `Article` 생성 - `board.views` 함수 정의

7. 만약 사용자가 데이터를 입력한 `ArticleForm`을 POST 방식으로 제출하여 다시 `create_article` 함수를 호출하면 `if request.method == 'POST':` 조건에 참이 될 것이다.