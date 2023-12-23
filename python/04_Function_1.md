# 함수(Function)
함수는 특정한 기능을 하는 코드의 묶음.
- 함수는 '작업 단위'이고, 하나의 작업을 실행하는 것이다.

## 함수를 사용하는 이유
1. 가독성
2. 재사용성
3. 유지보수
   - 코드에 에러가 나서 고칠 때, 고칠 부분이 더 적어지기 때문

## 함수의 선언과 호출
1. 함수의 선언 - 정의/ def
    1. 함수의 선언은 `def` 키워드를 활용
    2. 들여쓰기(4space)로 함수의 body(코드 블럭)를 작성
    3. Doctstirng은 함수 body 앞에 선택적으로 작성 가능
       > Docstring(독스트링) : 함수나 클래스, 모듈에 첨부할 수 있는, 큰 따옴표 세 개 (""") 혹은 작은 따옴표 세 개 (''')로 둘러싸여진 문자열이다. 
    4. `return` 뒤에 함수의 동작 후에 반환될 결과값인 value(return value)를 작성
       - `return` 값이 없으면 `None`을 반환 
  
> 활용법
```python
def 함수이름(parameter1, parameter2)
    코드 블럭
    return value

# parameter : 매개변수
```

2. 함수의 호출 - call
   - 함수의 호출은 `함수명()`으로 한다.
   - ex. max(), sum(1, 2)


> 예제) 입력 받은 수를 세제곱하여 반환(return)하는 함수 `cube()`을 작성해보세요.
```python
def cube(x):
    return x ** 3

cube(2)
```
```
8
```

## 함수의 Output
### 함수의 return
- 함수의 return value는 한 개이다.
- 함수는 반환 되는 값이 있으며, 오직 한 개의 객체만 반환된다.

> 아래는 함수를 call 한 코드이다. 아래는 그 자체 덩어리로 묶어 return value인 6으로 보도록 노력하자.
```python
sum([1, 2, 3])
```
```
6
```

> `sum([1, 2, 3])` 이 return value 인 6으로 보기 때문에, 아래처럼 `int` 와 연산자로 계산할 수 있는 것이다.
```python
sum([1, 2, 3]) + 6
```
```
12
```

- 함수의 `return` 유무
  - 함수는 `return`이 없으면, 끝까지 실행되고, None을 반환
  - 함수는 `return`이 있으면, 그 자리에서 바로 종료. 함수를 호출한 곳으로 돌아간다.

> 아래 함수를 call 했을 때, `return`에서 종료되기 때문에 아래 있는 `print('루프')` 에 대해 `루프`는 출력되지 않는다.
```python
def infinite():
    print('무한')
    return 1
    print('루프')

infinite()
```
```
무한
1
```

> 아래 함수를 call 했을 때, `while` 뒤에는 항상 True 이기 때문에 무한루프가 되는 반복문이지만, `return`이 있기 때문에 종료된다.
```python
def infinite2():
    while True:
        print('무한')
        return 1

infinite2()
```
```
무한
1
```

> return 뒤에 value로 아무것도 작성하지 않으면, `None`이 output으로 나온다. python에서 `None`은 return으로 보통 나오지 않기 때문에, `print()`로 확인해주었다.
> 
> `print()`는 return value가 없는 함수라서 출력해서 보여주기는 하지만, 사실은 `None Type`이다.
```python
def infinite3():
    return

print(infinite3())
```
```
None
```
## 함수의 Input
### 매개변수와 전달인자
```python
def func(x):
      return x + 2

func(3)
```
1. 매개변수(parameter)
   - 함수의 정의(선언) 부분의 `x`는 매개변수  
   - 입력을 받아 함수 내부에서 활용할 **변수**
2. 전달인자(argumetn)
   - 함수의 호출(call) 부분의 `3`은 함수의 (전달)인자
   - 실제로 전달되는 **입력값**

### 함수의 인자
함수는 입력값으로 인자(argument)를 넘겨줄 수 있다.
1. 위치 인자
   - Positional Arguments 
   - **기본적으로 인자는 위치에 따라 함수 내에 전달된다.** 인자가 어떤 위치에 있는 지에 따라 retrun value가 달라지기 때문이다. 


   - ```python
     def my_func(a,b):
          return (a ** b) + b
     ```
   -  `my_func(3,5)` : my_func 함수에 매개변수 a와 b에 각각 매개변수의 위치에 따라 `a = 3`, `b = 5` 라고 인자를 할당하여 함수를 실행한다. 
   - ```python
     def my_func(a, b):
         # a = 3
         # b = 5
         return (a ** b) + b
     ```    
   - 인자의 순서를 바꾸면 다른 값이 나올 수 있기 때문에 매개변수의 위치에 맞춰 인자를 할당해야 한다.
     - my_func(3, 5)와 my_func(5, 3)의 return value는 다르다. 

2. 기본 인자 값
   - Default Argument Values
   - **함수를 정의할 때** 기본값을 지정하면, 함수를 호출할 때 인자의 값을 설정하지 않아도 기본값이 나온다.
   - 정의된 매개변수 개수보다 더 적은 개수의 인자들로 호출 될 수 있다.
   - 함수의 정의 중 기본 인자 값을 설정하는 소괄호()에서는 기존 스타일 프레임과 달리 연산자 사이에 스페이스를 하지 않는 쪽을 추천한다.
   - ```python
     def func(p1=v1):
         return p1

     func()   
     ```
     ```
     p1
     ```
   - 매개변수가 여러 가지일 때, 일부만 기본 인자 값을 설정할 수 있다. 대신, **기본 인자값(Default Argument Value)을 가지는 인자 다음에 기본 값이 없는 인자를 사용할 수는 없다.**
     -  기본 인자 값을 설정하는 매개변수 위치는 위치 인자 뒤로 가야한다.
     1. 기본 인자 값이 설정되어 있더라도, 기존함수의 호출과 동일하게 매개변수의 위치에 맞게 위치 인자를 할당해 return value를 계산
        - ```python
          def my_sum(a, b=0)
              return a + b
          ``` 
          ```python
          my_sum(3, 5)

          # 아래와 같은 할당 과정이 진행되어 호출된다고 이해하면 된다.
          def my_sum(a, b=0)
              # b = 0
              # a = 3
              # b = 5
              return a + b
          ```
          ```
          8
          ```
     2. 인자의 값이 없는 곳에 기본값을 활용해 return value를 계산
        - ```python
          my_sum(3)

          # 아래와 같은 할당 과정이 진행되어 호출된다고 이해하면 된다.
              # b = 0
              # a = 3
              return a + b
          ``` 
          ```
          3
          ```
3. 키워드 인자
   - Keyword Argumets
   - **함수를 호출할 때** 키워드 인자를 활용하여 직접 변수의 이름으로 특정 인자를 전달할 수 있다.

   > 아래처럼 매개변수와 위치가 맞지 않아도, 키워드 인자를 통해 매개변수에 인자를 할당할 수 있다. 단, 기본값 인자와 같은 이유로 키워드 인자를 활용한 다음에 위치 인자를 활용할 수 없기 때문에, 위치 인자와 같이 사용하는 경우 키워드 인자는 그 뒤에 순서해야 한다. 
   - ```python
     def greeting(age, name):
         return f'{name}는 {age}살 입니다.'

      greeting(name='한노아', age=21)
     ```
     ```
     '한노아는 21살입니다.'
     ```



## 정해지지 않은 여러 개의 인자 처리
### 가변(임의) 인자 리스트 (Arbitrary Argument Lists)
 **함수를 정의할 때** 가변 인자 리스트 `*args`를 활용하면 `print()`처럼 개수가 정해지지 않은 임의의 인자를 받을 수 있다.
- 매개변수에 `*`로 표현
- `*args` : 임의의 개수의 위치인자를 받음을 의미. 
  - arguments(인자들)의 약자
  - args는 변수명이라 다른 식별자로 사용해도 상관없고 `*`가 가변 인자로 역할을 부여함
```python
def func(a, b, *args)
   return args

print(func(1, 2, 'a', [1, 2, 3]))
print(type(func(1, 2, 'a', [1, 2, 3])))
```
```
(1, 2, 'a', [1, 2, 3])
<class 'tuple'>
```
- 가변 인자 리스트는 `tuple`로 처리된다.
- 보통, 가변 인자 리스트는 매개변수 목록의 마지막에 위치한다.
### 가변(임의) 키워드 인자 (Arbitrary Keyword Arguments)
**함수를 정의할 때** 가변 키워드 인자 `**kwargs`를 활용해 정해지지 않은 키워드 인자들을 받을 수 있다.
- 매개변수에 `**`로 표현
-  `**kwargs` : 임의의 개수의 키워드 인자를 받음을 의미
```python
def func(**kwargs)
```
- 가변 키워드 인자는 **`dict`** 형태로 처리
```python
def my_dict(**kwargs):
    return kwargs

print(my_dict(한국어='안녕', 영어='hi', 독일어='Guten Tag'))
```
```
{'한국어': '안녕', '영어': 'hi', '독일어': 'Guten Tag'}
```
- 구조상 URL도 가변 키워드 인자를 활용해 생성할 수 있다.