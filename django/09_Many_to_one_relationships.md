# 1:N 관계
1:N 관계가 뭔지 설명

# `board.models` - `Comment` 모델 정의
`board.models`에서 `Article` 모델과 `Comment` 모델의 관계가 1:N인 `Comment` 모델을 정의한다.
```python
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.CharFields(max_length=200)
```
- `article` 필드를 `Article` 모델을 참조하는 FK로 설정
  - `ForeignKey`는 반드시 `on_delete`를 인자로 받는다.
  - `CASCADE`로 설정 : 참조하는 Article의 데이터 레코드가 수정 및 삭제될 때 `Comment`모델에서 참조중인 데이터 레코드도 수정 및 삭제 

# `Comment` 모델 마이그레이션
`Comment` 모델을 DB 테이블에 매핑될 수 있도록 마이그레이션한다.
```bash
$ python manage.py makemigrations board

$ python manage.py migrate board
```

## DB에서 확인
- `board_commnet` 테이블이 생성됨
- FK로 만든 필드가 `article_id` 필드로 생성된 것을 확인

# 1:N 관계에서 데이터 생성
터미널을 `shell_plus`로 열기

1:M 관계에서 N인 `Comment` 모델의 인스턴스 생성


```shell
IntegrityError: NOT NULL constraint failed: board_comment.article_id
```
- FK인 `article` 필드값을 지정하지 않고 `save()` 메서드로 저장하면 에러 발생
- DB에 `article_id` 필드에 들어갈 데이터가 없기 때문에 에러 발생
  
모델의 인스턴스의 FK 필드를 의미하는 변수는 정확히 `article`이다. 하지만 DB의 필드로 생성된 `article_id`로 변수를 사용해도 장고에서 `article`로 이해하고 처리해준다. 하지만 DB의 필드인 `article_id` 변수는 장고의 파이썬상에서 존재하지 않는 변수이기 때문에 `article`을 사용하는 것을 권장한다.

# 1:N 관계에서 데이터 조회
- 한 가지 객체를 반환할 때는 `get()`메서드를 사용하고, 여러 가지 객체를 반환할 때는 `filter()` 메서드를 사용한다.
1:N 관계에서 1이 소유한 N을 조회하는 방법
```python
<N에해당하는모델명의소문자>_set
```

## 특정 FK를 가지는 N 모델의 모든 객체 조회
```shell
in : a1 = Article.objects.get(pk=1)

in : a1.comment_set
out : 어찌구저찌구

in : a1.comment_set.all()
out : 어찌구저찌구
```

## 특정 FK를 가지는 N 모델의 특정 필드값 조회
```shell
in : a1 = Article.objects.get(pk=1)

in : for c in a1.comment_set.all():
        c.content
```
- for 문으로 `Article` 모델에 특정한 조건의 인스턴스를 FK로 가지는 모든 `Comment`모델 객체의 필드값을 조회할 수 있다.

## N 모델이 소속된 1 모델을 조회
```shell
in : c1 = Comment.objects.get(pk=1)

in : c1.article
out : 해당 아티클 객체 뱉
```

## N 모델이 소속된 1 모델의 특정 필드값 조회
```shell
in : c1 = Comment.objects.get(pk=1)

in : c1.article.title
out : 해당 아티클 객체의 title 필드값 뱉
```

1:N 관계에서 데이터를 조회하는 방법을 참고해, 모델과 마찬가지로 특정한 조건의 데이터 객체의 필드에 접근해 데이터를 수정 및 삭제할 수 있다.

# 댓글 입력창 만들기
## `Comment` 모델의 ModelForm 생성
`board.forms`에서 `CommentForm` 생성

## URL Conf
`board.urls`에서 댓글 생성할 수 있는 URL 경로, 함수, URL 별칭을 작성한다.

## View - `create_comment` 함수 정의
`create_article`함수와 유사하게 HTTP request method와 사용자 입력 데이터 유효성 검사를 조건문으로 작성한다.

## Template - `detail.html` 수정
`board/templates/board/` 경로의 `detail.html` 문서에 댓글입력창을 `<form>`으로 생성한다.

### `include` DTL 태그 이용하기
`detail_commnet.html`을 `detail.html`의 부품으로 만들기
- 복잡한 HTML 문서를 보기 편하게 정리할 수 있다.
- 하나의 HTML 문서에 너무 많은 내용이 들어있으면 나중에 문제가 발생할 수 있기 때문에 특정 코드를 부품으로 만들고 `include`를 활용해 연결한다.

같은 경로에서 `detail_commnet.html`을 생성해서 `detail.html`에서 댓글 입력창과 관련된 코드를 복사해 넣는다.


`detail.html`에서는 `{% include "board/detail_comment.html" %}`로 `detail_commnet.html`을 연결해준다.

## 브라우저에서 확인
FK인 `article` 필드의 필드값에 들어갈 데이터가 없어서 오류 발생
함수 수정

## View - `create_comment` 함수 수정
- `article`인스턴스 생성
- `comment`가 `article` 인스턴스를 활용해 해당 `Comment` 모델의 FK인 `article` 필드값에 접근
- `save(commit=False)` 활용
  - `comment` 인스턴스의 내용을 form에 채우되 저장 직전에 멈추라는 의미
  - `save()`sms `save(commit=True)`가 기본값으로 설정되어 있어 저장된다.
  - `comment.article = article` : FK인 `article` 필드의 필드값에 들어갈 데이터에 들어갈 값을 설정

## Template - `detail_comment.html` 수정
`index.html`처럼 for문을 활용해 해당 게시물에 관련된 모든 댓글이 보이도록 수정한다.

파이썬에선 `set.all()`로 작성했지만 DTL에서는 괄호를 지원하지 않기 때문에 `{% for comment in article.comment_set.all %}`으로 작성한다.
- `article.comment_set.all` :  해당 `article` 객체를 FK로 가지고 있는 모든 `comment` 객체를 조회
- `{{ comment.content }} ` : for문으로 순회하여 해당 게시글의 모든 `Comment` 모델의 `content` 필드값을 리스트로 보여준다.

## 브라우저에서 확인
잘 생성되나유?

# 댓글 삭제버튼 추가
각 댓글에는 해당 댓글을 삭제할 수 있는 삭제버튼이 있고, 삭제 버튼을 클릭 시 해당 댓글이 달린 게시글 상세페이지로 재요청(`redirect`)되도록 작성한다.

## URL Conf 

## VIEW - `delete_comment` 함수 정의

## Template - `detail_comment.html` 수정
- `<form>` 태그 안에 `<button>` 태그로 댓글 삭제버튼 생성
- POST 방식
  - 보안상의 이유로 `{% csrf_token %}` 들어가야 한다.
-  `<button>` 태그 클릭시 확인 메세지가 뜨도록 설정
-  `style="display: inline-block;`
   -  `<form>` 태그에 `style`속성은 CSS 옵션으로 댓글의 내용과 삭제버튼을 한줄로 만들어 주었다.
  
## 서버 및 DB에서 확인
잘 지워지나유?
