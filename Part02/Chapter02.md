# Chapter02 셸(Shell)
리눅스 운영체제에서 하드웨어와 사용자가 상호작용하기 위해서는 이를 돕는 두 소프트웨어가 필요하다. 하나는 `커널(Kernel)`이고, 하나는 `셸(Shell)`이다. 사용자가 하드웨어에 명령을 내리기 위해서 셸을 이용한다. 우리가 작성하는 모든 명령이 셸을 통해 이루어지는 작업이다. 셸은 사용자의 명령을 받아 커널에게 적절한 명령으로 변환하여 전달한다. 커널은 이를 하드웨어가 이해할 수 있도록 변환하여 전달한다. 

## 셸 종류
|분류|세부 분류|실행파일|
|:-:|:-:|:-:|
|본셸|본셸(Bourne shell)|/bin/sh|
|본셸|콘셸(korn shell)|/bin/ksh|
|본셸|배쉬셸(Bourne Again shell)|/bin/bash|
|본셸|지셸(z shell)|/bin/zsh|
|C셸|C셸|/bin/csh|
|C셸|tcsh셸|/bin/tcsh|

## 셸 확인 및 변경
시스템에 사용할 수 있는 셸 종류는 `/etc/shells`에서 확인할 수 있다. 환경변수 `SHELL`을 통해 로그인 시 실행되는 셸을 확인할 수 있다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/bin/rbash
/bin/dash
/bin/zsh
/usr/bin/zsh
root@goorm:/workspace/g0pher/git/linux-master/Part02# echo $SHELL
/usr/bin/zsh
root@goorm:/workspace/g0pher/git/linux-master/Part02# cat /etc/passwd | grep root
root:x:0:0:root:/root:/usr/bin/zsh
root@goorm:/workspace/g0pher/git/linux-master/Part02# /bin/sh
# ls
Chapter01.md  Chapter02.md
# exit
```
셸들은 모두 실행 가능한 소프트웨어이므로 위와같이 실행을 하면 해당 쉘을 이용할 수 있다. 하지만 이는 일시적인 것이고, `chsh` 명령을 이용하여 로그인할 때 실행되는 셸을 변경할 수 있다.
```
root@goorm:/workspace/g0pher/git/linux-master/Part02# cat /etc/passwd | grep g0pher
g0pher:x:1000:1000::/home/g0pher:/bin/bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# chsh g0pher -s /bin/zsh
root@goorm:/workspace/g0pher/git/linux-master/Part02# cat /etc/passwd | grep g0pher
g0pher:x:1000:1000::/home/g0pher:/bin/zsh
root@goorm:/workspace/g0pher/git/linux-master/Part02# su g0pher
goorm% id
uid=1000(g0pher) gid=1000(g0pher) 그룹들=1000(g0pher)
goorm% echo $SHELL
/bin/zsh
```

## 변수
셸에서 이용하는 변수는 두 가지가 있다. 환경변수(전역변수)와 셸 변수(지역변수)가 이것인데, 환경변수의 경우 모든 셸이 사용 가능하도록 공유되어 있으며, 상속이 가능하다. 셸 변수의 경우 해당 셸에서만 사용 가능한 변수로 상속이 불가능 하다. 각각 `env`와 `set` 명령으로 확인이 가능하다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# env

(... 중략 ...)

MAIL=/var/mail/root
SHELL=/usr/bin/zsh
TERM=xterm-color
SHLVL=2
LANGUAGE=ko_KR.UTF-8
LOGNAME=root
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
LESSOPEN=| /usr/bin/lesspipe %s
_=/usr/bin/env
root@goorm:/workspace/g0pher/git/linux-master/Part02# set
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extquote:force_fignore:histappend:hostcomplete:interactive_comments:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_LINENO=()
BASH_SOURCE=()
BASH_VERSINFO=([0]="4" [1]="4" [2]="20" [3]="1" [4]="release" [5]="x86_64-pc-linux-gnu")
BASH_VERSION='4.4.20(1)-release'
COLUMNS=216
DIRSTACK=()
EUID=0
GROUPS=()
HISTCONTROL=ignoredups:ignorespace
HISTFILE=/root/.bash_history
HISTFILESIZE=2000
HISTIGNORE='df /'
HISTSIZE=1000
HOME=/root
HOSTNAME=goorm
HOSTTYPE=x86_64

(... 중략 ...)

TERM=xterm-color
TZ=Asia/Seoul
UID=0
USER=root
_=env
```
환경변수는 `export` 명령을 이용하고, 셸 변수는 `등호(=)`를 이용하여 등록할 수 있다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# env | grep test
root@goorm:/workspace/g0pher/git/linux-master/Part02# test=123
root@goorm:/workspace/g0pher/git/linux-master/Part02# env | grep test
root@goorm:/workspace/g0pher/git/linux-master/Part02# set | grep test
test=123
root@goorm:/workspace/g0pher/git/linux-master/Part02# echo $test
123
root@goorm:/workspace/g0pher/git/linux-master/Part02# export test
root@goorm:/workspace/g0pher/git/linux-master/Part02# env | grep test
test=123
```
변수 삭제는 `unset`으로 할 수 있다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# export test=1
root@goorm:/workspace/g0pher/git/linux-master/Part02# env | grep test
test=1
root@goorm:/workspace/g0pher/git/linux-master/Part02# unset test
root@goorm:/workspace/g0pher/git/linux-master/Part02# env | grep test
root@goorm:/workspace/g0pher/git/linux-master/Part02#
```

## 주요 환경변수
|변수|기능|
|:-:|:-|
|PATH|실행할 명령어를 찾기 위한 경로|
|HOME|사용자의 홈 디렉터리 경로|
|HOSTNAME|호스트명|
|USER|유저명|
|DISPLAY|X 응용프로그램이 화면 출력을 위해 접속할 X 서버의 주소|
|PS1|셸 프롬프트 선언 시 사용하는 변수|
|PS2|2차 셸 프롬프트 선언 시 사용하는 변수|
|PWD|현재 디렉터리 절대경로|
|SHELL|로그인 셸의 절대경로|
|TERM|터미널 종류|
|TMOUT|로그아웃 관련 시간제어|
|LANG|기본 언어|
|MAIL|메일 저장 경로|

## 셸 환경설정 파일
셸이 실행되면 설정파일을 읽어 초기 설정을 완료한다. 이 때, 참조하는 파일들은 다음과 같다.  

|분류|경로|기능|
|:-:|:-|:-|
|전역 설정|/etc/profile|변수와 프로그램 제어|
|전역 설정|/etc/bashrc|별칭(alias)와 함수 제어|
|지역 설정|~/.bash_profile|개인 셸 환경 제어|
|지역 설정|~/.bash_history|명령이나 입력 기록|
|지역 설정|~/.bashrc|별칭(alias)와 함수 제어|
|지역 설정|~/.bash_logout|로그아웃 직전 실행 설정|


## 별칭(alias)
리눅스에서는 별칭이라는 개념이 존재해서 긴 명령을 짧게 재정의할 수 있다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part02# gogo
bash: gogo: 명령어를 찾을 수 없음
root@goorm:/workspace/g0pher/git/linux-master/Part02# alias gogo='echo "this is test"'
root@goorm:/workspace/g0pher/git/linux-master/Part02# gogo
this is test
root@goorm:/workspace/g0pher/git/linux-master/Part02# unalias gogo
root@goorm:/workspace/g0pher/git/linux-master/Part02# gogo
bash: gogo: 명령어를 찾을 수 없음
```