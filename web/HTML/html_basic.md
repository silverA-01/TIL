# HTML basic
## HTML 이란?
Hyper Text Markup Language의 약자로, **웹 페이지를 작성하기 위한 역할 표시 언어**
* `Hyper Text`
  - `hyper`는 초월의, 최고의 의미
  - 하이퍼 텍스트 이전의 텍스트의 상징은 '책'이었다. 원하는 정보를 찾기 위해서 순차적으로 정보를 찾아봐야하는 선형적인 정보 탐색이 필요했다.
    - 선형적 : 일렬로 나열되어 순서가 있음
  - 하이퍼 텍스트는 **하이퍼 링크를 넘나들면서** 원하는 데이터를 찾기 위해 다른 페이지들을 거쳐야 할 필요가 없는 비선형적인 구조를 가지고 있다.
    -` HyperLink` : 하이퍼텍스트 문서 안에서 직접 모든 형식의 자료를 연결하고 가리킬 수 있는 참조 고리 
  - `HTTP(S)` : Hyper Text Transfer Protocol의 약자로, 하이퍼 텍스트를 주고 받는 통신 규약을 의미한다.

* `Markup`
  - '표시'를 뜻하며, 역할을 표시하는 것이 제일 핵심 기능이다.
    - ex. 큰 제목, 작은 제목, 본문, 순서가 있는 리스트, 하위 리스트 등
  - `Markdown`은 `Markup`에서 파생된 것으로 옛날에 만들어진 `Markup`을 개선해서 만든 것이다. 

* `Language`
  - '언어'를 뜻하며, 특정한 약속이 정해져있다는 것을 알 수 있다.

### HTML을 배우는 이유
Web Service를 만드는 것은 서버 컴퓨터에서 요청(request)와 응답(response)을 처리할 프로그램을 개발한다는 것과 같은 의미이다. Web Service에서 요청에 대해 응답으로 주는 것이 `HTML`이기 때문에 `HTML`을 선행적으로 배울 필요가 있다.


## HTML의 기본 구조
### HTML의 기본 단위 - HTML 태그(tag)
태그는 HTML 요소(element)라고도 부르며, HTML 문서를 구성하는 기본 단위이다.
- `<>`(오프닝태그) `</>`(클로징태그) 형태
  - 클로징태그가 없는 태그도 존재한다.
- `<!-- -->` : 주석(comment)을 정의한다.
   - VScode에서 `Ctrl` + `/`로 간편하게 주석 태그를 입력할 수 있다.


### HTML 기본 구조 작성
1. HTML 파일 생성
   - `01_html_basic.html` 파일을 특정 폴더에 만들어준다.
   
2. 아래와 같이 HTML의 기본적인 구조를 태그를 통해 작성해준다.
    
   1. `<!DOCTYPE>` : 해당 문서(document)의 타입을 정의한다. `<!DOCTYPE html>`는 해당 문서가 html 타입이라는 의미이다.
   2. `<html>` : HTML 문서의 루트 요소(root element)를 정의한다. 
      - `<html>` `</html>` 사이에 모든 문서 내용이 들어가야 한다. 
   3. `<head>` : 해당 문서에 대한 정보인 메타데이터(metadata)의 집합을 정의한다.
      - 메타데이터 : 데이터의 데이터 (ex.핸드폰 사진이라는 데이터 안에는 촬영된 시간, 날짜, 장소 등의 메타데이터가 포함) 
   4. `<body>` : 해당 문서의 내용/콘텐츠 영역을 정의한다.
```html
<!DOCTYPE html>

<html>
    <head>
    </head>
    <body>
    </body>
</html>
```
3. VScode에서 `!` + `Tab`으로 위 HTML 기본구조가 적힌 코드를 자동생성할 수 있다.
> - VScode와 다른 에디터에는 `Emmet`(에밋) 이라는 플러그인이 기본적으로 설치되어 있다.에밋은 기본구조를 자동 생성해준다. 에밋은 HTML과 CSS의 작성의 시간을 아주 빠르게 단축 시켜주는 에디터 확장기능으로 타이핑 몇자를 적으면 자동으로 나머지 코드들을 자동생성해주는 기능이다.
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
* `<html lang>` : HTML 문서에 관련 언어를 지정하는 속성
  - 웹접근성 차원에서, 검색엔진 및 브라우저를 지원하는 목적 등으로 사용한다. 
  - ex. lang 설정과 크롬 브라우저 언어 설정이 다른 경우, 크롬자동번역 인터페이스가 뜨도록 설정되어 있다.
  - `<html lang="en">` : 영어로 HTML 문서 관련 언어 지정
  - `<html lang="ko">` : 한국어로 HTML 문서 관련 언어 지정

* `<head>` 태그에 들어갈 메타데이터와 관련된 `<meta>` 태그
   - `<meta charset>` :  HTML 문서의 문자 인코딩 방식을 명시. 
     - `<meta charset="UTF-8">` : HTML 문서의 문자 인코딩 방식을 유니코드(Unicode)를 위한 문자셋인 `UTF-8`으로 지정
       - HTML의 문자 인코딩 방식으로 `UTF-8`를 가장 많이 사용된다.
       - 참고로, HTML에서는 반드시 `"`(쌍따옴표)를 사용해야 한다. 
         - `"`(쌍따옴표)가 `'`(작은따옴표)와 호환되지 않기 때문에 주의해야 한다.
   - `<meta name="viewport" content="width=device-width, initial-scale=1.0">` : 화면에서 표시될 기본적인 정보에 대해 지정하는 부분이다.
   - `<title>` : HTML 문서의 제목이다. HTML 문서를 웹 브라우저로 열었을 때 Tab 제목으로 표시된다. 문서 내용은 `<body>` 부분이 들어가기 때문에 문서상에 표시되지 않는다.

* `<body>` `</body>` 사이에 들어가는 내용은 실제 문서에 표시되는 부분이다.


## Heading(제목) 관련 태그
```html
<body>
    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <h3>Heading 3</h3>
    <h4>Heading 4</h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>
</body>
```
- `<h#>` (`<h1>` ~ `<h6>`) : 제목을 지정하는 태그 
  - h1이 가장 크며 h6이 가장 작음
  - 사용표준에 따라 상위 태그부터 순차적으로 사용하는 것이 바람직하다.

## `<BODY>` 관련 태그
### 스타일링 및 강조
```html
<strong>강조1</strong>
<em>강조2</em>

<b>굵게</b>
<i>이탤릭체</i>
```
* 스타일링 태그
  - `<b>` 태그 : 텍스트를 굵게 한다.(bold)
  - `<i>` 태그 : 텍스트를 기울게 한다.(italic)

* 강조 태그
  - `<strong>` 태그 : 텍스트를 굵게 보여줘 강조한다.
  - `<em>` 태그 : 텍스트를 기울게하여 강조한다.(emphasize)
  - 보여지는 것은 `<b>`태그, `<i>` 태그와 같지만 텍스트를 강조하는 역할로 쓰였다는 점에 차이가 있다.

### white space 관련
```html
줄 바꿈 전 텍스트 작성<br>줄 바꿈 후 텍스트 작성
```
* `<br>` 태그 : 텍스트 줄 바꿈을 설정(Line Breaks)
  - 기본적으로 HTML은 코드 가독성 향상을 위해 줄 바꿈을 해도 줄 바꿈이 화면에 출력되지 X
  - 닫는 태그가 없음
```html
<pre>
줄 바꿈 태그 없이도 줄 바꿈 및 띄어쓰기
탭    과 같은 white space들이 그대로      출력됩니다.
</pre>
```
* `<pre>` 태그는 공백을 설정
  - 줄 바꿈 뿐만 아니라 띄어쓰기, 탭 등 원래 무시되던 문자(white space)들이 그대로 출력
  - 즉, 입력하는 내용 그대로 표현된다.

### 하이퍼링크 연결
```html
<!-- 새 탭으로 상대 주소(relative URL)가 연결되는 동작 -->
<a href="/product/details.html" target="_blank">
```
* `<a>` 태그 : 하이퍼링크 URL 연결하는 태그
  - `href`: 클릭시 이동 할 링크
  - `target`: 링크를 여는 방법
    - `_self`: 현재 페이지 (기본값)
    - `_blank`: 새 탭
    - `_parent`: 부모 페이지로, iframe 등이 사용된 환경에서 쓰입니다.
    - `_top`: 최상위 페이지로, iframe 등이 사용된 환경에서 쓰입니다.
    - `*프레임이름*`: 직접 프레임이름을 명시해서 사용할 수도 있습니다.

### 블락(`block`) 요소
* `<p>` 태그 : 하나의 문단/단락을 나타내는 태그 (Paragraphs)
  - `<p>` ~ `</p>` 태그 사이에 텍스트를 입력하면, 입력한 내용 앞뒤로 빈 줄이 생기면서 텍스트 단락이 생성됨
  - 줄 바꿈이 없는 텍스트 단락은 화면 너비를 넘어갈 경우 자동으로 아래 줄로 넘겨 표시 됨
  - html 코드 상에서 white space(띄어 쓰기, 줄 바꿈)은 한 칸씩 밖에 적용되지 않는다. 따라서 `<p>` 태그 내부에서 엔터나 띄어쓰기를 사용해도 무조건 한 줄로 표현된다.
  - 내부에 `<div>`와 같은 다른 블록 요소 포함할 수 X

```html
<div style="strong">구역1</div>
<div>구역2</div>
```
* `<div>` 태그 : HTML 문서를 구획으로 나누는 데 사용되는 기본적인 태그 (Division)
  - 특별한 기능을 가지고 있지는 않고, 레이아웃(블록이나 구획)을 만들거나 콘텐츠를 나누는(division) 컨테이너로 사용한다.
  - 줄 바꿈 가능 : `display` 속성이 `block` 
  - 레이아웃(블록이나 구획)을 구성하거나 그룹화된 마크업이나 콘텐츠에 스타일이나 자바스크립트를 적용하기 위한 컨테이너나, HTML 속성을 적용하기 위한 범위를 나타내기 위한 컨테이너로 사용
  - `<p>`와 같은 다른 블록 요소 포함 가능

### 인라인(`inline`) 요소
```html
<p>
    빛의 삼원색은
    <span style="color: red;">빨강</span>,
    <span style="color: green;">초록</span>,
    <span style="color: blue;">파랑</span>으로
    구성되어 있습니다.
</p>
```
* `<span>` 태그 : 자체적으로 특별한 의미가 전혀 없는 인라인 컨테이너
  - 단순 텍스트나 인라인 콘텐츠 등에 스타일이나 속성, 스크립트를 위한 범위를 위해 감싸주는 태그
  - 줄 바꿈 불가능 : `<div>` 태그와 달리, `display` 속성이 `inline` 
  - CSS 적용, HTML 속성 적용, JavaScript에서 **특정 부분**을 선택하거나 조작하는 데 주로 사용
  - 단순 텍스트나 텍스트에 관련된 마크업 등 구문 콘텐츠에 스타일이나 자바스크립트를 적용하기 위한 범위를 감싸주거나, HTML 속성을 적용하기 위한 범위를 감싸주기 위해 사용

### 목록
```html
<ul>
  <li>목록1</li>
  <li>목록2</li>
  <ol>
    <li>목록2-1</li>
    <li>목록2-2</li>
  </ol>
</ul>
```
* `<ul>` 태그 : 순서가 없는 목록을 나타내는 태그 (unordered list)
* `<ol>` 태그 : 번호를 메겨 순서가 있는 목록을 나타내는 태그 (ordered list)
* `<li>` 태그 : 목록 항목을 나타내는 태그 (list)
  - 단순히 리스트 나열 뿐만 아니라 메뉴등을 만들때도 사용
  - `<ul>`, `<ol>` 태그 내부에 들어가서 사용된다.

### 입력 양식
```html
<form name="LoginForm" action="/user/login.html" method="POST">
  <div class="loginform">
    <label for="user-id">아이디</label>
    <input type="text" id="user-id" name="user-id" placehold="아이디를 입력하세요" required>
  </div>
  <div class="loginform">>
    <div>패스워드</div>
    <input type="password" id="user-password" name="user-password" placehold="비밀번호를 입력하세요" required>
  </div>
  <div>
    <button type="submit">LOGIN</button>
  </div>
</form>
```
* `<form>` 태그 : 웹 페이지에서의 입력 양식을 나타내는 태그로 전체 양식을 의미하며, 화면에 보이지 않는 추상적인 태그
  - `name`: 폼의 이름
  - `action`: 폼 데이터가 전송되는 백엔드 url
  - `method`: 폼 전송 방식 (GET / POST)

* `<input>` 태그 : 실제로 사용자가 양식을 입력하기 위한 태그
  - `<type>` : 속성 값
    - `text`: 일반 문자
    - `password`: 비밀번호
    - `button`: 버튼
    - `submit`: 양식 제출용 버튼
    - `reset`: 양식 초기화용 버튼
    - `radio`: 한개만 선택할 수 있는 컴포넌트
    - `checkbox`: 다수를 선택할 수 있는 컴포넌트
    - `file`: 파일 업로드
    - `hidden`: 사용자에게 보이지 않는 숨은 요소
  - `name` : 관련 데이터 이름
  - `value` : 기본값 지정
  - `placehold` : 입력 필드에 사용자가 적절한 값을 입력할 수 있도록 도와주는 짧은 도움말을 명시

* `<button>` 태그 : 내용물에 의해 레이블이 지정된 버튼을 나타낸다.
  - 웹 페이지에 사용자가 클릭할 수 있는 버튼을 만들고, 버튼 안에 포함된 텍스트나 이미지가 버튼의 기능을 표현
  - `<type>` : 속성 값
    - `submit` : 양식(`form`) 제출 버튼. 이 버튼을 클릭하면 해당 요소가 포함되어 있는 양식의 모든 컨트롤의 값을 제출한다.(기본 값)
      - 컨트롤 : 사용자가 웹 페이지와 상호작용할 수 있도록 하는 요소
        - `<input>`, `<textarea>`, `<select>`등 사용자가 데이터를 입력하고, 선택하고, 제출하는 등의 작업을 할 수 있는 요소들이 해당
    - `reset` : 양식(`form`) 초기화 버튼. 이 버튼을 클릭하면 해당 요소가 포함되어 있는 양식의 모든 컨트롤의 값을 초기화한다. 
    - `button` : 기본 동작이 없는 일반 버튼 유형의 컨트롤을 나타냄. 
      - 주로 JavaScript와 함께 사용하여 사용자가 클릭하면 다양한 동작을 컨트롤할 목적으로 이 버튼이 사용
      - 클라이언트측 스크립트와 연결해서 사용

```html
<form>
  <div>
    <label for="user-color" style="display: block;">색상 선택</label>
    <select id="user-color" required>
        <option value="" disabled selected>좋아하는 색상 선택</option>
        <option value="red">빨강</option>
        <option value="blue">파랑</option>
        <option value="yellow">노랑</option>
        <option value="green">초록</option>
    </select>
  </div>
  <div>
    <button type="submit">제출</button>
  </div>
</form>
```
* `<select>` 태그 : 옵션 메뉴를 제공하는 컨트롤(드롭다운 목록 or 셀렉트 박스)
  - 사용자가 원하는 옵션을 선택할 수 있는 방법
  - `<option>` 태그 : `<select>` 태그 내에서 각각의 옵션을 나타낸다.

* `<textarea>` 태그 : 여러 줄로 된 **텍스트** 입력 필드를 나타내는 태그
  - 사용자가 댓글 작성, 리뷰 작성, 간단한 메모 작성, 소스 코드 입력 등 여러 줄의 일반 텍스트를 쉽게 입력할 수 있도록 하는 데 유용
  -`value` 속성을 지원하지 X : 기본값을 지정하려면 콘텐츠에 직접 삽입하면 된다.