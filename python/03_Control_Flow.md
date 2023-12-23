# 제어문 (Control Statement)
코드 실행의 순차적인 흐름을 제어하는 것
* 조건문
* 반복문


## 1.조건문
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
if dust > 50:
    print("50 초과")
else:
    print("50 이하")
```

### if else
### elif

## 반목문
### while
### for

### enumerate()
- 내장함수 중 하나로 **index**와 값을 같이 결과 값으로 보내준다.
- 단독으로 사용하기 보다는, list 같이 iteralbe한 특성을 가진 데이터 타입과 같이 사용된다.
- 결과 값의 데이터 타입은 tuple 
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

## 반복 제어

### 1. break
반복문을 종료한다.
- `for` / `while` 문에서 빠져나가 `break` 조건이 참이 될 때, 반복문의 반복이 종료된다.
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