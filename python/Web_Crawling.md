# 크롤링 (Crawling)
web에서 필요한 data를 가져오는 것.

웹페이지를 그대로 가져와서 거기서 데이터를 추출해 내는 행위.

본래 무수히 많은 컴퓨터에 나누어져 저장되어 있는 문서를 수집해, 검색 대상의 색인으로 포함시키는 기술을 말한다. **보통 웹페이지의 내용을 그대로 복제한 뒤 필요한 데이터를 추출하는 행위를 일컬으며** 웹(web)크롤링, 스크래핑(scraping)이라고도 한다.

> ※ 크롤링을 하는 프로그램 - 크롤러(crwler) or 스파이더(spider)라고 한다.

## 크롤링 전 VSCODE에서 Python 파일 생성 및 라이브러리 설치

1. Home dir에 KDT-DATA-33 dir 생성 후 VSCODE로 폴더 열기
   ```bash
    cd ~
    mkdir KDT-DATA-33
    cd KDT-DATA-33
    code .
    ``` 
2. VSCODE 터미널 열기
   > Ctrl + ` 
3. 터미널에서 KDT-DATA-33 dir에 python-starter dir 생성
   ```bash
   mkdir python-starter
   ``` 
4. python-starter dir에 kospi.py 새 파일 생성
   ```bash
   touch kospi.py
   ``` 
5. 터미널에서 다음을 실행 - 파이썬 라이브러리 설치
   ```bash
   pip install requests beautifulsoup4
   ``` 
   > `pip install` : 외부에서 추가적으로 도구를 가져와 설치하는 것
6. kospi.py에서 설치한 파이썬 라이브러리 requests, BeautifulSoup 불러오기
   ```python
   import requests
   from bs4 import BeaurifulSoup
   ``` 

## 크롤링 실습
> **[실습 예제]**
> 
> Naver 증권에 접속하여 전체 페이지를 다운 받는다.
>
> KOSPI 현재 지수 데이터를 찾아 낸다.
> 
> 찾은 데이터를 출력한다.

### 1. 페이지 소스보기를 통해 직접 데이터를 찾는 방법
1. Naver 증권에 접속하여 전체 페이지를 다운 받는다.
   1. [Naver 증권 사이트](https://finance.naver.com/sise/) 국내 증권 페이지 접속
   2. 페이지 소스 보기
      1. `페이지 우클릭 > 페이지 소스 보기 선택`
      2. 페이지 내에서 `Ctrl + u`
   3. 페이지 소스 문서를 다운로드 or 복사한다.
2. KOSPI 현재 지수 데이터를 찾아 낸다.
   1. 가져온 페이지 소스 data에서 `Ctrl+F` 기능을 이용해  `코스피` 단어를 찾아준다.
   2. 코스피 현재 지수가 적혀져 있는 라인을 찾는다.
3. 찾은 데이터를 출력한다.
   - KOSPI 현재 지수 > 2,506.19

> 하지만, 파이썬을 이용해 원하는 데이터를 좀 더 효율적으로 찾는 방법을 아래에서 알아보자.

### 2. 파이썬 라이브러리를 이용해 원하는 데이터 출력
1. Naver 증권에 접속하여 전체 페이지를 다운받는다.
   1. requests 라이브러리가 URL을 요청하여 브라우저에 접속하는 역할을 해주고 있다.
   ```python
   URL = 'https://finance.naver.com/sise/'
   page = requests.get(URL)
   ```
   2. 아래 코드로 URL page가 잘들어왔는지 확인한다.
    ```python
    print(page)
    ```
   3. 파이썬 실행
     - 실행버튼 아이콘을 누른다(재생버튼 모양)
    - or
     - 터미널에서 `python-starter` dir 경로에서 아래 code를 입력한다.
     ```python
     cd python-starter
    python kospi.py
     ``` 
   4. 파이썬을 실행하면 <Response [200]> 라고 오류가 뜬다. `print(page)`를 `print(page.text)`로 바꾼 후 저장하고 다시 파이썬을 실행한다.
      > text가 page에서 텍스트로 된 부분만 가져와준다. text는 핵심 본문과 관련된 뜻에 가깝다.
      ```python
      print(page.text)
      ``` 
   5. 파이썬을 실행하면 URL이 담긴 `page.text`가 성공적으로 불러와지는 것을 확인할 수 있다. `print(page.text)`는 확인용이기 때문에 지우거나 주석으로 바꿔준다.
      ```python
      import reqeusts
      from bs4 import BeautifulSoup

      URL = 'https://finance.naver.com/sise/'

      page = requests.get(URL)
      ```
 
2. Parsing (파씽_구문분석/해석)
   > BeautifulSoup 라이브러리를 이용해 `page.text`를 parsing 작업된 data로 만들어준다.
   ```python
   data = BeautifulSoup(page.text, 'html.parser')
   ``` 
   ※ 엄연히 BeautifulSoup 라이브러리는 크롤링보다 추출과 관련된 '스크랩핑'의 영역이다.
3. KOSPI 현재 지수 데이터를 찾아낸다.
    1. 국내 증권 페이지인 `URL`을 크롬 브라우저에서 열어준다.
    2. 해당 페이지에서 `F12`를 누르면 개발자도구(DevTool) 창이 나타난다.
    3. Inspector 아이콘을 누르고, 원하는 데이터 값(코스피지수가 나타난 숫자)을 페이지에서 선택하면 개발자 도구 창에 선택한 데이터가 작성된 코드 라인이 표시된다.
        ![DevTool_Inspector](https://postfiles.pstatic.net/MjAyMzEyMDZfMzIg/MDAxNzAxODczMDc3OTI0.ZAsmY64oRpVbBRovDKoL-BuHnl3ThpK4eUgQ8fDFB5Ig.5KcfZvLAyKSHMNZvh0SB3ZpJcqMy4PN9QZoiMtJStLcg.PNG.mita_02/devtool.png?type=w773) 
    4. 표시된 라인 우클릭 > copy > copy selector 
    5. 복사한 값을 붙여 넣으면 `#KOSPI_now`가 나오는 것을 확인할 수 있다. 아래 코드에 값을 넣어준다.
       > `kospi`를 아까 parsing 작업을 한 `data`에서 `#KOSPI_now` 만 선택한 값으로 지정한 것이다.
        ```python
        kospi = data.select_one('#KOSPI_now')
        ```
    6. `kospi`를 출력한다는 code 작성 후 파이썬을 실행한다.
       ```python
       print(kospi)
       ``` 
       
       > 실행 성공시 KOSPI 현재 지수가 표시 된다.

       > 필요한 2,506.73 데이터 외에 다른 데이터도 같이 보이기 때문에 7번 작업을 진행한다.
       >
       > ※참고 : 2,506.73라는 값은 KOSPI 현재 지수이기 때문에 계속 바뀌기 때문에 다른 값이 나올 수 있다.
    7. 필요한 데이터만 보기 위해 `print(kospi)`를 `print(kospi.text)`로 수정한다. 최종적으로 사용한 파이썬 코드는 아래와 같다.
        ```python
        import requests
        from bs4 import BeautifulSoup

        URL = 'https://finance.naver.com/sise/'

        page = requests.get(URL)

        data = BeautifulSoup(page.text, 'html.parser')

        kospi = data.select_one('#KOSPI_now')

        print(kospi.text)
        ```
        터미널에 `python kospi.py`를 실행하면 KOSPI 실시간 현재 지수가 표시된다.
        
        ```
        2,506.73
        ```
        > [참고1] 현재 지수는 실시간이라 값이 계속 변한다.
        > 
        > [참고2] 출력된 2,506.73은 숫자형 데이터처럼 보이지만, 문자형 데이터이다. 보이지 않지만 ' '안에 들어간 문자. 숫자형 데이터에는 ',' 기호가 들어가지 않는다.

## 파이썬이란?
파이썬(Python)은 컴퓨터 프로그래밍 언어이다. 컴퓨터는 계산기라고 할 수 있고, 프로그래밍은 일(작업)을 시키는 것을 의미하며, 언어는 모두가 사용할 수 있도록 약속하는 것이다.

즉, 파이썬은 컴퓨터에게 작업을 시키는 언어라고 할 수 있다.

## 파이썬을 이용해 웹브라우저 열기
### 1. 웹브라우저 열기
파이썬이 자체적으로 가지고 있는 도구인, webbrowser을 활용해 웹브라우저를 열 수 있다.

1. 열고 싶은 웹브라우저 URL 주소를 가져온다.
2. URL 주소를 (' ')안에 넣어준다.
   ```python
   webbrowser.open('https://www.google.com/finance/quote/NVDA:NASDAQ')
   ``` 
3. 파이썬 실행하면 웹브라우저가 열린다.

### 2. 여러 개의 브라우저를 동시에 열고 싶을 때
1. 아래와 같은 명령어를 반복해서 작성하고 파이썬을 실행해주면 여러 브라우저가 동시에 열린다. 
```python
webbrowser.open('https://www.google.com/finance/quote/NVDA:NASDAQ')
webbrowser.open('https://www.google.com/finance/quote/APPL:NASDAQ')
webbrowser.open('https://www.google.com/finance/quote/TSLA:BMV')
```
2. 1번과 같은 방법보다 더 깔끔하고 효율적으로 코드를 작성할 수 도 있다.
```python
import webbrowser

urls = [
    'https://www.google.com/finance/quote/NVDA:NASDAQ'
    'https://www.google.com/finance/quote/APPL:NASDAQ'
    'https://www.google.com/finance/quote/TSLA:BMV'
]
for url in urls:
    webbrowser.open(url)
```
3. 2번보다 더 깔끔하고 효율적으로 코드를 작성할 수 도 있다.
```python
import webbrowser

tickers = [
    'NVDA:NASDAQ', 
    'APPL:NASDAQ',
    'TSLA:BMV',
]
for tick in tickers:
    url = 'https://www.google.com/finance/quote/' + tick
    webbrowser.open(url)
```

> 1, 2, 3번 모두 같은 결과가 나타나지만, 좋은 개발자는 더 깔끔하고 효율적으로 코드를 짤 수 있어야 한다.
>
## API
- API는 두 소프트웨어 구성 요소가 **서로 통신**할 수 있게 하는 메커니즘이다.
- Application Programming Interface(애플리케이션 프로그래밍 인터페이스)의 줄임말
- API의 맥락에서 애플리케이션(Application)은 고유한 기능을 가진 모든 소프트웨어를 지칭
- 인터페이스(Interface)는 두 애플리케이션이 서비스와 관련된 요청과 응답을 사용하여 서로 통신하는 방법, 접점을 의미
- API의 구조는 클라이언트와 서버 측면에서 설명된다.
  
### Web의 법칙
| WHO | WHAT | HOW |
|---|---|---|
|클라이언트(Client)가|요청(request)을|URL로 보내고|
|서버(Server)는|응답(response)을|문서로 보낸다.|

- 클라이언트와 서버는 고정된 개념이 아니라 요청을 한 주체와 요청에 응답해야하는 주체로 정해진다. 다시 말해 클라이언트이기 때문에 요청을 보낸 것이 아니라, 요청을 보냈기 때문에 클라이언트라고 부를 수 있는 것이다.

> 같은 개념으로, 가장 유명한 (요청을 보내기 위해 사용하는) 클라이언트 프로그램은 브라우저이다. 브라우저를 대체해서 위에서 사용한 라이브러리는 `requests`이다. `requests`로 URL을 요청했기 때문에, 아래의 `page = requests.get(URL)` 코드 전체가 클라이언트의 역할을 하게 되는 것이다. 위의 웹 크롤링 예제에서는, URL과 관련된 네이버 증권 서버에 요청(request)해 응답(response)된 문서를 받은 것이다.
```python
URL = pass
page = requests.get(URL)
```

### API를 이용한 웹 크롤링
동행복권 서버 웹 API URL을 이용해 다음과 같은 데이터를 크롤링할 것이다.
- 로또 1등 총 당첨금(금액만)

1. requests 라이브러리로 브라우저를 대체한다. 동행복권 Server에 필요한 문서를 요청하는 클라이언트 역할을 한다.
```python
import requests

# URL 주소는 필요한 데이터가 담긴 동행복권 서버의 웹 API
URL = 'https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=1096'

data = requests.get(URL).json()
```
2. URL로 요청한 `data`가 어떤 데이터 타입인지 출력해보니 딕셔너리라는 것을 알 수 있다. 딕셔너리는 {key1: value1, key2: value2, ...} key와 value로 이루어진 컨테이너형 자료구조이다.
```
# URL로 요청한 'data'가 어떤 데이터 타입인지 확인해보자.
print(type(data)) 
```
```
<class 'dict'> 
```
3. 확인을 위한 `print(type(data))` 코드는 지우거나 주석으로 바꿔준다. `data` 중 필요한 데이터만 추출하기 위해 필요한 key 값을 찾아 추출해준다. 필요한 데이터의 key 값은 `'firstWinamnt'`이다. 
```python
print(data['firstWinamnt'])
```
```
2539391175
```
4. 최종적으로 1등 총 당첨금을 뽑기 위해 사용한 코드는 아래와 같다
```python
URL = 'https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=1096'

data = requests.get(URL).json()

print(data['firstWinamnt'])
```
KOSPI 지수는 `GUI`와 관련된 URL에서 데이터를 추출했다면, 로또 1등 총 당첨금은 동행복권 서버의 웹 `API`와 관련된 URL에서 데이터를 추출했다. 후자인 `API`를 이용할 때, 훨씬 효율적으로 데이터를 가져올 수 있다. 더 단축된 코드를 사용했고 가져오는 데이터의 양도 `GUI`보다 `API`가 적기 때문에 URL을 요청해서 문서를 응답받는 속도도 빠르다. 때문에 개발자는 `API`를 이용해 크롤링하는 것이 더 효율적이라고 할 수 있다.