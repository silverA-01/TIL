# 함수(function) ||

## 1. 함수와 스코프(scope)
함수를 호출(call)하면 코드 내부에 스코프(scope)를 생성한다. 스코프는 **영역** 혹은 범위로 본다.

![python_scope](https://images.datacamp.com/image/upload/f_auto,q_auto:best/v1588956604/Scope_fbrzcw.png)

- `지역 스코프(local scope)` : 함수가 만든 스코프로 함수 내부에서만 참조할 수 있는 공간
  - 함수 정의 내부 영역
  - 지역 변수(local variable) : 지역 스코프에 정의된 변수 
- `전역 스코프(global scope)` : 코드 어디에서든 참조할 수 있는 공간
  - 함수 내부 공간인 지역 스코프 아닌 그 외 공간
  - 함수 정의 외부 영역
  - 전역 변수(global variable) : 전역 스코프에 정의된 변수
- `빌트 인 스코프(Built-in scope)` : 파이썬 안에 내장되어 있는 공간(개인적인 할당 불가능)
  - 따로 식별자를 지정해주지 않았는데, 사용가능한 것들. 
  - ex. `print()` - 우리가 `print` 에 대한 식별자에 값을 할당하지 않았는데 빌트 인 스코프에 할당된 함수가 있어서 사용가능
  
```python
# global scope(전역에서 사용)
a = 10

#local scope : b, c(함수 내부에서만 사용)
def func(b):
    c = 20
    print(a, b, c)

func(a)
```
```
10, 10, 20
```
- 함수가 종료되면 함수의 local scope는 사라진다. 
> `b`와 `c`는 지역 스코프 안에서 정의된 지역변수이기 때문에, `print(b, c)`는 전역 스코프에서 할당된 value를 찾을 수 없어 에러가 발생한다.
- local scope에서 global scope를 참조하는 것은 가능하다.
  - 반대는 불가능.
  - 함수가 종료되면 local scope가 종료되기 때문에, global scope에서 local scope를 참조하는 것은 불가능
- local scope와 global scope에 같은 식별자_이름(변수, 함수 등)이 있다면, 함수 내부에서는 local을 더 우선시 한다.
```python
x = 10

def func(x):
    x = 20
    return x

print(x)
func(x)
```
```
10
20
```
> `print(x)`는 gloabl scope의 `x = 10`을 참조해 출력
>
> `func(x)`는 함수 내부에서 global scope `x = 10`을 참조하고, 내부의 `x = 20`을 참조해 local scope 내부를 우선시하는 결과가 나온다.

### 변수의 수명주기(lifecycle)
변수의 이름은 각자의 수명주기가 있다.
| scope | 수명주기|
|---|---|
|built-in scope|파이썬이 실행된 이후부터 영원히 유지
|global scope|모듈이 호출된 시점 이후 or 이름 선언된 이후부터 인터프리터가 끝날 때 까지 유지|
|local scope|함수가 호출될 때 생성, 함수가 종료될 때가지 유지(함수 내에서 처리되지 않는 예외를 일으킬 때 삭제됨)
  

### 이름 검색 규칙
파이썬에서 사용되는 이름(식별자)들은 이름공간(namesapce)에 저장되어 있다. 이름을 찾는 규칙은 `LEGB RULE`이라고 하며 아래 순서로 이름을 찾아 나간다.
1. `L`ocal scope : 함수
2. `E`nclosed scope : 특정 함수의 상위 함수
3. `G`lobal scope : 함수 밖의 변수 or import된 모듈
4. `B`uilt-in scope : 파이썬 안에 내장되어 있는 함수 또는 속성
- 기본적으로 함수에서 선언된 변수는 local scope에 생성되며, 함수 종료 시 사라진다.
- 해당 스코프에 변수가 없는 경우 LEGB rule에 의해 이름을 검색한다.

```python
a = 10

def func():
    print = 10

func()
print(a)
```
```
123
```
> `func()`는 함수 내부 `print` 식별자에 `10`을 할당. 하지만 함수가 종료되면서 local scope가 사라진다.
>
> `print(a)`는 built-in scope에서 `print` 식별자에 할당된 값인 출력과 관련된 함수 참조하여 `print()`를 사용할 수 있는 것.
- `enclose scope`는 아래와 같이 부모(상위)함수가 있을 경우를 말한다.
```python
def outer_func(x):
  def inner_func(y):
    return x + y
  return inner_func
```
> 위 코드에서 `inner_func`를 정의할 때 `x`는 함수 내에서 변수를 찾을 수 없기 때문에 `LEGB rule`에 따라 부모(상위)함수에서 변수를 검색한다.

- 변수에 접근은 가능하지만 해당 변수를 수정할 수는 없다. 값을 할당하는 경우 해당 scope의 이름공간에 새롭게 생성되기 때문이다. 단, 함수 내에서 필요한 상위 scope 변수는 인자로 넘겨서 활용한다. (클로저 제외)

- 상위 스코프에 있는 변수를 수정하고 싶을 경우 `global`, `nonlocal` 키워드를 활용 - 일반적으로 권장하지는 X
```python
a = 10

def func():
    global a
    a = 100
    print(a)

func()
print(a)
```
```
100
100
```
> `global a` 키워드를 사용한 이후에 나온 식별자 `a`를 global `a`로 선언하여 `print(a)`는 100이 출력된다.

## 2. 재귀 함수(recursive funchtion)
재귀 함수는 **함수 내부에서 자기 자신을 호출하는 함수** 를 뜻한다.
- 알고리즘 설계 및 구현에서 유용하게 활용된다.

### 팩토리얼(Factorial) 계산
* **팩토리얼** :  1부터 n가지 양의 정수를 차례대로 곱한 값으로 `!` 기호로 표기하다.
  - ex. 3! = 3 * 2 * 1 => 결과는 6

1. 반복문을 이용한 팩토리얼 계산
> 팩토리얼을 계산하는 fact(n) 함수를 정의해보자. 단, n은 1보다 큰 정수라고 가정한다.
> 
> `while` 문은 조건식이 `True`이면 아래 코드 블럭을 계속 실행한다. n이 1 이하의 정수가 될 때 멈춰야하기 때문에 `n > 1`을 조건식에 넣어준다.
```python
def fact(n):
  answer = 1
  while n > 1:
    answer *= n
    n -= 1
  return answer
```
```python
def fact(n):
  answer = 1
  for idx in range(1, n+1):
    answer *= idx
  return answer
```

2. 재귀를 이용한 팩토리얼 계산
> 팩토리얼을 계산하는 factorial(n) 함수를 정의해보자. 
>
> 아래 fact() 함수 내부에는 fact() 함수를 계속 참조하여 반복하고, 마지막에 n == 1 이 될 때까지 함수를 반복해서 참조하여 팩토리얼 계산을 하게 된다.
```python
def factorial(n):
  if n == 1:
    return 1
  return n * factorial(n-1)
```
> `factorial()`을 정의하는데 함수 내부에서 `factorial` 함수를 참조하게 된다.
>
> n에 1이 할당되면 if 조건문의 `return 1`을 수행하고 함수의 정의를 종료하기 때문에 아래 `return n * factorial(n-1)`로 넘어가 실행하지 않는다.

- 재귀함수를 작성할 때 반드시 `base case`가 존재해야 한다. `base case`는  점점 범위가 줄어들어 반복되지 않는 최종적으로 도달하는 곳을 의미한다. 그렇지 않다면 함수가 무한 재귀에 빠지게 된다
> 위 재귀를 이용한 팩토리얼 계산에성 `retrun 1 if n == 1`는 `base case`로 이 조건이 없으면 위 함수의 정의는 무한재귀에 빠지게 된다.

* 재귀함수 장점
  - 알고리즘 구현시 많이 사용
  - 코드가 더 직과적이고 이해하기 쉬운 경우가 있음
* 재귀함수 단점
  - 함수가 호출될 때마다 메모리 공간이 쌓이기 때문에, 메모리 스택이 넘치거나(Stack overflow) 프로그램 실행 속도가 느려진다.


### 3. 최대 재귀 깊이 (maximum recursion depth)
```python
def func():
  print(1)
  func()

func()
``` 
- `func()`를 호출하면 문자열이 계속 출력되다가 `RecursionError`가 발생한다.
- 파이썬에서는 재귀함수의 단점(메모리 문제, 실행속도 문제)을 방지하기 위해 `최대 재귀 깊이`가 1,000으로 정해져 있다. 호출되는 함수가 1,000번이 넘어가게 되면 더이상 함수를 호출하지 않고 종료된다.

### 4. 피보나치 수열
첫째 및 둘째 항이 1이며 그 뒤의 모든 항은 바로 앞 두항의 합인 수열
- ex. 1, 1, 2, 3, 5, 8

$$
F_0 = F_1 = 1
$$
$$
F_n = F_{n-1} + F_{n-2}\qquad(n\in\{2,3,4,\dots\})
$$
1. 재귀를 이용한 피보나치 값을 리턴하는 함수 정의
```python
def fib(n):
  if n == 0:
    return 0
  elif n == 1:
    return 1
  return fib(n-1) + fib(n-2)
```   
2. 반복문을 활용하여 피보나치 값을 리턴하는 함수 정의
```python
def fib_loop(n):
  anwer = [0, 1]
  for _ in range(n-1)
    answer.append(answer[-1] + answer[-2])
  retrun answer[n]
# '.append()' 리스트 메서드로 ()안에 들어간 요소를 리스트에 추가한다.
```
```python
def fib_loop2(n):
  a, b = 0, 1
  while n > 1:
    a, b = b, a + b
    n -= 1
  return b
```
### 5. 반복문과 재귀 함수의 차이
- 알고리즘 자체가 재귀적인 표현이 자연스러운 경우 재귀함수를 사용한다.
- 재귀 호출은 `변수 사용`을 줄여줄 수 있다.
- 단, 재귀 호출은 입력 값이 커질 수록 `연산 속도`가 늘어난다.