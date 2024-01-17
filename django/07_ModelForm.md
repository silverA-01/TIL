# [실습] Form과 Model 응용
`05_form.md`에서 정리한 Form과 `06_model.md`에서 정리한 Model을 활용해 Form에 사용자가 입력한 데이터를 DB에 저장하도록 아래와 같이 설계해보자.

1. `01_INTRO` 프로젝트에서 `board` App 생성
2. `Article` 모델 클래스 정의
   1. `title` 컬럼 => `CharField(300)`
   2. `content` 컬럼 => `TextField()`
3. `Article` 모델 클래스 데이터 베이스에 반영
4. `board/new/` URL로 요청시  `board.views`의 `new`함수가 실행되면서`new.html` 랜더링되는 응답
    1. `new.html `은 제목을 입력받을 `<input>` 과 내용을 입력받을 `<textarea>` 를 포함해야함
    2. 작성한 데이터를 `<form>` 을 통해 `POST` 방식으로 `board/create/`로 제출
5. `board/create/` URL이 요청시 `board.views`의 `create` 함수가 실행
    1. `new.html` 을 통해 작성한 데이터가 넘어옴
    2. 해당 데이터를 `Article` 모델을 통해 데이터베이스에 생성 (Create)시 `board/detail/<int:pk>/`로 제출
       - `pk`는 데이터베이스에 생성된 해당 row의 `pk` 칼럼의 필드
6. `board/detail/<int:pk>/` URL로 요청시 `board.views`의 `detail`함수가 실행되면서 `detail.html` 랜더링되는 응답
   - `detail.html`은 `pk`에 해당하는 row의 `title`과 `content`를 보여준다.
   - `<button>`으로 수정 버튼을 생성하고 버튼을 클릭시 `POST` 방식으로 `board/update/<int:pk>/`로 제출
   - `<button>`으로 삭제 버튼을 생성하고 버튼을 클릭시 `POST` 방식으로 `board/delete/<int:pk>/`로 제출
7. `board/update/<int:pk>/` URL로 요청시 `board.views`의 `update`함수가 실행되면서 `pk`에 해당하는 row의 `title`과 `content`가 담겨있는 `update.html`이 랜더링되는 응답
8. `board/delete/<int:pk>/` URL로 요청시 `board.views`의 `delete`함수가 실행되면서 `pk`에 해당하는 row를 삭제하고 `board/index/` 요청
9. `board/index/` URL로 요청시 `board.views`의 `index`함수가 실행되면서 `index.html` 랜더링되는 응답
    - `index.html`은 데이터베이스에 저장된 각 row의 제목을 리스트 형태로 보여준다.

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

## 2. URL 설정
### 1. ROOT URL `intro.urls` 포워딩
`intro.ulrs` 에서 `http://localhost:8000/board/` URL로 요청할 때 `board.urls`로 포워딩되도록 
### 2. `board.urls` URL 경로 설정
`board.urls`

## 3.`board.views` 함수 정의

