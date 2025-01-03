# 02. Java 변수
## 패키지(package)
- 클래스의 묶음으로 클래스를 용도별이나, 기능별로 그룹화 한 것
1. `src` 디렉토리 내 package 생성 : `variable` (임의)
2. `variable` package 내 class 생성 : `Var1` (임의)
```java
package variable; //자바 파일 첫 줄에 소속된 패키지를 선언

public class Var1 {
    public static void main(String[] args) {
        System.out.println(10);
        System.out.println(10);
        System.out.println(10);
    }
}

```
```
10
10
10
```
- 자바 파일이 위치하는 패키지와 `package variable` 선언 위치가 같아야 한다.
- 출력 결과를 모두 20으로 바꾸고 싶으면 수동으로 `10`을 `20`으로 바꿔야 한다. 하지만, 복잡한 코드의 경우 모든 수를 찾아 바꾸는 것은 번거로운 일이다. 이 때 변수를 활용하면 편리하다.

## 변수(variable)
- 변할 수 있는 수를 의미
```java
package variable; //자바 파일 첫 줄에 소속된 패키지를 선언

public class Var1 {
    public static void main(String[] args) {
        int a; //변수 선언
        a = 10; //변수 초기화(대입)
        System.out.println(a);
        System.out.println(a);
        System.out.println(a);
    }
}

```
```
10
10
10
```
- `System.out.println();` 안의 값을 하나씩 수정하는 것보다 변수를 활용하여 함께 변경할 수 있게 코드를 효율적으로 작성할 수 있음
### 변수 선언
- 변수를 만드는 것
- 변수를 선언하면 컴퓨터의 메모리 공간을 확보해서 그곳에 데이터를 저장할 수 있다. 그리고 변수의 이름을 통해 해당 메모리 공간에 쉽게 접근할 수 있다. 
- 즉, 데이터를 보관할 수 있는 공간을 만들고, 그곳에 이름을 부여한다.
- `int a` : 숫자 정수(integer)를 보관할 수 있는 `a`라는 이름의 데이터 저장소를 만드는 것으로 이를 변수라고 한다.
  - 변수 선언을 하면 변수 `a`에 int 데이터 타입을 보관할 수 있다.
```java
package variable;

public class Var2 {
    public static void main(String[] args) {
        int a; // 변수를 하나씩 선언 가능
        int b,c; // 한 번에 여러 변수를 선언할 수 있음
    }
}
```

### 변수 초기화
- 변수를 선언하고, 처음 선언한 변수에 처음으로 값을 대입해서 저장하는 것
- `a = 10` : 숫자를 보관할 수 있는 데이터 저장소인 변수 `a`에 숫자 정수 값 `10`을 저장
  - 자바에서 `=`은 오른쪽에 있는 값을 왼쪽에 저장한다는 뜻. 수학에서 두 값이 같다(equals)는 것과 다른 뜻
```java
package variable;

public class Var3 {
    public static void main(String[] args) {
        //1. 변수 선언, 초기화 각각 따로
        int a;
        a = 1;
        System.out.println(a);

        //2. 변수 선언과 초기화를 한 번에
        int b = 2;
        System.out.println(b);

        //3. 여러 변수 선언과 초기화를 한 번에
        int c = 3, d = 4;
        System.out.println(c);
        System.out.println(d);
    }
}
```
```
1
2
3
4
```
- 변수 선언과 초기화는 각각 따로도 가능하고, 동시에도 가능하다.
```java
package variable;

public class Var4 {
    public static void main(String[] args) {
        int a;
        System.out.println(a);
    }
}
```
```
C:\Users\user\java\java-start\src\variable\Var4.java:6:28
java: variable a might not have been initialized
```
- 변수는 반드시 초기화 해야 한다. 변수 선언만 하고 변수를 읽으려고 하면 초기화 되지 않았다는 컴파일 에러 발생
    - 컴퓨터에서 메모리는 여러 시스템이 함께 사용하는 공간으로 어떠한 값들이 계속 저장된다. 변수를 선언하면 컴퓨터 메모리 상 어떤 공간을 차지하고 사용한다. 그 공간에 기존에 어떤 값이 있었는지 아무도 모르기 때문에 초기화를 하지 않으면 이상한 값이 출력될 수 있다. 이러한 문제를 예방하기 위해 자바는 변수를 초기화 하도록 강제한다.
- `6:28` : 6번째 줄, 28번째 단어에 에러가 있다는 뜻으로 `System.out.println(a);`에서 `a`에 에러가 발생핬다는 것
> **참고** : 개발자가 직접 초기화 해야하는 것은 지역 변수(Local Variable)에 해당하는 내용으로, 클래스 변수 및 인스턴스 변수는 자바가 자동으로 초기화를 진행해줌

### 변수 값 읽기
- `System.out.println(a)` : - 변수에 저장되어 있는 값을 읽어서 사용하는 방법은, 변수 이름(`a`)을 적어주면 된다.
  - 변수 `a`에 `10`이 들어가 있다면 자바는 실행 시점에 변수의 값을 읽어서 사용한다.
    > 1. 변수 `a`의 값을 읽음
    > 2. `a`의 값인 `10`으로 변경
    > 3. 숫자 정수 `10`을 출력
  - 변수의 값은 반복해서 읽을 수 있다. 변수의 값을 읽는다고 값이 없어지는 것이 아니다.

### 변수 값 변경
```java
package variable; //자바 파일 첫 줄에 소속된 패키지를 선언

public class Var1 {
    public static void main(String[] args) {
        int a; //변수 선언
        a = 10; //변수 초기화(대입) : a(10)
        System.out.println(a);
        a = 50; //변수 값 변경 : a(10 -> 50)
        System.out.println(a);
        System.out.println(a);
    }
}
```
```
10
50
50
```
- 변수의 값을 변경하면 변수에 들어있던 기존 값은 삭제된다.

## 변수의 타입
- 변수는 데이터를 다루는 종류에 따라 다양한 형식(type)이 존재
- 각 변수는 지정한 타입에 맞는 값을 사용해야 한다. 그렇지 않을 경우 컴파일 오류 발생
- 변수를 선언하면 타입별 표현 범위에 따라 메모리 공간을 차지하기 때문에, 필요에 맞도록 적절한 타입의 변수를 선택해야 함
    > 참고 : 메모리 용량은 매우 저렴하다. 따라서 메모리 용량을 약간 절약하기 보다는 개발 속도나 효율에 초점을 맞추는 것이 더 효과적이다. 
```java
package variable;

public class Var5 {
    public static void main(String[] args) {
        int a = 100; //정수
        double b = 10.5; // 실수
        boolean c = true; // boolean : 참(True) or 거짓(false)
        char d = 'A'; // 문자(Character) 하나 : ''(작은따옴표)로 감싼다.
        String e = "Hello Java"; //문자열, 문자열을 다루기 위한 특별한 타입, 앞에 대문자 주의 : ""(큰따옴표)로 감싼다.
        String f = "A"; // 문자 하나도 문자열에 포함

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
        System.out.println(e);
        System.out.println(f);
    }
}
```
```
100
10.5
true
A
Hello Java
A
```

### 리터럴(literal)
```java
int a = 100; //정수 리터럴
double b = 10.5; // 실수 리터럴
```
- 리터럴 : 문자 또는 글자를 의미
- 코드에서 개발자가 직접 `00`, `0.5`와 같은 고정된 값을 프로그래밍 용어로 리터럴이라 함
- 변수의 값은 변할 수 있지만, 리터럴은 개발자가 직접 입력한 고정된 값으로 리터럴 자체는 변하지 않는다.

### 정수 타입
|정수 타입 변수|크기(byte)|범위|비고|
|---|---|---|---|
|**byte**|1byte|$-2^{7}$ ~ $2^{7}-1$(-128 ~ 127)|파일을 다룰 때 사용|
|**short**|2byte|$-2^{15}$ ~ $2^{15}-1$(-32,768 ~ 32,767)||
|**int**|4byte|$-2^{31}$ ~ $2^{31}-1$(-2,147,483,648 ~ 2,147,483,647)|약 20억, 대부분 정수는 `int`를 사용|
|**long**|8byte|$-2^{53}$ ~ $2^{53}-1$(-9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807)|정수 리터럴 뒤에 `l` 또는 `L` 붙여야 함|
- `long`의 경우 리터럴 뒤에 `L`을 붙이는 것을 권장(`l`은 숫자 1과 착각할 수 있어 궈ㅏㄴ장하지 ㅇ낳음)
- `byte`와 `short`는 표현 길이가 너무 작아 실무에서 거의 사용하지 않는다.
  - 대신 `byte`의 경우 파일을 바이트 단위로 다루기 때문에 파일전송, 파일 복사 등에 주로 사용된다.
- 또한 자바는 기본으로 4byte(`int`)를효율적으로 계산하도록 설계되어 있기 때문에 대부분 `int`를 사용하고 `int`의 표현 범위를 넘어가는 경우에만 `long`을 사용한다.

### 실수 타입
|정수 타입 변수|크기(byte/bit)|범위|비고|
|---|---|---|---|
|**float**|4byte, 32bit|$-3.4*10^{38}$ ~ $3.4*10^{38}$(-3.4E38 ~ 3.4E38), 7자리 정밀도(precision)|실수 리터럴 뒤에 `f` 또는 `F` 붙여야 함|
|**double**t|8byte, 64bit|$-1.7*10^{308}$ ~ $1.7*10^{308}$(-1.7E308 ~ 1.7E308), 15자리 정밀도|대부분 실수는 `double`를 사용|
```Java
float flovar1= 3.14;     // f 를 붙이지 않고 저장하면 컴파일 에러 발생!
float flovar2= 3.14f;    // 3.14 실수 리터럴이 저장된다.
```
- `float`는 표현길이와 정밀도가 낮기 때문에 `double`을 사용한다.

### 문자와 문자열 타입
|문자 타입 변수|크기(byte)|범위|
|---|---|---|
|**char**|2byte|모든 유니코드 문자|
- `char` : character의 약자로 문자(글자) 하나를 다룰 때 사용. 작은따옴표(`'`)를 사용해서 감싸야 함
- `String` : 문자들의 집합을 의미하는 문자열을 다룰 때 사용. 큰따옴표(`"`)를 사용해서 감싸야 함
  - 첫 글자가 대문자로 시작하는 특별한 타입
  - 메모리 사용량은 문자 길이에 따라 동적으로 달라진다.
  - 문자 하나도 문자열에 포함되고, 문자 하나만 사용하는 경우는 거의 없기 때문에 `char`보다 `String`을 사용한다.
    ```java
    String f = "A";
    ```
- **이스케이프(escape)** : 문자열 안에 큰따옴표(`"`)를 넣고 싶을 때 `\` 기호를 앞에 위치시킨다.
  ```java
  System.out.println("egoing said \"Welcome programming world\"");
  ```
  ```
  egoing said "Welcome programming world"
  ```
- **여러 줄 표시** : `\n`을 활용
  ```java
  System.out.println("HTML\nCSS\nJavaScript\n");
  ```
  ```
  HTML
  CSS
  JavaScript
  
  ```
- 문자의 연산 : `+` 기호를 활용해 아래와 같이 문자와 문자를 더할 수 있다.
  ```java
  System.out.println("문자"+"더하기");
  ```
  ```
  문자더하기
  ```

### boolean 타입
- `boolean` : 불리언 타입. `true` or `false` 값만 사용 가능. 주로 참과 거짓을 판단하는 곳에 사용. (1byte)
- 조건문에서 자주 사용

## 변수 명명 규칙
- 자바에서 변수의 이름을 짓는데는 규칙과 관례가 존재
  - 규칙은 필수적으로 따라야 하는 것으로 지키지 않을 경우 컴파일 오류 발생
  - 관례는 필수는 아니지만 전세계 게발자가 해당 관례를 따르기 때문에 사실상 규칙이라고 생각해도 된다.
- 참고: 변수 이름은 의미있고, 그 용도를 명확하게 설명해야 한다.
  - `int a;` : `a`는 변수의 용도를 설명하지 않기 때문에 단순 예제에서만 사용하는 것이 좋다.
  - `studentCount`, `maxScore`와 같이 변수명으로 용도를 명확하게 설명해야 한다.

### 규칙
- 변수 이름은 숫자로 시작할 수 없다. (ex. `1num`)
  - BUT 숫자를 이름에 포함하는 것은 가능 (ex. `num1`)
- 이름에는 공백이 들어갈 수 없다.
- 자바의 예약어를 변수 이름으로 사용할 수 없다. (ex. `int`, `class`, `public)
- 변수 이름에는 영문자(`a-z`, `A-Z`), 숫자(`0-9`), 달러 기호(`$`) 또는 밑줄(`_`)만 사용할 수 있다.

### 관례
- 소문자로 시작하는 낙타표기법(Camel Case) : 변수명을 소문자로 시작하는 것이 일반적임
  - 여러 단어로 이루어진 변수 이름의 경우, 첫 번째 단어는 소문자로 시작하고 그 이후의 각 단어는 대문자로 시작하도록 표기하는 낙타표기법을 사용
  -  ex. `orderDetail`, `myAccount`
> **낙타표기법(Camel Case)**
> - 이름이 여러 단어로 구성되어 있을 때, 각 단어의 첫 글자가 대문자로 시작하고, 이 대문자들이 낙타의 등봉처럼 보이는 것으로 유래
> - 프로그래밍에서 변수, 함수, 클래스 등의 이름을 지을 때 많이 사용하는 표기법 중 하나.
> - 낙타표기법을 사용하면 이름에 공백을 넣지 않고도 여러 단어를 쉽게 구분할 수 있으므로, 변수의 이름을 이해하기 쉽게 만들어 준다.

### 자바 언어의 관례(참고)
- 클래스는 대문자로 시작 + 낙타표기법 적용
- 클래스 외 나머지(변수, 함수 등)는 소문자로 시작 + 낙타표기법 적용
  - 자바에서 클래스 이름의 첫 글자는 대문자로 시작한다. 클래스 외 나머지는 모두 첫 글자를 소문자로 시작한다.
  - 클래스명 : `Person`, `OrderDetail`
  - 변수명 : `firstName`, `userAccount`
- 예외 1) 상수(변하지 않는 값)는 모두 대문자로 사용하고 언더바로 구분한다.
  - 상수명 : `USER_LIMIT`
- 예외 2) 패키지는 모두 소문자를 사용한다.
  - ex. `org.spring.boot`

## 참고
> - [김영한의 자바 무료 입문 강의](https://www.youtube.com/watch?v=JEzBDk0E9Rw&t=1312s)
> - [생활코딩 JAVA : 숫자와 문자](https://opentutorials.org/module/4294)
> - [생활코딩 JAVA : 데이터 타입](https://opentutorials.org/module/516/5375)
> - [Kephi의 Java 공부 노트 : 03-1. 실수 타입 (float, double)](https://wikidocs.net/81917)