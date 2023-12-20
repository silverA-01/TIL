# CLI 기초 (Unix Commands)

CLI : Command Line Interface
- 명령어(커맨드)를 줄 단위로 읽고 실행하는 인터페이스
- 명령어를 통해 작동하는 인터페이스
- 키보드를 이용해 OS와 상호 작용하는 소프트웨어 메커니즘
- GUI(Graphic User Interface)와 반대되는 개념
  
## 1. 대표적인 Commands

### 프롬프트
- `$` : 프롬프트
  - 현재 명령어를 받을 준비가 되었다.
  - 터미널 명령어
    - `$`는 터미널 명령어이기 때문에 commands(흰색 글씨)에 넣으면 안 된다.

### 파일/폴더 생성 및 삭제
- `touch` + `파일명` : 파일 생성
- `rm` : 파일 삭제 (remove)
- `rm -r` : 파일/폴더 **모두** 삭제 
  - `-r` : recursively(재귀적으로)라는 뜻의 옵션
    - 재귀는 자기참조적인 특징을 띈다. 파일과 폴더를 삭제할 때 폴더 내부의 파일도 참조해 삭제하는 것을 말한다.
- `rm -rf` : 파일/폴더 모두 강제 삭제
    - `-f` : force 강제 옵션. 강제로 실행하도록 한다.
    - 모두 지워버리고 처음부터 해버리겠다고 meme처럼 사용
    - **※** meme으로서 참고할 뿐 절대 사용하지 않기를 추천
![rm -rf 밈](https://pbs.twimg.com/media/ENC2kioVUAArJxQ?format=jpg&name=medium)
---
- `mkdir + 폴더명` : 폴더 생성 (make directory)
- `rmdir` : **비어있는** 폴더 삭제 (remove directory)
  - 내용물이 있는 폴더는 error 메세지가 나온다. (Directory not empty)
  - `rmdir`는 잘 사용하지 않고 `rm - r`을 더 많이 사용
  - 
### 폴더 관련
- `cd` : 폴더 이동 (chage directory)
- `.` : 현재 폴더
- `..` : 상위 폴더
  - `cd ..` : 상위 폴더로 이동
  - `cd .` : 현재 폴더로 이동
- `~` : home directory
  - Why home directory is tilde?
    - 옛날 키보드에 `home키`와 `~`이 같이 있어서 그렇다.
     ![~ measn home dir](https://i.stack.imgur.com/L3esv.jpg)
  - `cd ~/CLI` : home directory 아래 있는 하위 폴더 CLI로 이동
- `/` : root dir
  - 컴퓨터는 Directory와 File들의 구성
  - 컴퓨터의 전체집합(모집합)이 root directory
  - `aaa./` : aaa라는 이름을 가진 폴더라는 의미
- `.`으로 시작하는 파일/폴더 : 숨김 파일/폴더
  - `.filename.확장자` : 숨김 파일
    - ex) .hidden.txt
  - `.dirname/` : 숨김 폴더
  - 숨김 파일/폴더는 현재 폴더의 내용물을 출력하는 `ls` 명령어로 보이지 않음
    - `ls -a` 명령어 입력시 숨김 파일/폴더가 보여짐
- `pwd` : 현재 작업 폴더. 내 위치 경로를 나타냄
  - Present Working Directory
  
### 내용물 출력
- `ls` : 현재 폴더의 내용물을 보여줌 (list)
- `ls -a` : 현재 폴더의 내용물을 모두 보여줌
  - `-a` : all 이라는 옵션
  - 숨김 파일도 보임
- `ls -l` : 현재 폴더의 내용물을 더 자세히 보여줌
  - `-l` : long 이라는 옵션. 더 길게.
- `cat` : 파일의 내용물을 출력

### 파일/폴더 복사
- `cp` : 파일 복사 (copy)
  - `cp <파일명> <위치>`로 원하는 위치에 파일을 복사할 수 있다.
    > cp a.txt ../ : a.txt 파일을 상위폴더에 복사
- `cp -r` : 파일/폴더 복사

### 파일/폴더 이동 및 이름 변경
- `mv` : 파일/폴더 이동 + 이름 바꾸기
- `mv <파일/폴더명> <위치>` : 파일/폴더를 이동경로 위치로 이동
  > ex. mv a.txt ../ : a.txt 파일을 상위폴더로 이동
- `mv <파일/폴더명> <위치><변경할 파일/폴더명>` : 파일/폴더를 이동경로 위치로 이동하고 이름을 바꾼다.
  - `mv A ./B` : A를 (현재 폴더에) B로 이름을 바꾼다.
    > ex. mv a.txt ./b.txt : a.txt를 b.txt로 이름을 바꾼다.
  - `mv A ../B` : A를 상위폴더로 이동하면서 B로 이름을 바꾼다.
    > ex. mv b.txt ../c.txt : b.txt를 상위폴더로 이동하고 c.txt로 이름을 바꾼다. 

### 기타 Commands
- `Ctrl + c` : 기존 행위를 취소(cancle)
- `Ctrl + l` = `clear` : 청소. 화면을 위로 올려 정리한다.
- `방향키 ↑, ↓` : 이전에 사용했던 명령어 list 이동
- `Tab` : 자동완성
  - 중복되는 값이 많을 경우 `tab` 한 번으로는 자동완성이 안 될 수 있음
  - `tab` 두 번 누르면, 중복되는 내용물들을 모두 보여줌
- `open <파일/폴더명>` : 파일/폴더를 GUI에서 열기
  - `open .` : 현재 폴더를 파일탐색기로 열기
- `sudo` : 관리자 권한으로 다음 명령어를 실행

## 2. CLI VS GUI

### CLI
* Command Line Interface
- 텍스트 기반 인터페이스
- 사용자는 명령어(커맨드) - 키보드를 입력하여 OS와 상호작용
- 개발자나 시스템관리자와 같은 전문가들이 사용
> 우리가 아는 'MS DOS'는 CLI 인 것을 알 수 있다.
![MS DOS](https://i.namu.wiki/i/Y-4-e6-ojp93QMThpqmi_ukmSaTmfVY4gUDtdCy_oZiOlNsVtdfP8P2_JKGhIxj_P8-2ylizZS1uJjGtvrGSMQ.png)

### GUI
* Graphical User Interface
- 사용자를 위한 시각적 표현을 한 인터페이스
- 그래픽을 사용하여 상호작용
  - 아이콘, 이미지 버튼, 창 등의 시각적인 요소를 탐색하고 마우스 등을 사용하여 클릭으로 작업을 수행
- 직관적이며 시각적으로 사용하기 쉬워 대부분의 컴퓨터 사용자가 익숙해질 수 있다.
> 'APPLE The Lisa'는 처음으로 대중적인 PC(personal computer) 시장을 점유했다. 아래 사진처럼 마우스를 이용해 작업하고 화면에 그래픽을 사용한 GUI가 만들어진 것이다.
![The Lisa](https://3894a8e173f5f8870a41-c88208a08312eda3cf96a15131ffd631.ssl.cf1.rackcdn.com/lisa11513184703168.jpeg)

  
### Interface
서로 다른 두 존재의 접점(만나는 지점)
- CLI와 GUI는 서로 다른 작업을 하는 것 같지만 같은 결과를 가져올 수 있다.
- Hardware Interface : 입출력장치 등
  - HDMI(High Definition Media Interface) : 본체와 모니터의 접점
- Software Interface : 컴퓨터 언어, 명령어, Zoom을 포함한 프로그램 파일 등



### CLI를 배워야 하는 이유
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


## OS Family Map

### OS (Operating System)
: 운영체제
- OS는 크게 Unix와 Windows 두 가지로 나뉜다.
- 
1. Unix
   1. Linux
      - Unix를 뜯어 고쳐 무료/오픈소스로 배포한 것이 Linux
      - Linux Kernal로 다양한 운영체제들이 파생되어 Unix family tree는 아주 많다
      - 파생 운영체제는 전제조건이 오픈 소스, 무료배포이다.
     - ex. Ubuntu, Centos, Android etc.
     - ![Unix family tree](https://i.gzn.jp/img/2021/08/10/os-timeline-and-family-rree/img-snap01947_m.png)
   2. APPLE
   - APPLE은 유료인 Unix를 정식 구매해 유료로 잠금 배포하는 운영체제
   - iOS, MacOS, iPadOS, visionOS
  
2. Windows
   - Unix와 달리 비교적 Windows 가계도는 깔끔하다.
   - Microsoft Winodws에서만 운영체제를 개발하여 배포하기 때문
   - ![Windows family tree](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcST2CkD07njPp32wTbE1zYuZD4Qx-X73KaEUxcyev5ysKR4Iz3bwp9EPF5az24xMWLrbLk&usqp=CAU)

---
### CLI와 OS
**CLI는 Unix OS에서 사용되는 인터페이스이다.** 사실, Windows 환경에서는 기본 터미널이 cmd를 사용해 Windows용 명령어를 입력해야 한다. 이를 위해 **Git bash**가 Unix의 CLI 명령어를 Winodws용 명령어로 변환해주는 역할을 해준다.

결론적으로 개발자들은 Unix OS의 CLI라는 환경을 사용해야하고, Windows에서 CLI를 사용하기 위해 터미널을 사용하는데, 터미널 내부에서 Bash 같은 쉘을 우리가 사용하고 있는 것이다.

## ETC
- [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/)
  - Computer tool을 다루는 방법에 대한 강의 참고
  - Command-line Environment = CLI
