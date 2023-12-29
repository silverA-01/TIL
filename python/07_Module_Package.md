# 모듈(Module)
1. 모듈 : 특정 기능을 .py 파일 단위로 작성하는 것으로, python 파일을 모듈이라고 한다.
2. 패키지 : 특정 기능과 관련된 여러 **모듈들의 집합**
   -  패키지 안에는 또 다른 서브 패키지를 포함 가능
   -  패키지는 파이썬 파일들이 모여있는 폴더의 개념으로 이해
3. 파이썬 표준 라이브러리(PSL) : 파이썬에 **기본적으로 설치된 모듈과 내장함수**를 묶어서 PSL(Python Standard Library)라 불림
   - ex. 내장함수 :  print(), set(), int() 등 
4. 패키지 관리자(pip) : `PyPI`에 저장된 외부 패키지들을 설치하도록 도와주는 패키지
   -  ex. 외부 패키지 : requests(), beautifulSoup() 

## 모듈(Module)
특정 기능을 하는 코드가 담긴 파일(.py) 또는 스크립트

### 1. 모듈 생성
특정한 기능을 가진 코드를 `.py` 확장자에 저장
```python
# 'new_module.py' 라는 파이썬 파일을 만든다.
# 'new_module.py'에 아래와 같이 함수 odd와 even을 정의한다.

# 정수를 확인하여 홀수이면 True를 반환, 짝수이면 False를 반환하는 함수 odd 정의
def odd(n):
   return bool(n % 2)

# 정수를 확인하여 짝수이면 True를 반환, 홀수이면 False를 반환하는 함수 even 정의
def even(n):
   return not bool(n % 2)

# 함수를 정의 후 파일을 저장한다.
```

### 2. 모듈 활용/불러오기 - `import`
모듈을 활용하기 위해서는 반드시 `import`문을 통해 내장 모듈을 이름공간으로 가져와야 한다.
1. 모듈 불러오기
```python
import <module>
```
2. 모듈 내의 특정한 데이터(함수, 클래스 등)을 가져오기
```python
from <module> import <var>, <function>, <Class>
```
3. 모듈 내부에 있는 모든 것을 가져오기
```python
from <module> import * 
```
> 아래 코드에서 `.odd()`는 모듈명 뒤에 붙었기 때문에 메서드로 보지 않고, 모듈이 가지고 있는 함수라는 것을 알 수 있다.
```python
# 'new_module.py`이 아닌 파일에서 'new_module'이라는 내장 모듈을 가져오려고 한다.
import new_module

new_module.odd(10), new_module.even(10)
```
```
(False, True)
```
- `dir()` 함수로 특정 모듈 안에 들어있는 내용 속성들을 확인할 수 있다.
> 함수 odd와 even이 있는 것을 확인할 수 있다.
```python
dir(new_module)
```
```
['__builtins__',
 '__cached__',
 '__doc__',
 '__file__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 'even',
 'odd']
```

## 패키지(Package)
- 특정 기능과 관련된 여러 **모듈들의 집합**
- 패키지 안에는 또다른 서브 패키지를 포함 할 수도 있다.
- 점(`.`)으로 구분된 모듈 이름(`package.module`)을 사용해 모듈을 구조화 하는 방법

### 1. 패키지 생성
1. 패키지로 사용할 폴더를 생성한다.
   - `my_package`라는 이름의 폴더를 생성

2.  `my_package` 폴더 안에 `__init__.py` 파일과 `test`라는 이름의 폴더를 생성
    - `__init__.py` : 구버전 파이썬에서는 폴더 내부에 `__init__.py` 모듈이 있으면 패키지로 인식했다. python3.3 버전부터는 해당 모듈이 없어도 패키지로 인식하지만, 하위 버전 호환 및 일부 프레임 워크에서의 올바른 동작을 위해 `__init__.py` 파일을 생성하는 것이 권장된다. 파일 내부는 비워둔다.

3. `test` 폴더 안에 `__init__.py` 파일과 `test_package.py` 파일을 생성
4. `test_package.py` 파일을 열어서 모듈로서 동작할 수 있도록 특정 기능이 담긴 코드를 작성한다.
```python
# 경로 my_package/test/test_package.py

pi = 3.14159265358979323846

e = 2.71828182845904523536

def my_max(a, b):
    if a > b:
        return a
    else:
        return b

```

### 2. 패키지 활용/불러오기 
1. 특정 패키지에서 모듈을 불러오기
```python
from <package> import <모듈>
```
   - `my_package`의 상위폴더에서 새로운 파이썬 파일을 생성해 `my_package`가 패키지로서 동작하는지 확인한다.
```python
from my_package.test import test_package

test_package. pi, test_package.e
```
```
(3.141592653589793, 2.718281828459045)
```

2. 특정 패키지 내부 모듈에서 특정한 데이터 혹은 함수만 활용하기
```python
from <package.module> import <data>
```
   - 예시
```python
from my_package.test.test_package import pi, my_max

pi, my_max(1,3)
```
```
(3.141592653589793, 3)
```
   - 이름을 지정하여 가져올 수 있다.
```python
from <package.module> import <data> as <별명>
```
   - 패키지 생성 4번에서 만든 `my_max` 함수의 별칭을 `mmax`로 패키지 내 `test_package` 모듈을 불러왔다. 이후에 `mmax()`으로 실행해도 `my_max()`와 동일한 실행결과가 반환된다.
```python
from my_package.test.test_package import my_max as mmax
mmax(1, 2)
```
```
2
```
1. 특정 패키지 내부 모듈에서 해당 모듈 내의 모든 변수, 함수, 클래스 가져오기
   - 모두 가져오기 때문에 메모리적으로 좋지 않으므로 추천하지 않는 방법
```python
from <package.module> import *
```
   - 예시
```python
from my_package.test.test_package import *
```