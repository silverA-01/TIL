# 데이터 구조(Data Structure)
데이터에 편리하게 접근하고 변경하기 위해서 **데이터를 저장하거나 조작하는 방법**
> Program = Data Structure + Algorithm
>
> - Niklaus Wirth

> 1. 알고리즘에 빈번히 활용되는 **시퀀스형** 데이터 구조
>  - 시퀀스형 데이터 타입은 **순서가 있는(ordered)** 특징을 가진다.
>    1. 문자열(String)
>    2. 리스트(List)
> 2. 알고리즘에 빈번히 활용되는 **비시퀀스형** 데이터 구조
> - 비시퀀스형 데이터 타입은 **순서가 없는(unordered)** 특징을 가진다.
>   1. 세트(Set)
>   2. 딕셔너리(Dictionary)
> 3. 데이터 구조에 적용 가능한 Built-in Function

### 데이터 타입
|**Data Type**|**순서(seqeunce)**|**순회/반복가능**|**수정가능**|
|---|---|---|---|
|1.1.1) 정수 integer/ int|X(단일값) |non-iterable(단일값) |immutable|
|1.1.2) 실수 float|X(단일값) |non-iterable(단일값)  |immutable|
|1.2) 참/거짓 Boolean/ bool|X(단일값) |non-iterable(단일값)  |immutable|
|1.3) 문자열 String/ str|ordered|iterable|immutable|
|2.1) 리스트 list|ordered|iterable|mutable|
|2.2) 튜플 tuple|ordered|iterable|immutable|
|2.3) 레인지 range|ordered|iterable|immutable|
|3.1) 세트 set|unordered|iterable|mutable|
|3.2) 딕셔너리 dictionary/ dict|unordered|iterable| mutable(value), immutable(key)|

### 메서드 확인
- `dir(object)` : 파이썬 내장함수로 `()`에 특정 객체(object)를 인자로 넣어주면, 해당 객체가 어떤 변수와 메서드를 가지고 있는지 나열해준다.
- `help(data type)` : 파이썬 내장함수로 `()`에 특정 객체(object)를 인자로 넣어주면,  다양한 메서드에 대한 class, 내용 등을 확인할 수 있다.
> `datatype` 에 들어갈 주요 datatype
>
> 
> - string or `''`
> - list or `[]`
> - tuple or `()`
> - dict or `{}`
> - range, set
> - int, float, bool
## 1. 문자열(String) 관련 method
문자열 데이터 타입의 특성
- ordered : 순서가 있음 - sequence형 컨테이너
- iterable : 순회 가능한 
- **immutable** : 변경할 수 없음
  - method를 실행해도 원본 문자열에 영향을 미치지 않는다.

### 1.1 조회 / 탐색
1. `.find(x)` 
   - x의 `첫 번째 위치(index)`를 반환한다. 
   - 문자열에 x가 없다면 `-1`을 반환한다.
2. `.index(x)`
   - x의 `첫 번째 위치(index)`를 반환한다. 
   - 문자열에 x가 없다면 **오류가 발생한다.**
     - 오류가 발생하는 쪽을 True/False 관점에서 더 유용하게 사용할 수 도 있다.

- return value : integer

```python
a = 'apple'
print(a.find('p')) # a[1]
print(a.index('p')) # a[1]
print(a.find('z')) # z in a => False
```
```
1
1
-1
```
   
### 1.2 문자열 변경
1. `.replace(old, new, count)`
- 바꿀 대상 글자 `old`를 새로운 글자 `new`로 바꿔서 반환
- `count` 지정 시 해당 갯수만큼 시행(생략 가능)
- return value : string
    ```python
    a = 'yaya!'

    b = 'wooowoo'

    print(a.replace('ya', '', 2))
    print(b.replace('o', '_'))
    ```
    ```
    '!'
    'w___w__'
    ``` 

2. `.strip([chars])`
- 특정한 문자들을 지정하면 양쪽 or 왼쪽 or 오른쪽을 제거하여 반환한다.
- return value : string
- ()안에 문자열을 지정하지 않으면 공백을 다 제거한다.
    - `a.strip()` : 변수 a의 양쪽 공백 제거
    - `a.lstrip()` : 변수 a의 왼쪽 공백 제거
    - `a.rstrop()` : 변수 a의 오른쪽 공백 제거

    ```python
    a = '    hello!    \n'
    b = 'hihihihahahihi'

    print(a.strip())
    print(b.rstirp('hi'))
    ```
    ```
    'hello!'
    'hihihihahahi'
    ```

3. `.split([chars])`
- 문자열을 **특정한 단위로 나누어 리스트로 반환한다.**
- return value : list
- `()` : 지정하지 않으면 ` ` 공백을 구분자로 사용하여 문자열을 나눈다.
- `('')` : 빈 문자열을 넣을 경우 오류 발생
    ```python
    a = 'a_b_c'
    print(a.split('_'))
    print(a.split())
    ```
    ```
    ['a', 'b', 'c']
    ['a_b_c']
    ```

4. `'separator'.join(iterable)`
- 특정한 문자열로 만들어 반환한다.
- 반복가능한(iterable) 컨테이너 요소들을 seperator(구분자)로 합쳐(`join()`) 문자열로 반환한다.
  - iterable container : string, list, tuple, range, set, dict
  - 인자(argument) : iterable conatainer 
  - return value : string
    ```python
    word = 'apple'
    word2 = ('a', 'b', 'c')
    words = ['hi', 'hello']

    print('!'.join(word))
    print(' '.join(word2))
    print(''.join(words))
    ```
    ```
    'a!p!p!l!e'
    'a b c'
    'hihello'
    ```

### 1.3 대/소문자 관련
1. 대문자 관련
   1. `.capitalize()` : 첫 글자만 대문자로 만들어 반환
   2. `.title()` : 첫 글자와 공백 이후 첫 글자, 어퍼스트로피(`'`)를 대문자로 만들어 반환
   3. `.upper()` : 모두 대문자로 만들어 반환
2. 소문자 관련
   - `.lower()` : 모두 소문자로 만들어 반환 
3. 대소문자 서로 변경
   - `.swapcase()` : 대문자와 소문자를 서로 변경하여 반환
    ```python
    a = 'hI! Everyone, I\'m kim'
    print(a.capitalize())
    print(a.tiitle()) # 제일 첫 글자도 대문자가 되는 것 확인
    print(a.upper())
    print(a.lower())
    print(a.swapcase())    
    ```
    ```
    "Hi! everyone, i'm kim"
    "Hi! Everyone, I'M Kim"
    "HI! EVERYONE, I'M KIM" 
    "hi! everyone, i'm kim"
    "Hi! eVERYONE, i'M KIM"
    ```
### 1.4 기타 문자열 관련 검증 : 참/거짓 반환
- `is`로 시작하는 method는 대부분 참/거짓을 반환한다.
- `.isdecimal()`, `.isdigit()`, `.isnumeric()` : 문자열 안에 숫자인지 확인가능 - 숫자이면 True 아니면 False를 반환한다.
  - 각 method의 기준으로 숫자인지 판단
    |isdecimal()|isdigit()|isnumeric()|Example|
    |---|---|---|---|
    |True|True|True| "038", "੦੩੮", "０３８"|
    |False|True|True| "⁰³⁸", "🄀⒊⒏", "⓪③⑧"|
    |False|False|True| "↉⅛⅘", "ⅠⅢ", "⑩⑬㊿", "壹貳參"|
 

## 리스트(list) 관련 method
리스트 데이터 타입의 특성
- ordered : 순서가 있음 - sequence형 컨테이너
- iterable : 순회 가능한 
- **mutable** : 변경 가능한
> 리스트는 mutable한 특성을 갖기 때문에, 리스트의 특정 method 실행시 return value가 나오지 않고, 원본의 리스트를 다시 출력하면 return value가 method에 영향을 받아 바뀌는 것을 확인할 수 있다. 
>
> ex. 리스트의 값 추가/삭제 method, `.sorted()`

### 2.1 리스트의 값 추가

1. `.append(x)` : 리스트에 'x'라는 값을 추가
   - 'x'(parameter)에 하나의 인자(argument)만 넣을 수 있다.
     > 아래에서 plave.append('bambie', 'eunho', 'hamin') 실행시 오류 발생
   - ```python
      plave = ['noah', 'yejun']
      plave.append('bambie')
      print(plave)
      ```
      ```
      ['noah', 'yejun', 'bambie]
      ``` 
      ```python
      plave = ['noah', 'yejun']
      plave.append({'bambie', 'eunho', 'hamin'}) # set
      plave.append({noah : 21}) # dict
      plave.append((5, 10)) # tuple
      plave.append(range(5, 10)) # range
      plave.append(5) # int
      plave.append(False) # bool
      plave.append(None) # None

      print(plave)
      ```
      ```
      ['noah', 'yejun', {'bambie', 'eunho', 'hamin'}, {'noah': 21}, (5, 10), range(5, 10), 5, False, None]
      ```
      > x에 리스트를 넣었을 때 ['bambie', 'eunho', 'hamin'] 리스트가 통째가 하나의 요소로 plave 리스트에 추가된 것을 확인할 수 있다. 아래 `.extend(iterable)` 메서드 에서 리스트를 넣었을 때 어떻게 다르게 들어가는지 확인하자.
      ```python
      plave = ['noah', 'yejun']
      plave.append(['bambie', 'eunho', 'hamin'])
      print(plave)
      ```
      ```
      ['noah', 'yejun', ['bambie', 'eunho', 'hamin']]
      ```

2. `.extend(iterable)` : 리스트에 'iterable' 값을 추가
    - iterable : list, range, tuple, string
    - > `.append(x)`와 달리 리스트를 넣었을 때, ['bambie', 'eunho', 'hamin'] 리스트의 각 요소가 plave 리스트에 추가된 것을 알 수 있다.
    - ```python
      plave = ['noah', 'yejun']
      
      # 아래의 실행은 리스트의 '+' 연산자를 이용한
      # plave + ['bambie', 'eunho', 'hamin']
      # 의 결과와 같다.
      plave.extend(['bambie', 'eunho', 'hamin']) 

      print(plave)
      ```
      ```
      ['noah', 'yejun', 'bambie', 'eunho', 'hamin']
      ```
      > 문자열을 넣을 경우 문자열의 요소가 각각 추가되는 것을 확인할 수 있다.
      ```python
      plave = ['noah', 'yejun']
      plave.extend('bambie')
      print(plave)
      ```
      ```
      ['noah', 'yejun', 'b', 'a', 'm', 'b', 'i', 'e']
      ```
3. `.insert(i, x)` : 리스트의 정해진 위치 `i`에 `x`라는 값을 추가
   - 리스트의 index를 이용해 `i` 위치 설정
   - 리스트의 길이(len)를 넘어서는 index는 마지막에 아이템이 추가된다.
   - > `i`에 -1을 넣으면 현재 리스트의 마지막 자리에 위치시키기 때문에, 그 자리에 x가 들어가고 원래 있던 제일 마지막 항목이 뒤로 가게된다. x를 제일 뒤에 넣고 싶다면 `i`에 len(plave)를 넣으면 된다. 하지만 이 경우 같은 결과를 가져오는 `.append(x)`를 더 많이 활용한다.
   - ```python
     plave = ['noah', 'yejun', 'bambie', 'eunho', 'hamin']

     plave.insert(0, 'start')
     plave.insert(-1, 'end1')

     # 아래 실행은 plave.append('end2')와 결과가 같다.
     plave.insert(len(cafe), 'end2')

     print(plave)
     ``` 
     ```
     ['start', 'noah', 'yejun', 'bambie', 'eunho', 'end2', 'end1', 'hamin']
     ```



### 2.2 리스트의 값 삭제
1. `.remove(x)` : 리스트에서 `x`라는 값을 삭제
   - 만약 값이 여러 번 나타나면 가장 처음 나타난 위치의 값을 제거
   - `x`가 없으면 Error 발생
```python
numbers = [1, 2, 3, 1, 2]
numbers.remove(1)
numbers
```
```
[2, 3, 1, 2]
```
2. `.pop(i)` : 리스트의 정해진 위치 `i`에 있는 값을 삭제하며, 그 항목을 반환. 
- `i`가 지정되지 않으면 마지막 항목을 삭제하고 반환.
- return value : 삭제한 항목(`list[i]`)
```python
numbers = [1, 2, 3, 4, 5, 6]
num_pop = numbers.pop(0)
numbers, num_pop 
```
```
([2, 3, 4, 5, 6], 1)
```
> `pop()` 메서드에 위치를 지정해주지 않았기 때문에 numbers 리스트의 가장 마지막 항목인 `6`이 numbers에서 삭제되고, `numbers.pop()` 실행에 대해 반환된다.
```python
numbers = [1, 2, 3, 4, 5, 6]
num_pop = numbers.pop()
numbers, num_pop 
```
```
[1, 2, 3, 4, 5], 6
```
3. `.clear()` : 리스트의 모든 항목을 삭제
```python
numbers = [1, 2, 3, 4, 5, 6]
numbers.clear()
numbers
```
```
[]
```
> `numbers.clear()`은 기존 `numbers` 의 리스트의 항목을 삭제해서 `[]`이 된 것으로 `numbers = []`라고 새로운 빈 리스트를 할당한 것과 다르다. 새로운 빈 리스트를 할당할 경우 `id(numbers)`가 다르게 반환될 것이다.

### 2.3 리스트의 탐색
1. `.index(x)` : 리스트 안에서 `x` 값을 찾아 해당 index 값을 반환
   - `x`에 해당하는 값이 리스트 안에 없을 경우 오류 발생
   - ```python
     a = [1, 2, 3, 4, 5]
     a.index(3)
     ```
     ```
     2
     ```
2. `.count(x)` : 리스트 안에서 `x`의 개수를 반환
```python
a = [1, 2, 5, 1, 5, 1]
a.count(1)
```
```
3
```
- 원하는 `x`의 값을 모두 삭제하고 싶을 때 `.count()`와 `.remove()` 메서드를 사용해서 삭제할 수 있다.
```python
a = [1, 2, 5, 1, 5, 1]
for _ in range(a.count(1)):
   a.remove(1)
a
```
```
[2, 5, 5]
```
### 2.4 리스트의 정렬
1. `.sort()` : 리스트를 오름차순 기준으로 정렬
   - 원본 리스트에 영향을 미쳐, 실행시 **원본 리스트가 변형된다.**
   - return value : None(원본이 변형되기 때문에)
   - 내장함수 `sorted()`는 리스트를 정렬하지만, 원본에 영향을 주지 않고 새로운 리스트를 출력한다.
   - `.sort(reverse=True)` : **reverse 옵션**을 이용하여 **역순 정렬(내림차순)** 도 가능하다.
   - ```python
     plave = ['noah', 'yejun', 'bambie', 'eunho', 'hamin']
     plave.sort()
     print(plave)

     lotto = [3, 39, 5, 7, 41, 13]
     lotto.sort()
     print(lotto)

     lotto.sort(reverse=True)
     print(lotto)
     ```
     ```
     ['bambie', 'eunho', 'hamin', 'noah', 'yejun']
     [3, 11, 24, 33, 35, 45]
     [41, 39, 13, 7, 5, 3]
     ```

    - `.sort()` method와 `sorted()` 함수를 비교해보면, `sorted()` 함수는 원본 리스트인 plave에 영향을 주지 않고 새로운 리스트를 만드는 것을 확인할 수 있다.
    - ```python
      plave = ['noah', 'yejun', 'bambie', 'eunho', 'hamin']
      print(plave)
      print(sorted(plave))     
      ```     
      ```
      ['noah', 'yejun', 'bambie', 'eunho', 'hamin']
      ['bambie', 'eunho', 'hamin', 'noah', 'yejun']
      ```
### 2.5 리스트의 역순 나열
* `.reverse()` : 리스트의 각 요소를 반대로 뒤집어서 나열한다.(정렬X)
```python
plave = ['noah', 'yejun', 'bambie', 'eunho', 'hamin']
plave.reverse()
plave
```
```
['hamin', 'eunho', 'bambie', 'yejun', 'noah']
```
### 2.6 리스트의 복사
`b = a`라고 `b`에 `a`를 할당하면 `a`가 할당받은 리스트 `[1, 2, 3]`을 `b`도 같이 참조하기 때문에, `a[0] = 5`로 리스트의 변화가 `b`에도 영향을 미친다.
```python
a = [1, 2, 3]
b = a
a[0] = 5
a, b
```
```
([5, 2, 3], [5, 2, 3])
```
#### 얕은 복사(shallow copy)
일부 상황에서만 복사된 값을 사용
1. slice 연산자 사용 `[:]`
> slice 연산자를 이용해 `b` 에 `a[:]`를 할당하여 `a`를 복사했다. 그 후 `a[0]`의 값을 새롭개 할당해도 `b`는 복사본이기 때문에 `a`에 영향을 받지 않는다.
```python
a = [1, 2, 3]
b = a[:]
a[0] = 5
a, b
``` 
```
([5, 2, 3], [1, 2, 3])
```  
2. `list()` 활용
```python
a = [1, 2, 3]
b = list(a)
a[0] = 5
a, b
```
```
([5, 2, 3], [1, 2, 3])
```
3. `.copy()` 활용
```python
a = [1, 2, 3]
b = a.copy()
a[0] = 5
a, b
```
```
([5, 2, 3], [1, 2, 3])
```
#### 깊은 복사(deep copy)
중첩된 상황에서 복사를 하고 싶을 때 사용. 내부에 있는 모든 객체까지 새롭게 값이 변경된다.
- `copy` 모듈을 활용하여 `deepcopy`를 불러온다.
> 아래 코드의 a[2]의 요소는 리스트 형태로 `[3, 4]`이다. b가 a를 얕은 복사를 해도 b[2]가 참조하는 것은 a[2]에 할당된 리스트를 같이 참조하기 때문에 `a[2][0] = 100`으로 리스트 내부의 리스트 요소에 새로운 값을 할당할 때 b에도 영향을 미친다. b에 영향을 미치지 않기 위해서는 아래와 같이 copy 모듈을 활용한 깊은 복사를 해야한다.
```python
a = [1, 2, [3, 4]]
b = a[:]
a[2][0] = 100
a, b
```
```
([1, 2, [100, 4]], [1, 2, [100, 4]])
```
> `from copy import deepcopy`를 작성해야 `deepcopy`를 불러올 수 있다.
```python
from copy import deepcopy
a = [1, 2, [3, 4]]
b = deepcopy(a)
a[2][0] = 100
a, b
```
```
([1, 2, [100, 4]], [1, 2, [3, 4]])
```

### List Comprehension
List Comprehension은 표현식과 제어문을 통해 리스트를 생성할 수 있다. 

여러 줄의 코드를 한 줄로 줄일 수 있다.

1. List Comprehension 활용법
```python
[expression for 변수 in iterable]
list(expression for 변수 in iterable)
```

```python
numbers = range(1,5)

new_list = []
for num in numbers:
    num = num ** 2
    new_list.append(num)

new_list
```
```
[1, 4, 9, 16]
```
> 위 코드를 List Comprehension으로 아래와 같이 한 줄로 줄일 수 있다.
```python
numbers = range(1,5)

# for문을 순회하면서 'num ** 2'에 대한 내용을 new_list에 채워나가겠다는 의미
new_list = [num ** 2 for num in numbers]
new_list
```
2. List Comprehension + 조건문 활용법
조건문에 참인 식으로 리스트를 생성한다.
```python
[expression for 변수 in iterable if 조건식]
```
```python
even_list = []

for num in range(1, 11):
    if num % 2 == 0:
        even_list.append(num)

even_list
```
```
[2, 4, 6, 8, 10]
```
> 위 코드를 List Comprehension으로 아래와 같이 한 줄로 줄일 수 있다.
```python
even_list = [for num in range(1, 11) if num % 2 == 0]
even_list
```
[2, 4, 6, 8, 10]
- 조건 표현식(Conditional Expression)을 사용할 때는 expression 뒤로 조건표현식이 들어간다.
  - **조건표현식**
  - ```python
    true_value if <조건식> else false_value
    ```
```python
new_list = [num ** 2 if num % 2 == 0 else num for num in range(1, 11) ]
new_list
```
```
[1, 4, 3, 16, 5, 36, 7, 64, 9, 100]
```

## 세트(Set)
세트 데이터 타입의 특성
- unordered : 순서가 없음 - non-sequence형 컨테이너
- iterable : 순회 가능한 
- **mutable** : 변경 가능한

### 추가
1. `.add(elem)` : 'elem'을 세트에 추가
```python
a = {'apple', 'peach', 'watermelon'}
a.add('orange')
a
```
```
{'apple', 'orange', 'peach', 'watermelon'}
```
> `set`는 요소들이 정렬되지 않은 집합을 나타내기 때문에 `set`에서 순서는 중요하지 않다. `a.add(orange)` 한 번더 실행해도 `set`는 중복을 피하기 때문에 'orange' 요소가 `a`에 추가되지 않는다.
2. `.update(*others)` : 여러 값을 추가할 수 있다. 인자로는 반드시 **iterable 데이터 구조**를 전달해야 한다.
- iterable 데이터구조 : string, list, tuple, range, set, dictonary
- 하나의 값을 넣어도 추가된다.(ex.{'lemon'})
```python
a = {'apple', 'peach', 'watermelon'}
a.update({'orange', 'tomato', 'graph'})
a
```
```
{'apple', 'graph', 'orange', 'peach', 'tomato', 'watermelon'}
```
> 문자열 string을 넣을경우 문자열의 인덱싱별로 들어간다.
```python
a = {'apple', 'peach', 'watermelon'}
a.update('lemon')
a
```
```
{'apple', 'e', 'l', 'm', 'n', 'o', 'peach', 'watermelon'}
```

### 삭제
1. `.remove(elem)` : 'elem'을 세트에서 삭제. 세트 안에 'elem'이 없으면 KeyError 발생
```python
a = {'apple', 'peach', 'watermelon'}
a.remove('apple')
a
```
```
{'peach', 'watermelon'}
```

2. `.discard(elem)` : 'elem'을 세트에서 삭제. 세트 안에 'elem'이 없어도 에러가 발생하지 않고 원래의 세트 상태로 있는다.
- 인자를 하나만 받는다.
```python
a = {'apple', 'peach', 'watermelon'}
a.discard('apple')
a
```
```
{'peach', 'watermelon'}
```
> `a`에 'lemon'이 들어있지 않지만, 에러가 발생하지 않고 원래의 세트를 그대로 반환한다.
```python
a = {'apple', 'peach', 'watermelon'}
a.discard('lemon')
a
```
```
{'apple', 'peach', 'watermelon'}
```
> 하나의 인자만 받기 때문에 아래와 같이 넣는다면 에러가 발생
```python
a = {'apple', 'peach', 'watermelon'}
a.discard('apple', 'lemon')
a
```

3. `.pop()` : 임의의 원소를 제거해 반환 
- 랜덤으로 원소를 제거하기 때문에 인자를 받지않는다.
- 랜덤이기 때문에 다시 처음부터 실행을 해도 값이 계속 바뀔 수 있다.
- 빈 세트 `set()`에서 `.pop()`을 실행하면 에러가 발생한다.
```python
a = {'apple', 'peach', 'watermelon'}
b = a.pop()
a, b
```
```
({'peach', 'watermelon'}, 'apple')
```

## 딕셔너리(Dictionary)
딕셔너리 데이터 타입의 특성
- `key: Value` 페어의 자료구조.
- unordered : 순서가 없음 - non-sequence형 컨테이너
- iterable : 순회 가능한
- **mutable** : Value값에 대해 변경 가능한
  
### 조회
1. `.get(key[, default])` : key를 통해 value를 가져온다. 
   - 절대로 KeyError가 발생하지 않는다. 
   - **default는 기본적으로 None이다.** key가 없을 때 반환될 value를 설정해줄 수 있다.
```python
my_dict = {'Noah':22, 'Yejun':22, 'Eunho': 20}
my_dict.get('Noah')
```
```
22
```
```python
my_dict = {'Noah':22, 'Yejun':22, 'Eunho': 20}
my_dict.get('Bambie', False)
```
```
False
```

### 추가
1. `.pop(key[, default])` : key가 딕셔너리에 있으면 제거하고 그 값을 돌려준다. 그렇지 않으면 default를 반환한다.
    - default가 없는 상태에서 딕셔너리에 없는 값을 인자로 넣으면 KeyError 발생
```python
my_dict = {'Noah':22, 'Yejun':22, 'Eunho': 20}
pop_dict = my_dict.pop('Noah')
pop_dict, my_dict
```
```
(22, {'Yejun': 22, 'Eunho': 20})
```

2. `.update()` : 값을 제공하는 key, value로 덮어쓴다.
> 아래 코드에서 `Eunho`에 문자열을 나타내는 기호 `'`로 감싸져있지 않아도 되는 이유는, 딕셔너리의 키를 변수로 지정할 때, 변수의 이름 자체가 키로 사용되기 때문이다.
>
> `my_dict.update(Eunho=21)`는 `my_dict.update({'Eunho': 21)}`와 같은 결과를 반환하고, `my_dict['Eunho'] = 21`과도 같은 결과를 반환한다.
```python
my_dict = {'Noah':22, 'Yejun':22, 'Eunho': 20}
my_dict.update(Eunho=21)
my_dict
```
```
(22, {'Yejun': 22, 'Eunho': 20})
```

### 딕셔너리 순회(반복문 활용)
딕셔너리에 `for` 문을 실행할 때 딕셔너리 순회
- for 구문으로 아래 코드와 같이 key와 value에 접근할 수 있다.
```python
grades = {'john':  80, 'eric': 90, 'justin': 90}

for key in grades:
    print(key, grades[key])
```
```
john 80
eric 90
justin 90
```
- 딕셔너리의 `.keys()`, `.values()`, `.items()` 메서드를 활용하여 for문에서 딕셔너리 순회할 수 있다.
```python
# 1. `.keys()` 활용
for key in dict.keys():
    print(key)
    print(dict[key])
    
    
# 2. `.values()` 활용
# 이 경우 key는 출력할 수 없음
for val in dict.values():
    print(val)

    
# 3. `.items()` 활용 - key, value 둘 다 반환할 수 있다.
for key, val in dict.items():
    print(key, val)
```
### Dictionary comprehension
1. Dictionary comprehension 활용법
`iterable`에서 `dict`를 생성할 수 있다.
```python
{<key> : <value> for <요소> in <iterable>}
dict({<key> : <value> for <요소> in <iterable>})
```
> **[실습 예제1]** for문과 range 함수를 통해 1~8까지의 숫자를 반복하며, key는 각 숫자, value는 각 숫자를 3제곱하는 값이 되도록하는 딕셔너리 cubic을 Dictionary comprehension를 사용해 작성하세요.
```python

cubic = {num: num ** 3 for num in range(1, 9)}
cubic
```
```
{1: 1, 2: 8, 3: 27, 4: 64, 5: 125, 6: 216, 7: 343, 8: 512}
```
> **[실습 예제2]** blood_types을 통해 {'-A': 40, '-B': 11, '-AB': 4, '-O': 45} 과 같은 값을 가지는 딕셔너리 negative_blood_types를 생성하는 코드를 Dictionary comprehension를 사용해 작성하세요.

```python
blood_types = {'A': 40, 'B': 11, 'AB': 4, 'O': 45}
negative_blood_types = {'-' + key: val for key, val in blood_types.items()}
negative_blood_types
```
```
{'-A': 40, '-B': 11, '-AB': 4, '-O': 45}
```

2. Dictionary comprehension + 조건 활용법
```python
{<key> : <value> for <요소> in <iterable> if <expression>}
```

- 조건문에 `else`도 사용해야 한다면, 관련된 key나 value에 조건 표현식으로 표현해준다.
```python
{<key> : <true_value> if <expression> else <false_value> for <요소> in <iterable>}
```

> **[실습 예제1]** dusts을 통해 미세먼지 농도가 80 초과 지역 값을 가진 딕셔너리 result를 생성하는 코드를 Dictionary comprehension + 조건문을 사용해 작성하세요.
```python
dusts = {'seoul': 72, 'busan': 82, 'jeju': 29, 'gwangju': 45}
result = {key: val for key, val in dusts.items() if val > 80}
result
```
```
{'busan': 82}
```

> **[실습 예제2]** dusts을 통해 미세먼지 농도가 80초과는 나쁨, 80이하는 보통으로 하는 value를 가지도록 하는 딕셔너리 result를 생성하는 코드를 Dictionary comprehension + 조건문을 사용해 작성하세요.
```python
dusts = {'seoul': 72, 'busan': 82, 'jeju': 29, 'gwangju': 45}
result = {k: '나쁨' if v > 80 else '보통' for k, v in dusts.items()}
result
``` 
```
{'seoul': '보통', 'busan': '나쁨', 'jeju': '보통', 'gwangju': '보통'}
```

## Lambda 표현식
간단한 함수의 경우, 짧게 줄여 사용할 수 있다.
* **기존 정의한 함수를 람다표현식으로 바꾸는 방법**
  1. 맨 앞에 `lambda`라고 적는다.
  2. `def`, 함수이름, 소괄호`()`를 지운다.
  3. 함수이름과 소괄호 안의 parameter에 공백(space)을 준다.
  4. 엔터와 `return`도 지운다.
```python
def cube(n):
   return n ** 3
```
> 위 cube 함수의 정의를 lambda 표현식으로 바꾸면 아래와 같다.
```python
lambda cube n: n ** 3
```
* lambda 표현식으로 바꿀 함수의 조건
   1. 매개변수(parameter)가 한 개 이상이어야 한다.
   2. `return` 구문 포함 한 줄인 코드에서만 가능하다.


## 순회가능한 데이터 구조에 적용가능한 Built - in Function
순회가능한(iterable) 데이터 타입 : list, dict, set, str, bytes, tuple, range
### 1. `map(funchtion, iterable)`
순회가능한 데이터구조(iterable)의 모든 요소에 함수(function)를 적용한 후 그 결과를 반환
   - return value : map object 형태 
   - 입력값을 처리할 때 자주 활용
   - 첫번째 인자 function은 사용자 정의 함수도 가능
> 아래 numbers 리스트의 각 요소를  `.join()` 메서드를 활용해 문자열 '123'으로 만들려고 한다.
```python
numbers = [1, 2, 3]
map(str, numbers)
```
```
<map at 0x1e92c2ce080>
```
> `<map at 0x1e92c2ce080>`는 `map object` 여서 알아보기 힘들지만, list로 확인해보면 numbers의 각 요소가 문자열로 바뀐 것을 확인할 수 있다.
```python
list(map(str, numbers))
```
```
['1', '2', '3']
```
> `map` 함수와 `join` 메서드를 활용하면 문자열 '123'으로 만들 수 있다.
```python
numbers = [1, 2, 3]
map(str, numbers)
''.join(map(str,numbers))
```
```
'123'
```
> map이 아닌 List comprehension을 활용할 경우 아래와 같다.
```python
numbers = [1, 2, 3]
str_numbers = [str(num) for num in numbers]
''.join(str_numbers)
```
```
'123'
```
### 2. `filter(function, iterable)` 
순회가능한 데이터구조(iterable)에서 함수(function)의 반환된 결과가 `True`인 것들만 구성하여 반환
   - return value : filter object 형태
```python
# is_odd 함수는 홀수라고 확인될 때 True, 그렇지 않을 경우 False 를 반환한다.
def is_odd(n):
    return True if n % 2 else False

filter(is_odd,  [1, 2, 3, 4, 5, 6, 7])
```
```
<filter at 0x1e92c377070>
```
> `map` 함수와 같이 filter object를 반환하기 때문에 `list()`로 `filter` 함수가 제대로 적용되었는지 확인할 수 있다.
```python
list(filter(is_odd,  [1, 2, 3, 4, 5, 6, 7]))
```
```
[1, 3, 5, 7]
```
> `is_odd` 함수의 정의를 lambda 표현식으로 바꾸면 아래와 같이 표현할 수 있다.
```
list(filter(lambda n: True if n % 2 else False, [1, 2, 3, 4, 5, 6, 7]))
```
> List comprehension을 활용할 경우 아래와 같다.
```python
[num for num in [1, 2, 3, 4, 5, 6, 7] if is_odd(num)]
```
### 3. `zip(*iterables)` 
복수의 iterable 객체를 모아준다.
   - return value : 튜플의 모음으로 구성된 `zip object` 형태 
```python
l1 = [1, 2, 3]
l2 = [4, 5, 6]

list(zip(l1, l2))
```
```
[(1, 4), (2, 5), (3, 6)]
```
> 아래처럼 리스트 각 인덱스별 합을 함수들을 활용해 나타낼 수 있다.
```python
list(map(sum, zip(l1, l2)))
```
```
[5, 7, 9]
```

> iterable 객체의 길이가 다르다면 짧은 쪽에 맞춰 반환한다.
```python
l1 = [1, 2, 3]
l2 = [4, 5, 6, 7]

list(zip(l1, l2))
```
```
[(1, 4), (2, 5), (3, 6)]
```