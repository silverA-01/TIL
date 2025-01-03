# 03. 연산자

## 연산자와 피연산자
```
3 + 4
a - b
```
- 연산자(operator) : 계산을 수행하는 연산 기호 ex.(`+`, `-`)
- 피연산자(operand) : 연산 대상 ex.(`3`, `4`, `a`, `b`)

## 연산자의 종류
- 산술 연산자 : `+`, `-`, `*`, `/`, `%`(나머지 연산자)
- 증감(증가 및 감소) 연산자 : `++`, `--`
- 비교 연산자 : `==`, `!=`, `>`, `<`, `>=`, `<=`
- 논리 연산자 : `&&`(AND), `||`(OR), `!`(NOT)
- 대입 연산자 : `=`, `+=`, `-=`, `*=`, `/=`, `%=`
- 삼항 연산자 : `? :`


## 산술 연산자
- 주로 숫자를 계산하는데 사용되며, 수학 연산을 수행

|산술 연산자|수행|
|---|---|
|+|더하기|
|-|빼기|
|*|곱하기|
|/|나누기|
|%|나머지|

```java
package operator;

public class Operator1 {
    public static void main(String[] args) {
        // 변수 선언 + 초기화
        int a = 5;
        int b = 2;

        // 덧셈
        int sum = a + b;
        System.out.println("a + b = " + sum);

        // 뺄셈
        int diff = a - b;
        System.out.println("a - b = " + diff);

        // 곱셈
        int multi = a * b;
        System.out.println("a * b = " + multi);

        // 나눗셈
        int div = a / b; // 5 / 2 = 2.5 -> int는 정수형이기 때문에 소수점이 날아가서 2가 출력
        System.out.println("a / b = " + div);

        // 나머지
        int mod = a % b;  // 5 / 2 의 몫은 2, 나머지는 1
        System.out.println("a % b = " + mod);
    }
}
```
```
a + b = 7
a - b = 3
a * b = 10
a / b = 2
a % b = 1
```
- 자바에서 같은 `int` 형끼리 계산을 했을 때 계산 결과도 `int`형을 사용한다. 정수형 데이터이기 때문에 소수점 이하를 포함할 수 없다.

> 참고 : `0`으로 나누기 불가능
> - 분모에 0을 두는 것은 수학에서 허용하지 않기 때문에 에러 발생
>   - `Exception in thread "main" java.lang.ArithmeticException: / by zero`
>  - ex. `10 / 0`과 같이 숫자는 0으로 나눌 수 없다.

## 문자열 더하기
- 문자열에도 `+` 연산자를 사용하면 두 문자를 연결할 수 있다.
```java
package operator;

public class Operator2 {
    public static void main(String[] args) {
        // 1-1) 문자열 + 문자열
        String result1 = "hello" + "java";
        System.out.println(result1);

        // 1-2) 문자열 + 문자열
        String s1 = "string1";
        String s2 = "string2";
        String result2 = s1 + s2;
        System.out.println(result2);

        // 2-1) 문자열 + 숫자
        String result3 = "a + b = " + 10;
        System.out.println(result3);

        // 2-2) 문자열 + 숫자
        int num = 20;
        String str = "a + b = ";
        String result4 = str + num;
        System.out.println(result4);
    }
}
```
```
hellojava
string1string2
a + b = 10
a + b = 20
```
- 문자열과 다른 데이터 형식이 더해지면 문자열이 됨
  - 문자와 숫자를 더하면 숫자를 문자열로 변경한 다음에 서로 더한다.
  - `System.out.println(result4.getClass().getName());` : 출력 결과 `java.lang.String`
  - `<변수명>.getClass().getName()` : 변수 타입을 가져오는 메서드

## 증감 연산자

## 비교 연산자

## 논리 연산자

## 대입 연산자

## 연산자 우선순위
|우선순위|연산자|내용|
|---|---|---|
|1|(), []|괄호, 대괄호|
|2|!, ~, ++, --|부정 / 증감 연산자 |
|3|*, /, % |곱셈, 나눗셈, 나머지 연산자|
|4|+, -|덧셈, 뺄셈 연산자|
|5|<<, >, >>>|비트 단위의 쉬프트 연산자|
|6|>, <, >=, <=|비교 연산자|
|7|==, !=|비교 연산자|
|8|&|비트 단위의 논리 연산자|
|9|^||
|10|||
|11|&&|논리 연산자(AND)|
|12|\|\||논리 연산자(OR)|
|13|? :|삼항(조건) 연산자|
|14|=, +=, -=, *=, /=, %=, <<=, >>=, &=, ^=, ~=|대입 / 할당 연산자|

## 참고
> - [김영한의 자바 무료 입문 강의](https://www.youtube.com/watch?v=JEzBDk0E9Rw&t=1312s)
> [자바의 연산자 및 연산자 우선순위](https://toma0912.tistory.com/66)