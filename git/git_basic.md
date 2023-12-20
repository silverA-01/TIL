# Git
**버전**을 통해 **코드를 관리하는 도구**
- 코드 관리 도구(SCM : Source Code Management)
  - 버전 관리 시스템 : VCS(Version Control System)
- 코드 협업 도구
- 코드 배포 도구

## Git을 사용하는 목적
1. Version 관리
2. Backup
3. Collaborate(협업)

## Git의 프로젝트 관리 단위
git은 **폴더** / 디렉토리 단위로 코드를 관리한다.

## Git의 코드 관리 3단계
![git의 3단계](https://miro.medium.com/v2/resize:fit:686/1*diRLm1S5hkVoh5qeArND0Q.png)
1. Working Directory(작업 폴더)
    - = Working Tree
  
2. Staging Area(스테이지)
    - `git add` 를 통해 1에서 파일을 2로 포함
    - commit 전에 버전관리를 할 파일들만 Staging Area에 모아준다.


3. Repository(저장소) - Commit Log
    - `git commit`를 통해 2에서 파일을 3으로 포함

## 버전관리를 위한 Git 명령어 
`git [명령어]`

### (1) `git init`
git으로 코드 관리를 시작하는 명령어
```bash
$ git init
```
- 디렉토리 경로는 git으로 코드 관리를 하고 싶은 폴더로 이동한 후 명령어를 입력해야 한다.

- `(master)` : 현재 브랜치(branch)명
    > `git init`를 실행하니 프롬프트의 현재 경로 옆에 `(master)`가 추가된 것을 확인할 수 있다. `(master)` 앞에는 현재 디렉토리 경로로 사용자가 `git init`을 시작한 폴더 경로에 따라 다를 수 있다.
    ```bash
    user@OS-2107250526 MINGW64 ~/kdt-data-33/github/test (master)
    $
    ```
- `git init`를 실행하면 현재 폴더에 `.git`이라는 폴더가 생성된다.
  - `.git` : git의 관리와 관련된 파일


### (2) `git status`
현재 상태를 출력(Git에게 현재 상태를 물어봄)
1. `git init` 직후 `git status` 실행
```
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
`git init` 직후 `git status` 명령어를 입력하니 위와 같이 출력된다. 
> 현재 master라는 이름의 branch에 있으며
> 
> 아직 commit이 없음
>
> commit할 것이 없음(파일을 만들거나 복사하고, `git add`를 통해 추적해봐)

1. 현재 폴더에서 git에 관리할 파일을 만들어 준다.
```bash
$ touch a.txt
```

1. 파일 생성 후 `git status` 실행
```bash
$ git status
On branch master

No commits yet

Untracked files: 
  (use "git add <file>..." to include in what will be committed)
```
파일을 생성후 `git status` 실행하니 마지막 문장이 바뀌어서 출력되었다.
> 현재 master라는 이름의 branch에 있으며
>
> 아직 commit이 없음
>
> 추적되지 않은 파일:
> (`git add <파일명>`을 사용해서 commit될 것에 포함시켜라)


### (3) `git add [파일명]`
- `git add .` : 현재 폴더의 모든 변경사항 Stage Area에 추가

1. `git add a.txt` 실행
   - a.txt 파일을 Stage Area에 추가
   - 파일을 commit하기 위해 먼저 파일이 Stage Area에 존재해야 한다.
```bash
$ git add a.txt
```
2. `git add a.txt` 실행 후 `git status` 실행
```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
```
파일을 Stage Area에 추가하고 `git status` 실행하니 마지막 문장이 바뀌어서 출력되었다.

> 현재 master라는 이름의 branch에 있으며
>
> 아직 commit이 없음
>
> commit 될 수 있는 변화 존재:
>   (`git rim --cached <파일명>`을 사용해서 unstage 해봐)
>       새로운 파일 : a.txt

### (4) `git commit -m "메시지"`
`commit`은 **버전을 생성하는 것**이다. 
- 작업물의 변화된 내용을 기록하는 것이다. 
- `-m` 옵션은 message의 약자
- `"메시지"`에 들어갈 내용은 버전을 기록하면서 어떤 내용이 변화되었는지 남기면 좋다.

1. 처음으로 `commit`을 시도할 경우
```bash
$ git commit -m "Fisrt commit"
Author identity unknown

*** Please tell me who you are.

Run

git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
처음 `commit`을 시도하는 경우 git이 사용자가 누군지 물어보는 내용이 나온다. " "안의 내용은 사용자가 설정할 본인의 이메일과 이름을 적으면 된다. 이메일은 github와 연결할 이메일로 적는 것이 좋다.
>
> 작자미상(신원을 알 수 없는 작성자)
>
> 당신이 누군지 알려달라.
>
> 아래의 명령어를 실행하라.
>
> 전역의(global) 사용자 이메일을 `"이메일주소"`로 설정
> 
> 전역의 사용자 이름을 `"사용자 이름"`으로 설정

2. `git config`로 이메일 주소와 사용자 이름을 설정
```bash
git config --global user.email "silvermare@gmail.com"
git config --global user.name "silverA-01"
```
3. `git commit`
   - `commit`을 하면서 "First commit"이라고 내용을 담는다.
    ```bash
    $ git commit -m "Fisrt commit"
    ```
    Repository에 파일이 commit되면 아래와 같이 출력된다.
   - 사용자의 위치경로 등에 따라 내용이 다를 수 있다.
    ```bash
    [master 216b26f] First commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 a.txt
    ```
    - 만약 `-m` 옵션으로 메시지를 입력하지 않고, 에디터창으로 넘어가고 싶다면 `git commit`만 입력한다.
    ```bash
    $ git commit
    ```

    > 아래처럼 commit message를 입력하라는 에디터창이 나온다. 편집모드(`i`)에서 commit message를 입력하고 `Esc`를 눌러서 편집모드에서 나간다. `wq`를 입력하여 저장하고 종료한다.
    ```bash
    
    # Please enter the commit message for your changes.

    # Lines starting with '#' will be ignored, and an empty message aborts the
commit.

    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    # new file: test.txt
    ```

### (5) `git config`
git에 관한 설정
- 전역으로(global) 사용자의 이메일을 설정
```bash
$ git config --global user.email "이메일주소"
```
- 설정값 확인
```bash
$ git config --global user.email
```

### (6) `git log`
현재까지의 `commit`을 출력
- `git log`를 실행하면 작성자, 날짜, commit message를 확인할 수 잇다.
```bahs
$ git log
commit bab6792111fa2c3eed036e7ef11401c4a5425b15 (HEAD -> master)
Author: silverA-01 <silvermare01@gmail.com>
Date:   Tue Dec 19 16:31:59 2023 +0900

    First commit
```
- `git log --oneline`를 실행하면 한 줄로 log가 출력된다.
```bash
$ git log --oneline
bab6792 First commit

```

### (7) `git remote`
- `git remote add <저장소 이름> <저장소 주소>` : git에게 원격저장소(remote)를 추가(add)하라는 명령어

