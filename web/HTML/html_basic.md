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
       - 참고로, HTML에서는 `"`(쌍따옴표)가 `'`(작은따옴표)와 호환되지 않기 때문에 주의해야 한다.
   - `<meta name="viewport" content="width=device-width, initial-scale=1.0">` : 화면에서 표시될 기본적인 정보에 대해 지정하는 부분이다.
   - `<title>` : HTML 문서의 제목이다. HTML 문서를 웹 브라우저로 열었을 때 Tab 제목으로 표시된다. 문서 내용은 `<body>` 부분이 들어가기 때문에 문서상에 표시되지 않는다.

* `<body>` `</body>` 사이에 들어가는 내용은 실제 문서에 표시되는 부분이다.

## Heading 관련 태그

## `<BODY>` 관련 태그
1. `<p>`
2. ㅇㄹㅇ
3. <pre>