# 01. Java 기초

## Java의 역사
- 원래 가전제품을 제어하기 위한 언어로 고안
- 웹의 등장으로 엄청난 성공을 거두며 주류 언어가 됨

## Java의 현재
- 기업(엔터프라이즈)용 시장에서 두각
- 한국에서는 정부나 기업의 시스템 통합 프로젝트가 대부분 Java로 구현되고 있음
    - 시스템 통합(System Integration) : 기관이나 기업의 업무 관리를 소프트웨어화 하는 것
    - 국내에서 시장 규모가 큰 언어 중 하나
- 대중적인 IT 기기 초창기에 강력한 객체지향 언어로 큰 역할
- 특히 안드로이드 앱 개발을 위한 언어로 채택
  - 모바일 플랫폼인 안드로이드가 대성공을 거두면서 자바의 수요 급중
  - 자바의 단점으로 보완하는 형식으로 코틀린(Kotlin), 플러터(Flutter) 언어가 발전되어 안드로이드 앱 개발 언어로 같이 사용

## Java의 특징
- 객체지향 언어

## 자바 표준 스펙
![Java 표준 스펙 및 구현](\_asset\Java_spec.png)
- 자바는 표준 스펙과 구현으로 나눌 수 있다.
### 자바 표준 스펙
- 자바는 이렇게 만들어야 한다는 설계도이며 문서이다.
- 이 표준 스펙을 기반으로 여러 회사에서 실제 작동하는 자바를 만든다.
- 자바 표준 스펙은 자바 커뮤니티 프로세스(JCP)를 통해 관리된다.
### 다양한 자바 구현
- 여러 회사에서 자바 표준 스펙에 맞추어 실제 작동하는 자바 프로그램을 개발
  - 변경의 용이 : 따라서 오라클 Open JDK를 사용하다 Amazon Corretto 자바로 변경해도 대부분 문제없이 작동함
- 각각 장단점 존재(ex. Amazon Corretto는 AWS에 최적화)
- 각 회사들은 대부분 윈도우, MAC, 리눅스 같이 다양한 OS에서 작동하는 버전의 자바도 함께 제공

> 참고 : [다양한 자바 구현에 대한 참조 사이트](https://whichjdk.com/ko/)

## 자바 프로그램의 동작
![Java 컴파일과 실행](\_asset\Java_compile_execute.png)
1. 개발자가 **코드 작성**
2. 컴퓨터가 실행할 수 있는 형태로 코드를 **컴파일**
   - 자바가 제공하는 `javac`라는 프로그램을 사용해 `.java` 파일을 변환하여 `.class` 파일을 생성
     - ex. `Hello.java` → `Hello.class`
   - 자바 소스 코드를 바이트코드로 변환하여 자바 가상 머신(JVM)에서 더 빠르게 실행될 수 있게 최적화하고 문법 오류도 검출한다.
3. 컴파일된 프로그램을 **실행**
  - 자바가 제공하는 `java` 프로그램을 사용
  - 자바 가상 머신(JVM)이 실행되면서 프로그램이 작동

### Java SE
- Java Platform, Standard Edition의 약자
- 자바의 표준안
- 자바라는 언어가 어떠한 문법적인 구성을 가졌는지와 같은 것들을 정의
  - 소프트웨어의 설계도라고 할 수 있음, 소프트웨어에서는 설계도 대신 명세서(spec, specification)이라고 표현
- Java SE 명세서에 따라 Java가 만들어지게 됨
  - Java SE 7은 버전 7에 대한 명세서라고 이해하면 됨
- JCP(Java Community Process) 조직을 통해 만들어짐

![Java의 구조](\_asset\Java_Structure.png)

### JDK
- Java Development Kit
- Java SE에 따라 만들어진 구체적인 소프트웨어
- 자바의 개발환경, 개발자를 위한 자바 버전
- 자바 프로그램을 실행하면 컴파일러, 개발자에 필요한 각종 도구, JRE가 포함되어 있음
- JDK ⊃ JRE ⊃ JVM 으로 이해할 수 있음

1. Java SE(Standard Edition)
   - 자바의 핵심, 일반적인 자바를 의미
2. JAVA EE(Enterprise Edition)
   - 기업용 시장에서 사용하는 자바 개발환경
3. Java Me(Micro Edition)
   - 모바일 개발을 위해서 사용하는 자바 버전

### JRE
- Java Runtime Environment
- 자바가 실제로 동작하는 데 필요한 JVM, 라이브러리, 각종 파일들이 포함
- 자바로 만들어진 프로그램을 구동하기 위한 것

### JVM
- Java Virtual Machine
- 자바가 실제로 구동하는 환경
- 자바로 만들어진 소프트웨어는 JVM이라는 가상화된 환경에서 구동됨
- 하드웨어나 운영체제에 따라서 달라질 수 있는 호환성 문제는 버전에 따라 만들어진 JVM이 알아서 해결
- 하나의 자바 프로그램을 만들면 어떤 환경에서도 실행할 수 있도록 하는 역할


## 개발 환경 설정 - IDE(Integrated Development Environment)
- IDE(통합 개발 환경) : 개발에 필요한 다양한 도구들이 결합되어 있는 소프트웨어
  - 소스 편집기, 컴파일러, 디버거, 유닛테스트 등과 같은 도구들이 결합되어 있음
### IDE : 인텔리제이(IntelliJ) VS 이클립스(Ecliose)
- 과거에는 이클리스를 많이 사용했지만, 최근에는 빠른 속도와 사용의 편의성 때문에 인텔리제이를 주로 사용
- 자바로 개발하는 대부분의 메이저 회사들도 최근에는 인텔리제이를 주로 사용

### 인텔리제이를 통한 자바 설치 관리
![인텔리제이를 통한 자바 설치 관리](\_asset\Java_IDE_01.png)
- 인텔리제이는 내부에 자바를 편리하게 설치하고 관리할 수 있는 기능을 제공
- 이 기능을 사용하면 인텔리제이를 통해 자바를 편리하게 다운로드 받고 실행할 수 있음
- 자바를 OS에 직접 설치해도 되지만, 처음 프로그래밍 시작하는 경우 환경 설정이 복잡할 수 있음

### 인텔리제이를 통한 자바 컴파일, 실행 과정
![인텔리제이를 통한 자바 컴파일, 실행 과정](\_asset\Java_IDE_02.png)
- 컴파일
  - 자바 코드를 컴파일 하려면 `javac`라는 프로그램을 직접 사용해야 하는데, 인텔리제이는 자바 코드를 실행할 때 이 과정을 자동으로 처리해준다.
  - 인텔리제이 화면에서 프로젝트에 있는 `out` 폴더에 가보면 컴파일된 `.class` 파일이 있는 것을 확인할 수 있다.
- 실행
  - 자바를 실행하려면 `java` 프로그램을 사용해야 한다. 이 때 컴파일된 `.class` 파일을 지정해주면 된다.
    - ex. `Hello.class`로 컴파일된 자바 파일을 실행하기 위해 `java Hello` 명령문 실행 (참고로 확장자는 제외)
- 인텔리제이에서 **자바 코드를 실행하면 컴파일과 실행을 모두 한번에 처리**한다.
- 인텔리제이 덕분에 매우 편리하게 자바 프로그램을 개발하고 학습할 수 있다.

## 개발 환경 설정 - OS(Operating system)
### OS : 윈도우 VS Mac
- 자바로 개발하는 대부분의 메이저 회사들은 Mac 사용 

### 자바와 운영체제 독립성
1. **일반적인 프로그램**
   ![일반 프로그램과 OS의 호환성](\_asset\Java_OS_01.png)
   - 일반적인 프로그램은 다른 OS에서 실행할 수 없음
   - 윈도우 프로그램은 윈도우 OS가 사용하는 명령어들로 구성되어 있기 때문에, 해당 명령어는 다른 OS와는 호환되지 않음
2. **자바 프로그램**
   ![자바 프로그램과 OS의 호환성](\_asset\Java_OS_02.png)
   - 자바 프로그램은 자바가 설치된 모든 OS에서 실행할 수 있음
   - OS 호환성 문제는 자바가 해결함 : 자바 개발자는 특정 OS에 맞추어 개발을 하지 않아도 되며, 자바에 맞추어 개발하면 됨. 
     - `Hello.class`로 컴파일된 자바 파일은 모든 자바 환경에서 실행 가능
   - 각 OS별 자바는 해당 OS가 사용하는 명령어들로 구성되어 있기 떄문에, 개발자는 각 OS에 맞도록 자바를 설치하기만 하면 된다.
3. **자바 개발과 운영 환경**
   ![자바 개발과 운영 환경](\_asset\Java_OS_03.png)
   - 개발할 때 자바와 서버에서 실행할 때 다른 자바를 사용할 수 있다.
   - 개발자들은 개발의 편의를 위해 윈도우나 MAC OS를 주로 사용함
   - 서버는 주로 리눅스를 사용함
     - 만약 AWS를 사용한다면 Amazon Corretto 자바를 AWS 리눅스 서버에 설치하면 됨
   - 자바의 운영체제 독립성 덕분에 각각의 환경에 맞추어 자바를 설치하는 것이 가능함



## IntelliJ IDEA 설치 및 실행
- [IntelliJ IDEA Community Edition 다운로드](https://www.jetbrains.com/ko-kr/idea/download/?section=windows) : OS에 맞게 다운로드

![IntelliJ_new_project](\_asset\IntelliJ_new_project.png)
1. New Project 생성
2. Language : Java
3. Name : 프로젝트 명(임의)
4. Location : 프로젝트 위치(임의)
5. Build system : IntelliJ 선택
6. JDK : 자바 버전 17 이상 사용
   - JDK는 자바 개발자를 위한 도구 + 자바 실행 프로그램의 묶음
   - 다운로드된 JDK가 없을 경우 앱 내에서 `Download JDK`에서 특정 버전의 JDK 다운로드 지원
     ![IntelliJ_new_project](\_asset\IntelliJ_new_project_download_JDK.PNG)
     - Version : 23 (임의)
     - Vendor : Oracle OpenJDK (임의)
       - aarch64 : 애플 M1, M2, M3 CPU 사용시 선택
       - 나머지는 뒤에 이런 코드가 붙지 않은 JDK 선택
     - Location : JDK 설치 위치, 기본값으로 사용 추천
7. `Add sample code`, `Generate code with onboarding tips` 선택시 샘플 코드 및 온보딩 팁을 위한 코드 생성

## IntelliJ IDEA 단축키
- `Shift` + `F10` : 코드 실행
- `Alt` + `Enter` : IntelliJ IDEA의 수정 제안사항 표시
- `Shift` + `F9` : 디버깅 시작
- `Ctrl` + `F8` : 디버깅 breakpoint 생성 및 제거 
- `Shift` + `Enter` : 코드 작성 시 줄 바꿈
- `Ctrl` + `D` : Duplicate Line, 코드 라인을 아래에 복제하여 생성
- `Alt` + `J` :  특정한 단어를 해당 라인 기준 뒤에서 하나씩 추가 선택하여 수정하기
- `Ctrl` + `Shift` + `Alt` + `J` :  특정한 단어를 한 번에 수정하기

## Java 프로그램 실행
1. Project 내 `src` 디렉토리에서 `New` - `Java Class` 클릭
2. Class Name : `HelloJava` (임의)
3. `Class` 선택
4. `HelloJava.java` 파일 생성
   - Class 명의 시작은 관례상 대문자로 작성해야 함

```Java
public class HelloJava {
    public static void main(String[] args) {
        System.out.println("hello java1");
        System.out.println("hello java2");
    }
}
```
```
hello java1
hello java2
```
- 자바 언어는 대소문자를 구분한다. 대소문자가 다르면 오류가 발생할 수 있다.

- `public class HelloJava`
  - 파일명과 클래스명이 같아야 한다
  - `{}` 블록을 사용해서 클래스의 시작과 끝을 나타낸다.

- `public static void main(String[] args)`
  - `main` 메서드(method, 함수)라고 한다.
  - 자바는 `main(String[] args)` 메서드를 찾아서 프로그램을 시작한다.
  - `{}` 블록을 사용해서 매서드의 시작과 끝을 나타낸다.
  - 프로그램은 `main()`을 시작으로 위에서 아래로 한 줄씩 실행된다.
  - `psvm`을 통해 IntelliJ IDEA에서 자동 생성 가능
  - `public` : 접근제어자 또는 접근제한자로 모든 클래스에서 접근이 가능하도록 한다. 자바는 어플리케이션이 실행되면 제일 먼저 메인 함수를 실행시키고, 메인 함수는 모든 실행 프로그램에 기본이 되는 함수이기 때문에 어디에서나 접근이 가능해야 한다. 해당 메서드는 JVM 어느곳에서든지 접근이 가능해야 하기 때문에 `public`을 사용.
  - `void` : 반환(return) 값을 의미. '존재하지 않음' 혹은 '아무것도 없이 비어 있음'을 의미하는 단어. 
    - `void`는 함수가 끝날 때 리턴값이 없이 끝내라는 의미. 메서드 내부에서 어떤 동작을 수행하고 나서 아무것도 반환하지 않을 때 사용.
    - 메서드가 종료되서 리턴값이 있어도 프로그램은 종료되어 있기 때문에, 값을 반환해주더라도 사용할 수 없기 때문에 `void` 외의 다른 type을 작성하면 에러가 발생한다.
    
  - `static` : 메서드 앞에 입력하여 정적 변수를 선언. 
    - `class loader`에 의해 class가 로딩될 때 `static`으로 선언된 자원들을 JVM의 `method area` 영역에 저장된다. 즉, 메모리에 메인 메서드가 로드되어 객체를 생성하지 않고 실행되어 작업을 수행할 수 있게 된다. 
    - 메인 메서드는 프로그램에 없어서는 안되는 기본 함수이기 때문에 `static`을 사용하여 메모리에 항상 살아있을 수 있게 선언해주어야 한다.
    - 자바에서 변수나 함수를 메모리에 할당하는 방법
      |메모리 할당 방식|메모리 할당 기준|메모리 정리 기준(Garbage Collector)|
      |---|---|---|
      |**static**|프로그램이 실행되는 순간|정리 대상이 아님|
      |**heap**|연산이 실행되는 순간|Garbage collector에 의해 정리|
  - `main` : 자바의 기본 메서드이며 고정된 형태. 자바의 시작은 main 함수명으로 시작해야 한다. 이것이 자바의 규칙!
  - `String[] args` : 자바에서는 기본 메서드에 `String` 배열 유형의 단일 인수를 허용한다. '자바 명령행 인수'라고도 한다. 명령인수를 통해 프로그램이 실행할 때 명령줄 인수를 전달할 수 있다.
    - "main 메소드를 실행하는 데 필요한 값들이 있다면 args이라는 문자열을 배열을 통해서 main 메소드에 전달하겠다"라는 의미
    - `args`는 변수명이기 때문에 꼭 `args`가 아니여도 상관은 없다. `String[] <변수명>` 구문 자체는 꼭 써줘야한다.

- `System.out.println("hello java1");`
  - `System.out.println()` : `()` 안의 값을 콘솔에 출력하는 기능
  - 자바는 문자열(String)을 사용할 때 `"`(쌍따옴표)를 사용한다.
    - > 참고 : `'`작은따옴표는 문자(Character)를 감싸는 기호로 사용한다. 작은따옴표 사이에는 문자 하나만 입력할 수 있다.
  - `;` : 자바는 세미콜론으로 문장을 구분한다. 문장이 끝날때 필수적으로 `;`을 넣어주어야 한다.
  - `sout`을 통해 IntelliJ IDEA에서 자동 생성 가능

## 주석(Comment)
- 한 줄 주석(single line comment) : `//` 기호로 시작. 이 기호 이후의 모든 텍스트는 주석 처리.
- 다중 줄 주석(multi line comment) : `/*`로 시작하고 `*/`로 끝난다. 이 사이의 모든 텍스트는 주석 처리
```java
public class CommentJava {
    public static void main(String[] args) {
        System.out.println("hello java1"); //hello java1을 출력합니다.(한 줄 주석 - 부분 적용)
        //System.out.println("hello java2"); 한 줄 주석 - 라인 전체 적용
        
        /* 여러 줄 주석
        System.out.println("hello java3");
        System.out.println("hello java4");
         */
    }
}

```
```
hello java1
```

## 참고
> - [생활코딩 JAVA1 강의](https://opentutorials.org/module/4294)
> - [김영한의 자바 무료 입문 강의](https://www.youtube.com/watch?v=JEzBDk0E9Rw&t=1312s)
> - [PSVM - public static void main 뭔가요?](https://choi-hye-min.github.io/post20190603/)
> - [자바. psvm 제대로 알고 사용하자!](https://velog.io/@tae_in/%EC%9E%90%EB%B0%94.-psvm-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%95%8C%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90)
> - [Java 표준 스펙과 구현](https://velog.io/@njw4803/Java-%ED%91%9C%EC%A4%80-%EC%8A%A4%ED%8E%99%EA%B3%BC-%EA%B5%AC%ED%98%84)
