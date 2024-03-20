# CLI Basic


## 1. CLI VS GUI

### 1. CLI
* Command Line Interface
- 명령어(커맨드)를 줄 단위로 읽고 실행하는 텍스트 기반 인터페이스
- 키보드를 통해 명령어(커맨드)를 입력하여 OS와 상호 작용하는 소프트웨어 메커니즘
- 표준 입출력 시스템(Standard I/O)을 통한 입력과 그에 따른 결과를 출력하는 형태
- 개발자나 시스템관리자와 같은 전문가들이 주로 사용
- 마우스와 각종 UI 컴포넌트로 실행되는 GUI(Graphic User Interface)와 반대되는 개념

> 우리가 아는 'MS DOS'는 CLI 인 것을 알 수 있다.
![MS DOS](https://i.namu.wiki/i/Y-4-e6-ojp93QMThpqmi_ukmSaTmfVY4gUDtdCy_oZiOlNsVtdfP8P2_JKGhIxj_P8-2ylizZS1uJjGtvrGSMQ.png)

### 2. GUI
* Graphical User Interface
- 사용자를 위한 시각적 표현을 한 인터페이스
- 그래픽을 사용하여 상호작용
  - 아이콘, 이미지 버튼, 창 등의 시각적인 요소를 탐색하고 마우스 등을 사용하여 클릭으로 작업을 수행
- 직관적이며 시각적으로 사용하기 쉬워 대부분의 컴퓨터 사용자가 익숙해질 수 있다.

> 'APPLE The Lisa'는 처음으로 대중적인 PC(personal computer) 시장을 점유했다. 아래 사진처럼 마우스를 이용해 작업하고 화면에 그래픽을 사용한 GUI가 만들어진 것이다.
![The Lisa](https://3894a8e173f5f8870a41-c88208a08312eda3cf96a15131ffd631.ssl.cf1.rackcdn.com/lisa11513184703168.jpeg)

### 3. Interface
서로 다른 두 존재의 접점(만나는 지점)
- CLI와 GUI는 서로 다른 작업을 하는 것 같지만 같은 결과를 가져올 수 있다.
- Hardware Interface : 입출력장치 등
  - HDMI(High Definition Media Interface) : 본체와 모니터의 접점
- Software Interface : 컴퓨터 언어, 명령어, Zoom을 포함한 프로그램 파일 등


## 2. CLI를 배워야 하는 이유
PC는 CLI를 거쳐서 GUI로 넘어왔다. 그렇지만 개발자는 왜 CLI를 배워야 할까?
- GUI는 일반 사용자들을 위해 기능적인 제한을 많이 걸어 두었다.
  - 기능적인 제한을 걸지 않는 초기 모델에서는, 일반 사용자들이 컴퓨터의 중요한 S.W를 지우는 등의 문제가 발생했다.
  - 이를 개선하기 위해 GUI는 파일/폴더를 삭제해도 휴지통 같이 복구할 수 있는 중간지대를 만들어 놓는 등의 작업이 추가되거나, 할 수 없는 기능들이 많다.
  
- CLI는 GUI보다 시스템 관리 작업을 하는데 있어서 효율적이고, 가상 또는 원격 환경에 적합하다.
  - 개발자와 시스템 관리자의 경우, CLI를 사용하는 것은 기본 시스템을 더 깊이 이해하는데 도움이 되고, 이를 통해 다양한 도구와 유틸리티를 더 능숙하게 사용하고 오류 관리를 개선할 수 있다.
    > GUI에서는 안 되지만 CLI에서 가능한 작업 : 동시에 여러 이름의 파일 생성 or 제거
    > - `touch a.txt b.txt c.txt` : a.txt, b.txt, c.txt 파일 생성
    > - `rm *.txt` : .txt 확장자인 모든 파일 제거
  
- 결론적으로, GUI보다 CLI에서 특정 환경에 국한되지 않고 유연하게 작업할 수 있다. 또한 자동화와 효율성을 강화하는데 도움이 된다. 개발자는 CLI를 이용할 때 기능적으로 다룰 수 있는 부분이 더 많기 때문에 CLI로 작업해야 한다.


## 3. OS Family Map
- OS는 Operating System의 약자로 운영체제를 의미
- OS는 크게 Unix와 Windows 두 가지로 나뉜다.

### 1. Unix
1. Linux
  - Unix를 뜯어 고쳐 무료/오픈소스로 배포한 것이 Linux
  - Linux Kernal로 다양한 운영체제들이 파생되어 Unix family tree는 아주 많다
  - 파생 운영체제는 전제조건이 오픈 소스, 무료배포이다.
  - ex. Ubuntu, Centos, Android etc.
  - ![Unix family tree](https://i.gzn.jp/img/2021/08/10/os-timeline-and-family-rree/img-snap01947_m.png)

2. APPLE
  - APPLE은 유료인 Unix를 정식 구매해 유료로 잠금 배포하는 운영체제
  - iOS, MacOS, iPadOS, visionOS
  
### 2. Windows
   - Unix와 달리 비교적 Windows 가계도는 깔끔하다.
   - Microsoft Winodws에서만 운영체제를 개발하여 배포하기 때문
   - ![Windows family tree](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcST2CkD07njPp32wTbE1zYuZD4Qx-X73KaEUxcyev5ysKR4Iz3bwp9EPF5az24xMWLrbLk&usqp=CAU)



## 4. CLI와 Unix
**CLI는 Unix OS에서 사용되는 인터페이스이다.** 

사실 Windows OS 환경에서는 기본 터미널인 cmd를 사용해 Windows용 명령어를 입력해야 한다. 하지만 `Git bash`와 같은 프로그램으로 Window OS에서도 CLI 명령어를 사용할 수 있다. 이 때 `Git Bash`는 Unix의 CLI 명령어를 Winodws용 명령어로 변환해주는 역할을 수행한다.

정리하자면 개발자들은 Unix OS의 CLI라는 환경을 사용해야하고 Windows OS에서 CLI를 사용하기 위해 터미널을 사용하는데, 터미널 내부에서 Bash 같은 shell을 사용하여 CLI 명령어를 사용할 수 있다. 


## ETC
- [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/)
  - Computer tool을 다루는 방법에 대한 강의 참고
  - Command-line Environment = CLI
