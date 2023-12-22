# 컨테이너(Container)
여러 개의 값을 저장할 수 있는 데이터 구조

- 컨테이너인 데이터 타입은 **반복/순회가능한(iterable)** 특성이 있다.
  - 내부의 요소를 하나씩 순회할 수 있다는 의미로, 주로 반복문에서 이러한 특성을 활용한다.

* 시퀀스(Sequence)형 컨테이너
   - 순서가 있는 ordered 데이터
   - 리스트(list), 튜플(tuple), 레인지(range), 문자열(String)
* 비 시퀀스(Non-sequence)형 컨테이너
   - 순서가 없는 unordered 데이터
   - 세트(set), 딕셔너리(dictionary)



## 1. 시퀀스(Sequence)형 컨테이너
시퀀스는 데이터가 **순서대로 나열된(ordered)** 형식을 나타낸다. 

### 특징
1. 순서를 가질 수 있다.
2. 특정 위치의 데이터를 가리킬 수 있다.
   - **인덱스(index)** 를 이용할 수 있다는 의미 

> 순서대로 나열된 것이 **정렬되었다(sorted)의 의미는 아니다.** 정렬은 오름차순, 내림차순등의 기준을 정해 여러가지 요소를 정리해 나열한 것이다.

### 종류
시퀀스형 데이터에는 아래와 같은 데이터 타입이 포함된다.
- 리스트(list), 튜플(tuple), 레인지(range), 문자열(String)

### 1.1 리스트(`list`)
```python
[value1, value2, value3]
```
리스트는 대괄호(`[]`) 및 `list()` 를 통해 만들 수 있다.

리스트의 값에 대한 접근은 `list[i]` 를 통해 한다.
```python
plave = ['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin']
plave[0]
```
```
'Noah'
```
### 2. 튜플(`tuple`)
```python
# 기본형(값 2개 포함)
(value1, value2)

# 2개 이상의 값을 포함할 수 있습니다.
(value1, value2, value3, value4, value5)
```
튜플은 리스트와 유사하지만, `()`로 묶어서 표현한다. 

리스트는 꼭 `[]` 부호가 필수적이지만 튜플은 `()` 소괄호를 생략할 수 있다.
- 괄호 없이 여러 값을 쉼표_콤마(`,`)로 구분하여 나열하면 파이썬은 자동으로 튜플로 처리한다. 하지만 괄호를 사용하는 것이 가독성을 높이고 코드를 명확하게 만드는데 도움이 된다.
```python
t = 1, 2, 3 , 4, 5

print(t, type(t)) 
```
```
(1, 2, 3, 4, 5) <class 'tuple'>
```
> 아래 코드에서 변수에 여러 값이 나올 수 있는 것은 `,`로 연결된 여러 값에 대해 자동으로 튜플 형태로 처리하기 때문이다.
```python
x, y = 1, 2
(x, y) = (1, 2)
type((x, y))
```
```
<class 'tuple'>
```


**튜플은 immutable**(불변의_변경가능성이 없는)한 특성 때문에 **값에 대한 수정이 불가능하다.**
> 아래 코드를 실행했을 때, 튜플 a의 인덱스값에 새로운 값을 할당할 때, 튜플은 값에 대한 수정이 불가능하기 때문에 오류가 발생한다.
```python
x, y = 1, 2
a = (x, y)
a[0] = 10
```

> 빈 튜플을 만들 수 있다. 빈 튜플은 길이가 0이다.
```python
empty_tuple = ()
print((type(empty_tuple)), len(empty_tuple))
```
```
<class 'tuple'> 0
```
> 하나의 요소(값)으로 구성된 튜플도 만들 수 있다. 이 경우 튜플의 길이가 1이다. 이 때 튜플이기 위해서 반드시 `,`가 필요하다. `,`가 없다면 아래 `single_tuple`의 타입은 `int`가 될 것이다.
```python
# single_tuple = (, 2) 라고 할당할 경우 오류가 발생한다.
single_tuple = (1, )
print(type(single_tuple), len(single_tuple))
```
```
<class 'tuple'> 1
```
> 하나의 요소(값)으로 튜플을 만들 때 앞 부분에 값을 넣지 않으면 오류가 생긴다.
```python

single_tuple = (None, 2)
print(type(single_tuple), len(single_tuple))
```
### 3. 레인지(`range()`)
`range`는 숫자의 시퀀스를 나타내기 위해 사용된다.

**Indexing**과 **Slicing**을 이용할 수 있다.
* 기본형 : `range(n)`
  - 0부터 n-1까지 값을 가짐
* 범위 지정 : `range(n, m)`
  - n부터 m-1까지 값을 가짐
  - 범위 내에 range로 뽑아낼 값이 없기 때문에 빈 리스트가 나온다.
* 범위 및 스텝 지정 : `range(n, m, s)`
  - n부터 m-1까지 +s만큼 증가한다.
  - 여기서 n과 m을 생략하지 않는다.
  - s에 음수가 들어가면 `range(stop, start, s)`로 들어가야 한다. 범위 내의 역순으로 값을 나열하기 때문이다.

보통 `list` 등으로 **형변환**하여 `range`의 각 요소(값)를 확인한다.

```python
r = range(0, 3)
print(r, type(r))
```
```
range(0, 3) <class 'range'>
```
> range는 list로 형변환을 해서 값을 확인할 수 있다.
```python
list(range(4, 9))
```
```
[4, 5, 6, 7, 8]
```
> step 자리에 음수가 들어가면 역순으로 추출하여 나열한다. 범위 내에 range로 뽑아낼 값이 없기 때문에 빈 리스트가 나온다.
```python
list(range(0, 10, -1)) 
```
```
[]
```
```python
list(range(10, 0, -1))
```
```
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

### 시퀀스형 데이터에 활용할 수 있는 연산자/함수
|operation(연산)|설명| return value
|---------|---|---|
|x `in` s |containment test (x가 s에 포함되어 있는지 평가)|`bool` - True/False|
|x `not in` s|containment test (x가 x에 포함되어 있지 않은지 평가)| `bool` - True/False|
|s1 `+` s2|concatenation||
|s `*` n|s에 대해 n번만큼 반복하여 더하기||
|`s[i]`|indexing||
|`s[i:j]`|slicing||
|`s[i:j:s]`|k 간격으로 slicing|
|`len(s)`|길이|`int`|
|`min(s)`|최솟값||
|`max(s)`|최댓값||
|s.count(x)|시퀀스형 데이터에서 x가 나타나는 개수(횟수)|`int`|

* `containment test` - `in` 연산자를 통해 포함되어있는지 확인
```python
my_list = [1, 2, 3, 5, 1]
3 in my_list
```
```
True
```
* `concatenation`으로 데이터 연결, 연쇄
```python
a = 'hi'
b = 'hello'
c = (1, 2)
d = (3, 4, 5)
print(a + b)
print(c + d)
```
```
hihello
(1, 2, 3, 4, 5)
```

* `slicing`, `indexing`, `count` 메서드 사용
```python
plave = ['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin', 'Noah']
print(plave[3])
print(plave[1:])
print(plave[4:2:-1])

print(plave.count('Noah'))
```
```
Eunho
['Yejun', 'Bambie', 'Eunho', 'Hamin', 'Noah']
2
['Hamin', 'Eunho']
```
- `min()`, `max()` 함수로 최솟값, 최대값 구하기
```python
new_list = list(range(2,15,3))
print(new_list)
print(max(new_list))
print(min(new_list))
```
```
[2, 5, 8, 11, 14]
14
2
```

## 2. 비 시퀀스형(Non-seqeunce) 컨테이너
순서가 없는 unordered 데이터
  - 순서가 없기 때문에 indexing, slicing을 할 수 없다.  
  - 세트(set), 딕셔너리(dictionary)

### 1. 세트(`set`)
`set`는 **순서가 없고 중복된 값이 없는** 자료구조이다.
```python
{value1, value2, value3}
```
- 수학에서 **집합**과 동일하게 처리된다.
- `{}`(중괄호) 혹은 `set()`를 통해 만든다.
  - 빈 세트를 만들 수는 없다.
  - `{}`는 빈 `dictionary`를 만들기 때문이다.
  - 빈 세트를 만들려면 `set()`을 사용한다.
- 활용 가능 연산자
> |집합|연산자|
> |---|---|
> |차집합| `-`|
> |합집합|`|`|
> |교집합|`&`|

```python
set_a = {1, 2, 3}
set_b = {3, 6, 9}
print(set_a - set_b)
print(set_a | set_b)
print(set_a & set_b)
```
```
{1, 2}
{1, 2, 3, 6, 9}
{3}
```
- `list`를 `set`으로 형변환 하면 중복된 값을 손쉽게 제거할 수 있다. 대신 set으로 변환하는 순간 순서가 없는 데이터가 되니 주의해야 한다. (`list` =>`set` => `list`로 다시 형변환은 가능, 순서가 없어진 후 list화 되기 때문에 주의할 것)

### 2. 딕셔너리(`dictionary`)
딕셔너리는 `key`와 `value`의 쌍으로 이루어져있다.
```python
{Key1:Value1, Key2:value2, Key3:value3, ...}
```
- `{}` 혹은 `dict()`로 만들 수 있다.
  - 딕셔너리와 세트의 중괄호가 같지만, 딕셔너리는 key와 value의 쌍으로 `:` 기호를 포함하기 때문에 구조가 달라서 구분할 수 있다. 
  - 단 `{}`는 빈 딕셔너리를 의미한다.
- `key`는 변경 불가능한(immutable)한 데이터만 가능하다.
  - numeric(int, float), string, boolean / tuple
- `value`는 모든 객체(Objec)가 가능하다.

* 전체 `key`값을 확인하고 싶으면 `<딕셔너리>.keys()` 메서드를 사용한다.
```python
plave = {'Noah':22, 'Yejun':[22], 'Bambie':(21, 50), 'Eunho':{20:1}, 'Hamin':None}
plave.keys()
```
```
dict_keys(['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin'])
```
* 전체 `value`값을 확인하고 싶으면 `<딕셔너리>.values()` 메서드를 사용한다.
```python
plave.values()
```
```
dict_values([22, [22], (21, 50), {20: 1}, None])
```
* 전체 `key`와 `value`값을 같이 확인하고 싶으면 `<딕셔너리>.items()` 메서드를 사용한다.
```python
plave.items()
```
```
dict_items([('Noah', 22), ('Yejun', [22]), ('Bambie', (21, 50)), ('Eunho', {20: 1}), ('Hamin', None)])
```
* `dict[key]`은 `key`에 해당하는 `value` 을 반환한다. 
```python
plave['Noah']
```
```
20
```
* `dict[key]`를 이용해 `value`에 새로운 값을 할당할 수 있다. (`key`는 immutable하기 때문에 수정 불가능)
```python
plave['Noah'] = 1
plave
```
```
{'Noah': 1, 'Yejun': [22], 'Bambie': (21, 50), 'Eunho': {20: 1}, 'Hamin': None}
```
## 컨테이너형 형변환
|데이터 타입 | 형변환 가능한 컨테이너형 데이터 타입|
|---|---|
|string|list, tuple, set|
|list|string, tuple, set|
|tuple|string, list, set|
|range|string, list, tuple, set|
|set|string, list, tuple|
|dictionary|string, `key`만 list, `key`만 tuple, `key`만 set|
```python
r = range(1, 5)

str(r) # => 'range(1, 5)'
list(r) # => [1, 2, 3, 4] => indexing, slicing 가능
tuple(r) # => (1, 2, 3, 4)
set(r) # => {1, 2, 3, 4} => indexing, slicing 불가능
```

```python
d = {'a': 1, 'b': 2}

str(d) = '{'a': 1, 'b': 2}'

list(d) = ['a', 'b']
tuple(d) = ('a', 'b')
set(d) = {'a', 'b'}
```
## 데이터의 분류
데이터는 변경가능성에 따라 변경가능한 것(`mutable`)들과 변경 불가능한 것(`immutable`)으로 나눌 수 있다.

### 변경 불가능한(`immutable`) 데이터
* 리터럴(literal)
  - 숫자(Number) : integer, float
  - 글자/문자열(String)
  - 참/거짓(Bool) 
* `tuple`
* `range`
* `frozenset`
  
### 변경 가능한(`mutable`) 데이터
* `list`
* `dict`
* `set`