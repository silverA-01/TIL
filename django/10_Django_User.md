# Django User
웹 서비스의 회원을 DB에 저장하고 활용하기 위해 장고 내부에 있는 `User` 모델 활용
- 회원가입, 로그인, 로그아웃, 회원탈퇴


- 특정한 Local App에서 회원을 관리하는 역할을 담당하는 것이 좋다.
- 장고에서는 `accounts` Local App을 생성해 회원관리하는 것을 권장
  - 물론 `accounts` 외에 다른 이름으로 App 이름을 사용해도 무관한다.
- 다른 프레임 워크는 외부 라이브러리 앱을 설치해 회원관리를 하는 경우가 대다수인데, 장고에서는 내부적으로 회원관리를 할 수 있게 잘 구성된 프레임워크이다.

## `accounts` Local App 생성 및 등록
```bash
$ python manage.py startapp accounts
```

`intro.settings`에 생성한 App 등록

## Model - 장고의 `User` 모델 사용
장고에서는 기본 App에 회원관리를 해주는 App에 대한 내용이 등록되어 있다.
```python
from django.contrib.auth.models import User
```
- 우리가 회원관리에 대한 Model을 따로 정의하지 않았지만 장고에서 `User`모델에 대해 회원관리에 필요한 필드와 내용을 정의해두었다.

### 마이그레이션
이제까지 특정 Local App에 대해서 마이그레이션을 진행했다.
서버를 실행할 때 아래처럼 마이그레이션하지 않은 항목이 있다는 메세지를 받았었다.

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```
- 특정 Local App 이름이 위 명령어 뒤에 붙지 않고 실행하면, `intro.settings`에 `INSTALLED_APPS`에 등록된 App을 순차적으로 모두 순회하면서 마이그레이션한다.

서버를 실행하면 마이그레이션이 필요하다는 메세지가 없어진다.

### DB 확인
다양한 테이블이 생김

`auth_user` 테이블 확인
- 장고의 `User` 모델의 필드에 `id`, `password` 등 다양한 필드들이 정의되어 있음을 알 수 있다.

## `superuser` - 관리자 생성
```bash
$ python manage.py createsuperuser
```
위 코드를 실행하면 Username, Password 등을 입력한다.

### DB 확인
`db.sqlite3 `확인 - `auth_user` 테이블
- `is_superuser` 필드에 `1`이라는 값으로 관리자 계정임을 체크
- `password` 필드값은 해싱되어 암호화된 값이 저장되어 있다.

### Root URL Conf
```python
path('admin/', admin.site.urls),
```
- 관리자 계정에 관련된 URL 경로임

### 서버에서 확인
`/admin/` URL 요청시 이미지

User과 해당 프로젝트의 App들에 대한 관리 가능

### `board` App에서 정의한 모델을 admin에 등록
`board.admin`에 `Article` 모델과 `Comment` 모델 등록
```python
from django.contrib import admin
from .models import Article, Comment

admin.site.register(Article)
admin.site.register(Comment)
```
- 모델 불러오기
- 모델 등록하기

### 서버에서 확인
`/admin/` URL 요청시 `board` App의 등록된 모델이 연동되어 관리자가 관리할 수 있다.

## `Article`모델과 `Comment`모델 수정
`board.models`에서 `Article`, `Comment`모델과 `User`모델의 관계 설정

1:N 관계
* 1 - User
* N - Article, Comment

- `Article` 모델과 `Comment`모델에 각각 `User` 모델에 대한 FK로 `user` 필드 생성
- `User` 모델을 FK로 설정할 때는
```python
from django.conf import settings
```
  - `settings`를 가져와 `User` 모델 대신 `settings.AUTH_USER_MODEL`을 사용한다.
  - `from django.contrib.auth.models import get_user_model` / `get_user_model(User)`을 사용해도 되지만 `settings.AUTH_USER_MODEL`을 사용하는 것을 권장

## 모델 수정 후 마이그레이션
```bash
$ python manage.py makemigrations
It is impossible to add a non-nullable field 'user' to article without specifying a default. This is because the database needs something to populate existing rows.
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit and manually define a default value in models.py.
Select an option:
```
- 기존 `Article` 모델과 `Comment` 모델에 데이터가 존재할 경우 새로 생기는 `user` 필드의 값으로 어떻게 default를 설정할지 묻는 것
- 1) 마이그레이션을 생성하는 과정에서 입력한 값으로 default 설정
- 2) 마이그레이션 생성을 멈추고 아래처럼 `user` 필드의 default 값을 `ForeignKey`의 옵션??으로 직접 작성
  - user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, default=1)

두 모델에 대한 default 설정을 순차적으로 마치면 마이그레이션을 완료한다.
```bash
$ python manage.py migrate
```

## DB 확인
- 해당 테이블에  `user_id` 필드가 생성된 것을 확인
- 이전에 저장된 row의 `user_id` 필드값이 default로 설정한 값이 들어간 것 확인


## `User` 모델의 데이터 생성
회원과 관련되었기 때문에 `account` Local App에서 진행

### URL Conf
- ROOT URL Conf
- `account.urls` 회원 가입, 로그인, 로그아웃 관련 URL 경로, 함수, URL 별칭 작성

### 1. 회원가입 기능 생성
#### VIEW - `signup` 함수 정의
- `accounts.views`에서 `signup` 함수 정의
- `User` 모델에 대한 Form을 따로 정의하지 않고 장고 내부에서 `User` 모델에 사용할 수 있는 `UserCreationForm`을 가져와 사용
- `UserCreationForm` : 사용자가 입력한 데이터를 생성해 DB에 저장하는 것이 목적. `ModelForm`을 상속받아 만들어진 form이다.
- HTTP 데코레이터

#### Template - `signup.html` 생성
- `base.html`을 기본 템플릿으로 상속
- `<form>` 태그 안에 `<button>` 태그로 회원 가입 버튼 생성
- 사용자 입력 데이터가 노출되지 않게 `POST` 방식으로 요청되도록 설정
  - {% csrf_token %}
  - `form` DTL 태그로 넣어준다.

- 서버에서 확인
  - 장고에서 기본으로 설정한 유효한 데이터의 조건이 나와있다.

#### Template - `signup.html` 수정
DTL 변수 옵션??
- as_p : `<p>` 태그로서 `{{ form }}`을 문단으로 사용하겠다고 HTML 설정

- 서버에서 확인 
  - 좀 더 보기 편하게 html이 수정되었다.
  - 회원가입 후 DB 확인 > `auth_user` 테이블에 회원가입 한 데이터가 저장된 것을 확인! 

### 2. 로그인 기능 생성
#### VIEW - `login` 함수 정의
- `AuthenticationForm` 불러오기
    - Authentication : 인증이라는 의미. 즉, 권한이 있는지 확인하는 것으로 로그인한 상태인지 확인을 위해 사용한다.
    - `ModelForm`이 아니라 `Form`을 상속받아 만들어진 form.
      - `ModelForm`처럼 필드에 설정된 조건을 데이터가 만족하는지 확인하는 것이 아님
      - `auth_user` 테이블에서 사용자가 입력한 `username` 필드값과 `password` 필드값이 특정 row 데이터의 각 필드값과 일치하는지 확인 =>  일치 시 유효 
    - 목적이 사용자 입력 데이터를 DB에 생성하는 것이 아니라 권한을 확인하는 것

- HTTP request method에 따라 조건 설정
  - GET 방식으로 요청할 때
    - 비어있는 `AuthenticationForm()`이 담긴 form이 렌더링되게
  - POST 방식으로 요청할 때
    - 사용자가 입력한 데이터가 담긴 `AuthenticationForm` 필요
    - 첫 번째 인자로 `request`를 받는다.
    - 두 번째 인자로 `data`에 form의 사용자 입력 데이터를 설정해줘야 한다. POST 방식으로 요청하기 때문에 `data=request.POST`가 들어간다.

- HTTP 데코레이터

#### Template - `login.html` 생성
- `base.html`을 기본 템플릿으로 상속
- `<form>` 태그 안에 `<button>` 태그로 로그인 버튼 생성
- 사용자 입력 데이터가 노출되지 않게 `POST` 방식으로 요청되도록 설정
  - {% csrf_token %}
  - `form` DTL 태그로 넣어준다.

#### VIEW - `login` 함수 재정의
- `login()` 함수 가져오기
  - 로그인 시키는 기능 ㅎㅎ 좀더 찾아보기!
  - `as auth_login` : 별칭을 활용해 `login` 함수를 가져온다. 
  - 로그인 관련 함수명을 `login`으로 정의했기 때문에 `login` 함수 내에 `login` 함수를 작성하면 재귀함수로서 실행된다.
- form이 유효하면
  - `user = form.get_user()` : `AuthenticationForm`을 사용했기 때문에 입력받은 form에 대해 `User` 모델에 해당하는 객체를 반환할 수 있다. `user` 변수에 할당
  - `auth_login(request, user)` : 별칭으로 가져온 `auth_login()`함수를 활용해 로그인시킨다. 
  - 로그인 되면 `board:article_index` URL 경로로 재요청한다.

#### VIEW - `signup` 함수 수정
회원가입을 하면 바로 로그인되도록 `signup` 함수 수정

### 3. 로그아웃 기능 생성
#### VIEW - `logout` 함수 정의
- 가져온 `auth_logout` 함수로 로그아웃 기능 수행
- `logout as auth_logout` 함수는 HTTP 데코레이터는 붙이지 않는 것이 일반적이다. 함수 자체가 로그아웃을 기능을 하여 보안적으로 안전한 함수이기 때문이다.


### 로그인과 로그아웃의 동작
`/account/login/` URL 요청 후 로그인하면 로그인 상태를 개발자도구/Applications/Cookies 에서 확인 가능
- 로그인을 하면 `Cookies`에 저장되는 것이다!
- `sessionid` 가 로그인 하면 생긴다.
- 개발자도구에서 `sessionid`를 지우면 로그인 상태가 풀린다.
- `sessionid`의 `Cookie Value`에 있는 값이 누가 로그인했는지 저장되어 있는 것

`db.sqlite3` 의 `django_session` 테이블 `session_key` 필드에 `sessionid`의 `Cookie Value`가 저장되어 있다.
- 장고 내부적으로 `Session`이라는 모델이 정의되어 있다. 이 테이블에 적힌 데이터 row에 대해 `get_decode` 하면 로그인한 사용자가 누구인지 알 수 있는 `auth_user_id` 가 나온다.

로그아웃 하면 `sessionid`가 지워지고 DB의 `django_session` 테이블에서도 관련 데이터가 지워진다.

## `base.html` 수정
필요한 기능 추가

if 조건문으로 사용자가 인증했는지 여부로 보여주는 리스트가 다르도록 설정

html에서만 하면 보안상 허점이 발생
함수에도 사용자 인증여부로 접근을 다르게 할 수 있도록 수정 필요


## 로그인 여부로 사용할 수 있는 기능 수정
## VIEW - `create_article` 함수 수정

if 조건문으로 가능하지만 데코레이터로 간편하게 기능 사용 가능
```python
from django.contrib.auth.decorators import login_required
```
- `login_required`

두 개의 데코레이터 작성 순서는 어떤 차이?
- `@login_required`이 먼저 써있을 때 ⇒ 로그인하러 가게 함
- `@require_http_methods(['GET', 'POST'])`이 먼저 써있을 때⇒ 405 method not allowed 에러 발생

`user` 컬럼에 들어갈 데이터를 설정
- `article = form.save(commit=False)` : 폼 저장전에 잠깐 멈춰! 하고
- `article.user = request.user` : user_id 칼럼에 대해 지정해준다
    - `request.user` : 로그인한 객체가 나옴 (로그인 안하면 어나니머스 유저라고 나옴)
    - `@login_required` 으로 이미 로그인 한 사람만 접근할 수 있으니 로그인한 객체가 나옴
- `article.save()` : 저장!

article_update 함수는 따로 user 관련 코드 적을 필요가 없다
이미 article이 처음 생성될 때, `article.user` 가 들어가있음!


## Template `detail.html` 수정
로그인 여부로 보여주기 다르게
+ 게시글 작성자가 누구인지 추가

## VIEW - `create_comment` 함수 수정
`user` 컬럼에 들어갈 데이터를 설정
- `comment.user = request.user` : 댓글을 생성할 사용자 지정
- 
## Template `detail_comment.html` 수정
+ 댓글 작성자가 누구인지 추가

## VIEW - `update_article`, `delete_article`, `delete_comment` 함수 수정
작성자만 작성한 게시글 혹은 댓글을 수정 및 삭제할 수 있도록 함수 수정

## Template `detail.html` 수정

## Template `detail_comment.html` 수정


## 회원 상세조회 - 프로필 페이지
`accounts` App에 사용자의 프로필 페이지 생성

프로필 페이지에 나오는 내용
- 사용자 username
- 사용자가 작성한 게시글들 ( 링크 > 클릭시 해당 글의 detail)
- 사용자가 작성한 댓글들(링크 > 클릭시 댓글이 달린 글의 detail)

### URL Conf
`accounts.urls` 프로필 페이지에 대한 URL 경로, 함수, URL 별칭 지정

### VIEW - `profile` 함수 정의
- `get_user_model` 함수를 실행하면 `User` 모델의 객체를 반환한다. 일반적으로 `User` 모델의 객체를 가져올 때 장고에서 이 방식으로 접근하길 권한다. 
- User는 함수 밖 global scope에 정의하면 다른 함수에서 사용할 수 있다.

사용자 인증 조건 추가
- 사용자가 로그인했으면 로그인/회원가입 GET으로 못가게 설정 View에서 추가
- 현재 Template에만 되있을 것
```python
    if request.user.is_authenticated:
        return redirect('board:article_index')
```
`signup`, `login` 함수에도 동일하게 조건 적용

### Template - `base.html`에서 나의 프로필 추가

### Template - `detail.html`에서 게시글 작성자의 프로필 페이지 연결

### Template - `detail_comment.html`에서 댓글 작성자의 프로필 페이지 연결

