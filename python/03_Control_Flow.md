# 제어문 (Control Statement)
코드 실행의 순차적인 흐름을 제어하는 것
* 조건문
* 반복문


## 1.조건문
### if else
```python
if <expression>:
    <code block>
else:
    <code block>
```
- `expression` : 일반적으로 참/거짓에 대한 조건식이 들어간다.
- 조건이 `참`인 경우 `if <expression>:` 이후의 `code block` 문장을 수행한다.
- 조건이 `거짓`인 경우 `else:` 이후의 `code block` 문장을 수행한다.
- `else`는 선택사항으로 생략 가능하다.
- `if`와 `else` 사이에 선택적으로 `elif`로 복수조건을 추가할 수 있다. 
- `code block` 앞에 들여쓰기(`4spaces`) 하는 형식을 지켜야한다.

```python
dust = 50
if dust > 50:
    print("50 초과")
else:
    print("50 이하")
```
```
50 이하
```
### elif
```python
if <expression1>:
    <code block>
elif <expression2>:
    <code block>
elif <expression3>:
    <code block>
else:
    <code block>
```
- 2개 이상의 조건을 활용할 경우 `elif <expression>:`을 활용한다.
- 조건문은 if 부터 앞의 조건을 순서대로 검증하므로 순서에 유의해야 한다. 조건을 만족하면 아래 조건 코드로 넘어가지 않는다.

```python
dust = 50
if dust > 50:
    print("50 초과")
elif dust == 50:
    print("50")
else:
    print("50 미만")
```
```
50
```
### 중첩 조건문(Nested Conditional Statement)
조건문은 다른 조건문에 중첩될 수도 있다.
```python
score = 96

if score >= 90 : 
    print('A')
    if score >= 95 :
        print('참 잘했어요.')
elif score >= 80 : 
    print('B')
elif score >= 70 : 
    print('C')
elif score >= 60 :
    print('D')
else :
    print('F')
```
```
A
참 잘했어요.
```
### 조건 표현식(Conditional Expression)
조건 표현식은 일반적으로 조건에 따라 값을 정할 때 활용된다.

**삼항 연산자(Ternary Operator)** 라고 부르기도 한다.

```python
if <expression>:
    <true_value>
else:
    <false_value>
```
> 아래는 위 조건문을 조건 표현식으로 표현한 것으로 같은 조건문이다.
```python
<true_value> if <expression> else <false_value>
```
> 아래 조건 표현식에 들어간 조건 `2`는 `True`에 가까운 값이라 참이라고 판단하여 `true_value`인 `1`이 반환되었다.
```python
1 if 2 else 3
```
```
1
```

## 2. 반복문
* while
* for

### `while` 반복문
`while` 문은 조건식이 `True`인 경우 반복적으로 코드를 실행
- 조건식 뒤에 콜론(`:`)이 반드시 필요
- 이후 실행될 코드 블럭은 `4spaces`로 들여쓰기를 해야한다.
```python
while <expression>:
    <code block>
```
> 아래 반복문에서 `num = 10`일 때, `num`은 `True`에 가까운 값으로 본다. `while` 반복문은 `True`인 조건식에서 계속 반복해서 코드를 실행하기 떄문에 `num`이 정수에서 `False`에 가까운 값, 즉 `0`이 되면 반복문을 종료한다.
```python
num = 10
total = 0

while num:
    total += num
    num -= 1

print(total)
```
```
55
```

### for
`for`문은 시퀀스를 포함한 순회가능한 객체(iteralble)의 요소들을 순회한다.
 - string, tuple, list, range, set, dictionary
  
```python
for <임시변수> in <순회가능한데이터(iterable)>:
    <code block>
```
- `for`문 안에서 요소 값에 다른 값을 할당해도 다음 반복구문에 영향을 주지 않는다. 다음 요소 값에 의해 덮어 씌워지기 떄문이다.
> `name = ['plave']`으로 다른 값이 할당되었지만 `for`구문으로 다시 돌아갈 때 `name = ['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin']`으로 in 뒤에 나온 데이터에 대해 할당받는 과정이 발생된다.
```python
for name in ['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin']:
    print(name)
    name = ['plave']
```
```
Noah
Yejun
Bambie
Eunho
Hamin
```

### 리스트(list) 순회에서 index 활용
`range(len(리스트))`
- `range()`와 순회할 list의 길이를 활용하여 index를 조작할 수 있다.

```python
plave = ['Noah', 'Yejun', 'Bambie', 'Eunho', 'Hamin']

for idx in range(len(plave)):
    print(plave[idx])
```
```
Noah
Yejun
Bambie
Eunho
Hamin
```
> 아래처럼 `for`문과 `f-strings`를 이용해서 출력할 수 있다.
```python
lunch = ['짜장면', '초밥', '피자']
for idx in range(len(lunch)):
    menu = lunch[idx]
    print(f'{idx+1}번째 메뉴: {menu}')
```
```
1번째 메뉴: 짜장면
2번째 메뉴: 초밥
3번째 메뉴: 피자
```
### `enumerate()`
- 내장함수 중 하나로 **index**와 값을 같이 결과 값으로 보내준다.
- 단독으로 사용하기 보다는, list 같이 iteralbe한 특성을 가진 데이터 타입과 같이 사용된다.
- 결과 값의 데이터 타입은 **tuple** 
```python
lunch = ['짜장면', '초밥', '피자']

for x in enumerate(lunch):
    print(x, type(x))
```
```
(0, '짜장면') <class 'tuple'>
(1, '초밥') <class 'tuple'>
(2, '피자') <class 'tuple'>
```
> tuple과 관련하여 for 반복문의 임시변수가 2개로 할당하면 결과값의 데이터 형식이 아래와 같이 각각 int, str으로 나올 수 있다.
```python
lunch = ['짜장면', '초밥', '피자']

for idx, menu in enumerate(lunch):
    print(idx, menu, type(idx), type(menu))
```
```
0 짜장면 <class 'int'> <class 'str'>
1 초밥 <class 'int'> <class 'str'>
2 피자 <class 'int'> <class 'str'>
```
> 보통 idx는 기본적으로 0부터 카운터하지만 아래와 같이 idx 숫자를 1부터 카운트 할 수도 있다. 하지만 많이 사용되는 기능은 아니기 때문에 참고로 알아둔다.
```python
lunch = ['짜장면', '초밥', '피자']
for idx menu in enumerate(lunch, start=1):
    print(idx, menu)
```
```
1 짜장면
2 초밥
3 피자
```

## 3. 반복 제어

### 1. break
반복문을 종료한다.
- `for` / `while` 문에서 빠져나가 `break` 
- 조건이 참이 될 때, 반복문의 반복이 종료된다.
```python
while n < 5:
    print(n)
    if n == 2:
        break
    n += 1
```
```
2
```
> 0부터 9까지 순회하는 for 반복문 안에서 1을 초과하는 경우 '1 초과' 를 출력하며 종료하는 코드 작성
```python
for num in range(10):
    print(num)
    if num > 1:
        print('1초과')
        break
```
```
0
1
2
1초과
```
### 2. continue
`continue` 이후의 코드를 수행하지 않고, 다음 요소부터 계속하여 반복을 수행한다.
- `break`가 반복문의 전체 종료라고 한다면, `continue`는 해당 조건이 Ture인 회차의 종료라고 볼 수 있다. 회차 종료 후 다음 요소의 반복문을 수행한다.
```python
for num in range(10):
    if num % 2:
        continue
    print(num)
```
```
0
2
4
6
8
```
### 3. for-else
`else`는 `break`가 있을 때만 고려되는 요소로, `break` 조건이 충족되지 않아 끝까지 반복문을 실행한 이후 실행된다.
- `break`를 통해 중간에 종료되지 않는 경우, 반복문이 종료될 때 실행된다
  - `for`의 경우 반복에서 list의 소진이나
  - `while`의 경우 조건이 거짓이 돼서
  - `break`문으로 종료될 때는 실행되지 않는다.
> 아래 예시는 break 조건이 충족되지 않아, 전체 반복문에 모든 회차가 반복되어 종료가 되었고, else 값이 실행되어 나왔다.
```python
for num in [1, 2, 3]:
    if num == 4:
        break
    print(num)
else:
    print('완주')
```
```
1
2
3
완주
```
> 아래 예시는 break 조건이 충족되어 전체 반복중 break 되었고, break로 중간에 종료되었기 때문에 else 값이 실행되지 않는다.
```python
for num in [1, 2, 3, 4]:
    if num == 4:
        break
    print(num)
else:
    print('완주')
```
```
1
2
3
```

### 4. pass
`pass`는 아무것도 하지 않는 것을 의미하고, 문법적으로 문장이 필요하지만, 프로그램이 특별히 할 일이 없을 때 자리를 채우는 용도로 사용한다.
- 어떤 것을 작성해야 할지 모르지만 문법적으로 오류가 나지 않을 때 사용한다.
```python
for num in rage(5):
    pass
```
> pass를 사용했기 때문에 실행시 값은 나오지 않는다.